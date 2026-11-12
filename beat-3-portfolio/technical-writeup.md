# Making Logixia's Logging Levels Predictable: Validation, Regression Tests, and a Merged Fix

## Overview

I contributed a TypeScript change to Logixia, an open-source logging library, through [PR #51](https://github.com/Logixia/logixia/pull/51), which addressed [issue #29](https://github.com/Logixia/logixia/issues/29). Logixia takes logging levels from configuration, environment variables, and calls to `setLevel()`. Before my change, it accepted unrecognized values without warning, and an uppercase built-in value such as `DEBUG` could behave differently from `debug`. I added level validation and normalization, guarded runtime changes, and wrote regression tests. The project maintainer merged the PR on October 23, 2026; the fix was later included in version 1.12.6.

## What happened

### Technology stack

I worked in **TypeScript** on a **Node.js** logging library. I used **Jest** for regression and compatibility tests, **TypeScript type checking** (`npm run typecheck`) and **ESLint** (`npm run lint`) for static checks, and **Git/GitHub** for version control, code review, and the merged pull request. I ran the project locally on **Windows 11** using **PowerShell** and npm. **Claude Code** helped with code exploration, drafting tests, and reviewing the diff; I checked its suggestions against the source and actual test results.

### Finding and reproducing the problem

I selected issue #29 because it described specific, testable behaviors in `src/core/logitron-logger.ts`. I forked the repository, created branch `fix-level-validation-29`, and checked the baseline before editing the code. TypeScript type checking and linting passed. The full Jest run had 938 passing tests and one Windows `EPERM` symlink-permission failure unrelated to logging. Recording that failure first helped me distinguish a pre-existing environment problem from any regression I might introduce.

I traced the flow from `resolveInitialLevel()` to the cached numeric threshold. The code stored a level name and later looked it up in a map with lowercase built-in keys. A missing lookup silently fell back to the numeric threshold for `info`. That meant `LOGIXIA_LEVEL=DEBUG` did not actually enable debug output. I also found that `setLevel('nope')` could rebuild the cache and reset the active threshold to `info`, instead of preserving the previous setting.

I added the four tests described in the issue and ran them against the pre-fix code. This is the recorded result from my contribution work:

```text
Before the fix: 3 of 4 issue tests failed.
LOGIXIA_LEVEL=DEBUG: expected "debug", received "DEBUG".
Unknown initial level: expected one warning, received zero.
setLevel('nope'): expected one warning, received zero.
Custom `kafka` level: passed.
```

These failures mattered because each checked observable behavior, not just an internal helper: the selected level, emitted messages, and warning output. The existing custom-level behavior was already correct and needed to remain correct.

### Implementing the change and revising it

I introduced `canonicalLevel()` to prefer an exact match for custom level names and then try a lowercase match for built-in levels. I added validation for configured levels and environment or namespace overrides, with warnings for invalid settings. I also updated `setLevel()` to reject an unknown level without changing the active threshold.

This excerpt from the [merged PR diff](https://github.com/Logixia/logixia/pull/51/files) shows the key runtime guard:

```typescript
const canonical = canonicalLevel(level, this._levelValues);
if (canonical === undefined) {
  // Refuse unknown levels so getLevel() and the active threshold stay unchanged
  internalWarn(
    `setLevel: unknown log level '${String(level)}' ignored; valid levels: ${this._validLevelList()}. ` +
      `Keeping '${this.getLevel()}'.`
  );
  return;
}
```

The first implementation passed all four issue tests, but reviewing the diff exposed another case they did not cover. `resolveInitialLevel()` gave a nonempty `LOGIXIA_LEVEL` environment variable precedence over a valid configured level even when the environment value was invalid. For example, `LOGIXIA_LEVEL=chatty` could displace a configured `warn` and make the logger fall back to `info`. I changed the initial resolution logic so an invalid environment value would not displace a valid configured level. I then added regression cases for this path and other affected override behavior, expanding the new test file from four tests to eight. This revision is why I would not describe the first green test run as the end of the fix.

### Testing, review, and result

My final recorded checks were:

```text
New level-validation tests:       8/8 passed
Existing custom-level tests:     31/31 passed
TypeScript typecheck:            passed
ESLint:                          passed
Full local Jest suite:           946 passed, 1 failed
```

The one failing local test was the same Windows `EPERM` symlink test seen in my baseline. I reported this limitation in the PR instead of claiming a completely passing suite. After the maintainer approved GitHub CI runs, the project's main quality, test, build, and security checks passed, although Dependency Review failed and I did not investigate that failure.

The maintainer reviewed PR #51, confirmed that uppercase environment levels worked, invalid levels warned, and `setLevel('nope')` preserved the previous threshold. They agreed with falling through from an invalid environment level to the next configured value. They also noted that returning the canonical value directly from `resolveInitialLevel()` would improve clarity, but said it was not a blocker. The PR merged on October 23, 2026, closing issue #29. Logixia later reported that the change was released in version 1.12.6.

## Limitations and what's next

The fix addresses the validation paths covered by issue #29 and the extra cases I found, but the eight tests are not proof that every possible configuration combination has been exercised. One known custom-level edge case, a mixed-case spelling such as `Kafka`, was outside the issue's scope. My local full suite also retained the pre-existing Windows symlink failure, and the GitHub Dependency Review failure remains unexplained. Finally, the maintainer's suggestion about making `resolveInitialLevel()` return its canonical value was not incorporated before the merge.

If I returned to this work, I would add a configuration-precedence test matrix, investigate the Dependency Review failure, and consider the maintainer's readability suggestion in a focused follow-up change. I would also commit the initial failing tests separately before implementing a fix, so anyone reviewing the history could see the reproduction independently. The biggest lesson I took from this contribution is that tests establish important evidence, but reviewing the assumptions behind those tests is how I found the problem my first implementation missed.

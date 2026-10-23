# Contribution: feat(config): warn on unknown log levels and accept upper-case LOGIXIA_LEVEL

Path: `beat-2-contribution/contribution-story.md`

**Contribution Number:** 1
**Student:** Disha Kempegowda
**GitHub Username:** Disha-k-gowda
**Issue:** https://github.com/Logixia/logixia/issues/29
**Pull Request:** https://github.com/Logixia/logixia/pull/51

---

## Toolkit

Each story section below, from Why I Chose This Issue through Pull Request, ends with a
Toolkit block recording which tool did that phase's work, what it produced, what fell
short, and what I changed because of it. The dated entries below are the toolkit's own
weekly timeline: what I built or changed, what broke, and how I responded.

**Unit 5: Wrote my issue-scout search strategy and patched the rubric after the first wild scan**

On 2026-10-17 I ran my first wild scan with three `gh search` queries tied to my fit profile
(Python and JavaScript good-first-issues, TypeScript help-wanted): it pulled 300 issues, kept
255 after dropping assigned and translation issues, and graded the top 5 as four accepts and
one reject. One accept, yfridelance/shelly-manager#7, was a false positive because it can
only be tested on a real Gen1 Shelly device, so I added a newcomer-scope fail condition for
work that needs physical hardware unless a mock or emulator is enough, and logged the change
in scan-notes.md without rerunning the scan. Search ranking is still an open problem: all
five top results tied at 0 comments, so update time favored brand-new issues in tiny repos.
I then graded sbt/website#553 with direct URL grading; it passed the required checks, and I
posted a claim comment on it. This story originally also reported a direct grade of
Logixia/logixia#119 that passed the required checks. (Logixia/logixia#119 was this issue's
earlier identifier, before the Logixia repository was recreated. The current issue is
Logixia/logixia#29.) I cannot verify that grade now: my current scout records
(`scan-output.md`, `scan-notes.md`) hold no #119 grade, and #119 no longer exists in the
recreated repository. My earlier work referenced issue #119 in the original repository,
but I cannot verify whether I posted a claim comment before the repository was recreated.

**Unit 6: Installed the voice guard, patched the scout's scope check, wrote repo memory, and
ran a retrospective claim and reproduction for #29**

All of this work happened on 2026-10-23, after PR #51 had merged (04:12:15 UTC) and #29
had closed, so none of it guided the implementation.

I installed the voice guard. `check_voice.py` and `hooks-settings.json` live in
`~/.claude/voice-guard/`, next to my voice guide, which is now the one canonical copy. The
`voice-guide.md` files in repro-check, plan-check, and pr-precheck are one-line pointers to
it. I added the Upstream section to the guide (claims, questions, pings), each rule with a
wrong/right pair. The settings check printed "voice guard hook found", and the wiring test
(`gh issue comment --help`) was stopped with "no body the guard can read", which is the
expected pass. I replaced repro-check's and plan-check's sandbox scopes with the wild
scopes, and patched the scout rubric so `scope-feasible` replaces `newcomer-scope`. A
regrade under the new rubric turned geoff-davis/aiogzip#161 from accept to reject, because
another contributor was assigned it on 2026-10-22. The regrade still accepted
yfridelance/shelly-manager#7 (ambitious difficulty, weak fit): the new scope check no
longer rejects hardware-only work, so my Unit 5 hardware fix no longer applies.
`scan-notes.md` proposes filtering hardware issues at the ranking stage instead; I have not
applied that yet. I also wrote `CLAUDE.local.md` in my
Logixia clone and kept it out of git with `.git/info/exclude`.

For #29 I ran the tools retrospectively. The scout's direct grade was accept with
moderate difficulty, although the rubric should not have accepted an issue that was
already closed. I wrote the claim I should have posted (`claim-draft.md`, never posted),
and the voice guard passed it. I reproduced the issue on the pre-fix and fix commits
(`repro-draft.md`). repro-check's final verdict on the full package was accept, with all
five checks passing, and the voice guard passed the final reproduction report. Neither
draft was posted. These steps are described in Why I Chose This Issue and Reproduction
Process.

**Unit 7: Installed the ship-gate, wrote a sourced manifest, and ran the gate retrospectively
on PR #51**

All of this happened on 2026-10-23, after PR #51 had merged (04:12:15 UTC), so the gate did
not guard the real submission. It is a retrospective check of the branch that shipped.

- Tool: the Unit 7 ship-gate (`~/.claude/ship-gate/check_gate.py`), which runs the must-pass
  checks in my `ship-manifest.md` and then my own six-check pr-precheck rubric in live mode.
  The install added the gate's hook next to the voice guard's, kept my old pr-precheck scope
  as `scope.md.sandbox`, and created the manifest in my Logixia clone, excluded from git.
- What it produced: one manual-doorway run (`check_gate.py --branch --base main`, with the
  real PR title, the merged PR description, `plan.md`, `test_evidence.md`, and
  `--issue https://github.com/Logixia/logixia/issues/29`), from 14:57 to 14:58 local time.
  Verdict PASS, exit code 0. All five manifest checks passed (type check, lint, the issue's
  8 tests, the test suite without the Windows symlink test, and build), and all six
  pr-precheck checks passed (plan-fidelity, description-fidelity, test-evidence,
  repo-checks, diff-reviewable, standards-compliant). I did not rerun it.
- Difficulties: my pr-precheck still assumed the Path Review sandbox. Its procedure required
  "the scoped Path Review repository", and its rubric, SKILL.md, and evidence guide pointed
  at `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`, while Logixia tracks
  `.github/pull_request_template.md` and a root `CONTRIBUTING.md`. `npm run format:check`
  exited 1 in my checkout: `core.autocrlf=true` gives CRLF line endings, and Prettier
  flagged 363 files (180 in the repo, 183 in a stray nested folder). The full `npm test`
  still fails on the known Windows `EPERM` symlink test, as it does on the pre-fix commit.
  Several of Logixia's checks (PR title, CodeQL, Dependency Review, Bundle Size, the Node
  18/20/22 matrix) only run on GitHub, so I had to separate what I could run here from what
  only CI showed.
- What changed: I wrote the manifest from CONTRIBUTING.md, `ci.yml`, and my
  `CLAUDE.local.md`, with a source for every row and a dated reason for every exclusion,
  instead of dropping checks that would fail. I narrowed the test row to skip only the
  `EPERM` test by name and verified it first through `cmd.exe` (946 passed, 1 skipped, 0
  failed, exit 0). I replaced the Path Review assumptions in pr-precheck with wording that
  follows the live scope, after backing up each file; the six checks and their pass and
  fail conditions did not change. I wrote a retrospective `plan.md` from this story's
  Solution Approach and a `test_evidence.md` that dates every result and separates saved
  logs from results reported earlier, and I used PR #51's merged description unchanged as
  `pr_draft.md`. My ship decision was not to ship: the PR was already merged, so I ran only
  the manual doorway and never `gh pr create`.
- Limitations: the full unfiltered Jest suite still fails locally on the `EPERM` test.
  Dependency Review failed on PR #51, and I have not investigated why. The gate ran after
  the merge, not before submission, so it shows the shipped branch would have cleared my
  manifest and rubric, not that I checked it before shipping. pr-precheck also noted that my
  procedure has no rule for an already-merged PR or for a plan that was never posted.
- Evidence: [`evidence/unit7/unit7-ship-gate-run.txt`](evidence/unit7/unit7-ship-gate-run.txt)
  (the full gate output) and
  [`evidence/unit7/unit7-gate-log.txt`](evidence/unit7/unit7-gate-log.txt) (the gate-log
  entry), each with a header recording the run.

**Unit 8: Installed the PR-monitor, wrote my playbook, and ran the monitor retrospectively
on PR #51**

PR #51 merged on 2026-10-23 at 04:12:15 UTC, after one review comment, before I installed
the monitor. So the monitor never watched the review period. The run below is a real run
against the merged PR on 2026-10-23, not pre-merge monitoring.

- Tool: the official Unit 8 PR-monitor (`~/.claude/pr-monitor/monitor.py`), which reads a
  PR's live state through read-only `gh` calls and drafts a next move to a file, plus my
  four-section playbook (Response rules, Staleness thresholds, Nudge etiquette, Walk-away
  criteria). I built the playbook from my voice guide's Upstream rules. Its main policies:
  - No nudge before 7 calendar days without maintainer activity. That is my chosen policy;
    my only data point is PR #51's first maintainer comment, about 4.2 days after I opened
    it.
  - At most one nudge, and never on a merged or closed PR.
  - Reassess after 21 quiet days following a nudge.
  - I rewrite and post every public message myself.
- What it produced: the free `--state` check found Logixia/logixia PR #51. One full run then
  detected MERGED and selected the Merged follow-up form. It wrote `run-report.md` and
  `drafted-move.md` and added a `[run]` entry to `monitor-log.md`. It exited with code 0.
  The draft was a short thank-you to the reviewer that acknowledged their
  `resolveInitialLevel()` note as a possible follow-up.
- Difficulties: the draft needed checking against the real PR and issue.
  - It suggested closing #29 "if it didn't auto-close", but #29 had already closed as
    completed when the PR merged.
  - It left an unresolved conditional placeholder ("[If the merged code still returns it as
    written:]") in the message body.
  - It called the reviewer's non-blocking readability note a "catch".
  - The run report's check, mergeability, and review-decision values (1 failing check,
    UNKNOWN, REVIEW_REQUIRED) were stale leftovers that GitHub stops updating after a merge,
    not the PR's real state.
- What changed: I reviewed the draft against PR #51 and issue #29 and decided not to post
  it. The PR is merged, the issue is closed, the reviewer's note was explicitly not a
  blocker, and a follow-up comment would add noise to a finished discussion. No GitHub
  comment was posted. I kept the 7-day no-nudge rule and the one-nudge limit for future open
  PRs. The monitor's working files stay on my machine; Assignment 5 asks for no monitor
  output.

---

## Why I Chose This Issue

My first issue-scout scan ran my three `gh search` queries across GitHub, pulled 300
issues, kept 255 after filtering out assigned and translation issues, and graded the top
five: four accepts and one reject. I did not take my final issue from that ranked list. I
first looked at sbt/website#553 (a broken TestsListener link on the sbt Testing docs page),
which I found through the CodePath tracker and which issue-scout's direct URL grading
accepted. I posted a claim comment there
(https://github.com/sbt/website/issues/553#issuecomment-6243471487) and cloned the site, but
I did not make any change or open a PR on sbt/website, so this story does not count it as a
contribution. I moved to the Logixia logging issue instead. My earlier story reported that
issue-scout graded it as Logixia/logixia#119 and that it passed the required checks, but my
current scout records hold no #119 grade, so I cannot verify that now. After the
repository was recreated, the same issue became Logixia/logixia#29.

Logixia #29 is labeled `good first issue` and `hacktoberfest`, and it is unusually well
scoped: it names the functions involved (`resolveInitialLevel`, `_buildPerfCaches`,
`setLevel` in `src/core/logitron-logger.ts`), lists four exact test cases, and gives
acceptance criteria I can check myself (`npx jest`, `npm run typecheck`, `npm run lint`).
It is TypeScript, which matches the TypeScript help-wanted part of my fit profile, and it is
a real behavior change with tests rather than a one-line docs edit, so it stretches me
without being open-ended. I wanted to learn how to reproduce a bug as failing tests first,
how a logging library resolves its level from config and environment variables, and how to
get a PR through a project's own checks. On the tool: the scout held up on the issues I
graded, but the wild scan exposed a hardware false positive (fixed in Unit 5, then reopened
when Unit 6 replaced `newcomer-scope`; see the Unit 6 Toolkit entry) and a weak ranking
signal (still open), as described below. My earlier work referenced issue #119 in the original
repository, but I cannot verify whether I posted a claim comment before the repository was
recreated. On #29 I did not post a claim comment before implementing the fix, even though
CONTRIBUTING.md asks contributors to comment first. #29 is now closed, with no comments and
no assignee. I linked my work to it with `Closes #29` in PR #51.

**Retrospective scout grade (2026-10-23).** For Unit 6 I graded #29 with issue-scout's
direct mode. This was after PR #51 had merged and #29 had closed, so it played no part in
choosing the issue. I ran it because repro-check's wild scope only grades drafts for
issues the scout has graded. All five required checks passed and the verdict was accept,
with a **moderate** difficulty note: the issue names the file and functions, but the work
spans code plus a new test file. The accept is a rubric error: `unclaimed` only looks for
an open PR, and no check asks whether the issue is still open, so a closed issue that is
already fixed still passes. The entry in `scan-output.md` is labeled retrospective and
"not available to take."

**Toolkit**

- Tool: issue-scout, used two ways: a wild GitHub scan driven by my written search strategy
  and rubric, and direct URL grading of sbt/website#553, which I found through the CodePath
  tracker, and (as my earlier story reported) of Logixia/logixia#119, now #29.
- What it produced: the wild scan searched 300 issues, kept 255, and graded 5 (4 accepted,
  1 rejected). Direct URL grading passed sbt/website#553 on the required checks. My earlier
  story reported the same for Logixia/logixia#119, but no #119 grade survives in my current
  scout records. I chose the Logixia issue, now #29.
- Difficulties: the rubric accepted yfridelance/shelly-manager#7, a false positive because it
  can only be tested on a real Gen1 Shelly device, and my fit profile says to avoid hardware
  work. Ranking was also weak: all five top results tied at 0 comments, so update time
  decided the order and pushed brand-new issues from tiny repos to the top.
- What changed: I added a newcomer-scope fail condition for work that needs physical
  hardware, unless the issue says a mock or emulator is enough. Search ranking is still
  open; I would add a signal beyond comments and update time, such as repository activity,
  so ties stop favoring brand-new issues in tiny repos.
- Unit 6 (retrospective): a direct grade of #29 on 2026-10-23, after the merge: accept,
  moderate difficulty. It showed that my rubric accepts closed issues, which I have not
  fixed yet.

---

## Understanding the Issue

**Problem Description**

Logixia accepts log levels from three places: the `LOGIXIA_LEVEL` environment variable,
`levelOptions.level` in the logger config, and `setLevel()` at runtime. None of them were
validated. The value was stored as-is and later looked up in a map whose keys are lower
case, and any miss silently fell back to `info` (the `?? 2` default). So a wrong or
differently-cased level never produced an error or warning; it just quietly changed what
got logged.

**Expected Behavior**

- `LOGIXIA_LEVEL=DEBUG` should behave like `debug` and actually enable debug output.
- An unknown level such as `levelOptions: { level: 'warning' }` should warn once per logger,
  naming the bad value and the valid levels, and then fall back to `info`.
- Custom levels declared in `levelOptions.levels` (for example `kafka`) must still be
  accepted without a warning.
- `setLevel('nope')` should warn and leave both `getLevel()` and the active threshold
  unchanged.

**Current Behavior**

- `LOGIXIA_LEVEL=DEBUG` stored `DEBUG`; `getLevel()` returned `"DEBUG"`, but the threshold
  fell back to `info`, so debug messages were dropped.
- `level: 'warning'` silently ran at `info` with no warning.
- `setLevel('nope')` stored `'nope'`. The issue says the old threshold is kept, but when I
  traced the code I found it was worse: `setLevel()` calls `_buildPerfCaches()`, which
  re-resolves the level from `getLevel()`, gets `'nope'`, misses the map, and resets the
  threshold to `info`. A logger set to `warn` would start printing `info` messages after
  one bad call.

**Affected Components**

- `src/core/logitron-logger.ts`: `resolveInitialLevel()`, the level-map setup in
  `_buildPerfCaches()`, `setLevel()` / `getLevel()`, and `resolveEffectiveLevel()` (the
  namespace and environment override chain).
- `src/utils/internal-log.ts`: `internalWarn()`, which the fix uses for warnings.
- `src/core/__tests__/custom-levels.test.ts`: the existing custom-level behavior the fix
  must not break.
- New: `src/core/__tests__/level-validation.test.ts`.

**Toolkit**

- Tool: Claude Code, used to read `logitron-logger.ts` with me and trace how a level string
  flows from config or the environment into `_minLevelValue`.
- What it produced: a walkthrough of the resolution path (`resolveInitialLevel` →
  `_buildPerfCaches` → `resolveEffectiveLevel`), which I checked against the source line by
  line and against the issue text.
- Difficulties: the issue text and the code disagreed about `setLevel('nope')`. The issue
  says the old threshold is kept, but the cache rebuild actually resets it to `info`. I had
  to confirm this myself in the code instead of trusting either summary.
- What changed: I wrote the threshold change into my own problem statement and later into
  the PR description, so the maintainer sees the real behavior.

---

## Reproduction Process

**Environment Setup**

- OS: Windows 11 Home (10.0.26200), PowerShell and Git Bash.
- Runtime: Node.js v24.14.0, npm 11.9.0.
- Project: Logixia 1.12.0 (TypeScript, Jest, ESLint).
- Setup: forked Logixia/logixia to https://github.com/Disha-k-gowda/logixia, cloned the
  fork, added `upstream`, and created the branch `fix-level-validation-29` from `main`.
- Challenge 1: `npm ci` failed because the repository has no committed lockfile. I used
  `npm install` instead, which resolved and installed the dependencies.
- Challenge 2: baseline checks. Before I changed anything, `npm run typecheck` and
  `npm run lint` passed, and `npx jest` reported 938 passing tests and 1 failure. The failure
  is a Windows `EPERM` symlink-permission error in `src/cli/__tests__/index.test.ts`, which
  is unrelated to logging levels. I recorded it as pre-existing so I would not mistake it
  for something I broke later.

**Steps to Reproduce**

1. On `main`, add `src/core/__tests__/level-validation.test.ts` with the four cases from
   the issue: upper-case `LOGIXIA_LEVEL=DEBUG`, unknown initial level, custom `kafka` level,
   and `setLevel('nope')`.
2. Run `npx jest src/core/__tests__/level-validation.test.ts --runInBand`.
3. Observed result: 3 of 4 tests failed, and only the `kafka` custom-level test passed.
   - The `DEBUG` test failed with `Expected: "debug"  Received: "DEBUG"`.
   - The unknown-level and `setLevel('nope')` tests failed with
     `Expected length: 1  Received length: 0` (no warning was emitted at all).

**Reproduction Evidence**

- **Commit showing reproduction:** I did not make a separate reproduction-only commit. The
  failing tests live in the same commit as the fix,
  https://github.com/Disha-k-gowda/logixia/commit/7b8c920. Anyone can reproduce the
  failures by running that test file against `main`'s `logitron-logger.ts`. I re-ran it that
  way on 2026-10-18 while writing this story: the final 8-test file gave 7 failed, 1 passed
  (the `kafka` test), which agrees with my original 3-fail, 1-pass result.
- **Screenshots/logs:** the Jest failure messages quoted in Steps to Reproduce.
- **My findings:** all three bugs in the issue reproduced. The custom-level path already
  worked, so I had to keep it working. The `setLevel('nope')` case did more than report a
  wrong level: it moved the effective threshold to `info`.

**Retrospective reproduction (2026-10-23, after the merge)**

For Unit 6 I reproduced the issue again, after PR #51 had merged. I extracted the pre-fix
commit (`657e84e`) and the fix commit (`7b8c920`) into separate trees with `git archive`,
linked each tree's `node_modules` to my clone's install with a directory junction, and ran
a small Jest harness in both that records what it observes without asserting anything.
Environment: Windows 11, Git Bash, Node.js v24.14.0, npm 11.9.0.

| Case | Before the fix (`657e84e`) | After the fix (`7b8c920`) |
|---|---|---|
| `LOGIXIA_LEVEL=DEBUG` | `getLevel()` = `"DEBUG"`, debug line dropped | `"debug"`, debug printed |
| `level: 'warning'` | `"warning"`, ran at info, no warning | `"info"`, one warning |
| `warn`, then `setLevel('nope')` | `"nope"`, **info line printed** | `"warn"`, info dropped, one warning |
| `debug`, then `setLevel('nope')` | `"nope"`, **debug line dropped** | `"debug"`, debug printed, one warning |
| custom `kafka` | accepted, printed | same |
| custom `Kafka` (mixed case) | `logger.kafka()` prints nothing | same, not in #29's scope |

This confirmed by observation what I had found on 2026-10-18 by tracing the code:
`setLevel('nope')` doesn't keep the old threshold, it resets it to `info`. The full suite
gave the same results as before: 938 passed and 1 failed before the fix, 946 passed and 1
failed after, exit 1 both times, with the same Windows `EPERM` symlink test failing in
both. The harness, JSON output, and logs are saved in
`ai301-unit6-starter/repro-evidence/`.

**Retrospective claim draft (never posted).** I did not post a claim comment on #29 before
implementing the fix, even though CONTRIBUTING.md asks contributors to comment first. For
Unit 6 I wrote the claim I should have posted, `ai301-unit6-starter/claim-draft.md`,
labeled as a retrospective practice draft. It was never posted, and no maintainer saw or
approved it.

**Toolkit**

- Tool: Claude Code, used to draft the four regression tests from the issue's checklist,
  following the capture pattern in `src/utils/__tests__/internal-log.test.ts`.
- What it produced: a Jest file that spies on `process.stdout` and `process.stderr`,
  isolates the `LOGIXIA_*` environment variables per test, and asserts on `getLevel()`,
  logged output, and `[logixia:warn]` lines.
- Difficulties: a newly written test that fails is not proof by itself. The test could be
  wrong rather than the code. I checked that each failure message matched the bug the issue
  describes, and that the one passing test (`kafka`) was the case the issue says should
  already work.
- What changed: I kept only tests whose failure I could explain from the source, and kept
  the passing `kafka` test as a guard against breaking custom levels.

**Toolkit (Unit 6, retrospective claim and reproduction)**

- Tool: the voice guard (`check_voice.py --draft`) and repro-check with its wild scope.
- What it produced: the voice guard passed the claim draft twice (original and revised)
  and the final reproduction report once. repro-check first refused to grade, because the scout had no record of #29. After the
  retrospective scout grade, it accepted the claim draft, then rejected the full
  reproduction on `steps-reproducible`. After I revised it, the final verdict was accept,
  with all five checks passing.
- Difficulties: the first reproduction draft told readers to copy a harness they couldn't
  see, and `7b8c920` can't be fetched from a plain upstream clone. repro-check also
  flagged that my claim question didn't show what I had already checked.
- What changed: I embedded the full harness, added
  `git fetch https://github.com/Logixia/logixia.git pull/51/head`, said where every
  command runs and that `REPRO_OUT` is required, and added the evidence I had found in the
  code to the claim question.

---

## Solution Approach

**Analysis**

The root cause is that level strings were trusted everywhere they entered the logger:

- `resolveInitialLevel()` returned `process.env.LOGIXIA_LEVEL` or `levelOptions.level`
  unchanged.
- `_buildPerfCaches()` looked the level up with `this._levelValues.get(level) ?? 2`, so
  wrong case or a typo silently became `info`.
- `setLevel()` stored whatever it was given, and its own call to `_buildPerfCaches()` then
  turned an unknown level into an `info` threshold.
- `resolveEffectiveLevel()` returned `LOGIXIA_LEVEL_<NS>`, `namespaceLevels`, and
  `LOGIXIA_LEVEL` values unchecked as well.

**Proposed Solution**

Validate each level against the real level map (built-ins plus custom levels), canonicalize
it, and warn instead of failing silently:

- Add `canonicalLevel()`: try an exact match first, so custom levels keep their declared
  casing, then a lower-case match, so `DEBUG` maps to `debug`.
- Add `_validLevel(level, source)`: canonicalize config and environment values, and warn
  once per logger per `source=value` pair, listing the valid levels.
- Validate `levelOptions.level` in `_buildPerfCaches()` after the custom levels are
  registered, store the canonical form, and fall back to `info`.
- In `setLevel()`, refuse unknown levels: warn and return without touching
  `getLevel()` or `_minLevelValue`.
- Validate namespace and environment overrides in `resolveEffectiveLevel()`, so an invalid
  override falls through to the next source.

What I deliberately did not change: the public API and level names, the built-in numeric
values, the existing `info` fallback, and custom-level behavior. I also did not throw
errors on bad levels, because the issue asks for a warning and a fallback, and throwing
would break existing applications at startup.

**Implementation Plan**

1. Write the four issue tests in `src/core/__tests__/level-validation.test.ts` and confirm
   they fail for the right reasons.
2. Add `canonicalLevel()` and `_validLevel()` to `src/core/logitron-logger.ts`.
3. Validate and canonicalize `levelOptions.level` in `_buildPerfCaches()`.
4. Make `setLevel()` reject unknown levels and normalize valid ones.
5. Validate the namespace and environment overrides in `resolveEffectiveLevel()`.
6. Re-run the new tests, `custom-levels.test.ts`, typecheck, lint, and the full suite.

Deviations recorded during the build:

- **Added `setLevel('WARN')` and override tests.** The issue asked for four tests. While
  writing the fix I added a case-normalization test for `setLevel()` and tests for invalid
  `namespaceLevels` and `LOGIXIA_LEVEL_DB` overrides, because the fix changed those paths
  and they had no coverage.
- **Environment-override precedence fix (found in code review).** While reviewing my diff I
  found that `resolveInitialLevel()` still returned any non-empty `LOGIXIA_LEVEL` before it
  looked at `levelOptions.level`. With `LOGIXIA_LEVEL=chatty` and `level: 'warn'`, the
  invalid environment value replaced the valid configured level, and validation then fell
  back to `info` instead of `warn`. I changed `resolveInitialLevel()` to accept the
  environment value only if it matches a known level (built-ins plus custom keys);
  otherwise the configured level applies and `resolveEffectiveLevel()` reports the warning.
  I added an eighth test for this case. The PR description flags this behavior so the
  maintainer can weigh in.

**Toolkit**

- Tool: Claude Code, used to propose the implementation in `logitron-logger.ts` and to
  review the resulting diff with me.
- What it produced: the `canonicalLevel()` / `_validLevel()` helpers, the `setLevel()`
  guard, and validation in the override chain. The final change was 81 lines in
  `logitron-logger.ts` plus a 189-line test file.
- Difficulties: the first version passed all four issue tests but still had the
  environment-precedence defect. The tests passing did not mean the change was correct,
  because the tests only covered what the issue listed. I also had to make sure
  case-insensitive matching did not break custom levels with mixed-case names, which is
  why `canonicalLevel()` tries an exact match first.
- What changed: I fixed the precedence defect, grew the suite from four to eight tests to
  cover every path the fix touched, and re-ran the custom-level suite to confirm
  compatibility.

---

## Testing Strategy

I prove the fix with the same commands before and after, plus the repository's own checks:

- **Reproduction, before → after:** `npx jest src/core/__tests__/level-validation.test.ts
  --runInBand`. Before the fix, 3 of the 4 issue tests failed (only `kafka` passed). After
  the fix, all 8 tests in the final file passed. Each test asserts something observable:
  `getLevel()` returns the expected level, a message at the threshold appears in stdout, a
  message below it does not, and the number of `[logixia:warn]` lines is exact, so
  "warns once" is really checked.
- **Compatibility:** `npx jest src/core/__tests__/custom-levels.test.ts --runInBand`
  passed 31/31, so custom levels still behave as before.
- **Static checks:** `npm run typecheck` and `npm run lint` both passed, as the issue's
  acceptance criteria require.
- **Full suite:** `npx jest` gave 946 passing tests and 1 failure. The failure is the same
  Windows `EPERM` symlink test in `src/cli/__tests__/index.test.ts` that failed in my
  baseline (938 passing + 1 failing before; the 8 new tests account for the difference).
- **Upstream CI:** after a maintainer approved the runs, PR #51's checks passed for
  Quality (lint, typecheck, format), Test on Node 18, 20, and 22, Build, Bundle Size,
  CodeQL, and the Conventional PR title. `Dependency Review` failed; I haven't looked into
  why, and the PR was merged with that check failing. `Semantic Release` was skipped.
- **Retrospective rerun (2026-10-23):** the same commands on the fix commit gave the same
  results (8/8, 31/31, typecheck and lint clean, 946 passed and 1 failed with exit 1). A
  full run on the pre-fix commit gave 938 passed and 1 failed with exit 1, with the same
  `EPERM` test failing.

**Toolkit**

- Tool: Jest, TypeScript (`tsc --noEmit`), and ESLint, run locally. Claude Code helped me
  run them and read the output.
- What it produced: 8/8 new tests, 31/31 custom-level tests, clean typecheck and lint, and
  946 passing / 1 pre-existing failure in the full suite.
- Difficulties: the one Windows-only failure means I cannot honestly tick "full test suite
  passes". Without the baseline run, I could not have shown that the failure was
  pre-existing.
- What changed: I recorded the baseline before any edit, and I left the "full suite passes"
  box unchecked in the PR with an explanation instead of claiming a clean run.

---

## Implementation Notes

**2026-10-17**

Ran my first issue-scout wild scan (300 → 255 → 5 graded) and patched the rubric after
the Shelly hardware false positive. Graded sbt/website#553 through direct URL mode, posted
a claim comment, and cloned the site. I later dropped it without making changes.

**2026-10-18: setup and baseline**

Picked Logixia #29. Forked and cloned the repo, added `upstream`, and branched
`fix-level-validation-29`. `npm ci` failed because there is no lockfile, so I used
`npm install`. Baseline: typecheck and lint passed; Jest had 938 passing tests and 1
Windows `EPERM` symlink failure, which I noted as pre-existing.

**2026-10-18: reproduction**

Used Claude Code to walk through `logitron-logger.ts` and draft the four tests from the
issue. Result: 3 failed, 1 passed (`kafka`). Tracing the failures, I found that
`setLevel('nope')` also resets the threshold to `info` through `_buildPerfCaches()`, which
the issue text does not mention.

**2026-10-18: fix and review**

Added level canonicalization and validation, the warn-once set, the `setLevel()` guard,
and override validation. Reviewing the diff, I found the environment-override precedence
defect (an invalid `LOGIXIA_LEVEL` overriding a valid configured level), fixed it in
`resolveInitialLevel()`, and grew the suite to 8 tests. Final checks: 8/8, custom levels
31/31, typecheck and lint clean, full suite 946 passing + 1 pre-existing failure.

**2026-10-18: PR**

Committed `7b8c920` (`fix(config): validate and normalize log levels`), pushed the branch
to my fork, and opened PR #51 using the repository's pull request template. The PR title
check passed; the other workflows and the review were waiting on a maintainer.

**2026-10-23 (UTC): review and merge**

webcoderspeed, the repository's code owner, commented on PR #51: the fix "reads well", and
they agreed with letting an invalid `LOGIXIA_LEVEL` fall through to the next configured
level. They added a non-blocking note that `resolveInitialLevel()` could return the
canonical value. They merged PR #51 at 04:12:15 UTC as `2d0bcde`, and #29 closed as
completed.

**2026-10-23: Unit 6 retrospective work (after the merge)**

Installed the voice guard, switched to the wild scopes, patched the scout rubric, and wrote
`CLAUDE.local.md`. Graded #29 retrospectively (accept, moderate), drafted the claim I
should have posted, reproduced the issue on both commits, and revised both drafts until
repro-check accepted them. Nothing was posted.

**2026-10-23: Unit 7 retrospective ship-gate run (after the merge)**

Installed the official ship-gate, wrote a sourced `ship-manifest.md`, and prepared
retrospective `plan.md`, `test_evidence.md`, and `pr_draft.md` (PR #51's merged
description). Ran the gate once, through its manual doorway, against the already-merged
`fix-level-validation-29` branch: PASS, with 5/5 manifest checks and 6/6 pr-precheck
checks. The gate didn't exist when PR #51 was reviewed and merged, so it played no part in
the merge.

**2026-10-23: Unit 8 retrospective monitor run (after the merge)**

Installed the official PR-monitor and wrote my four-section playbook. Ran the monitor once
against PR #51, which was already merged: it detected MERGED and drafted a merged
follow-up. I reviewed the draft against the PR and issue #29, and decided not to post it,
because the PR was merged and #29 was closed. No comment was posted, and the monitor
played no part in the merge.

**Toolkit**

- Tool: Claude Code for code reading, test drafting, implementation, and diff review; git
  and the GitHub CLI for branch, commit, push, and PR.
- What it produced: commit `7b8c920` on `fix-level-validation-29` (2 files, +261/−9) and
  PR #51.
- Difficulties: the wrong turns were the missing lockfile, the gap between the issue text
  and the real `setLevel()` behavior, and the precedence defect that slipped past the first
  passing test run.
- What changed: I now treat "the tests Claude wrote pass" as the start of review, not the
  end. I read the diff myself and asked what inputs the tests did not cover.

---

## Pull Request

**PR Link:** https://github.com/Logixia/logixia/pull/51

**PR Description:** The PR is titled `fix(config): validate and normalize log levels` and
says `Closes #29`. It explains the three problems: upper-case levels were mishandled,
invalid levels were silently accepted, and `setLevel('nope')` could change the effective
threshold. It lists the changes: upper-case built-in levels are normalized while custom
names are preserved; configured, environment, and namespace levels are validated; invalid
config warns once per logger; invalid `setLevel()` calls are rejected without changing the
level; and eight regression tests are added. It calls out that invalid environment
overrides now fall through to the next configured level, and invites maintainer feedback
on that choice. The testing section lists the exact commands and results (8/8, 31/31,
typecheck, lint, full suite 946 passed / 1 failed) and names the Windows `EPERM` failure as
pre-existing. In the checklist, "full test suite passes locally" is left unchecked with
that explanation.

**Maintainer Feedback:**

- 2026-10-18: none when the PR was opened.
- 2026-10-23 (UTC): webcoderspeed, the repository's code owner, confirmed that upper-case
  environment levels work, that unknown levels warn once per source, and that
  `setLevel('nope')` leaves the threshold alone. They agreed with the fall-through for an
  invalid `LOGIXIA_LEVEL` ("ignoring a typo beats silently switching to it"). They also
  suggested that `resolveInitialLevel()` return the canonical value rather than `envLevel`
  as written, and said it was not a blocker. I didn't push a follow-up change; the PR
  merged with its single commit, `7b8c920`.

**Status:** Merged 2026-10-23 04:12:15 UTC by webcoderspeed (merge commit `2d0bcde`).
Issue #29 closed as completed at the same time.

**Toolkit**

- Tool: my pr-precheck habits from Unit 4 (match the PR to the issue's acceptance criteria,
  state test results exactly, flag anything unchecked), plus the repository's
  `.github/pull_request_template.md` and its Conventional Commits title check.
- What it produced: a PR description that maps each change to the issue and reports the
  real test results, including the one failure. The `Conventional PR title` check passed.
- Difficulties: I could not show a fully green CI run. When I opened the PR, four upstream
  workflows were waiting for maintainer approval (once approved, all passed except
  `Dependency Review`), and the local suite has one Windows-only failure.
- What changed: I stated both limits plainly in the PR instead of implying a clean run.
  The PR merged before the Unit 8 monitor existed.

---

## Learnings and Reflections

**Technical Skills Gained**

- Reproducing a bug as failing Jest tests before touching the code, and reading a failure
  message closely enough to tell a real bug from a bad test.
- Capturing `process.stdout` / `process.stderr` with `jest.spyOn` and isolating
  environment variables per test, so tests about `LOGIXIA_LEVEL` do not leak into each
  other.
- Tracing configuration precedence (environment → config → runtime → namespace overrides)
  through a real TypeScript codebase, and seeing how a cached value (`_minLevelValue`) can
  drift from the stored one.
- Designing validation that is backward compatible: canonicalize, warn once, fall back,
  and never throw.
- The fork, branch, `upstream`, Conventional Commits, PR-template flow on a real project.

**Challenges Overcome**

- `npm ci` failed with no lockfile; I switched to `npm install` and wrote down why.
- A Windows-only test failure could have looked like my regression. A baseline run before
  any edit let me prove it was pre-existing.
- The issue described `setLevel('nope')` as keeping the old threshold, but the code reset
  it to `info`. I trusted the code over the summary and documented the difference.
- The first implementation passed every test the issue asked for and was still wrong about
  environment-variable precedence. Reviewing the diff myself caught it, and I added a test
  so it stays fixed.

**What I'd Do Differently Next Time**

- Grade the issue with the scout and post my claim before I write any code. I did not post a
  claim on #29 before implementing, and for Unit 6 I had to grade it and draft its claim
  after the merge, which works as practice but is no substitute for a real claim on the
  thread.
- Release my earlier claim on sbt/website#553 as soon as I decide to move on, so
  maintainers are not left guessing.
- Commit the failing tests on their own before the fix, so the reproduction has its own
  commit link instead of living in the fix commit.
- Ask "which inputs does this not test?" right after the AI-drafted tests first pass, rather
  than discovering the precedence gap later in review.
- Check early whether CI on the target repo needs maintainer approval, so I can plan for a
  slower feedback loop.

---

## Resources Used

- Logixia issue #29, the checklist and hints I worked from:
  https://github.com/Logixia/logixia/issues/29
- `src/utils/internal-log.ts` and its tests, named in the issue's hints, for how
  `internalWarn` writes `[logixia:warn]` lines and how tests capture them:
  https://github.com/Logixia/logixia/blob/main/src/utils/internal-log.ts and
  https://github.com/Logixia/logixia/blob/main/src/utils/__tests__/internal-log.test.ts
- `src/core/__tests__/custom-levels.test.ts`, for how custom levels are configured and
  the 31 tests I re-ran for compatibility:
  https://github.com/Logixia/logixia/blob/main/src/core/__tests__/custom-levels.test.ts
- Logixia contributing guide and pull request template, for branch flow, tests, and the PR
  checklist: https://github.com/Logixia/logixia/blob/main/CONTRIBUTING.md and
  https://github.com/Logixia/logixia/blob/main/.github/pull_request_template.md
- My fork, branch, and commit: https://github.com/Disha-k-gowda/logixia/tree/fix-level-validation-29
  and https://github.com/Disha-k-gowda/logixia/commit/7b8c920
- My pull request: https://github.com/Logixia/logixia/pull/51

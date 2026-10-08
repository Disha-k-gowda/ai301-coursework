# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

**Where it lives:** In eval mode, read the plan-context block's scope, non-goals, files or components to change, implementation approach, and deviation notes against the candidate PR's unified diff and description. In live mode, read `plan.md`, including its `## Deviations` section, against the complete branch diff from `git diff main...HEAD` and the title and description in `pr_draft.md`.

**What good looks like:** Every material file and behavior changed by the diff falls inside the plan's stated boundary or is covered by an explicit deviation note, and required planned work is not silently omitted. An honest deviation can preserve fidelity when it states what changed and why. The PR description must also accurately represent the diff; claims that add, hide, or contradict material implementation scope are silent drift.

## Test evidence (harness category: not-tested)

**Where it lives:** In eval mode, read the candidate PR's test-evidence section against the plan-context block's test plan, the supplied reproduction evidence, and the repo-facts block's required checks. In live mode, read `test_evidence.md` against the test plan in `plan.md`, the Unit 2 reproduction evidence or applicable house repro evidence, and the repository checks required by `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`.

**What good looks like:** The evidence shows an observable before/after result, or an equivalent real-code result, that distinguishes the intended fixed behavior from the original problem. It also records the actual outcome of each required repository check rather than merely saying that tests pass. An honestly disclosed failure, unavailable check, or expected repository condition is evaluated by what it proves and does not automatically make the package unready.

## Diff quality (harness category: unreviewable)

**Where it lives:** In eval mode, read the candidate PR's complete unified diff and commit information, using the issue and plan context to identify the intended change. In live mode, inspect the complete output of `git diff main...HEAD` and the branch's commits, comparing every changed file and hunk with the issue, `plan.md`, and any deviation notes.

**What good looks like:** The intended fix is visible without unrelated material obscuring it, and every material changed hunk has a connection to the issue, accepted plan, or recorded deviation. Debug leftovers, generated debris, temporary files, dead or commented-out code, unrelated formatting churn, accidental edits, and drive-by cleanup are evidence that the diff may be unreviewable.

## Standards and comms (harness category: standards-wall)

**Where it lives:** In eval mode, read the repo-facts block's PR-template requirements, contribution policy, disclosure requirements, and thread instructions against the candidate PR title and description. In live mode, read `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`, and relevant maintainer instructions in the issue thread against `pr_draft.md`. Also read `voice-guide.md` for live-mode writing feedback, while remembering that voice affects the verdict only when a rubric check explicitly uses it.

**What good looks like:** The PR draft substantively satisfies the repository's stated submission requirements, including accurate issue linkage, change summary, truthful testing status, reviewer-relevant notes, and required AI-use disclosure. A truthful `N/A` is acceptable when a template request genuinely does not apply. Boilerplate, unsupported checked boxes, omitted required disclosure, or ignoring an explicit maintainer or repository requirement indicates a standards wall. Whether the description accurately matches the diff is graded under plan fidelity rather than here.
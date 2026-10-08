---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Grade exactly one PR package and answer one question: is this pull request ready to submit?

A PR package consists of the candidate PR title and description, the branch diff and commits, test evidence, and the plan the change claims to implement, including any recorded deviations. Read these artifacts against the issue the plan belongs to, the repository's PR template and contribution rules, and the evidence required by the rubric. Do not grade unrelated work or answer a different question.

## Inputs and modes

Run in exactly one of two modes.

- **Live mode:** grade the student's own submission. Read `plan.md`, including any deviation notes; the complete branch diff relative to the default branch using `git diff main...HEAD`; the draft PR title and description from `pr_draft.md`; the test evidence from `test_evidence.md`; and the issue the plan belongs to. Gather issue-side evidence from the real Path Review repository, including the issue thread, `.github/PULL_REQUEST_TEMPLATE.md`, and `docs/CONTRIBUTING.md`. Read the committed branch diff rather than relying on a description of the change. For a house-chain student, use the assigned house plan and house reproduction pack instead of a personal plan and reproduction history, while applying the same checks.
- **Eval mode:** treat the supplied package bundle as the whole world. Use only evidence contained in that bundle. Do not fetch GitHub, inspect a working directory, read outside files, or infer missing facts. Run every rubric check and apply the full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` before grading anything else. Use its `Repo:` entry to determine whether the PR targets the allowed Path Review repository and apply the house rules stated there.

Refuse to grade a PR outside the scoped repository. If the `Repo:` line still contains an unfilled placeholder, stop without grading and tell the student to fill that line with their section's Path Review repository. Never guess the repository.

In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` and check the outgoing PR title and description against its writing rules. Report any violated voice rule in the readable summary and identify the rule that was broken.

The voice guide does not change the final verdict by itself unless `rubric.md` contains a check that explicitly uses it.

In eval mode, ignore `voice-guide.md` entirely.

## Component reads

Read `rubric.md` to obtain the checks, their evidence requirements, pass conditions, weights, and the verdict rule.

Read `references/evidence-guide.md` to determine where each required evidence family can be found in a live PR package and in an eval bundle.

Execute `procedure.md` exactly as written. Use it to determine the read order, evidence gathering process, check execution, and verdict assembly. If the procedure is silent about a necessary step, report that gap rather than inventing a new procedure during the run.

If `rubric.md` contains no completed checks or `procedure.md` contains no completed operating steps, refuse to grade. State that the tool cannot produce a verdict without both a populated rubric and procedure.

## Verdict and output

Use only two final verdicts: `accept` means the PR package is ready to submit, and `reject` means it must be held.

A short readable summary may appear before the machine-readable result. End every completed grading response with the following fenced JSON block. It must be valid, must use this schema exactly, and nothing may appear after it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Gather evidence before assigning a grade. Every check must name the concrete fact or quote that determined its result. Do not use impressions such as "looks fine" as evidence.
- Grade the PR package itself, not its polish. A concise package can pass and a polished package can fail if its implementation drifts from the plan, lacks evidence, or violates repository requirements.
- Let `rubric.md` decide the grades and verdict. If a check satisfies its written pass condition, grade it accordingly even if intuition suggests otherwise. Fix weaknesses in the rubric rather than changing its meaning during a run.
- Let `procedure.md` decide how grading is performed. Follow it as written and report gaps instead of silently inventing steps.
- Grade unverifiable evidence as `unclear`. Apply the rubric's verdict rule to `unclear`; if the rubric does not specify how to handle it, treat `unclear` as a failure because an unverifiable PR package is not ready to submit.
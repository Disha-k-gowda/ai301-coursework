# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73

**Verdict output**

I'll load the issue-select skill to grade these against the rubric.

● Skill(issue-select)
Successfully loaded skill

I'll read the skill's scope and rubric first.

  Read 3 files, ran 2 shell commands

No gh CLI — I'll use the GitHub REST API directly.

  Ran 5 shell commands

Mode: live. Scope confirmed — all thw-ai301-fa26-s3, the scoped repo.Path Review house rule applied (classmate claim comments do not block).                 
One gap: scope.md's fit profile is still the placeholder (Write a few sentences here.). der accepted issues, never change cts stand as graded — but the ranking below falls back to the issues' own tier/label/effort signals rather than your preferencat section if you want a ranking tared evidence (all three candidate
- Last default-branch commit: 2026-09-16 by Aburke225 (non-bot) — 2 days before today → maintainer-active passes.
- Repo archived: false, pushed_at: 2026-09-16 → repo-active passes. (No releases published; last-push limb satisfies the check.)
- docs/CONTRIBUTING.md sets workflow/CI conditions, states no AI ban → contribution-policy passes.
- No pull requests exist in the repopty) → no linked or mentioned PRsanywhere.

Ranked read-out — 3 accepted, 0 rejected:

1. #73 — README / .env.example LLM key disagreement. tier-1, good first issue, docs-only two-file
   edit, 1–2 h, zero comments. Lowesarness, no xfail marker, no classmate activity.
2. #68 — ZeroDivisionError on empty irst issue, but 2–4 h and includesremoving a strict=True xfail marker. A classmate (acordero4852, association NONE) posted an investigation comment on 2026-09-t is not a claim, so unclaimedpasses; claim it yourself anyway.
3. #71 — indented heading-hierarchy l-specified, but tier-2 and carriesno good first issue label, so it ranks last on newcomer-friendliness despite the 1–2 h estimate.

json
[
  {
    "item": "https://github.com/code/issues/73",
    "checks": [
      {"name": "maintainer-active", "Last default-branch commit2026-09-16 by non-bot Aburke225, 2 days before capture; issue opened by Aburke225 (COLLABORATOR)."},
      {"name": "repo-active", "gradearchived: false; pushed_at2026-09-16, within 180 days."},
      {"name": "newcomer-scope", "gre outcome: 'Make the two files agree' across README.md and .env.example; est. 1-2 hours, no open design question."},
      {"name": "unclaimed", "grade":es: none; 0 comments; repo has nopull requests in any state."},
      {"name": "contribution-policy": "docs/CONTRIBUTING.md setsCI/testing conditions only; no AI-contribution ban stated."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/code/issues/68",
    "checks": [
      {"name": "maintainer-active", "Last default-branch commit2026-09-16 by non-bot Aburke225; issue author Aburke225 is COLLABORATOR."},
      {"name": "repo-active", "gradearchived: false; pushed_at2026-09-16, within 180 days."},
      {"name": "newcomer-scope", "grncrete bug: 'index([]) raisesZeroDivisionError' plus remove the H-01 xfail marker; two named files, est. 2-4 hours."},
      {"name": "unclaimed", "grade":gnee and no PRs exist; sole commentis classmate acordero4852 (association NONE), which the Path Review house rule says does not block."},
      {"name": "contribution-policy": "docs/CONTRIBUTING.md requiresgreen CI and xfail-marker removal but does not ban AI-assisted work."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/code/issues/71",
    "checks": [
      {"name": "maintainer-active", "Last default-branch commit2026-09-16 by non-bot Aburke225, within 90 days."},
      {"name": "repo-active", "gradearchived: false; pushed_at2026-09-16, within 180 days."},
      {"name": "newcomer-scope", "grngle specified fix: 'Remove theindentation' in test_extract_heading_hierarchy plus drop the H-04 xfail marker; est. 1-2 hours."},
      {"name": "unclaimed", "grade":es: none; 0 comments; no linked ormentioned PRs."},
      {"name": "contribution-policy": "docs/CONTRIBUTING.md imposesconditions (conventional commits, green CI), no AI ban."}
    ],
    "verdict": "accept"
  }
]
---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

agreement: 17/20 scored items

agreement: 2/3 scored items

agreement: 1/1 scored items

agreement: 18/20 scored items  (bar: 18/20: PASS)

agreement: 18/20 scored items  (bar: 18/20: PASS)

**Issue analysis**

issue-15: My rubric initially returned accept, while the gold label was reject. The issue passed my original checks because the repository was active, the issue appeared bounded, there was no current assignee, the linked pull requests were closed, and the contribution policy did not prevent the work. However, the issue had been open for more than two years and had multiple closed unmerged PRs or abandoned contribution attempts. I updated the newcomer-scope check to account for this evidence. After the revision, my rubric returned reject, matching the gold label.

**Check rationale**

> | newcomer-scope | Issue body and Comments section; Repo facts linked PRs for abandoned attempts | Pass if the issue has one coherent, clearly specified outcome that a contributor can implement without first resolving an open design decision. Documentation work may span multiple pages or include supporting updates and still counts as bounded when those changes serve one documented feature or workflow. A concrete bug may list multiple possible causes, implementation steps, or optional suggestions and still counts as bounded. Fail if it is explicitly an umbrella/tracking issue containing independent work items, a pure usage/support question, an unresolved design debate with no maintainer-set direction, work a maintainer explicitly says requires changes to core internals, or an issue open for more than 2 years with at least 2 closed unmerged PRs or clearly abandoned contribution attempts. | required |

I changed this check because my earlier version was too strict about some issues that involved multiple files or possible causes even though they still had one coherent outcome. At the same time, it was too permissive for an old issue with repeated abandoned attempts. The current version distinguishes between genuinely broad or unresolved work and a bounded task that simply requires changes in more than one place.

**Trade-offs**

The updated newcomer-scope check is more permissive for coherent multi-file work, but stricter for very old issues with repeated abandoned contribution attempts. I re-ran issue-01, issue-15, and issue-19 as canaries after changing the check. That targeted run reached 2/3. I then adjusted the check again and re-ran issue-01, which reached 1/1. The next full run reached 18/20. In that final run, issue-04 and issue-09 were still rejected by newcomer-scope even though their gold labels were accept. This is a trade-off I accept because the check remains conservative about first-issue scope while the overall rubric meets the 18/20 agreement bar.

---

## Selection rationale

1. Issue #73 fits my interests because it involves LLM configuration and documentation, and it is a small, clearly defined task. The estimated effort is 1–2 hours, which fits the time I have available for a first contribution.

2. The verdict correctly identified that the repository is active, the issue has one clear outcome, it is unclaimed, and the contribution policy does not prevent the work. I also considered that it is labeled good first issue and tier-1, involves only README.md and .env.example, and had no comments when I evaluated it.

3. I expect claiming the issue to be straightforward because it had no assignee and no comments when I ran the skill. The main difficulty is that its status could change before I claim it, so I will check the issue again before claiming it in Unit 2.


Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.

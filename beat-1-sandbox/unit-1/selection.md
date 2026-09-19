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

Mode: live, single candidate. Scope confirmed — issue is in
codepath/pathreview-ai301-fa26-s3, the only scoped source.

- maintainer-active — pass. Last default-branch commit 2026-09-16 by
  Aburke225, a non-bot, 2 days before the capture date; the issue's own
  author carries COLLABORATOR.
- repo-active — pass. archived: false, pushed_at: 2026-09-16, well inside
  180 days. (No releases exist; the last-push limb of the condition carries
  it.)
- newcomer-scope — pass. One stated outcome — "Make the two files agree" —
  over two named files, est. 1–2 hours, no open design decision and no
  core-internals warning.
- unclaimed — pass. No assignee, 0 comments, and the repo contains no pull
  requests in any state.
- contribution-policy — pass. docs/CONTRIBUTING.md sets conditions
  (conventional commits, green CI, xfail-marker removal) but states no ban
  on AI-assisted contributions.

Every required check passes, so the verdict rule accepts. This is the
cleanest of the candidates graded: docs-only, tier-1, good first issue, and
no test harness or xfail marker to untangle.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73",
  "checks": [
    {"name": "maintainer-active", "grade": "pass", "evidence": "Last default-branch commit 2026-09-16 by non-bot Aburke225, 2 days before capture; issue opened by Aburke225 (COLLABORATOR)."},
    {"name": "repo-active", "grade": "pass", "evidence": "Repo archived: false; pushed_at 2026-09-16, within 180 days of capture."},
    {"name": "newcomer-scope", "grade": "pass", "evidence": "Single outcome 'Make the two files agree' across README.md and .env.example; est. 1-2 hours, no unresolved design decision."},
    {"name": "unclaimed", "grade": "pass", "evidence": "assignees: none; 0 comments; repo has no pull requests in any state."},
    {"name": "contribution-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md sets CI/commit conditions only; no AI-contribution ban stated."}
  ],
  "verdict": "accept"
}
```

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

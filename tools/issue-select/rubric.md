# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-active | Repo facts: last 5 default-branch commits and maintainer first-response sample; issue Comments author_association | Pass if at least one of the last 5 default-branch commits is from a non-bot contributor within 90 days of the capture date, OR the maintainer first-response sample shows an Owner, Member, or Collaborator response within 30 days. | required |
| repo-active | Repo facts: archived flag, latest release, and last push to any branch | Pass if the repository is not archived AND either the latest release or last push occurred within 180 days of the capture date. | required |
| newcomer-scope | Issue body and Comments section; Repo facts linked PRs for abandoned attempts | Pass if the issue has one coherent, clearly specified outcome that a contributor can implement without first resolving an open design decision. Documentation work may span multiple pages or include supporting updates and still counts as bounded when those changes serve one documented feature or workflow. A concrete bug may list multiple possible causes, implementation steps, or optional suggestions and still counts as bounded. Fail if it is explicitly an umbrella/tracking issue containing independent work items, a pure usage/support question, an unresolved design debate with no maintainer-set direction, work a maintainer explicitly says requires changes to core internals, or an issue open for more than 2 years with at least 2 closed unmerged PRs or clearly abandoned contribution attempts. | required |
| unclaimed | Repo facts: this issue assignees and linked PRs; Comments section for claim statements and PR mentions | Pass if the issue has no assignee, no open linked or mentioned PR, and no comment showing another contributor is currently working on the issue. Closed unmerged PRs or clearly abandoned attempts do not count as active claims. | required |
| contribution-policy | Repo facts: contribution policy, including CONTRIBUTING.md, AI policy files, linked contributor documentation, and templates | Pass unless the contribution policy explicitly bans AI-generated or AI-assisted contributions. Policies requiring disclosure, testing, personal understanding, or human review pass. If no AI policy is stated, pass. | required |

## Verdict rule

Accept the issue only if every required check passes. A failed required check rejects the issue. If the available evidence is insufficient to determine whether maintainer-active, repo-active, newcomer-scope, or unclaimed passes, treat unclear as fail. For contribution-policy, absence of an AI policy passes because the evidence guide explicitly states that silence is not a restriction.

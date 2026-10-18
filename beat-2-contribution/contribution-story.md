# Contribution: TestsListener link from Testing page is broken.

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Disha Kempegowda
**GitHub Username:** Disha-k-gowda
**Issue:** https://github.com/sbt/website/issues/553
**Pull Request:** Not opened yet

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Wrote my issue-scout search strategy and patched the rubric after the first wild scan**

I wrote three `gh search` queries tied to my fit profile (Python and JavaScript
good-first-issues, TypeScript help-wanted) plus ranking filters, and my first scan on
2026-10-17 pulled 300 issues, kept 255 after dropping assigned and translation issues, and
graded the top 5 as four accepts and one reject. The rubric accepted
yfridelance/shelly-manager#7 even though it can only be tested on a real Gen1 Shelly device,
which my profile says to avoid. I added a newcomer-scope fail condition for work that needs
physical hardware unless the issue says a mock or emulator is enough, logged it in
scan-notes.md without rerunning the scan, and noted that all five top results tied at 0
comments, so update time picked brand-new issues from tiny repos, a strategy fix still open.
I then claimed and graded Logixia/logixia#119 and sbt/website#553, and both passed the
required checks.

**Unit 6: [one line on the tool work]**

[2-4 sentences: the voice-guard, the repo-memory file. What broke or
fell short, and what changed because of it. "Nothing broke" counts when
it is true - say how you know.]

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

My first issue-scout scan ran my three `gh search` queries across GitHub, pulled 300
issues, kept 255 after filtering out assigned and translation issues, and graded the top
five: four accepts and one reject. I did not pick this issue from that scan. I found
sbt/website#553 separately through the CodePath tracker and ran it through issue-scout's
direct URL grading mode, which accepted it against the same rubric. The issue is that the
TestsListener link on the sbt Testing documentation page is broken, so the work is a small,
well-defined documentation fix: find where the link should point and correct it.

That size fits where I am as a software engineer making a first open-source contribution. I
am comfortable reading and editing code and Markdown, but I have not yet been through a real
project's contribution flow, so a scoped docs fix lets me focus on that flow instead of on a
large code change. I hope to learn how the sbt website is built and organized, how to check
my change locally before submitting it, and how to work with maintainers through review on
an established project. As for the tool: the scout held up on this issue, but the wild scan
showed two real gaps, which I describe in the Toolkit block below. Claim comment:
https://github.com/sbt/website/issues/553#issuecomment-6243471487

**Toolkit**

- Tool: issue-scout, run first as a wild GitHub scan using my written search strategy and
  rubric, then in direct URL grading mode on sbt/website#553 after I found it through the
  CodePath tracker.
- What it produced: The wild scan searched 300 issues, kept 255, and graded five (four
  accepted, one rejected). Direct URL grading accepted sbt/website#553 against the rubric.
- Difficulties: The rubric accepted yfridelance/shelly-manager#7, a false positive because
  it can only be tested on a real Gen1 Shelly device, which my fit profile says to avoid.
  Search ranking also fell short: all five top results tied at 0 comments, so update time
  decided the order and pushed brand-new issues from tiny repos to the top.
- What changed: I added a newcomer-scope fail condition to the rubric for work that needs
  physical hardware unless the issue says a mock or emulator is enough. The search-ranking
  limitation is still open; I would add a ranking signal beyond comments and update time,
  such as repository activity, so ties do not favor brand-new issues in tiny repos.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]

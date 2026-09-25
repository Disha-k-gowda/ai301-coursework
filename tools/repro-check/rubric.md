# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment-recorded | The repro report's environment record, read against any environment or version requirements stated in the issue and repo-facts block. | Pass if the environment records the relevant software, version, platform, configuration, or other conditions needed for another person to understand the setup used for the reproduction. Fail if a material environment detail needed to interpret or repeat the result is missing or contradicted. | required |
| steps-reproducible | The reproduction steps in the repro report, together with commands, inputs, setup actions, and referenced artifacts needed to perform them. | Pass if a stranger could follow the recorded setup and actions in order without having to invent a material command, input, configuration, or transition. Fail if a missing or ambiguous action prevents the reported outcome from being independently attempted. | required |
| behavior-matches-issue | The observed output, logs, screenshots, or other artifacts in the repro package read against the behavior described by the issue. | Pass if the evidence demonstrates the specific behavior the issue describes, or provides concrete evidence that the specific behavior could not be reproduced. Fail if the evidence demonstrates only an adjacent, different, or unrelated behavior. | required |
| outcome-honest | The repro report's stated outcome read against its observed artifacts and reproduction evidence. | Pass if the stated conclusion is supported by the evidence, including an honestly evidenced cannot-reproduce result. Fail if the report claims reproduction, non-reproduction, or another conclusion that the supplied evidence does not support. | required |
| repo-conventions | The claim comment and repro comment read against repository contribution or communication requirements identified in repo-facts and the conventions sources listed in references/evidence-guide.md. | Pass if the comments satisfy the repository-specific requirements actually stated in the supplied evidence. Apply only requirements that the repository explicitly imposes; do not invent stricter disclosure or formatting requirements. If the repository requires an AI-use disclosure, verify that a disclosure is present and includes each detail the repository explicitly requires. For example, if the repository requires the AI tool and extent of assistance to be disclosed, both must be stated. Fail if an explicitly required disclosure, disclosure detail, template field, contribution requirement, or other applicable convention is missing or contradicted. | required |

## Verdict rule

Accept only if every required check passes. Reject if any required check fails or is unclear. Preferred checks, if any are added later, never change the final verdict. The final verdict is binary: accept or reject.
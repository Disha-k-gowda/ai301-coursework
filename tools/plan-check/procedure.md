# Procedure: how this skill grades a plan package

## Read order

1. Read the reproduced evidence first. Record the expected behavior, the observed failure, the exact reproduction path or commands, relevant inputs, and any evidence that identifies or narrows the cause. Do not use the plan's diagnosis to reinterpret the reproduction evidence.
2. Read the issue and thread highlights next. Record maintainer requests, explicit constraints, clarifications, and any scope decisions that the plan must respect.
3. Read the repo-facts and repository-conventions information. Record relevant file locations, test commands, contribution rules, and conventions that constrain how the change should be implemented or described.
4. Read the full plan after the evidence above is recorded. Extract the stated diagnosis, scope, non-goals, files to touch, implementation approach, test plan, risks, assumptions, and unknowns.
5. Read the draft plan comment last. Record the diagnosis, scope, approach, testing claims, and any statements about issue or repository requirements that will be visible when the comment is posted.
6. Keep the facts gathered from the reproduction, thread, and repo separate from claims made by the plan. Use the former to evaluate the latter.

## Evidence gathering

1. For diagnosis-grounded, compare the plan's stated cause with the reproduced expected behavior, observed behavior, commands, inputs, and output. Record the specific reproduction fact that supports or conflicts with the diagnosis.
2. For scope-bounded, collect every proposed file, component, behavior change, cleanup, refactor, feature, and explicit non-goal from the plan. For each proposed change, record whether the plan connects it directly to the reproduced problem.
3. For cause-targeted, record the diagnosed cause and the concrete behavior the proposed implementation changes. Determine whether changing that behavior would remove the diagnosed cause rather than only suppress the visible failure.
4. For executable, record the files or components the plan says will change and the implementation behavior described for each. Compare these with repo facts and conventions. Record any basic implementation decision that would still have to be discovered before another contributor could begin.
5. For test-observable, record the original reproduction path, its failing observable result, the plan's post-fix test command or steps, and the expected post-fix observable result. Determine whether the planned result would distinguish fixed behavior from the reproduced failure.
6. For unknowns-honest, record every explicit risk, assumption, and unknown in the plan. Also record material gaps visible in the evidence that could change the implementation or test strategy. Determine whether each material gap is acknowledged or already resolved by package evidence.
7. For thread-conventions, compare the draft plan comment with the recorded issue-thread constraints and repository conventions. Record any direct agreement, omission, or contradiction that affects the proposed change.
8. Use only evidence available in the package in eval mode. In live mode, gather external evidence only from the locations allowed by scope.md and references/evidence-guide.md.

## Check execution

1. Grade the checks in this order: diagnosis-grounded, scope-bounded, cause-targeted, executable, test-observable, unknowns-honest, then thread-conventions.
2. For each check, use only the evidence named for that check in rubric.md and gathered by the corresponding evidence-gathering step. Do not fail a check because unrelated information is absent.
3. Apply the pass condition in rubric.md literally. Grade pass only when the available evidence establishes the pass condition.
4. Grade fail when the available evidence establishes a condition that the rubric explicitly identifies as a failure.
5. Grade unclear when evidence required to decide the check is genuinely absent, incomplete, or internally unresolved. Do not invent missing facts or resolve uncertainty in the plan's favor.
6. Do not turn unclear into fail during individual check execution. Preserve the grade as unclear so the output shows that the package lacked enough evidence; the verdict rule will determine its effect.
7. Once the evidence needed for a check has been gathered, grade from those recorded facts without re-reading unrelated parts of the package. Re-read a source only when two recorded facts conflict or the exact wording is needed to decide the pass condition.
8. For every fail or unclear grade, identify the smallest specific piece of evidence or missing evidence that caused that grade. For a pass, identify the evidence that directly satisfies the condition.

## Verdict assembly

1. Collect the final grade for every rubric check as pass, fail, or unclear.
2. Apply the verdict rule from rubric.md exactly: accept only when every required check passes.
3. Treat any required unclear grade as verdict-blocking in the same way as a required failure. Preferred checks, if any are added later, never change the verdict.
4. If all required checks pass, return accept.
5. If one or more required checks fail or are unclear, return reject.
6. For a reject verdict, quote or point to the smallest evidence excerpt for the first verdict-blocking check in rubric order. If that check is unclear because evidence is absent, state exactly what evidence is missing instead of inventing a quote.
7. For an accept verdict, cite the strongest evidence supporting each required check and keep the explanation tied to the rubric's pass conditions.
8. End with the required structured output and JSON verdict defined by SKILL.md. Do not introduce a third verdict or override the rubric because the plan seems generally reasonable.

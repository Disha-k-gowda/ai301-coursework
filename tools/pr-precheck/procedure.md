# Procedure: how this tool grades a PR package

## Read order

1. In live mode, read `scope.md` first and confirm that the candidate PR targets the scoped Path Review repository. Record the repository rules that apply. In eval mode, ignore `scope.md`.
2. Read the issue and issue-thread evidence next. Record the expected behavior, reproduced problem, maintainer constraints, clarifications, and scope decisions relevant to the implementation.
3. Read `plan.md`, including all deviation notes. Record the planned scope, non-goals, files or components to change, implementation approach, and test plan. Establish this boundary before reading the diff so the implementation does not redefine what the plan originally promised.
4. Read the complete branch diff using `git diff main...HEAD` in live mode, or the supplied diff in eval mode. Record every changed file, material changed behavior, unrelated-looking hunk, generated artifact, debug change, or other content that may affect reviewability.
5. Read `test_evidence.md`. Record the issue-specific before/after evidence or equivalent observable evidence, each repository check that was run, its actual result, and any disclosed failure, unavailable check, or expected repository condition.
6. Read the draft PR title and description from `pr_draft.md`. Record its summary of the change, issue linkage, change claims, testing claims, limitations, deviations, AI-use disclosure, and any statements about repository requirements.
7. Read the repository standards evidence: `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`, and relevant issue-thread requirements in live mode, or the corresponding repo-facts and standards evidence in the eval bundle.
8. In live mode, read `voice-guide.md` and record any rule the PR title or description violates. Keep voice findings separate from rubric grades unless a rubric check explicitly uses the voice guide.
9. Keep observed evidence separate from claims. In particular, do not use the PR description to decide what the diff contains, and do not use a testing claim as proof that a command actually ran.

## Evidence gathering

1. For `plan-fidelity`, list the material files and behavior changed by the diff and compare each with the scope, non-goals, implementation approach, and deviation notes in `plan.md`. Record any changed work that is outside the plan, any required planned work missing from the diff, and whether a material difference is explicitly documented as a deviation.
2. For `description-fidelity`, compare every material claim in the draft title and description with the actual diff, issue, plan, and recorded deviations. Record any claim that accurately describes the implementation and any contradiction, omission, or hidden limitation that could mislead a reviewer.
3. For `test-evidence`, pair the plan's issue-specific test strategy with the evidence in `test_evidence.md`. Record the original failing observable behavior and the post-change observable result, or an equivalent real-code result that distinguishes the fixed behavior from the original problem. Record disclosed testing shortfalls without automatically treating them as failures.
4. For `repo-checks`, obtain the required repository checks from the PR template and contribution rules. For each required check, record whether it was run and its exact reported outcome in `test_evidence.md`. Distinguish an honest expected or unrelated non-passing result from a missing, hidden, or unsupported testing claim.
5. For `diff-reviewable`, inspect every changed file and hunk in the complete diff. Record unrelated cleanup, generated debris, temporary files, debug artifacts, accidental edits, or unrelated changes that make the intended change harder to review. Also record when every changed hunk has a direct connection to the issue, accepted plan, or recorded deviation.
6. For `standards-compliant`, compare the draft PR title and description with the PR template, `docs/CONTRIBUTING.md`, and relevant issue-thread requirements. Record whether required information is substantively present, including issue linkage, truthful testing status, required disclosure, and any applicable reviewer notes. Treat a truthful `N/A` as evidence when the requirement genuinely does not apply.
7. In eval mode, gather evidence only from the package bundle. Do not fetch or infer anything outside it. In live mode, gather evidence only from the locations permitted by `scope.md` and `references/evidence-guide.md`.

## Check execution

1. Grade checks in rubric order: `plan-fidelity`, `description-fidelity`, `test-evidence`, `repo-checks`, `diff-reviewable`, then `standards-compliant`.
2. For each check, use only the evidence named for that check in `rubric.md` and gathered by the corresponding evidence-gathering step.
3. Apply each pass condition literally. Grade `pass` when the available evidence establishes the pass condition.
4. Grade `fail` when the available evidence establishes a failure condition stated by the rubric.
5. Grade `unclear` when evidence required to decide the check is genuinely absent, incomplete, contradictory, or unverifiable. Do not invent missing facts or assume that an unsupported claim is true.
6. Preserve `unclear` as the individual check grade. Do not rewrite it as `fail` in the checks output; the verdict rule determines its verdict effect.
7. Honest disclosure alone is not a failure. When a package explicitly records a deviation, limitation, failed check, unavailable check, or expected repository condition, judge the underlying outcome using the rubric's pass condition instead of rejecting it merely because a shortfall exists.
8. Once the necessary evidence for a check has been gathered, grade from those recorded facts without re-reading unrelated material. Re-read a source only when recorded facts conflict or exact wording is necessary to apply the pass condition.
9. For every check, record one concise evidence line containing the fact, quote, comparison, or missing evidence that decided the grade.

## Verdict assembly

1. Collect the final `pass`, `fail`, or `unclear` grade for every rubric check.
2. Apply the verdict rule in `rubric.md` exactly. Accept only when every required check passes.
3. Treat every required `unclear` grade as verdict-blocking, just like a required failure. Preferred checks, if added later, never change the verdict.
4. Return `accept` when all required checks pass.
5. Return `reject` when one or more required checks fail or are unclear.
6. For a reject verdict, identify the first verdict-blocking required check in rubric order as the primary deciding check. Quote or point to the smallest specific evidence that caused it. If it is unclear because evidence is absent, state exactly what evidence is missing.
7. When multiple required checks block the verdict, still report the evidence for each check in the structured output, while using the first blocking check in rubric order as the primary explanation.
8. For an accept verdict, provide a concise evidence line showing why each required check satisfied its pass condition.
9. In live mode, include any voice-guide violations in the readable summary without changing the verdict unless a rubric check makes that violation verdict-relevant.
10. End with the exact structured JSON output required by `SKILL.md`. Do not add text after the JSON block and do not create a third verdict.
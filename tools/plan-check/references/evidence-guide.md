# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

**Where it lives:** In eval mode, read the candidate plan's diagnosis or stated cause together with the package's repro-evidence block, especially the expected behavior, observed behavior, reproduction steps, commands, inputs, and output. In live mode, read the diagnosis in `plan.md` and `comment.md` against the reproduction evidence posted on the issue during Unit 2.

**What good looks like:** The stated cause explains behavior that the reproduction evidence actually demonstrates and does not contradict the observed output. A diagnosis that only repeats the visible symptom, introduces a cause with no supporting evidence, or conflicts with the reproduction is not sufficiently grounded.

## Scope

**Where it lives:** In eval mode, read the candidate plan's scope statement, non-goals, files or components to change, and implementation approach. Compare those with the reproduced problem and any relevant issue constraints. In live mode, use the scope, files-to-touch, non-goals, and approach in `plan.md` and the corresponding claims in `comment.md`.

**What good looks like:** The proposed work forms one bounded change directed at the reproduced problem, and each named file, component, or behavior has a stated or evident role in that fix. Unrelated cleanup, broad refactoring, extra features, or changes without a demonstrated connection to the issue indicate scope creep.

## Executability

**Where it lives:** In eval mode, read the candidate plan's files-to-touch and implementation approach together with the repo-facts block and any stated repository conventions. In live mode, read those parts of `plan.md` against the actual repository locations and relevant contribution or implementation conventions identified by the evidence guide.

**What good looks like:** Another contributor can identify where to begin and what behavior to change without first having to discover the basic implementation strategy. The plan should identify the relevant code, documentation, configuration, or tests and explain the intended behavior of the change, while leaving ordinary coding details to implementation.

## Test plan

**Where it lives:** In eval mode, read the candidate plan's test plan against the package's repro-evidence block, including the original reproduction steps, inputs, commands, failing output, and expected behavior. In live mode, compare the test plan in `plan.md` with the Unit 2 reproduction steps and evidence.

**What good looks like:** The test plan re-runs the relevant reproduction path, or an equivalent check through the real code, and names an observable post-fix result that differs from the reproduced failure. A statement such as "run tests," "verify the fix," or "make sure it works" is not decisive unless it identifies what result will demonstrate that the reproduced behavior changed correctly.

## Honesty

**Where it lives:** In eval mode, read the candidate plan's risks, assumptions, unknowns, and any deviations together with unresolved gaps visible in the repro evidence and implementation approach. In live mode, use the risks and unknowns in `plan.md`; after implementation, also read the `## Deviations` section for differences between the posted plan and the actual build.

**What good looks like:** Material uncertainty that could change the implementation or test strategy is either explicitly acknowledged or resolved by evidence already available. The plan must not present an unresolved material assumption as established fact. After the build, a real departure from the plan is recorded under Deviations with what changed and why; if nothing changed, that is stated explicitly.

## Comms

**Where it lives:** In eval mode, read the candidate plan comment against the issue context, thread highlights, repo-facts block, contribution policy, templates, and any stated AI-use disclosure requirements included in the package. In live mode, read `comment.md` against the GitHub issue thread, maintainer comments, repository contribution documentation, and relevant repository conventions.

**What good looks like:** The comment reflects the student's own diagnosis, bounded scope, implementation approach, and test intent while respecting relevant maintainer requests and repository rules. It must not contradict thread constraints, ignore a relevant contribution requirement, claim unsupported certainty, or substitute boilerplate such as "same approach as above" for the student's own plan.

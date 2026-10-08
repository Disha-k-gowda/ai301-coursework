# Voice guide: how I talk upstream

## Who I am in threads and pull requests

I am a student contributor learning to work with an existing codebase and its maintainers. I describe what I actually changed and tested rather than presenting assumptions as facts. My pull requests should make it easy for a reviewer to understand the issue, the implementation, the evidence, and any limitations or deviations.

## Rules I write by

### Rule: Say only what I have done

In a pull request, I describe completed work and actual test results. I do not claim a change, test, or result that is not present in the diff or test evidence.

- Wrong: "All tests pass." when the required checks were not run.
- Right: "Unit tests, lint, and type checking passed. The integration command reported no tests collected."

### Rule: Name the specific issue

I describe the actual behavior, configuration, documentation, or code changed instead of using generic PR language.

- Wrong: "This PR fixes the issue."
- Right: "This PR adds the `OPENROUTER_API_KEY` placeholder to `.env.example` so it matches the existing setup documentation."

### Rule: Report evidence, not assumptions

Testing statements should identify observable results. If a check failed, was unavailable, or produced an expected repository condition, I state that accurately instead of hiding it.

- Wrong: "Everything works correctly now."
- Right: "After the change, the copied environment example contains `LLM_PROVIDER`, `OPENAI_API_KEY`, and `OPENROUTER_API_KEY`."

### Rule: Keep the title specific

The PR title should identify the type and purpose of the change without exaggerating its scope. I use the repository's naming conventions when they are stated.

- Wrong: "Fix everything"
- Right: "docs: add OpenRouter API key example for #73"

### Rule: Keep the description faithful to the diff

The description should explain what actually changed, not what I originally hoped to change. If implementation departed materially from the posted plan, I disclose the deviation.

- Wrong: "Updated configuration handling and provider selection." when the diff only changes `.env.example`.
- Right: "Added the existing `OPENROUTER_API_KEY` setting to `.env.example`; runtime provider-selection behavior was not changed."

### Rule: Be honest about testing

I do not check boxes or claim success without evidence. A failed, unavailable, or non-applicable check is reported as such rather than converted into a success.

- Wrong: Checking "Integration tests pass" when the command reported no tests collected.
- Right: "Integration check: command ran and reported no tests collected."

### Rule: Respect repository requirements

I follow the repository's PR template, contribution instructions, issue-thread requirements, and disclosure rules. I include required AI-use disclosure rather than treating it as optional.

- Wrong: Leaving out a required disclosure because the code change is small.
- Right: "I used AI assistance while preparing and reviewing this change."

### Rule: Keep reviewer notes useful

Notes for reviewers should identify boundaries, deviations, limitations, or details that materially help review. I do not fill them with generic requests to review the PR.

- Wrong: "Please review and let me know what you think."
- Right: "This change is intentionally limited to `.env.example`; it does not alter runtime provider-selection behavior."

## Things I never post

- A test result I did not actually observe.
- A claim about behavior that the diff does not support.
- A description that hides a material deviation from the posted plan.
- Unsupported checked boxes in the PR template.
- Generic wording that could describe any pull request.
- A required AI-use disclosure left out because the change seems small.
- Blame toward the issue author, maintainers, or other contributors.
- A title that exaggerates the scope of the change.
- A claim that all checks pass when the evidence shows otherwise.
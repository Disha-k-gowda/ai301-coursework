# Unit 2 — Claim and Reproduce

## Issue

Issue #73: README and .env.example disagree about which LLM API key to set

Repository: codepath/pathreview-ai301-fa26-s3

---

## Claim

**Claim link:**  
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73#issuecomment-5840096614

**Claim text:**

Hi! I’d like to investigate #73. I’ll compare the `OPENROUTER_API_KEY` setup described in `README.md` with the variables and `LLM_PROVIDER` options in `.env.example`, then check `core/config.py` to see which OpenRouter settings are actually defined. I’ll follow the documented setup and report the environment, steps, and what I observe, including if the reported mismatch cannot be reproduced.

---

## Reproduction

**Reproduction link:**  
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73#issuecomment-5840160122

**Reproduction text:**

### Reproduction report

**Outcome:** Reproduced

**Environment**
- OS: Microsoft Windows NT 10.0.26200.0
- Repository: `codepath/pathreview-ai301-fa26-s3`
- Commit: `2f4e82f52efbcfcc57d65b3fa5348672163ca088`
- Branch: `main`

**Steps**
1. Checked the README configuration instructions:
   `Select-String -Path README.md -Pattern "OPENROUTER_API_KEY|OPENAI_API_KEY|LLM_PROVIDER" -Context 2,2`
2. Checked the example environment file:
   `Select-String -Path .env.example -Pattern "OPENROUTER_API_KEY|OPENAI_API_KEY|LLM_PROVIDER" -Context 2,2`
3. Checked the application configuration:
   `Select-String -Path core/config.py -Pattern "OPENROUTER|OPENAI|LLM_PROVIDER" -Context 2,2`
4. Checked the setup documentation:
   `Select-String -Path docs/SETUP.md -Pattern "OPENROUTER_API_KEY|OPENAI_API_KEY|LLM_PROVIDER" -Context 2,2`

**Observed behavior**
- `README.md:24` says to add `OPENROUTER_API_KEY` to `.env`.
- `docs/SETUP.md:47` also says to set `OPENROUTER_API_KEY`.
- `.env.example:17` documents the `LLM_PROVIDER` options as only `"mock"` and `"openai"`.
- `.env.example:18-19` sets `LLM_PROVIDER=mock` and provides `OPENAI_API_KEY`, but does not provide `OPENROUTER_API_KEY`.
- `core/config.py:18-22` defines `llm_provider`, `openai_api_key`, `openrouter_api_key`, `openrouter_base_url`, and `openrouter_model`.

**Conclusion**

I reproduced the reported documentation/configuration mismatch. The setup documentation directs users to configure `OPENROUTER_API_KEY`, while `.env.example` does not include that variable and does not document OpenRouter as an `LLM_PROVIDER` option, even though the application configuration defines OpenRouter settings.

---

## Reflection

The main challenge in this assignment was making the rubric strict enough to reject unsupported reproduction packages without making it stricter than the repository's actual requirements. I initially treated disclosure requirements too broadly. Testing against targeted evaluation packages showed that a repository may allow AI assistance without requiring the contributor to name a specific AI product. I refined the `repo-conventions` check so that it enforces only requirements explicitly stated by the repository while still requiring every detail that the repository explicitly asks contributors to disclose.

For the live issue, I kept the claim separate from the reproduction. The claim described what I intended to investigate without stating that I had already reproduced the problem. I then reproduced the issue using my own fork and evidence. The mismatch was visible directly in `README.md`, `.env.example`, `core/config.py`, and `docs/SETUP.md`, so I did not need to claim a runtime failure that I had not tested.

---

## Run history

### Initial smoke test
I first ran the evaluator on `pkg-01`, `pkg-02`, and `pkg-03` using my completed rubric and evidence guide. All three matched their gold labels, giving 3/3 agreement. This provided an initial check that the rubric could distinguish a clear acceptance from rejection cases, including the wrong-target case represented by `pkg-02`. I made no rubric changes after this run.

### First full evaluation
I then ran all 20 evaluation packages. Three packages, `pkg-04`, `pkg-07`, and `pkg-11`, failed to complete because the Windows PowerShell/Python environment was using `cp1252` output encoding and encountered characters it could not encode. Of the 17 packages that completed, 16 matched their gold labels. The substantive mismatch was `pkg-20`, which was accepted by my rubric even though its gold label was reject.

Because the three package errors were an execution-environment problem rather than a rubric problem, I did not change the rubric in response to them. I set `PYTHONUTF8=1` and `PYTHONIOENCODING=utf-8`, verified that Python was using UTF-8 for input and output, and reran only `pkg-04`, `pkg-07`, and `pkg-11`. All three then matched their gold labels.

### Disclosure-rule revision
I inspected `pkg-20` to determine why it was misclassified. The package's repository facts explicitly required AI use to be disclosed and required the disclosure to state the tool used and the extent of assistance. The candidate communication contained no AI disclosure. I strengthened `repo-conventions` so that an explicitly required repository disclosure and its required details would be mandatory.

I then reran `pkg-20` together with `pkg-01`, `pkg-02`, and `pkg-07` as canaries. `pkg-20` changed from the incorrect accept to the correct reject, while `pkg-01` and `pkg-02` remained correct. However, `pkg-07` regressed from accept to reject.

### Refining the repository-conventions rule
I inspected `pkg-07` to understand the regression. Its repository allowed assistive AI use and required the contributor to understand and take responsibility for the contribution, but it did not explicitly require the disclosure to name a particular AI product. The candidate had disclosed AI assistance and stated that the work was personally run, verified, and understood. My previous revision had therefore become stricter than the repository itself.

I changed `repo-conventions` again so that it applies only requirements explicitly imposed by the repository and does not invent additional disclosure or formatting requirements. At the same time, when a repository explicitly requires particular disclosure details, every stated detail remains mandatory.

I reran the same targeted set: `pkg-20`, `pkg-01`, `pkg-02`, and `pkg-07`. All four then matched their gold labels. This showed that the revised rule rejected the missing required disclosure in `pkg-20` without incorrectly rejecting the acceptable disclosure in `pkg-07`.

### Final confirming evaluation
After the targeted checks passed, I ran the complete 20-package evaluation again and saved it using `--save-run eval-run.txt`. The final run matched all 20 gold labels.

Category results were:
- clear-accept: 8/8
- disclosure: 1/1
- no-evidence: 4/4
- unfollowable-comms: 3/3
- wrong-target: 4/4

Final agreement was 20/20, which passed the 18/20 target and every category floor. The harness-generated confirming run is submitted separately as `eval-run.txt`.

---

## Package analysis

The most informative packages for refining my rubric were `pkg-20` and `pkg-07`.

`pkg-20` exposed an under-specified repository-conventions check. The reproduction evidence itself was strong, but the repository explicitly required AI-use disclosure, including the tool used and extent of assistance. Because the candidate omitted that required disclosure, a rubric that focused only on technical reproduction quality incorrectly accepted the package. This showed that repository communication requirements must be treated as part of the evidence package rather than as optional style preferences.

`pkg-07` exposed the opposite failure mode. After tightening the disclosure rule for `pkg-20`, my rubric became too broad and rejected a package even though its repository did not explicitly require the extra disclosure detail I had started demanding. This package demonstrated why the check must be repository-specific: the evaluator should enforce what the repository actually requires, not a universal disclosure format invented by the rubric.

Together, these packages led to the final rule: repository-specific requirements are mandatory when explicitly stated, but unstated requirements must not be added by the evaluator.

---

## Check rationale

### environment-recorded
This check exists because reproduction results can depend on software versions, platforms, configuration, or other environmental conditions. A report should record the material conditions needed for another person to interpret or repeat the result. It should not require irrelevant environment details when they do not affect the reproduction.

### steps-reproducible
This check asks whether another person could actually follow the report. The steps need enough commands, inputs, setup actions, and transitions to reach the attempted behavior without requiring the reader to invent a material step.

### behavior-matches-issue
A reproduction is useful only if the evidence addresses the behavior described in the issue. This check prevents a report from passing merely because it demonstrates a related error or another problem in the same repository.

### outcome-honest
The conclusion must match the evidence. A successful reproduction needs evidence of the reported behavior, while an honestly documented cannot-reproduce result can also be valid when the report accurately records the attempt and observed result. The check prevents stronger conclusions than the artifacts support.

### repo-conventions
Reproduction work is also upstream communication, so applicable repository requirements matter. This check enforces contribution, communication, template, and disclosure requirements when the supplied repository evidence explicitly imposes them. It intentionally does not invent additional rules that the repository never stated.

---

## Trade-offs

The main trade-off in the rubric is between strictness and repository specificity. A very strict universal rule can appear safer, but it can incorrectly reject valid contributions when a repository has different expectations. A rule that is too permissive can miss explicit requirements such as mandatory AI-use disclosure. I addressed this by grounding `repo-conventions` in the repository-specific evidence supplied with each package.

Another trade-off is how much detail to require in environment and reproduction steps. Requiring every possible system detail would make reports noisy without necessarily making them more reproducible. The final checks focus on material information: details that another person actually needs to understand the setup, repeat the steps, and evaluate the observed result.

For the live reproduction, I also chose not to run unrelated application functionality merely to make the report look more extensive. Issue #73 is a static documentation/configuration mismatch. Directly inspecting the relevant files at a pinned commit demonstrated the reported inconsistency without introducing an unsupported claim about runtime behavior.
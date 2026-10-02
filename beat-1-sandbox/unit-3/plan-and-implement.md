# Unit 3 â€” Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

Disha-k-gowda

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73#issuecomment-5961104050

Plan for #73 based on the reproduction I posted earlier.

The reproduction showed that `README.md:24` and `docs/SETUP.md:47` tell users to configure `OPENROUTER_API_KEY`, but `.env.example` contains `LLM_PROVIDER=mock` and `OPENAI_API_KEY` without an `OPENROUTER_API_KEY` entry. `core/config.py` already defines `openrouter_api_key`, so the example environment file does not expose the variable referenced by the setup instructions.

I plan to update `.env.example` only by adding an `OPENROUTER_API_KEY` placeholder beside the existing LLM configuration. I will keep `LLM_PROVIDER=mock` and the existing `OPENAI_API_KEY` entry unchanged.

I am not changing `README.md`, `docs/SETUP.md`, `core/config.py`, or runtime provider-selection behavior. My investigation did not establish that `openrouter` is currently wired as a selectable `LLM_PROVIDER` value, so I will not document that value as supported as part of this fix.

For verification, I will repeat the reproduction checks and confirm that copying `.env.example` produces an environment file containing `OPENROUTER_API_KEY`, while the existing `LLM_PROVIDER=mock` and `OPENAI_API_KEY` entries remain unchanged. I will also check the diff to make sure no unrelated files or settings changed.

---

## Your branch

**Branch**

docs-73-add-openrouter-api-key

**Evidence**

### Before

Unit 2 reproduction was run against commit `2f4e82f52efbcfcc57d65b3fa5348672163ca088` on `main`.

Commands:

```powershell
Select-String -Path README.md -Pattern "OPENROUTER_API_KEY|OPENAI_API_KEY|LLM_PROVIDER" -Context 2,2
Select-String -Path .env.example -Pattern "OPENROUTER_API_KEY|OPENAI_API_KEY|LLM_PROVIDER" -Context 2,2
Select-String -Path core/config.py -Pattern "OPENROUTER|OPENAI|LLM_PROVIDER" -Context 2,2
Select-String -Path docs/SETUP.md -Pattern "OPENROUTER_API_KEY|OPENAI_API_KEY|LLM_PROVIDER" -Context 2,2
```

Observed output:

```text
README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)

.env.example:17:# Options: "mock" (default, no API key needed), "openai"
.env.example:18:LLM_PROVIDER=mock
.env.example:19:OPENAI_API_KEY=sk-your-key-here

docs/SETUP.md:47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)

core/config.py:18:llm_provider
core/config.py:19:openai_api_key
core/config.py:20:openrouter_api_key
core/config.py:21:openrouter_base_url
core/config.py:22:openrouter_model
```

Before the fix, the setup documentation instructed users to configure `OPENROUTER_API_KEY`, while `.env.example` did not contain that variable.

### After

After implementing the change on `docs-73-add-openrouter-api-key`, I reran the configuration checks.

Observed output:

```text
README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)
.env.example:17:# Options: "mock" (default, no API key needed), "openai"
.env.example:18:LLM_PROVIDER=mock
.env.example:19:OPENAI_API_KEY=sk-your-key-here
.env.example:20:OPENROUTER_API_KEY=sk-or-your-key-here
docs\SETUP.md:47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)
core\config.py:18:llm_provider
core\config.py:19:openai_api_key
core\config.py:20:openrouter_api_key
core\config.py:21:openrouter_base_url
```

I also copied the built `.env.example` and checked the resulting environment file:

```powershell
Copy-Item .env.example .env.unit3-test
Select-String -Path .env.unit3-test -Pattern "LLM_PROVIDER|OPENAI_API_KEY|OPENROUTER_API_KEY"
Remove-Item .env.unit3-test
```

Output:

```text
.env.unit3-test:18:LLM_PROVIDER=mock
.env.unit3-test:19:OPENAI_API_KEY=sk-your-key-here
.env.unit3-test:20:OPENROUTER_API_KEY=sk-or-your-key-here
```

The built change therefore adds the missing `OPENROUTER_API_KEY` placeholder while preserving the existing `LLM_PROVIDER=mock` and `OPENAI_API_KEY` entries.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. First full evaluation: 18/20 agreement. The mismatches were `pkg-05`, which failed `unknowns-honest`, and `pkg-14`, which failed `executable`.

2. After revising those checks, I reran `pkg-05` and `pkg-14` together with `pkg-10` and `pkg-17` as canaries using `--only`. The targeted run matched 4/4 packages.

3. Final full evaluation saved to `eval-run.txt`: 19/20 agreement. Category results were `clear-accept` 6/7, `scope-creep` 4/4, `thread-convention` 2/2, `unbuildable` 3/3, and `wrong-cause` 4/4. The only mismatch was `pkg-05`, where the gold label was accept and the rubric returned reject because `unknowns-honest` failed.

**Package analysis**

`pkg-05` was the only mismatch in the final full evaluation. The gold verdict was `accept`, while my rubric returned `reject` because `unknowns-honest` failed. The check treated the package as containing a material uncertainty that should have been identified or resolved explicitly. I kept the check rather than weakening it further because the final rubric already reached 19/20 overall agreement and passed every category floor, while still protecting against plans that present unresolved material assumptions as established facts.

**Check rationale**

I focused on the `unknowns-honest` check:

> Pass when any material uncertainty is either identified as an unknown/risk or resolved by evidence already present in the package. A plan does not need to invent an unknown when the available evidence reveals no unresolved material assumption. Fail when the plan presents an unresolved material assumption as established fact and that assumption could change the implementation or test strategy.

I revised this check after the first full evaluation because the earlier wording could penalize a plan simply for not listing an unknown, even when the available evidence had already resolved the relevant uncertainty. The revised wording makes the threshold more concrete: a plan passes when material uncertainty is either disclosed or resolved by evidence, and fails only when an unresolved material assumption is presented as fact in a way that could affect implementation or testing.

**Trade-offs**

After revising `unknowns-honest` and `executable`, I reran the two affected packages, `pkg-05` and `pkg-14`, together with `pkg-10` and `pkg-17` as canaries. That targeted run matched 4/4. On the final full run, however, `pkg-05` again produced a reject instead of the gold accept, leaving the final score at 19/20.

I chose not to loosen `unknowns-honest` further just to make `pkg-05` pass. Doing so could allow genuinely unresolved material assumptions to pass the rubric. The trade-off is one remaining false rejection in exchange for keeping a stricter check on assumptions that could change the implementation or test strategy. The final rubric still exceeded the 18/20 target and met every category floor.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.












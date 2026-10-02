# Plan for Issue #73

## Diagnosis

The reproduction confirmed a configuration documentation mismatch between the setup instructions and `.env.example`.

`README.md:24` tells users to add `OPENROUTER_API_KEY` to `.env`, and `docs/SETUP.md:47` also tells users to set `OPENROUTER_API_KEY`. However, `.env.example` contains `LLM_PROVIDER=mock` and an `OPENAI_API_KEY` placeholder but does not contain an `OPENROUTER_API_KEY` placeholder.

The reproduction also found that `core/config.py:18-22` defines `llm_provider`, `openai_api_key`, `openrouter_api_key`, `openrouter_base_url`, and `openrouter_model`. This establishes that the OpenRouter configuration fields exist, while the example environment file does not expose the API key referenced by the setup documentation.

A repository-wide search did not establish that `openrouter` is currently wired as a selectable `LLM_PROVIDER` value. Therefore, this change will not add `openrouter` to the provider-options comment or modify runtime provider behavior.

## Scope

Update `.env.example` so a user who copies it to `.env` has an `OPENROUTER_API_KEY` entry corresponding to the setup instructions.

### In scope

- Add an `OPENROUTER_API_KEY` placeholder to the LLM configuration section of `.env.example`.
- Preserve the existing `LLM_PROVIDER=mock` default.
- Preserve the existing `OPENAI_API_KEY` entry.

### Out of scope

- Changing `README.md` or `docs/SETUP.md`.
- Changing `core/config.py`.
- Adding or modifying runtime provider-selection logic.
- Claiming that `LLM_PROVIDER=openrouter` is supported without runtime evidence.
- Changing unrelated environment settings.

## Files

- `.env.example` — add the missing OpenRouter API key placeholder beside the existing LLM configuration variables.

No application source files are planned for modification.

## Approach

1. Edit the LLM provider section of `.env.example`.
2. Keep `LLM_PROVIDER=mock` unchanged.
3. Keep the existing `OPENAI_API_KEY` placeholder unchanged.
4. Add an `OPENROUTER_API_KEY` placeholder so the example environment file exposes the variable referenced by `README.md` and `docs/SETUP.md`.
5. Do not add `openrouter` to the documented `LLM_PROVIDER` options because the investigation did not establish runtime provider-selection support for that value.

## Test Plan

Re-run the same static checks used during reproduction.

Before the change, the reproduction established:

- `README.md` references `OPENROUTER_API_KEY`.
- `docs/SETUP.md` references `OPENROUTER_API_KEY`.
- `.env.example` does not contain `OPENROUTER_API_KEY`.
- `core/config.py` defines `openrouter_api_key`.

After the change:

1. Search `.env.example` for `OPENROUTER_API_KEY`, `OPENAI_API_KEY`, and `LLM_PROVIDER`.
2. Verify that `OPENROUTER_API_KEY` is now present.
3. Verify that `LLM_PROVIDER=mock` remains unchanged.
4. Verify that the existing `OPENAI_API_KEY` entry remains present.
5. Copy `.env.example` to a temporary `.env` and verify that the copied configuration also contains `OPENROUTER_API_KEY`.
6. Confirm with `git diff` that no unrelated files or settings were changed.

The observable success condition is that a user following the documented copy step receives an environment file containing the `OPENROUTER_API_KEY` variable referenced by the setup documentation.

## Risks and Unknowns

The repository defines OpenRouter-related settings in `core/config.py`, and `ReviewGenerator` can receive an OpenAI-compatible base URL and API key. However, the investigation did not find code that constructs `ReviewConfig` or selects OpenRouter through `LLM_PROVIDER`.

Because runtime OpenRouter provider selection was not established, this plan deliberately avoids changing provider-selection documentation or application behavior. The fix is limited to the configuration-template mismatch reproduced in Issue #73.

## Deviations

There were no deviations from the accepted plan. The implementation changed only .env.example by adding the OPENROUTER_API_KEY placeholder, while preserving LLM_PROVIDER=mock and the existing OPENAI_API_KEY entry.
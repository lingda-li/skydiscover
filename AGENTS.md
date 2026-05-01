# Repository Guidelines

## Project Structure & Module Organization

SkyDiscover is a Python package in `skydiscover/`. Core orchestration lives in `runner.py`, `api.py`, and `cli.py`; search implementations are under `skydiscover/search/`; evaluators and benchmark resolution are under `skydiscover/evaluation/` and `skydiscover/benchmarks/`; prompt construction is under `skydiscover/context_builder/`; LLM utilities are under `skydiscover/llm/`.

Tests live in `tests/`, grouped by feature (`config`, `evaluation`, `search`, `cli`). Benchmark definitions and evaluator containers live in `benchmarks/`. Examples are in `examples/`, shared configs in `configs/`, images in `assets/`, reproduction scripts in `scripts/reproduce/`, and docs in `docs/`.

## Build, Test, and Development Commands

- `uv run skydiscover-run benchmarks/math/circle_packing/initial_program.py benchmarks/math/circle_packing/evaluator.py --config benchmarks/math/circle_packing/config_azure.yaml --search adaevolve --iterations 2`: run a single test.
- `uv sync --extra dev`: install the package and development tools.
- `uv run pytest`: run the full Python test suite.
- `uv run pytest -m "not slow"`: skip tests marked `slow`.
- `uv run black skydiscover tests benchmarks examples`: format Python files.
- `uv run isort skydiscover tests benchmarks examples`: sort Python imports.
- `uv run mypy skydiscover`: type-check package code.
- `uv run skydiscover-run <initial.py> <evaluator.py> --config <config.yaml>`: run discovery locally.
- `cd docs && npm install && npm run dev`: run the docs site locally.
- `cd docs && npm run build && npm run types:check`: validate docs build and types.

## Coding Style & Naming Conventions

Use Python 3.10+ syntax. Format with Black at 100 columns and isort’s `black` profile. Prefer typed functions; mypy enables `disallow_untyped_defs`. Use `snake_case` for modules, functions, variables, and YAML keys; use `PascalCase` for classes. Keep benchmark directories descriptive and lowercase, for example `benchmarks/math/circle_packing/`.

## Testing Guidelines

Pytest is the test framework. Name files `test_*.py` and keep tests near the feature area they cover. Use `@pytest.mark.slow` and `@pytest.mark.integration` for expensive or external tests. Add focused tests for configuration parsing, search controllers, evaluators, and CLI changes.

## Commit & Pull Request Guidelines

Recent history uses concise, imperative commit subjects, usually sentence case, for example `Fix code view in monitor dashboard`. Some commits use prefixes such as `feature:`; keep either style short and specific.

Pull requests should include a clear summary, test commands run, and benchmark or docs impact. Link issues when available. Include screenshots or recordings for dashboard or docs UI changes, and note required API keys, Docker images, or external services.

## Security & Configuration Tips

Do not commit secrets, API keys, generated datasets, or large run outputs. Use environment variables such as `OPENAI_API_KEY` and local `.env` files. Keep default configs in `configs/` generic; keep machine-specific paths outside version control.

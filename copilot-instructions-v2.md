# GitHub Copilot Guide

A concise reference to keep AI suggestions aligned with our architecture, style, and workflow.

## 1. Project Snapshot
| Area | Command / File | Notes |
|------|----------------|-------|
| Activate venv before running python commands | `source venv/bin/activate && <python command>` | Python 3.11+ |
| Install deps | `pip install ".[dev]"` | uses `pyproject.toml` |
| First‑time setup | `make local-first-time-setup` | runs DB migration + sample import |
| Run tests | `pytest` | target ≥ 90 % coverage |

*CSV layout and shot‑string legend live in **`app/config.py`** – keep suggestions consistent with that file.*

## 2. Core Principles (remember **KISS · DRY · YAGNI**)
1. **Small units, single purpose** – one class or function per concern.
2. **SOLID** – design for extension, not modification.
3. **Law of Demeter** – talk to friends, not strangers.
4. **Fail fast & loudly** – explicit exceptions over silent `None`s.
5. **Document _why_, not _what_** – concise Google‑style docstrings.

## 3. Coding Standards
- **Python 3.11**, `black` + `ruff` for formatting/linting.
- Strict **type hints**; `mypy --strict` must pass.
- **SQLAlchemy ORM** for DB
- **Pydantic V2** for all validation & settings.
- Style & Typing – Follow PEP 8, PEP 257, and the modern typing guidelines (PEP 585, 604, 673). Black/Ruff enforce formatting; mypy --strict must stay green.
- Do not fix linting issues automatically unless specifically asked to do so.
- Parameterised queries only – never raw f‑strings in SQL.
- Use `logging` – never `print`.
- Prefer immutable built‑ins (`tuple`, `frozenset`) where practical.
- Context managers for external resources.
- No secrets in code – load via `config.py` from `.env`.

## 4. Architecture Cheatsheet (example)
```
app/
  cli.py              # Typer CLI entry‑points
  data_access/        # SQLAlchemy models & CRUD
  services/           # business logic
  utils/              # InputParser, validators, common methods
  reports/            # ReportGenerator
  web_ui/             # (future) FastAPI endpoints
tests/
  fixtures/           # sample CSV & objects
```

## 5. Testing & QA
- Write tests alongside code; aim for red‑green‑refactor.
- Use `pytest` + fixtures; no hidden I/O.
- Add happy‑path and edge‑case tests for every utility.
- CI pipeline: `black --check`, `ruff`, `pytest`, `mypy`.

## 6. AI‑Specific Guidelines for Copilot
1. Stick to the directory structure above.
2. Suggest small, composable functions with docstrings & type hints.
3. Include example usages or test snippets when adding utilities.
4. Respect existing symbols & config – never rename without reason.
5. Default to pure functions; use classes only when stateful behaviour is needed.
6. Add meaningful TODO comments if context is missing rather than hallucinating.

## 7. Advanced Rules
- **REST API**: Use **FastAPI**, prefix paths with `/v1/`, return JSON.
- **Async**: Use `asyncio`/async SQLAlchemy only when IO‑bound.
- **Performance**: Profile before optimising – avoid avoidable nested loops.
- **Security**: Validate & sanitise all external input. Implement rate‑limiting on public endpoints.


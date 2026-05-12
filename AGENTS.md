# AI Coding Agent Instructions — Soc Ops

## MANDATORY DEVELOPMENT CHECKLIST

Before committing any changes:
- [ ] `uv run ruff check .` passes (no errors)
- [ ] `uv run pytest` passes (all tests green)
- [ ] Code builds: `uv run uvicorn app.main:app --reload --port 8000`

---

## Quick Start

**Project:** Social Bingo game for in-person mixers (FastAPI + HTMX + Jinja2 + Python 3.13+)

**Setup:**
- `uv sync` — Install dependencies
- `uv run uvicorn app.main:app --reload --host 0.0.0.0 --port 8000` — Dev server
- `uv run pytest` — Run tests
- `uv run ruff check .` — Lint

---

## Architecture

**Key Files:**
- `app/main.py` — FastAPI routes & HTMX endpoints
- `app/game_service.py` — Session state management
- `app/game_logic.py` — Board generation, bingo detection (pure functions)
- `app/models.py` — Pydantic models
- `app/templates/` — Jinja2 + HTMX components
- `tests/` — 25 integration & unit tests

**Key Patterns:**
- State: `GameSession` dataclass, persisted via signed cookies (immutable updates)
- Logic: Pure functions, no side effects
- UI: HTMX for partial updates, no JavaScript required

---

## Code Conventions

- **Python:** `snake_case`, type hints required, Pydantic `BaseModel`, dataclasses for state
- **Linting:** Ruff rules E, F, I, N, W; line length 88
- **Testing:** Pytest with FastAPI `TestClient`
- **CSS:** Custom utilities (Tailwind-like); see `.github/instructions/css-utilities.instructions.md`
- **Frontend:** Distinctive designs, no generic AI aesthetics; see `.github/instructions/frontend-design.instructions.md`

---

## Critical Pitfalls

- **Browser:** NO Simple Browser for HTMX. Use full browser (`Start-Process http://localhost:8000`)
- **Environment:** `uv` not in PATH by default; use `python -m uv` or activate venv
- **State:** In-memory (resets on restart); session ID is UUID
- **Questions:** 24 unique per board (`app/data.py`); center always FREE SPACE

---

## Resources

- README.md, CONTRIBUTING.md, workshop/, .solutions/

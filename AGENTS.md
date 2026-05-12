# AI Coding Agent Instructions — Soc Ops

This document helps AI coding agents be immediately productive in the Soc Ops project.

## Quick Start

### Project Overview
**Soc Ops** is a Social Bingo game for in-person mixers. Players find people matching bingo questions and mark squares to get 5 in a row.

**Tech Stack:** FastAPI + Jinja2 templates + HTMX + Python 3.13+ + uv

### Essential Commands
- Setup: uv sync
- Development: uv run uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
- Tests: uv run pytest
- Lint: uv run ruff check .

### Environment Setup
- Python 3.13+
- Package manager: uv
- Virtual environment: .venv (created by uv sync)

## Architecture

### Directory Structure
- app/main.py: FastAPI routes and HTMX endpoints
- app/game_service.py: Session state management
- app/game_logic.py: Board generation and bingo detection
- app/models.py: Pydantic models
- app/data.py: Question bank
- app/templates/: Jinja2 templates with HTMX
- app/static/css/app.css: Custom utility classes
- tests/: Integration and unit tests (25 tests)

### Key Patterns

State Management:
- GameSession dataclass holds game state
- Persisted via signed cookies (Starlette SessionMiddleware)
- Immutable state updates

Game Logic:
- Pure functions (no side effects)
- Bingo detection: rows, columns, diagonals

UI Updates:
- HTMX for partial updates
- HTML fragment responses
- No JavaScript required

## Styling and Frontend
- Custom CSS utilities (Tailwind-like)
- See .github/instructions/frontend-design.instructions.md
- See .github/instructions/css-utilities.instructions.md

Avoid generic AI aesthetics; create distinctive designs.

## Code Conventions

Python:
- snake_case for functions/variables
- Type hints required (Python 3.13+)
- Pydantic BaseModel for data
- Dataclasses for internal state

Linting:
- Ruff rules: E, F, I, N, W
- Line length: 88
- Check: uv run ruff check .

Testing:
- Pytest with TestClient
- Run: uv run pytest

## Important Pitfalls

Environment:
- uv not in PATH; use python -m uv or activate venv
- VS Code tasks may fail without venv activation

HTMX and Browser:
- DO NOT use VS Code Simple Browser
- HTMX requires full browser (Chrome, Firefox, etc.)
- Use Start-Process http://localhost:8000 to open

State:
- Game state is in-memory (resets on server restart)
- Session cookies signed with dev key
- Session ID is UUID

Questions:
- Stored in app/data.py
- 24 unique per board (plus free space)
- Random board generation

## Resources
- README.md, CONTRIBUTING.md, workshop/, .solutions/

## Pre-Commit Checklist
- ruff check . passes
- pytest passes
- No unused imports
- Code follows conventions
- Tested in full browser

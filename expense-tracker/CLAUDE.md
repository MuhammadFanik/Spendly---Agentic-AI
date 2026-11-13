# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

"Spendly" — a Flask expense tracker built as a step-by-step learning project (course by Nitish). Much of the app is intentionally unfinished: stubs are marked "Step N" for the learner to implement one at a time.

## Repository layout

The git root is the outer `expense-tracker/` folder; the actual app lives in the nested `expense-tracker/expense-tracker/` folder (this directory). The outer folder also holds `venv/`, `.idea/`, `__MACOSX/` and a scratch `file.txt` — ignore those.

## Commands

Run from the app directory (the one containing `app.py`):

```
pip install -r requirements.txt     # flask, werkzeug, pytest, pytest-flask
python app.py                        # dev server, debug mode, http://localhost:5001
pytest                               # run all tests (no tests exist yet)
pytest path/to/test_file.py::test_name   # run a single test
```

No linter or build step is configured. The port is 5001 (set in `app.py`), not Flask's default 5000.

## Architecture

- `app.py` — single Flask app; all routes are defined here. Two groups:
  - Implemented: `/`, `/register`, `/login`, `/terms`, `/privacy` just render templates. Note `/register` and `/login` only handle GET — there is no form handling or auth yet.
  - Placeholder routes returning plain strings: `/logout` (Step 3), `/profile` (Step 4), `/expenses/add` (Step 7), `/expenses/<id>/edit` (Step 8), `/expenses/<id>/delete` (Step 9). Replace these in place when implementing the step.
- `database/db.py` — currently only a comment describing the intended contract: `get_db()` (SQLite connection with `row_factory` and foreign keys on), `init_db()` (`CREATE TABLE IF NOT EXISTS`), `seed_db()` (sample data). `expense_tracker.db` is gitignored.
- `templates/` — all pages extend `base.html` (navbar, footer, blocks `title`, `head`, `content`; links use `url_for`). Fonts are loaded from Google Fonts in `base.html`.
- `static/css/style.css` — single shared stylesheet; `static/js/main.js` is an empty placeholder.

## Conventions

- Use `url_for(...)` for links in templates, as `base.html` does.
- Commit messages in history follow a `landing: <what changed>` style for landing-page work.

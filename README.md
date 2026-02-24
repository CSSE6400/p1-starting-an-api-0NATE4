[![Open in Codespaces](https://classroom.github.com/assets/launch-codespace-2972f46106e565e64193e422d61a12cf1da4916b45550586e14ef0a7c637dd04.svg)](https://classroom.github.com/open-in-codespaces?assignment_repo_id=22798770)

# CSSE6400 Week 1 Practical

Construction of a minimal REST-style HTTP API for a todo app using Flask.

## Summary (from week01.pdf)

- **Context:** HTTP sits in the application layer (on top of TCP). URLs have protocol, host, path, optional port and query params. HTTP is request–response; common methods: GET (read), POST (create), PUT (update), DELETE (delete). JSON is used for request/response bodies.
- **API:** All endpoints live under `/api/v1`. For week 1 you return **hardcoded** data only (no database or in-memory store yet).
  - **GET /api/v1/health** — 200, JSON `{"status": "ok"}`.
  - **GET /api/v1/todos** — 200, JSON array of todos (one hardcoded item).
  - **GET /api/v1/todos/{id}** — 200, single todo JSON.
  - **POST /api/v1/todos** — 201, JSON of “created” todo (same hardcoded item).
  - **PUT /api/v1/todos/{id}** — 200, JSON of “updated” todo.
  - **DELETE /api/v1/todos/{id}** — 200, JSON of “deleted” todo.
- **Stack:** Python 3.12+, Poetry, Flask. App lives in a `todo` package with `create_app()` and a blueprint under `todo/views/routes.py`.

## How to run

```bash
poetry install
poetry run flask --app todo run -p 6400
```

Then open http://localhost:6400/api/v1/health (and other endpoints as above).

---

## Actionable steps (do these yourself)

1. **Create Python project**
   - In the repo root: `poetry init` (accept defaults).
   - In `pyproject.toml` set `requires-python = ">=3.12"`.
   - Run: `poetry add flask`.

2. **Create package layout**
   - `todo/__init__.py` — implement `create_app()` that creates a Flask app and registers the API blueprint (see PDF §5.2.2).
   - `todo/views/routes.py` — create Blueprint with `url_prefix='/api/v1'`, add health route returning `jsonify({"status": "ok"})`, then add the five todo routes that each return the same hardcoded todo (or list `[todo]` for GET /todos). Use the exact todo object from the PDF so it matches the tests.

3. **Wire blueprint into the app**
   - In `todo/__init__.py`, import the blueprint from `todo.views.routes` and call `app.register_blueprint(api)`.

4. **Verify**
   - Structure: `./.csse6400/bin/validate_structure.sh`
   - Unit tests: `./.csse6400/bin/unittest.sh`
   - Health (server must be running on port 6400): `./.csse6400/bin/health.sh`

5. **Keep repo clean**
   - Ensure `.gitignore` includes `__pycache__`, `*.pyc`, `.DS_Store`, and similar so `./.csse6400/bin/clean_repository.sh` passes.

6. **Push and check CI**
   - Commit, push, and confirm all four autograder checks pass on GitHub.

All code you need for step 2 is in the PDF (§5.2.2–5.2.5); copy the snippets from there.

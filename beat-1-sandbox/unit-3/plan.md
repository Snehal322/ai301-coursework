## Diagnosis
Executing `GET /health` causes the database probe in `api/routes/health.py` to fail. In SQLAlchemy 2.x, executing a raw string query via `db.execute("SELECT 1")` raises `sqlalchemy.exc.ArgumentError: Textual SQL expression 'SELECT 1' should be explicitly declared as text('SELECT 1')`. This exception is caught by the `except Exception:` block, setting `dependencies["postgres"] = "unhealthy"` and returning an overall `503 Service Unavailable` status.

Grounding reproduction report: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61#issuecomment-6007521993

> **Reproduction Evidence:**
> `sqlalchemy.exc.ArgumentError: Textual SQL expression 'SELECT 1' should be explicitly declared as text('SELECT 1')`
> Response status: `503 Service Unavailable`
> Body: `{"status": "unhealthy", "dependencies": {"postgres": "unhealthy"}}`

## Scope
- **In Scope:**
  - Import `text` from `sqlalchemy` in `api/routes/health.py`.
  - Wrap `'SELECT 1'` as `await db.execute(text("SELECT 1"))`.
  - Add a regression unit test in `tests/unit/test_health.py`.
- **Out of Scope:**
  - Modifying `pyproject.toml` or dependencies (Redis issue #62).
  - Modifying non-postgres health probes.

## Files Touched
- `api/routes/health.py`
- `tests/unit/test_health.py`

## Approach
1. Add `from sqlalchemy import text` in `api/routes/health.py`.
2. Update line 32 to `await db.execute(text("SELECT 1"))`.
3. Add a unit test in `tests/unit/test_health.py` asserting `dependencies["postgres"] == "healthy"`.

## Test Plan
- **Pre-Fix Output:**
  `curl -i http://localhost:8000/health` returns `HTTP 503` with `"postgres": "unhealthy"` due to `ArgumentError`.
- **Post-Fix Verification:**
  1. Re-run `curl -i http://localhost:8000/health` to confirm `dependencies.postgres` returns `"healthy"`.
  2. Run `make test-unit` to confirm regression tests pass.
  3. Run `make typecheck` to verify no static typing errors.

## Risks and Unknowns
- Low risk of side effects as `text()` is standard SQLAlchemy 2.0 syntax for raw SQL strings.
- Unknown: DB connection availability during local unit tests requires a running PostgreSQL instance or mock fixture.

## Deviations
No deviations from the planned approach.
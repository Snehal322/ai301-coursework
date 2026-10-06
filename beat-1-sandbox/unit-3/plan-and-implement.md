# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

[Your GitHub username, exactly as it appears on your profile - no @, no
profile URL. Your comment upstream is identified by this name, and it is
the only thing that ties it to you. Several students may plan the same
house issue, so this is what keeps their comments off your score and
yours off theirs.]

snehal322

**Plan comment**

[Link to the comment where you posted your plan on the issue. Use the comment's own
permalink. **Then paste the text of that comment underneath the link** — the pasted text is
what this field is graded on, so copy across what you actually posted.]

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61#issuecomment-6010252644

## Root Cause
The `health_check` endpoint in `api/routes/health.py` executes a raw string query `db.execute("SELECT 1")`. In SQLAlchemy 2.0+, passing raw strings directly to `execute()` is no longer supported and raises an `ArgumentError: Textual SQL expression 'SELECT 1' should be explicitly declared, or be used via 'text()'`.

## Proposed Fix
1. Import `text` from `sqlalchemy` in `api/routes/health.py`.
2. Update the query execution in `health_check()` from `await db.execute("SELECT 1")` to `await db.execute(text("SELECT 1"))`.
3. Add or update unit test coverage in `tests/unit/test_health.py` to verify that `health_check()` successfully executes `db.execute()` using the `text()` clause and returns a `200` status / `healthy` status for the `postgres` dependency.

## Verification
- Run `poetry run pytest tests/unit/test_health.py -v` to confirm the test passes.
- Run `poetry run mypy api/routes/health.py` to verify static typing passes without issues.

---

## Your branch

**Branch**

[The name of the branch you built the change on, exactly as it appears in your fork. The
naming shape is a type prefix, then the issue number, then a short description. **The issue
number in the branch name must be the number of the issue you claimed** — a name carrying
any other number does not satisfy this field.]

fix/61-sqlalchemy-text-clause

**Evidence**

[Your Unit 2 reproduction steps re-run against the built change: the before, then the
after. Paste both, including the commands you ran and their output.]

**BEFORE FIX (Reproduction):**
```bash
$ poetry run pytest tests/unit/test_health.py -v
=================================== FAILURES ===================================
________________________ test_health_check_postgres_healthy ________________________
    @router.get("")
    async def health_check(db=Depends(get_db)):
>       await db.execute("SELECT 1")
E       sqlalchemy.exc.ArgumentError: Textual SQL expression 'SELECT 1' should be explicitly declared, or be used via 'text()'


After fix(Verification):

$ poetry run pytest tests/unit/test_health.py -v
=============================== test session starts ================================
platform darwin -- Python 3.13.5, pytest-9.1.1, pluggy-1.6.0
collected 1 item

tests/unit/test_health.py::test_health_check_postgres_healthy PASSED          [100%]

============================== 1 passed in 0.71s ==============================

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.


**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

# eval run written by run_eval.py at 2026-10-05T05:44:18Z
# model: sonnet (pinned)
# graded: /Users/snehalchavan/.claude/skills/plan-check
# packages: 20 scored
#   rubric.md  sha256:d42fce3755b89cd5
#   evidence-guide.md  sha256:186f43aebb27a411
#   procedure.md  sha256:951e3822b510fe15
#   SKILL.md  sha256:4688d0d0f4cf6cb3
#
grading 20 package(s) with rubric.md + evidence-guide.md + procedure.md, model sonnet, 5 worker(s)...
  pkg-03: accept
  pkg-05: accept
  pkg-04: reject
  pkg-01: reject
  pkg-02: accept
  pkg-06: reject
  pkg-08: accept
  pkg-10: reject
  pkg-09: accept
  pkg-07: reject
  pkg-11: reject
  pkg-12: reject
  pkg-13: accept
  pkg-14: accept
  pkg-15: reject
  pkg-16: reject
  pkg-17: reject
  pkg-18: reject
  pkg-19: reject
  pkg-20: reject

item    category           gold    verdict  agree  note
pkg-01  wrong-cause        reject  reject   yes    
pkg-02  clear-accept       accept  accept   yes    
pkg-03  clear-accept       accept  accept   yes    
pkg-04  thread-convention  reject  reject   yes    
pkg-05  clear-accept       accept  accept   yes    
pkg-06  scope-creep        reject  reject   yes    
pkg-07  wrong-cause        reject  reject   yes    
pkg-08  clear-accept       accept  accept   yes    
pkg-09  clear-accept       accept  accept   yes    
pkg-10  unbuildable        reject  reject   yes    
pkg-11  wrong-cause        reject  reject   yes    
pkg-12  scope-creep        reject  reject   yes    
pkg-13  clear-accept       accept  accept   yes    
pkg-14  clear-accept       accept  accept   yes    
pkg-15  scope-creep        reject  reject   yes    
pkg-16  wrong-cause        reject  reject   yes    
pkg-17  unbuildable        reject  reject   yes    
pkg-18  unbuildable        reject  reject   yes    
pkg-19  scope-creep        reject  reject   yes    
pkg-20  thread-convention  reject  reject   yes    

categories: clear-accept 7/7  scope-creep 4/4  thread-convention 2/2  unbuildable 3/3  wrong-cause 4/4
agreement: 20/20 scored items  (bar: 18/20: PASS)


**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

Package pkg-01: The rubric decided reject and the gold label was reject. The rubric rejected this plan because the proposed fix misdiagnosed the root cause by attempting to modify connection arguments rather than wrapping raw SQL strings with text().

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/plan-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

"Verify that raw SQL strings passed to db.execute() are explicitly wrapped in SQLAlchemy's text() construct."
This check was added directly to catch SQLAlchemy 2.0 migration errors where raw text queries fail execution. I kept this explicit wording over broader database error checks to ensure precise rule matching during evaluation.


**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

By making the text() check strict, the rubric accepts that it will fail to catch generic database execution failures unrelated to textual SQL expressions.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.

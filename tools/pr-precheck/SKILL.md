# SKILL: pr-precheck

Evaluate whether a candidate pull request package is ready to submit by grading it against its plan, issue thread, diff, and quality standards.

## Purpose

The `pr-precheck` tool answers a single binary question: **Is this pull request ready to submit?** It operates deterministically using explicit evidence from the provided artifacts, returning an `accept` or `reject` verdict with per-check justifications and ending with a rigid JSON block.

## Modes of Operation

### 1. Live Mode (Local Repository Check)
Used when evaluating your own local work before opening or finalizing a PR.
- **Inputs to Read:**
  - `scope.md` (Must match the scoped Path Review repository; stops and refuses if unfilled or mismatched).
  - `voice-guide.md` (Personal writing rules carried forward from Unit 2).
  - `beat-1-sandbox/unit-3/plan.md` (or the current task plan including deviation notes).
  - Git diff (`git diff main...HEAD`).
  - Issue thread and requirements context.
  - Repository PR template and `docs/CONTRIBUTING.md`.

### 2. Eval Mode (Package Bundle Evaluation)
Used when grading a frozen evaluation package bundle from `eval/packages/`.
- **Inputs to Read:**
  - The standalone package bundle text exclusively.
  - **Constraints:** Nothing is fetched from external repositories, live git diffs, or local files. Every fact must come strictly from the package text.

---

## Operating Procedure

1. **Scope Verification:** Read `scope.md`. If the `Repo:` line contains a placeholder or does not match the active environment, refuse to grade and halt immediately.
2. **Evidence Gathering:** Collect evidence according to `references/evidence-guide.md` for each rubric check.
3. **Rubric Evaluation:** Execute every check listed in `rubric.md`. Every check requires:
   - A clear binary grade (`pass`, `fail`, or `unclear`).
   - Explicit evidence (exact quote or fact from the artifacts).
4. **Verdict Determination:** Apply the verdict rules from `rubric.md`.
5. **Output Formatting:** Summarize findings per check and conclude with the mandatory JSON block.

---

## Refusal Rules

- **Unfilled Scope:** If `scope.md` contains an unfilled placeholder, stop and instruct the user to update the `Repo:` line.
- **Empty Rubric / Procedure:** If `rubric.md` or `procedure.md` is empty or lacks checks, refuse to grade to prevent false verdicts.

---

## Output Schema

Every run must conclude with the exact JSON block below as the final element in the response, with no text following it:

```json
{
  "item": "<PR URL bundle id or>",
  "checks": [
    {
      "name": "<check name>",
      "grade": "pass|fail|unclear",
      "evidence": "<one line: the fact or quote that decided it>"
    }
  ],
  "verdict": "accept|reject"
}
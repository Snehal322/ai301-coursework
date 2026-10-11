# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides where the plan sits in the order (before the diff? before the
description?) and says why the order matters for the side-by-side
checks that come later. -->

Execute the read steps in this strict sequence before grading any check:

1. **Read Scope & Mode Inputs**:
   - In **Live Mode**: Read `scope.md`. Verify the `Repo:` line contains a valid repository matching the current section's Path Review repository. If empty or containing a placeholder, halt immediately and refuse to grade. Next, read `voice-guide.md` to load communication preferences.
   - In **Eval Mode**: Skip `scope.md` and `voice-guide.md`. Read the package bundle text strictly.
2. **Read the Plan**: Read `plan.md` (or the bundle's `plan-context` block). Note down:
   - The primary root cause and intended fix boundary.
   - The list of explicitly planned files and expected behavioral changes.
   - Any documented deviations in the `## Deviations` section.
   - The expected test plan and verification steps.
3. **Read Repo Standards & Asks**: Read the repo's PR template, `docs/CONTRIBUTING.md`, and policy requirements (or the bundle's `repo-facts` block). Note required PR description fields, issue link formats, and required test evidence disclosures.
4. **Read the Candidate PR Artifacts**:
   - Read the candidate PR title and description.
   - Read the unified git diff (`git diff main...HEAD` in live mode, or the bundle's `diff` block). List every modified, added, or deleted file path.
   - Read the candidate's test evidence logs/artifacts.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which file, diff,
or page per your evidence guide) to pull the fact from, and what to
record. The load-bearing gathers this week are pairings: diff files
against plan scope, claimed evidence against the plan's test plan and
the repo's checks, description claims against diff contents. A
complete procedure leaves no check whose evidence an executor would
have to hunt for. -->

Gather evidence side-by-side for each family named in `rubric.md` following `references/evidence-guide.md`:

1. **Plan Fidelity (Silent Drift)**:
   - Compare the list of changed file paths in the diff against the planned file list in `plan.md`.
   - Compare the actual logic changes in the diff against the planned fix steps and deviation notes.
   - Compare the candidate PR description's claims of work completed against what the diff actually delivers.
   - Record: Specific file paths or logic present in the diff but missing from the plan, or claimed in the description but absent in the diff.
2. **Test Evidence (Not Tested)**:
   - Compare the candidate's provided test execution logs against the test plan in `plan.md` and the issue's requirements.
   - Verify that test output displays actual passing execution results (e.g., `pytest` session summaries showing passing test names and runtime metrics) rather than raw text claims like "tests pass".
   - Record: Exact test command run, test pass counts, or note total absence of observable test logs.
3. **Diff Quality (Unreviewable)**:
   - Scan every hunk in the diff for debug debris (`print()`, `console.log()`, `breakpoint()`), commented-out code, temporary files (`.DS_Store`, `.pyc`), or unrelated reformatting in untouched files.
   - Record: File path and line numbers of any identified noise or stray changes.
4. **Standards and Comms (Standards Wall)**:
   - Compare the draft PR description against the template prompts in `repo-facts` or the repo PR template.
   - Verify every mandatory heading/section is present and populated with real content (not boilerplate placeholders or empty strings).
   - Record: Any missing or unfulfilled PR template section.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

Grade each check defined in `rubric.md` in top-to-bottom table order using the gathered evidence:

1. **Comparison & Evaluation**: Evaluate the gathered facts against the check's stated **Pass condition**.
2. **Grade Assignment**:
   - Assign `pass` if the evidence completely satisfies the pass condition.
   - Assign `fail` if the evidence violates the pass condition.
   - Assign `unclear` if required evidence is missing, truncated, or unverifiable from the package.
3. **Evidence Record**: Record exactly **one line of evidence** (a concise fact or direct quotation) explaining the grade.
4. **No Assumption Rule**: Do not re-evaluate or guess unstated context. If a fact cannot be verified, it must be assigned `unclear`.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check: the
check whose failure the verdict turned on. When more than one check
failed, your procedure picks which one gets quoted (first failing
required check in rubric order is a fine rule); nothing picks it for
you, so write the rule down. A complete procedure produces the same
verdict from the same grades, every time. -->

1. **Apply Verdict Rule**:
   - If any `required` check in `rubric.md` receives a grade of `fail` or `unclear`, the final verdict is **`reject`**.
   - If all `required` checks receive a grade of `pass`, the final verdict is **`accept`**.
   - `preferred` checks report feedback in the check list summary but never alter the verdict.
2. **Identify Deciding Evidence**:
   - If the verdict is `reject`, identify the **first failing `required` check** in `rubric.md` table order. This is the primary deciding check.
3. **Format Output**:
   - Provide a brief human-readable check summary.
   - End the response with the mandatory fenced JSON block with no trailing text:
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

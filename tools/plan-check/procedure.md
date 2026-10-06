# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

1. **Read 'scope.md' / Repo facts first.** Record the repository name, baseline contributing guidelines, and explicit AI disclosure requirements.
2. **Read the Issue Context.** Record the core bug behavior, affected endpoints/modules, and any explicit maintainer/contributor guidelines in the issue thread.
3. **Read the Repro Evidence block.** Record:
   - The exact environment setup (Python/OS/dependencies).
   - The minimal steps to reproduce the failure.
   - The exact failure output (e.g., error messages, stack traces, or broken SQL assertions).
4. **Read 'plan.md' and 'comment.md'.** Do not evaluate or grade checks while reading; simply absorb the proposed diagnosis, file changes, test plan, and comment text.
5. **Order Rationale:** The issue and repro evidence define the ground truth boundary. Reading them before the plan prevents confirmation bias and ensures you evaluate the plan against objective repro facts rather than taking the author's assertions at face value.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

1. **Scope & House Rules Evidence:** Read 'comment.md' and compare it against the issue thread comments and repo guidelines for thread conventions, required disclosures, or prohibited edits.
2. **Diagnosis Evidence:** Locate the root cause statement in 'plan.md' and compare it directly to the exact stack trace/error output in the Repro Evidence block and source code.
3. **Scope Evidence:** Locate the "In Scope", "Out of Scope", and "Files Touched" sections in 'plan.md'. Check if changes stay minimal and bounded to fixing the issue.
4. **Test Plan Evidence:** Locate the "Test Plan" section in 'plan.md'. Compare its steps and expected post-fix output against the reproduction steps and repo CI commands (`pytest`, `make typecheck`).

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. Execute checks strictly in this order:
   - Check 1: Scope & House rules
   - Check 2: Diagnosis
   - Check 3: Scope
   - Check 4: Test Plan
2. **Missing Evidence Protocol:** If evidence for a check is missing from 'plan.md' or 'comment.md', mark that check as 'fail' or 'unclear'. Do not assume or invent evidence.
3. **Context Preservation:** Grade each check against recorded facts without re-reading unneeded parts of the package.


## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->

1. Apply the rubric's verdict rules:
   - **'accept' ('ready')**: ALL 4 required checks receive a 'pass' grade.
   - **'reject' ('hold')**: ANY required check receives a 'fail' or 'unclear' grade.
2. Treat all 'unclear' grades as 'fail'.
3. Output the final JSON object containing the verdict and per-check evidence notes.
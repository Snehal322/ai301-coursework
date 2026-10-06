# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

- **Where it lives:**
  - Eval package: The candidate plan's '## Diagnosis' section compared against the '## Repro Evidence' block and issue context.
  - Live mode: 'plan.md' under '## Diagnosis', evaluated against the repro comment posted on GitHub and the local reproduction output.
- **What good looks like:**
  - The diagnosis directly references the observed runtime failure or error output from the repro report (e.g., citing the specific `ArgumentError` when executing raw SQL strings with SQLAlchemy 2.x).
  - The stated root cause explains *why* the failure occurs without contradicting the repro logs or making unsupported assumptions.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

- **Where it lives:**
  - 'plan.md' under '## Scope' and '## Files Touched'.
- **What good looks like:**
  - Identifies target files and bounds the fix. A plan that touches files relevant to the issue's root cause passes, even if it lists minimal non-code collateral files (e.g., test files).

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

- Eval package: 'plan.md' under '## Approach' and implementation steps.
  - Live mode: 'plan.md' under '## Approach' and implementation steps.
- **What good looks like:**
  - A reviewer can follow the steps sequentially without asking clarifying questions.
  - Names specific functions, modules, or wrapper calls to use (e.g., "Wrap raw SQL string 'SELECT 1' in SQLAlchemy's 'text()' function imported from `sqlalchemy`").

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

- **Where it lives:**
  - Eval package: 'plan.md' under '## Test Plan'.
  - Live mode: 'plan.md' under '## Test Plan'.
- **What good looks like:**
  - Re-runs the exact reproduction commands from the Unit 2 repro steps.
  - Clearly states the exact expected outcome after the fix (e.g., 'GET /health' returns HTTP '200 OK' with '{"status": "ok"}' instead of throwing 'ArgumentError').

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

- **Where it lives:**
  - Eval package: 'plan.md' under '## Risks and Unknowns' and '## Deviations'.
  - Live mode: 'plan.md' under '## Risks and Unknowns' and '## Deviations'.
- **What good looks like:**
  - Clearly identifies potential failure modes, side effects, or unknown dependency behaviors.
  - If no deviations occurred during build, explicitly states that (e.g., "unit 3: no deviations from plan").

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

- **Where it lives:**
  - Eval package: The draft comment ('comment.md') compared against repo facts, contribution guidelines, and thread policies.
  - Live mode: 'comment.md' cross-referenced with 'docs/CONTRIBUTING.md' and repository AI disclosure policy.
- **What good looks like:**
  - Adheres strictly to thread conventions and house rules.
  - Includes mandatory AI attribution/disclosure notices if required by repository policy.
  - A comment that ignores repo contribution policy, uses prohibited generic phrasing, or omits required AI disclosure tags MUST fail this check.

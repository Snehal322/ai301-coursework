# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->

- **Where it lives:** 
  - *Eval mode:* The 'Environment' or 'Repo-facts' section of the package bundle.
  - *Live mode:* The environment section of the draft repro comment or the issue context on GitHub.
- **What good looks like:** Lists specific operating system, runtime/Python version, and relevant library dependency versions. The environment matches or explicitly contrasts with the target specified in the issue.
 

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

- **Where it lives:**
  - *Eval mode:* The 'Reproduction Steps' or 'Setup' section in the candidate repro report.
  - *Live mode:* The setup and execution commands in the student's draft repro report.
- **What good looks like:** Sequential, copy-pasteable terminal commands starting from a clean checkout, including environment creation, dependency installation, and the exact trigger command.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

- **Where it lives:**
  - *Eval mode:* The terminal output, stack trace, screenshot block, or log excerpt in the candidate repro report.
  - *Live mode:* Code blocks and output excerpts in the draft repro comment are evaluated against the original issue description.
- **What good looks like:** The excerpted log or stack trace contains the exact error message or unexpected output described in the issue (e.g., 'ArgumentError' on raw SQL string), demonstrating the bug was triggered rather than a setup script failure.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

- **Where it lives:**
  - *Eval mode:* The summary/conclusion section of the repro report compared against the attached evidence artifacts.
  - *Live mode:* The claims made in the draft comment compared to the attached log evidence.
- **What good looks like:** The report's claim ('reproduced' vs 'cannot reproduce') aligns 100% with what the output logs prove. If setup failed or output differed, the report honestly states `cannot reproduce` with the actual trace shown.


## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

- **Where it lives:**
  - *Eval mode:* The 'Claim Comment' and 'Repro Comment' sections of the bundle checked against repo policies in `repo-facts`.
  - *Live mode:* Draft comments checked against 'voice-guide.md' and repository policies ('CONTRIBUTING.md', 'AI_POLICY.md').
- **What good looks like:** Pass standard claim statements ("I am looking into this issue..."). 

 **CRITICAL:** Check the repo policy for mandatory AI disclosure notices. If the repo policy requires AI disclosure tags (e.g., 'Generated with AI' or explicit disclosure headers) and the comment contains AI-generated report sections without that required disclosure tag, **Scope & House rules MUST FAIL**.
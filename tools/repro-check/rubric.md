# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment recorded | Repro report's environment section | Names OS/platform and primary runtime or dependency versions used in the test, matching or explicitly comparing against the issue target environment. | required |
| Complete steps | Repro report's setup and reproduction steps | Provides copy-pasteable execution commands or clear setup steps sufficient to reach and trigger the reported behavior. | required |
| Behavior matches issue | Output excerpts, terminal logs, stack traces, or screenshots in the repro report read against issue description | The captured log, stack trace, or error output demonstrates the specific bug, exception, or failure mode described in the issue. | required |
| Honest outcome statement | Repro report's conclusion and claim statement | Outcome accurately reflects what the evidence demonstrates (stating `reproduced` when logs show the error, or 'cannot reproduce' when logs show normal execution). | required |
| Scope & House rules | Claim comment and repro report read against repo policy and issue thread | Package follows repo contribution house rules, including any mandatory AI-use disclosure tags/notices, and does not violate thread claiming conventions. | required |
| Clear concise comms | Claim and repro comment prose | Comment text is professional, relevant, and free of toxic tone, spammy preamble, or deceptive statements. | preferred |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept if every 'required' check receives a grade of 'pass'. If any 'required' check receives a grade of 'fail' or 'unclear', the verdict is 'reject'. 'preferred' checks provide feedback in the summary but never change the final verdict on their own.

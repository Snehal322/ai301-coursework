# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer alive | Last five branch commits | At least one of the last commits is within 90 days | required |
| Repo in use | Latest release + push date | Latest realease or push within last 60 days| required |
| Scope fits | issue + thread | issue describes the bounded task| required |
| Nobody is working on the issue | Assignee, Linked PRs, claim comments | No assignee, opened PR links or claim comments | required |
| Label | Issuelabels | Labeled "good first issue" or equivalent | preferred |
| Issue reponse latency | Maintainer first response sample | Manrainer has responded within 30 days | required |
| AI contribution policy | contibuting.md | No outright ban on AI usage and contribution | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept if and only if all required checks pass.

- A 'fail' on any required check -> reject
- 'unclear' on any required check is treated as 'fail' → reject
- Preferred checks ("Label" and "AI contribution policy" if you keep it
  preferred) never affect the verdict. They are used only to rank
  accepted issues by fit - an accepted issue labeled "good first issue"
  ranks higher among other accepted candidates.

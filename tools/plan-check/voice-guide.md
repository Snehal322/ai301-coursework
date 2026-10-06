# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

I am a student contributor in the AI 301 course, working on open-source contributions. I write direct, professional, and clear issue comments that detail objective reproduction steps, environment facts, and progress updates without fluff or artificial confidence.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

### Rule: Lead with objective evidence over opinion

Always accompany findings with exact error traces, logs, or command outputs instead of general impressions.

- Wrong: "The health check seems broken on my machine."
- Right: "Running 'python -m api.routes.health' produced 'ArgumentError: Textual SQL expression 'SELECT 1' should be explicitly declared using text()'."

### Rule: State environment details explicitly

Include exact version numbers and system details when describing reproduction results.

- Wrong: "Tested on my Mac with Python 3."
- Right: "Tested on macOS 14.5 using Python 3.11.4 and SQLAlchemy 2.0.25."

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

- Unverified claims that a bug is fixed before posting reproducible code or logs.
- Demands for issue assignment or maintainer attention.
- Generic comments like "I want to work on this" without outlining initial investigation steps.
- AI-generated fluff, long conversational preamble, or redundant apologies.

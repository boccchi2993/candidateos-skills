---
name: tailor-resume
description: Tailor an existing resume to one specific job while preserving factual accuracy. Optimize for both automated screening and fast human recall. Use the JD vocabulary naturally, foreground the strongest relevant evidence, and create one memorable candidate identity without fabricating experience.
---

# tailor-resume

## Goal

Produce a role-specific resume that does two things simultaneously:

1. survives keyword/semantic screening;
2. makes a human interviewer remember a specific candidate thesis within ~10 seconds.

## Inputs

- current resume / candidate evidence;
- target JD;
- fit report from `evaluate-fit` when available;
- company research when available.

## Rules

### Accuracy first

Never convert:

- "interested in" -> "expert in";
- transferable experience -> direct production experience;
- AI-assisted implementation -> entirely handwritten engineering;
- architecture idea -> shipped production system;
- benchmark reading -> benchmark ownership.

If the candidate uses coding Agents as the main implementation layer, say so accurately and frame the retained responsibilities: system boundaries, review, tests, acceptance, and direct takeover when needed.

### ATS / semantic screening

Mirror important JD terminology where truthful, especially:

- exact role family;
- core technical nouns;
- workflow nouns;
- expected tools;
- duration/location availability.

Do not create a keyword landfill. Terms should appear inside evidence-bearing bullets.

### Human recall

Create one memorable top-line identity such as:

> Does not collapse every Agent badcase into "model not strong enough"; decomposes failures across model / context / tool / parser / state / verifier.

or

> Treats Personal Agent personalization as a learnable but reversible policy system, not a giant memory prompt.

The identity must be supported by projects below it.

### Project order

Order projects by relevance to the role, not chronology or prestige.

A project should answer one of:

- what problem was solved;
- what architecture / workflow was designed;
- what hard decision did the candidate make;
- what failed and how was it repaired;
- what evidence shows the project is real.

### Evidence-rich bullets

Prefer:

> Built generate-review-repair with structured validation and regression tests; migration checkpoint held 70/70 tests.

over:

> Familiar with multi-Agent systems.

## Output

Return the complete revised resume content or a file-ready structure.

Also list:

- the 5–10 JD terms intentionally covered;
- any claims deliberately *not* added because evidence is weak;
- expected interviewer follow-up topics.

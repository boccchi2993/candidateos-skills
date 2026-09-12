---
name: evaluate-fit
description: Evaluate one candidate-role match using explicit evidence. Produce apply/reject, blockers, fit dimensions, interview risks, narrative angle, and recommended resume changes. Use after a JD and at least minimal company context are available. This skill may say DO NOT APPLY.
---

# evaluate-fit

## Goal

Make an evidence-backed decision, not a vibes-only match score.

The output must explain *why* a role should or should not be pursued.

## Inputs

Required:

- role / JD;
- candidate profile or resume evidence.

Preferred:

- company research;
- location and internship constraints;
- application history;
- long-term career policy.

## Evidence hierarchy

Prefer stronger evidence:

1. shipped/public project with inspectable code or demo;
2. paid delivery or real customer use;
3. tests / CI / measurable outcome;
4. interview/work outcome;
5. documented architecture/design decisions;
6. self-description;
7. interest only.

Do not treat interest as proof of capability.

## Fit decomposition

Evaluate separately:

### Hard eligibility

Examples:

- graduation year;
- degree level;
- explicit school restriction;
- mandatory location / attendance;
- internship duration;
- language requirement.

Hard blockers must not be averaged away by a high skill match.

### Direct evidence

Map each important JD requirement to concrete candidate evidence.

### Transferable evidence

Mark related but non-identical experience as transferable, not direct.

Example:

> Candidate designed Policy Memory and regression tests, but has not built a production benchmark platform.

This supports Agent evaluation reasoning, not "production eval platform experience".

### Product / technical judgment

Look for specific recurring patterns in the candidate's decisions, e.g.:

- separates model failure from context/tool/state failure;
- preserves human approval for consequential actions;
- values reversible systems;
- rejects thin abstraction layers likely to be eaten by native harnesses.

### Interview risk

Predict what a strong interviewer is likely to probe:

- coding depth;
- benchmark knowledge;
- ML training knowledge;
- English communication;
- production experience;
- role-specific domain knowledge.

### Career value

Estimate whether the role advances the candidate's stated long-term path.

### Opportunity cost

Estimate customization cost, relocation cost, response probability, and whether a better target exists.

## Anti-pattern: observed behavior != latent preference

Do not infer durable preferences from isolated actions.

Example:

```text
Candidate often takes over AI-generated code
!= candidate prefers manual coding
possible cause: generated code quality is insufficient
```

Treat actions as observations requiring causal interpretation.

## Decision labels

Use one of:

- `strong_apply`
- `apply`
- `low_cost_apply`
- `watch`
- `do_not_apply`

## Output schema

Follow `../../schemas/fit-report.schema.json` when structured output is useful.

At minimum provide:

- decision;
- fit score range, not fake precision;
- strong evidence;
- weak/missing evidence;
- hard blockers;
- interview risks;
- strongest narrative angle;
- resume changes;
- reason not to apply, when applicable.

## Scoring discipline

A numerical score is optional. If used, show component reasoning. Never output an unexplained `92%`.

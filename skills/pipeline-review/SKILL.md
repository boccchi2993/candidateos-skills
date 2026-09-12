---
name: pipeline-review
description: Review an active job-search pipeline, compare application outcomes, recommend next actions, and propose conservative updates to preferences or career policy. Use after multiple applications, interviews, rejections, or periods of no response.
---

# pipeline-review

## Goal

Turn application outcomes into better future decisions without overfitting to noise.

## Inputs

- active applications;
- application dates;
- role/company;
- resume variant used;
- outreach channel;
- current status;
- interview feedback / rejection reason if known;
- candidate's existing preferences and policies.

## Status model

Recommended states:

- discovered
- researched
- shortlisted
- prepared
- applied
- recruiter_reply
- interview_scheduled
- interviewing
- waiting
- rejected
- offer
- withdrawn

Track timestamps when available.

## Review tasks

### Pipeline health

Report:

- response rate;
- interview rate;
- time-to-response;
- stale applications;
- concentration risk by company/role/location;
- whether application volume is too low or customization cost is too high.

### Outcome attribution

Do not assume correlation is cause.

Example:

```text
Two large companies rejected the candidate
```

is not enough to conclude:

```text
Large companies are a bad target.
```

Look for explicit evidence such as school gating, coding bar, role mismatch, or location constraints.

### Policy update ladder

Use this conservative escalation path:

```text
single event
→ case note
→ repeated evidence
→ soft preference adjustment
→ repeated high-confidence evidence
→ long-term policy proposal
```

Never silently promote one failure into permanent policy.

### Next actions

Recommend concrete actions such as:

- follow up;
- wait;
- prepare interview material;
- re-tailor resume;
- deprioritize a company;
- run another discovery sweep;
- build a missing artifact / project;
- practice one interview weakness.

## Output

Produce:

- pipeline snapshot;
- what changed since last review;
- evidence-backed lessons;
- policy changes proposed (if any);
- next 3–5 actions in priority order.

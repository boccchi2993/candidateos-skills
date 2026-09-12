---
name: candidateos
description: Orchestrate a candidate-side AI job-search workflow: discover opportunities, research companies, evaluate fit with evidence, tailor resumes, draft outreach, and review application pipeline state. Use when the user wants end-to-end job search help rather than one isolated subtask. Keep consequential actions such as sending applications human-approved.
---

# CandidateOS

CandidateOS is the orchestrator for the skills in this repository.

## Core principle

Treat job search as a stateful decision system, not as independent prompts.

The default workflow is:

```text
discover-jobs
    ↓
research-company
    ↓
evaluate-fit
    ├── do_not_apply / watch
    └── apply
          ↓
     tailor-resume
          ↓
     draft-outreach
          ↓
     HUMAN APPROVAL
          ↓
      external send
          ↓
    pipeline-review
```

## Routing

Use `discover-jobs` when the user asks what to apply to next or wants a market sweep.

Use `research-company` when the company/product/technical moat is unclear or current verification matters.

Use `evaluate-fit` before spending significant time tailoring materials. This skill is allowed to reject an opportunity.

Use `tailor-resume` only after the role is sufficiently understood. Optimize for truthful JD coverage plus one memorable candidate thesis.

Use `draft-outreach` after the resume/narrative is stable.

Use `pipeline-review` after applications or interviews produce new evidence.

## State discipline

Maintain conceptual separation between:

- current case facts;
- application pipeline state;
- soft candidate preferences;
- long-term career policy.

A single event must not silently rewrite long-term policy.

## Decision discipline

A recommendation must be evidence-backed. Preserve uncertainty and distinguish:

- direct evidence;
- transferable evidence;
- inference;
- missing evidence.

Do not produce unexplained match percentages.

## Approval boundary

CandidateOS may prepare external actions but should not execute consequential actions without explicit user approval, including:

- sending emails/messages;
- submitting applications/forms;
- accepting/declining offers;
- withdrawing applications;
- publishing private candidate information.

When approval is given, execute only the approved action with the approved content/target.

## Failure-aware behavior

When an application or Agent step fails, do not default to "the model is weak" or "the candidate is weak". Decompose failure across plausible layers:

- source/data quality;
- retrieval;
- candidate evidence;
- company/JD ambiguity;
- ranking policy;
- context;
- tool/action failure;
- resume narrative;
- screening rule;
- interview performance;
- external organizational factors.

This decomposition should inform pipeline learning.

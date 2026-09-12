# CandidateOS Skills

A candidate-side Agent workflow extracted from a real AI internship search.

CandidateOS treats job hunting as a stateful decision system instead of a pile of prompts. It discovers opportunities, researches companies, ranks role fit with evidence, maintains preference/policy memory, tailors application materials, drafts outreach, and reviews the application pipeline. Consequential actions remain human-approved.

## Why this exists

Most job-search agents optimize for *more recommendations*. CandidateOS optimizes for **better decisions**:

- It can return **DO NOT APPLY**.
- It separates hard constraints, soft preferences, and long-term career policy.
- It requires evidence for positive fit claims.
- It tracks uncertainty and interview risk.
- It avoids turning a single observed behavior into a permanent preference.
- It keeps application sending, form submission, and other high-impact actions behind explicit approval.

The system is intentionally symmetric with recruiter-side agents:

```text
Recruiter side                         Candidate side
-------------                         --------------
role brief                            candidate profile
candidate retrieval                   job discovery
candidate ranking                     role fit ranking
company / person research             company research
outreach                              tailored application
recruiting pipeline                   application pipeline
preference learning                   career policy memory
```

## Architecture

```text
Candidate Profile / Career Policy
              │
              ▼
        discover-jobs
              │
              ▼
      research-company
              │
              ▼
         evaluate-fit
          │        │
      reject    shortlist
                    │
          ┌─────────┴──────────┐
          ▼                    ▼
   tailor-resume        draft-outreach
          └─────────┬──────────┘
                    ▼
              Human Approval
                    │
                    ▼
           Application State
                    │
                    ▼
            pipeline-review
                    │
                    └──> policy updates / new evidence
```

## Skills

| Skill | Purpose |
|---|---|
| `candidateos` | Orchestrate the end-to-end workflow and route work across the specialized skills. |
| `discover-jobs` | Search for jobs and normalize raw listings into comparable structured records. |
| `research-company` | Build a company/product/role dossier focused on durable differentiation and hiring reality. |
| `evaluate-fit` | Produce an evidence-backed apply/reject decision, blockers, risks, and narrative angle. |
| `tailor-resume` | Tailor a resume to one role without inventing experience or flattening the candidate into keywords. |
| `draft-outreach` | Draft concise recruiter/mentor outreach grounded in a specific role and company thesis. |
| `pipeline-review` | Review all active applications, outcomes, and repeated evidence; propose policy updates conservatively. |

The six specialized skills can be used standalone. The `candidateos` skill orchestrates them as one workflow.

## Core decision model

CandidateOS distinguishes three layers:

1. **Hard constraints** — facts that can make a role non-viable, e.g. mandatory location, graduation year, explicit school restriction.
2. **Soft preferences** — weighted preferences, e.g. Shanghai > Beijing, remote-friendly, smaller teams.
3. **Long-term policy** — stable strategic rules supported by repeated evidence, e.g. prioritize Agent runtime/evaluation over thin workflow wrappers.

A single rejection or one bad interview should **not** automatically become long-term policy.

## Evidence-first fit scoring

A fit report should never be just `92% match`.

It should explain:

- What evidence supports the fit?
- What evidence is weak or missing?
- What hard blockers exist?
- What would the interviewer likely probe?
- What is the opportunity cost of applying?
- What is the strongest candidate narrative for this specific role?

See `schemas/fit-report.schema.json`.

## Human approval boundary

CandidateOS may research, rank, draft, and recommend autonomously. It should not independently perform consequential external actions such as:

- sending an application;
- submitting a form;
- accepting an offer;
- publishing personal information;
- withdrawing another application.

These require explicit user approval at the point of action.

## OfferDAO integration

`discover-jobs` can use OfferDAO when available. The skill assumes credentials come from the environment (for example `OFFERDAO_API_KEY`) or a local config file. **Never commit API keys.** See `skills/discover-jobs/references/offerdao.md`.

## Repository layout

```text
candidateos-skills/
├── README.md
├── LICENSE
├── skills/
│   ├── candidateos/
│   ├── discover-jobs/
│   ├── research-company/
│   ├── evaluate-fit/
│   ├── tailor-resume/
│   ├── draft-outreach/
│   └── pipeline-review/
├── schemas/
├── examples/
└── docs/
```

## Status

This is an opinionated working system, not a universal career oracle. The interesting part is not the prompts; it is the decision model, state separation, evidence discipline, and feedback loop.

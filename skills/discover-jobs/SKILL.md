---
name: discover-jobs
description: Discover current job opportunities for a candidate using structured sources first, normalize them into comparable records, and maximize relevant recall before downstream fit evaluation. Use for "find jobs", "scan openings", "what should I apply to next", or periodic market sweeps. Do not make final apply decisions here; pass candidates to evaluate-fit.
---

# discover-jobs

## Goal

Find *plausibly relevant* roles without prematurely discarding opportunities, then normalize the listings so `evaluate-fit` can make a stricter decision.

Discovery and ranking are separate on purpose. A search skill that also tries to decide fit tends to miss unconventional but high-value roles.

## Inputs

Accept any combination of:

- candidate profile;
- target role families;
- preferred locations / remote constraints;
- employment type;
- recency window;
- company stage or type preferences;
- excluded companies;
- previously applied companies/roles.

If no profile is supplied, use only explicit constraints from the current conversation. Never invent missing candidate facts.

## Search order

Prefer structured/current sources over generic web search when available:

1. OfferDAO or another structured job source;
2. official company careers pages;
3. trusted job boards;
4. targeted web search for missing details.

Use multiple broad queries rather than one over-constrained AND query.

Recommended query families for AI-native product/Agent candidates:

- Agent
- Harness
- Runtime
- Evaluation / Eval / Badcase
- AI Product
- Product Engineer
- AI Coding
- Workflow
- MCP
- Memory / Context
- GUI Agent / Computer Use
- Developer Platform

## Normalization

Convert each role into the structure in `../../schemas/job.schema.json` when possible.

At minimum capture:

- company;
- role;
- location;
- employment type;
- publish date or freshness evidence;
- role summary;
- hard requirements;
- contact / application link;
- source URL;
- raw evidence snippets.

Do not infer a requirement that the posting does not state.

## Deduplication

Deduplicate by the tuple:

`company + role + team + location`

Keep the freshest source and preserve alternate source URLs when useful.

## Exclusions

You may filter obvious non-matches only when they are explicit hard constraints, e.g.:

- candidate requires internship, role is full-time only;
- role explicitly requires PhD and candidate is an undergraduate;
- explicit school list excludes the candidate;
- geography is impossible under stated constraints.

Do **not** exclude a role merely because the title is unusual. A "Product Engineer", "Agent Eval PM", or "AI for Infra Intern" may still be highly relevant.

## Output

Return:

1. a concise list of normalized opportunities;
2. which search families surfaced each role;
3. freshness / source quality;
4. any missing information that `research-company` or `evaluate-fit` should verify next.

Do not claim a role is "best fit" here. That belongs to `evaluate-fit`.

## OfferDAO

If OfferDAO is available, load `references/offerdao.md` and follow it. Never embed or print API keys.

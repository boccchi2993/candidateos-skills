# CandidateOS Architecture

## Design principles

### 1. Evidence beats self-description

A candidate claim such as "good at Agent systems" is weak evidence. A public repository, production artifact, test suite, interview outcome, or paid delivery is stronger evidence. Fit decisions should cite the strongest available evidence.

### 2. Observed behavior is not latent preference

If a candidate repeatedly takes over an Agent task, that does not necessarily mean they *prefer* manual work. The Agent may simply be failing. CandidateOS therefore treats behavior as evidence to interpret, not a policy to copy blindly.

### 3. Policy updates require repeated evidence

A single event updates the current case. Repeated consistent evidence may update a soft preference. Long-term policy changes require stronger support.

### 4. Search and ranking are different tasks

Discovery should maximize relevant recall. Fit evaluation should aggressively reject weak opportunities. Mixing both into one prompt tends to produce noisy recommendations.

### 5. Consequential actions stay approval-gated

The system may prepare applications, but sending remains an explicit approval boundary.

## State layers

```text
Ephemeral state
- current JD
- current company research
- one interview outcome

Operational state
- application pipeline
- contact state
- next actions
- resume variant used

Preference state
- preferred cities
- remote tolerance
- role-family weights

Policy state
- durable career strategy
- hard exclusions
- repeated evidence-backed rules
```

## Policy update example

Bad update:

```text
One company rejects candidate because of school background
→ Never apply to large companies again
```

Better update:

```text
Repeated explicit school-gating across several companies
→ increase penalty for roles with hard prestige filters
→ do not generalize to companies whose JDs explicitly de-emphasize school pedigree
```

## Fit decomposition

CandidateOS evaluates fit across separate dimensions:

- hard eligibility;
- direct evidence of required skills;
- transferable evidence;
- product/technical taste alignment;
- interview risk;
- role quality / learning value;
- career-path alignment;
- customization cost;
- expected response probability.

The final decision should preserve these components rather than collapse everything into one magical percentage.

---
name: consistency-audit
description: Audit the STAMPED manuscript for internal consistency across all locations where each property/dimension is defined. Use when the user asks to check consistency, audit dimensions, or verify the paper is internally coherent.
disable-model-invocation: true
---

# STAMPED Consistency Audit

Deploy one agent per STAMPED dimension in parallel (7 total).
Each agent audits a single dimension and reports findings — no edits.
This session collects results and applies fixes.

## Dimensions

| LETTER | NAME           |
|--------|----------------|
| S      | Self-contained |
| T      | Tracked        |
| A      | Actionable     |
| M      | Modularity     |
| P      | Portability    |
| E      | Ephemeral      |
| D      | Distributable  |

## Per-dimension agent task

Launch each agent with the Task tool (subagent_type: general-purpose).
Substitute `{LETTER}` and `{NAME}` from the table above into the template below.
All 7 agents run in parallel.

---

### Consistency Audit — {NAME} ({LETTER})

You are auditing the STAMPED manuscript for internal consistency of the **{NAME} ({LETTER})** property.

#### Step 1: Discovery

Find the manuscript source files (look for `.tex` files in the repository and follow any `\input{}` includes).
Read the manuscript and identify **every location** where {NAME} or its requirements ({LETTER}.1, {LETTER}.2, etc.) appear.
At minimum you should expect to find:

- An **introductory mention** where all seven STAMPED properties are first presented
- A **summary table** that gives a short definition for each property
- A **dedicated section** that treats {NAME} in detail (requirements, spectrum, cross-references)
- A **normative requirements table or list** that enumerates formal requirements per property

There may be additional locations (abstract, discussion, checklist, examples, future directions, etc.).
Record every location you find before proceeding to the audit.

#### Step 2: Audit

Compare all discovered locations against each other:

- **Definition alignment**: Does the summary table's one-liner accurately reflect the dedicated section's definition? Does the introductory mention match both?
- **Requirement coverage**: Do the requirements referenced in the dedicated section (e.g., {LETTER}.1, {LETTER}.2…) match exactly what the normative table lists? Any missing, extra, or renumbered?
- **Terminology drift**: Are the same terms used consistently? Flag cases where the same concept uses different wording across locations.
- **Cross-references from other sections**: When other dimensions' sections mention {NAME}, is what they say accurate and consistent with the {NAME} section itself?
- **Scope creep**: Does any location claim something about {NAME} that another location contradicts or doesn't support?

#### Output format

For each finding, report:

```
## [LOCATION A] vs [LOCATION B]

**Issue**: One-sentence description of the inconsistency.
**Detail**: Quote the conflicting text from each location (with line numbers).
**Suggested fix**: Which location should be authoritative, and what the other should say.
```

If the dimension is fully consistent across all locations, say so explicitly.

Do NOT edit any files. Report only.

---

## After all agents return

1. Collect all findings into a single summary, grouped by dimension.
2. Present the summary to the user.
3. Wait for the user to decide which fixes to apply — this session is where edits happen.

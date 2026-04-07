---
name: Worklog
description: Mandate evidence-chained work documentation for all multi-session advisory projects
---

# Worklog

## Applicability

- Applies to: All agents (Butler creates and maintains; all members contribute findings and decisions)

## Rule Content

### Every Multi-Session Project Must Have a Worklog

Any advisory project spanning more than one conversation — including major decision tracking, structured life reviews, and multi-session planning — must maintain a worklog under `.worklog/`.

Single-session conversations do not require a worklog. Memory consolidation in `memory/accumulated.md` is sufficient.

### Directory Structure and Naming

```
.worklog/{yyyymm}/{topic-name}/session-{n}-{label}/
  references.md
  findings.md
  decisions.md
```

- `{yyyymm}`: Year-month the project began (e.g., `202603`)
- `{topic-name}`: kebab-case description of the project (e.g., `career-pivot-2026`)
- `session-{n}-{label}`: sequential session number with descriptive label (e.g., `session-1-initial-framing`)

### Required Files Per Session

#### references.md

Record all information consulted during this session:
- User statements that informed the analysis (quote directly where significant)
- Profile data referenced (which sections, what was relevant)
- Member analyses that informed the session
- External context the user provided

Each reference must include: source description and how it was used.

#### findings.md

Record insights and patterns identified during this session:
- Patterns across the user's situation that become visible in this session
- Connections between domains identified by members
- Constraints or risks surfaced during analysis
- What the user revealed that was not in their profile

Each finding must trace back to at least one entry in `references.md`.

#### decisions.md

Record every decision the user made during this session:
- The decision itself (what was decided)
- The context that led to it
- Which members weighed in and what their positions were
- The user's final choice and their stated reasoning

Each decision must be traceable through findings to references. A decision recorded with no evidence chain is a violation.

### Evidence Chain Requirement

**references → findings → decisions** is a strict chain. Every decision must trace back through findings to references. When no external reference exists for a decision, `references.md` must explicitly note: "No external reference for {topic}. Decision based on first-principles reasoning documented in decisions.md."

### Worklog Creation Timing

Butler creates the worklog directory at the start of the first session when a project is identified as multi-session. The worklog must exist before any session-end memory consolidation for that project.

## Violation Determination

- Multi-session project has no worklog directory → Violation
- Session worklog missing any of the three required files → Violation
- `decisions.md` contains a decision with no traceable evidence → Violation
- `findings.md` contains a finding with no source reference → Violation
- Worklog directory or file names do not follow kebab-case → Violation

## Exceptions

- Sessions that produce no user decisions (e.g., exploratory conversation, emotional support without a decision point) may have an empty `decisions.md` with a note: "No decisions made this session."

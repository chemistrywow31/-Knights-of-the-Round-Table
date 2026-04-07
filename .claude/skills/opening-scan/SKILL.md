---
name: Opening Scan
description: Reads profile and memory at session start, triages member notes, detects patterns, and generates proactive interventions
---

# Opening Scan

## Description

Opening Scan is the coordinator's mandatory session-start ritual. It reads memory in a defined sequence, applies priority triage to member notes, detects patterns across recent conversations, and generates a structured internal scan report. If actionable patterns are detected, the coordinator opens the session with a natural conversational observation rather than a system notification. The scan report feeds into mode-detection.

## Users

This skill belongs exclusively to `agents/butler.md`

## Core Knowledge

### Read Sequence

Execute in this exact order. Do not skip steps.

1. `profile/base.md` — Identity, current life context
2. `profile/values.md` — Core values and decision criteria
3. `profile/domains.md` — Domain-specific profile data
4. `memory/accumulated.md` — Last 5 session summaries (read most recent first)
5. `memory/notes/*.md` — All member notes (read all, triage by priority)

### Priority Triage for Member Notes

Each note has a priority field: HIGH / NORMAL / LOW.

| Priority | Action |
|----------|--------|
| HIGH | Surface to user at session start, before they state their topic |
| NORMAL | Factor into member routing decisions; do not surface proactively unless relevant |
| LOW | Read and retain; do not surface unless directly relevant |

A note is HIGH when a member flagged: time-sensitive concern, unresolved crisis, safety-adjacent issue, or urgent follow-up requested by the user in a previous session.

### Pattern Detection

After reading all files, check for:

1. **Recurring struggles**: The same theme appears across 3+ session summaries (e.g., user repeatedly raises work-life balance but never resolves it)
2. **Unresolved open threads**: A decision or action was discussed but no outcome was recorded in subsequent sessions
3. **Approaching milestones**: Dates or deadlines mentioned in profile or memory that are within 2 weeks
4. **Emotional trajectory**: Is the user's emotional state trending positive, negative, or volatile across recent sessions?
5. **Member disagreement unresolved**: A previous roundtable or deliberation ended without the user deciding

Pattern detection is informational. Not every pattern requires intervention. Apply the threshold: **only surface a pattern if acting on it now would be materially better than waiting for the user to raise it**.

### Proactive Intervention Generation

When a HIGH note or significant pattern is detected:

**Do NOT say**: "I noticed in my scan that member X flagged you for Y..."

**DO say**: Open with a natural reference to the pattern, as if you remembered it the way a person would.

Example of correct framing:
> "Last time you mentioned the contract negotiation still hadn't reached a conclusion — would you like to start with an update on that today, or is there something else on your mind?"

The user should feel remembered, not analyzed.

### Scan Report Structure (Internal)

The scan report is not shown to the user. It is the coordinator's internal working document for the session.

```
## Session Scan Report — {date}

### Time-Sensitive Items
- {HIGH notes, verbatim from notes/}
- {Approaching milestones from profile/memory}

### Detected Patterns
- {Pattern description} — first appeared: {date} — evidence: {session refs}

### Emotional Trajectory
- {Positive / Negative / Volatile / Stable} — basis: {evidence}

### Recommended Mode
- {Daily / Roundtable / Review} — reason: {1 sentence}

### Suggested Member Activations
- Primary: {member-id} — reason
- Secondary (standby): {member-id} — reason
```

### Staleness Detection

If `memory/accumulated.md` shows no entries for more than 4 weeks, flag this:
> "We haven't had a session in a while. My context on recent events is limited — let me catch up as you fill me in today."

Do not speculate about what happened during the gap.

## Application Guide

### Scenario A: Normal Session Start

1. Read all files in sequence (silently)
2. Build scan report internally
3. Check for HIGH priority notes → if present, open with natural reference
4. Check for approaching milestones → if present, weave into opening
5. If nothing urgent: open with neutral welcome and let user lead
6. Pass scan report context to mode-detection

### Scenario B: Multiple HIGH Priority Notes

When 2+ HIGH notes exist:

Prioritize by: (1) recency, (2) domain relevance to user's stated priority areas, (3) member confidence level.

Address only the highest-priority item in the opening. Other HIGH items surface when relevant during the session.

Do not open with a list of problems. One focused opening, not a status report.

### Scenario C: No Memory Exists Yet (New User)

If `memory/accumulated.md` does not exist or is empty:

- Skip pattern detection and note triage (nothing to read)
- Scan report contains only: profile summary, no patterns, recommended mode = daily
- Open naturally without references to memory
- Proceed with profile-interview skill if onboarding is incomplete

## Quality Checkpoints

- [ ] Files read in the correct sequence (profile before memory)
- [ ] ALL member notes read, not just recent ones
- [ ] HIGH notes surfaced proactively (not silently absorbed)
- [ ] Proactive intervention phrased as natural memory, not system report
- [ ] Scan report produced before mode-detection runs
- [ ] No speculation about events during session gaps

## Examples

### Normal Case: Session with One HIGH Note and No Pattern

**Memory state**: 3 session summaries, one HIGH note from psychologist: "User mentioned feeling burned out but dismissed it quickly. Watch for this resurfacing."

**Coordinator opening**:
> "How have things been lately? Last time you mentioned feeling a bit tired — has that gotten any better since?"

Scan report internal: HIGH note surfaced, emotional trajectory: possible negative trend, recommended mode: daily, primary: psychologist on standby.

### Edge Case: Three Patterns Detected Simultaneously

**Memory state**: 5 sessions, patterns: (1) recurring avoidance of financial planning discussion, (2) startup pivot mentioned twice but never followed up, (3) relationship with partner mentioned with increasing tension

**Priority decision**: The startup pivot is an open thread. The financial avoidance is recurring but not urgent. The relationship tension is most recent and emotionally loaded.

**Coordinator opening**: Reference the most recent emotionally relevant thread (relationship), not all three.

Surface the startup pivot when relevant in conversation. Note the financial avoidance for cfo routing if finances come up.

### Rejection/Failure Case: Member Note Contains Speculative Content

**Example bad note from a member**: "User is probably considering leaving their job based on how they talked about work"

**Coordinator action**: Treat this as LOW priority regardless of the member's assigned priority. Do not surface speculative inferences as if they were facts. Memory criteria require explicitly stated information, not inferred states.

Log this as a quality issue in the session's memory consolidation: member notes should record facts, not inferences.

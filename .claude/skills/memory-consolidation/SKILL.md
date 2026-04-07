---
name: Memory Consolidation
description: End-of-session process where members leave notes, coordinator writes a summary, and oversized memory is archived
---

# Memory Consolidation

## Description

Memory Consolidation is the terminal skill for every session. It runs in three sequential phases: members leave structured notes for the next session, the coordinator writes a session summary to accumulated memory, and the coordinator checks whether accumulated memory needs archiving. This ensures memory stays accurate, actionable, and within size bounds across hundreds of sessions.

## Users

This skill belongs exclusively to `agents/butler.md`

Members contribute Phase 1 notes when activated by the coordinator at session close.

## Core Knowledge

### Memory Criteria (Three Gates)

Before writing anything to memory, apply all three gates:

1. **Durable**: Is this information likely to remain true for months? Fleeting mood ≠ durable. Pattern across 3+ sessions = durable.
2. **Actionable**: Does this information change how a future member would respond? Background color ≠ actionable. Known trigger pattern = actionable.
3. **Explicitly stated**: Did the user directly state this, or is it inferred? Inference must NOT enter memory as fact. Record inferences only as hypotheses, labeled as such.

Information that fails any gate is not written to memory.

### Phase 1 — Member Notes

At session close, the coordinator asks each active member: "Do you have observations worth flagging for next time?"

Members write to `memory/notes/{member-id}.md` using this structure:

```markdown
## Note — {date}

**Priority**: HIGH | NORMAL | LOW
**Context**: {1 sentence: what situation generated this observation}
**Observation**: {The durable, actionable, explicitly stated fact or pattern}
**Suggested Action**: {What the coordinator or this member should do with this next session}
**Expires**: {date when this note is no longer relevant, or "ongoing"}
```

**Priority assignment criteria**:
- HIGH: Requires proactive opening in next session (crisis, unresolved urgent decision, explicit user request for follow-up)
- NORMAL: Useful routing context for next session
- LOW: Background enrichment, useful if the topic resurfaces

Members clear their own stale notes when updating. A note past its Expires date is deleted, not archived.

### Phase 2 — Session Summary

The coordinator writes one entry to `memory/accumulated.md`:

```markdown
## Session — {date}

**Topics covered**: {comma-separated list}
**Key decisions or conclusions**: {bullet points — explicitly decided things only}
**Open threads**: {things discussed but not resolved — max 3}
**Member positions recorded**: {if members disagreed, note each position}
**Emotional state observed**: {only if explicitly stated by user — "user said they felt X"}
**Profile update needed**: {yes/no — if yes, which field}
```

Keep each entry under 200 words. If a session was rich, write more bullets per category, not longer sentences.

### Phase 3 — Consolidation Check

After writing the new session entry, count total lines in `memory/accumulated.md`.

If line count exceeds 500:
1. Archive current content to `memory/archive/{YYYY-MM}.md`
2. Create fresh `memory/accumulated.md` containing:
   - Last 5 session summaries (verbatim copy)
   - Section: `## Active Threads` — unresolved threads from the archived period
   - Section: `## Established Patterns` — durable patterns that persist

The archived file is never deleted. It is read only when context recovery is needed.

### Conflict Resolution

When two members have contradictory observations about the same user behavior:

1. Most recent observation wins for active memory
2. Both observations are recorded with timestamps and member attribution
3. Format: `[{date}, {member-id}]: {observation} | CONFLICTS WITH [{earlier-date}, {member-id}]: {earlier observation}`
4. Do not silently overwrite the earlier observation

### Profile Update Trigger

If the session contained significant new information about the user's life context (job change, major relationship change, new venture launched, significant health event), the coordinator updates the relevant profile section immediately after writing the session summary.

Profile updates are prefixed: `*Updated: {date}*`

## Application Guide

### Scenario A: Normal Session Close

1. Coordinator signals session end: "Before we wrap up, I need to do a quick internal check-in with the partners who were active today."
2. Coordinator requests notes from each active member (parallel — all members asked simultaneously)
3. Members write notes (or explicitly decline: "Nothing to flag")
4. Coordinator writes session summary to accumulated.md
5. Coordinator checks line count → if under 500, done
6. If over 500, execute archival procedure

### Scenario B: Session Ended Abruptly (User Disconnected Mid-Conversation)

1. Write a partial session summary flagged: `**Status: INCOMPLETE**`
2. Note the last known topic and state
3. Member notes are optional — members write only what they confidently observed before the cutoff
4. Do not speculate about session content that did not occur

### Scenario C: No Meaningful Content to Record

If the session was extremely brief (user said 2-3 sentences and left) or purely administrative:

Write a minimal entry: `## Session — {date} — *Brief/administrative only. No memory-worthy content.*`

Do not force memory entries. Empty sessions do not generate notes.

## Quality Checkpoints

- [ ] All three memory gates applied before writing (durable, actionable, explicit)
- [ ] Inferences clearly labeled as hypotheses, not facts
- [ ] Each member note follows the standard structure with all required fields
- [ ] Session summary is under 200 words
- [ ] Consolidation check performed (line count verified)
- [ ] Conflicts recorded with both versions and timestamps
- [ ] Profile updates applied if significant life changes occurred

## Examples

### Normal Case: Session with Business Decision

**Session**: User discussed whether to accept a board position at another startup.

**startup-partner note**:
```
Priority: NORMAL
Context: User evaluated board seat opportunity at Company X
Observation: User stated "I'm worried about spreading too thin" — this is a recurring concern
Suggested Action: If the board seat topic resurfaces, I'll reference this pattern explicitly
Expires: 2026-06-01
```

**Session summary**:
```
## Session — 2026-03-27
Topics covered: board seat evaluation, time allocation
Key decisions: Decision deferred — user wants to consult partner first
Open threads: Board seat decision still open
Member positions recorded: startup-partner cautious, business-strategist favorable with conditions
Emotional state observed: User said "I'm excited but nervous"
Profile update needed: No
```

### Edge Case: Member Flags Concerning Emotional Pattern

**Observation**: psychologist has seen low mood mentioned in 3 consecutive sessions.

**psychologist note**:
```
Priority: HIGH
Context: Low mood mentioned in sessions 2026-03-13, 2026-03-20, 2026-03-27
Observation: User explicitly described feeling "drained" in each session. Three-session pattern, not isolated.
Suggested Action: Open next session checking in on energy/mood before other topics
Expires: 2026-04-10
```

This note is HIGH because the pattern is explicit and the suggested action is proactive.

### Rejection/Failure Case: Member Writes Speculative Note

**Bad note from cfo**:
```
Priority: HIGH
Observation: User seems to be in financial trouble based on the way they talked about money
```

**Coordinator action**: Reject this note. "Seems to be" fails the explicitly stated gate. Rewrite as:

```
Priority: NORMAL
Observation: User expressed anxiety when discussing investment losses. No explicit financial crisis stated.
Suggested Action: If finances come up, check in gently before diving into analysis.
```

Do not let speculative inferences enter memory as facts. Return the note to the member for correction.

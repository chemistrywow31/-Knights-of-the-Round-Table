---
name: Profile Portability
description: Prohibit hardcoded user data in agent definitions and enforce profile as a swappable module
---

# Profile Portability

## Applicability

- Applies to: All agents (all 14 members and butler)

## Rule Content

### Absolute Prohibition: No User Data in Agent Files

No agent .md file may contain user-specific information of any kind:

- Personal identifiers (name, age, gender, occupation, location)
- Family information (partner, children, parents)
- Financial specifics (income, debt, assets)
- Health information (conditions, medications)
- Personal history (past decisions, significant events)
- Stated preferences or goals tied to a specific person

User data lives exclusively in `profile/` and `memory/`. It must never be embedded in agent definitions.

### Profile Reference Standard

All agents access user data exclusively through these paths:

```
@profile/base.md      ← Read at dispatch
@profile/values.md    ← Read at dispatch
@profile/domains.md   ← Read at dispatch
@memory/accumulated.md ← Read at dispatch (coordinator only, or as provided by coordinator)
@memory/notes/{member-id}.md ← Read by relevant member at dispatch
```

Agents must not reconstruct user data from memory or reference user details inline. If the profile files are empty, the agent must not assume any user details.

### The Swap Test

The swap test validates portability. Apply it by:

1. Delete all files in `profile/` (keep the directory)
2. Delete all files in `memory/accumulated.md` and `memory/notes/` (keep the directories and `memory/archive/`)
3. Attempt to start a new onboarding conversation

**Pass condition**: All 14 members and the coordinator operate normally. No agent fails, references missing data, or assumes user-specific context. The team is ready to onboard a new person.

**Fail condition**: Any agent references a specific person's details, produces an error due to missing profile data, or behaves as if it knows something about the previous user.

Run the swap test before deploying the team for any new user.

### Memory Isolation

`memory/` is user-specific and swappable alongside `profile/`. Accumulated memory and member notes belong to the user-team relationship, not to the team itself.

When performing a user swap, delete both `profile/` contents and `memory/` contents. The team architecture — agents, skills, rules — remains unchanged.

## Violation Determination

- Any agent .md file contains a person's name, age, occupation, or any other user-specific detail → Violation
- Agent produces output referencing user details that are not present in the current profile files → Violation
- Swap test fails: agent errors or references missing user data after profile deletion → Violation
- Agent embeds profile content in its own .md during a session (writing user data into its definition) → Violation

## Exceptions

- `profile/` and `memory/` files themselves contain user data by design — this is their purpose
- During a live session, agents may hold user data in their working context window. The prohibition applies to persistent storage in agent definition files only

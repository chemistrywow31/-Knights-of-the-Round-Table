---
name: Context Management
description: Enforce task isolation, summary-based reporting, and worklog-based context recovery for all agents
---

# Context Management

## Applicability

- Applies to: All agents (Life Steward has additional coordinator responsibilities)

## Rule Content

### Coordinator Must Include Worklog Paths in Task Dispatch

When Life Steward dispatches a task to any member via the Task tool, the dispatch must include:

1. **Current worklog path**: Where this member must write outputs, if a multi-session worklog is active
2. **Upstream reference paths**: Paths to relevant profile or memory files this member must read
3. **Task scope summary**: What this specific task must accomplish — not the entire conversation history

Life Steward must not pass full conversation content inline. Pass paths; let the member read what it needs.

### XML Tag Separation in Dispatch

When dispatching tasks with variable data, wrap each variable block in descriptive XML tags:

```
<task_scope>Provide financial risk analysis for the startup funding decision.</task_scope>
<user_context>User is considering raising a seed round. Details in profile/domains.md.</user_context>
<memory_path>memory/accumulated.md</memory_path>
```

Instructions stay outside the tags. Data goes inside.

### Member Return Format: Structured Summaries

When a member completes a task and returns results to Life Steward, the return must be a structured summary:

```markdown
## Task Completion: {task name}

### Status: {DONE / DONE_WITH_CONCERNS / BLOCKED / NEEDS_CONTEXT}

### Key Outcomes
- {Outcome 1}
- {Outcome 2}

### Decisions Made
- {Decision with brief rationale}

### Issues / Blockers (if any)
- {Issue description and suggested resolution}
```

Members must not return raw conversational output exceeding 500 words without a worklog reference.

### Completion Status Protocol

Every member must end its task with exactly one of these statuses:

- **DONE**: All steps completed. Evidence of completion provided.
- **DONE_WITH_CONCERNS**: Task completed, but Life Steward must be aware of an issue. List each concern with recommended action.
- **BLOCKED**: Cannot proceed. State what was attempted (up to 3 attempts), what failed, and what is needed. Do not retry the same approach more than 3 times.
- **NEEDS_CONTEXT**: Missing profile or conversation information needed to begin or continue. List each missing item.

Life Steward must handle each status before proceeding. Do not re-dispatch a BLOCKED task without addressing the blocker.

### Task Isolation via Subagents

Every independent unit of advisory work executes as a separate Task (subagent). This ensures:
- Each member starts with a clean context window focused on its specific task
- Life Steward's context accumulates only summaries, not execution details
- Parallel roundtable participants cannot see each other's in-progress outputs

Life Steward must not perform advisory work inline. All member-level analysis goes through Task dispatch.

### Memory as Context Offloading

Once information is written to `memory/accumulated.md` or a member note, members release it from active context. The memory system is the persistent external memory:
- Members read from memory paths instead of receiving full history in task dispatch
- At conversation end, Life Steward writes consolidated memory; subsequent conversations read from memory, not from the current conversation context

## Violation Determination

- Life Steward dispatches a Task without specifying the relevant profile or memory paths → Violation
- Life Steward passes full conversation history inline instead of referencing memory paths → Violation
- Member returns unstructured output exceeding 500 words without worklog reference → Violation
- Life Steward performs advisory analysis inline instead of dispatching a Task → Violation
- A BLOCKED task is re-dispatched without resolving the stated blocker → Violation

## Exceptions

- During initial onboarding (profile-interview), Life Steward may include more inline context because no memory files exist yet to reference
- Brief clarification exchanges (under 100 words) between Life Steward and a member do not require structured return format

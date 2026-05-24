---
name: subagent-driven-development
description: Use when executing implementation plans with independent tasks in the current session
---

# Subagent-Driven Development

Execute a plan by dispatching a fresh subagent per task, with two-stage review after each. **Core principle:** fresh subagent per task + spec-compliance review *then* code-quality review = high quality, fast iteration.

**Why subagents:** each gets exactly the context you construct — never your session history — so they stay focused and your own context stays free for coordination.

**Use when:** you have a plan, tasks are mostly independent, and you're staying in this session. (Tightly coupled tasks → manual; parallel session → use `executing-plans`.)

**Continuous execution:** run all tasks without pausing to check in. Only stop for an unresolvable BLOCKED status, genuine ambiguity, or completion. No "should I continue?" prompts.

## Per-task loop

1. **Once up front:** read the plan, extract all tasks with full text + context, create a TodoWrite list.
2. **Dispatch implementer** (`./implementer-prompt.md`) with the task's full text + scene-setting context — never make the subagent read the plan file. Answer any questions it asks *before* it implements. It implements, tests, commits, self-reviews.
3. **Spec-compliance review** (`./spec-reviewer-prompt.md`): does the code match the spec, nothing missing or extra? Issues → same implementer fixes → re-review until ✅.
4. **Code-quality review** (`./code-quality-reviewer-prompt.md`) — only after spec is ✅. Issues → implementer fixes → re-review until approved.
5. Mark task complete; next task.
6. **After all tasks:** dispatch a final reviewer over the whole implementation, then use `finishing-a-development-branch`.

## Implementer status handling

- **DONE** → spec review.
- **DONE_WITH_CONCERNS** → read concerns; fix correctness/scope ones before review, note observations.
- **NEEDS_CONTEXT** → provide the missing info, re-dispatch.
- **BLOCKED** → fix the cause: more context, or a more capable model, or split the task, or escalate to the human if the plan is wrong. Never force the same model to retry unchanged.

## Model selection

Least capable model that fits the role: mechanical task in 1-2 files with a complete spec → cheap/fast model; multi-file integration/judgment → standard; architecture/design/review → most capable.

## Red flags (never)

Implement on main/master without consent · skip either review or its re-review loop · proceed with open issues · run code-quality review before spec is ✅ · dispatch multiple implementers in parallel (conflicts) · make the subagent read the plan file · ignore its questions · let self-review replace actual review · fix a failed subagent's work manually (re-dispatch instead).

## Integration

Pairs with `using-git-worktrees` (isolated workspace), `writing-plans` (produces the plan), `requesting-code-review` (reviewer template), `finishing-a-development-branch` (wrap up). Subagents follow `test-driven-development`.

---
name: using-superpowers
description: Use when starting any conversation - establishes how to find and use skills, requiring Skill tool invocation before ANY response including clarifying questions
---

<SUBAGENT-STOP>
If you were dispatched as a subagent to execute a specific task, skip this skill.
</SUBAGENT-STOP>

# Using Skills

**The rule:** if there's even a ~1% chance a skill applies, invoke it via the `skill` tool BEFORE responding or acting — including before clarifying questions or exploring code. If a loaded skill doesn't fit, discard it.

**Instruction priority:** (1) the user's explicit instructions (CLAUDE.md / AGENTS.md / direct requests) win over everything; (2) skills override default behavior where they conflict; (3) default behavior is lowest. If the user says "don't use TDD," don't.

**How to load:** use the native `skill` tool to list/load skills. Follow a loaded skill directly; never `Read` skill files manually.

**Order when several apply:** process skills first (brainstorming, debugging — they decide HOW), then implementation skills. "Build X" → brainstorm first. "Fix bug" → debug first.

**Skill types:** *rigid* (TDD, debugging) — follow exactly, don't dilute the discipline. *flexible* (patterns) — adapt to context. The skill says which.

**If a skill has a checklist,** make one todo per item before starting.

**Don't rationalize skipping.** "Just a quick question / simple thing / I'll do one thing first / I already know this" all mean STOP and check for a skill. Any action — including answering — is a task. Skills evolve; use the current version, not memory.

**User instructions say WHAT, not HOW.** "Add X" / "Fix Y" does not mean skip a skill's workflow.

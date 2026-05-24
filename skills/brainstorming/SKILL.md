---
name: brainstorming
description: "You MUST use this before any creative work - creating features, building components, adding functionality, or modifying behavior. Explores user intent, requirements and design before implementation."
---

# Brainstorming Ideas Into Designs

Turn ideas into a fully-formed design through collaborative dialogue, then hand off to implementation.

<HARD-GATE>
Do NOT invoke any implementation skill, write code, scaffold, or take any implementation action until you have presented a design and the user has approved it. This applies to EVERY project regardless of perceived simplicity.
</HARD-GATE>

"Too simple to need a design" is the anti-pattern — that's where unexamined assumptions waste the most work. The design can be a few sentences for a simple project, but you must present it and get approval.

## Checklist (make one todo per item, do in order)

1. **Explore project context** — files, docs, recent commits.
2. **Ask clarifying questions** — one at a time, multiple-choice when possible. Focus on purpose, constraints, success criteria. (If the request is several independent subsystems, stop and help decompose into sub-projects first — each gets its own spec → plan → build cycle.)
3. **Propose 2-3 approaches** — with trade-offs; lead with your recommendation and why.
4. **Present the design** — in sections scaled to complexity (a few sentences to ~250 words each); confirm each section before moving on. Cover architecture, components, data flow, error handling, testing. Design for isolation: small units with one clear purpose and well-defined interfaces.
5. **Write the design doc** to `docs/superpowers/specs/YYYY-MM-DD-<topic>-design.md` and commit it (user's preferred location overrides).
6. **Spec self-review** — scan for placeholders/TODOs, internal contradictions, scope creep, ambiguous requirements; fix inline.
7. **User reviews the written spec** — ask them to review before proceeding; if they request changes, revise and re-review.
8. **Transition to implementation** — invoke the `writing-plans` skill. That is the ONLY skill you invoke after brainstorming (not frontend-design, mcp-builder, etc.).

## Principles

One question at a time · multiple-choice preferred · YAGNI ruthlessly · always explore 2-3 approaches · validate incrementally · go back and clarify when something doesn't fit · follow existing patterns in existing codebases and stay focused (no unrelated refactoring).

*(If a visual companion for mockups/diagrams would help, offer it once as its own message before asking visual questions; see `visual-companion.md`.)*

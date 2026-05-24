---
name: writing-skills
description: Use when creating new skills, editing existing skills, or verifying skills work before deployment
---

# Writing Skills

**Writing a skill IS TDD applied to process documentation.** You write a test (a pressure scenario run on a subagent), watch it fail (baseline behavior without the skill), write the minimal skill, watch it pass (the agent now complies), then refactor (close loopholes). If you didn't watch an agent fail without the skill, you don't know the skill teaches the right thing.

**REQUIRED BACKGROUND:** understand `test-driven-development` first — same RED-GREEN-REFACTOR cycle. **Official patterns:** see `anthropic-best-practices.md`.

## The Iron Law

```
NO SKILL WITHOUT A FAILING TEST FIRST
```

Applies to new skills AND edits. Wrote/edited before testing? Delete it, start over — not for "just a section" or "doc update." No exceptions.

## What a skill is

A reusable reference guide for a proven technique, pattern, or tool — NOT a narrative of how you solved something once. Create one when the technique wasn't obvious, applies broadly (not project-specific → that goes in CLAUDE.md), and you'd reference it again. If it's enforceable by regex/validation, automate it instead.

## SKILL.md structure

Frontmatter: `name` (letters/numbers/hyphens only) and `description`, max 1024 chars total.

**The critical CSO rule — description = WHEN to use, NOT what it does.** Start with "Use when…" and give concrete triggers/symptoms. NEVER summarize the workflow: testing showed that when the description summarizes the process, the model follows the description and skips the skill body (e.g. a "code review between tasks" summary caused ONE review instead of the skill's TWO). Third person, technology-agnostic unless the skill is technology-specific.

```
# ❌ description: Use when executing plans - dispatches subagent per task with review between tasks
# ✅ description: Use when executing implementation plans with independent tasks in the current session
```

Body: Overview + core principle → When to use (symptoms, and when NOT to) → core pattern/quick-reference table → implementation (inline for simple, link to a file for heavy reference) → common mistakes.

**Keep inline:** principles, concepts, code patterns <50 lines. **Separate file:** heavy reference (100+ lines), reusable scripts/tools. **Token efficiency:** frequently-loaded skills <200 words; others <500. Move flag details to `--help`, cross-reference instead of repeating, one excellent example beats many.

## Cross-referencing other skills

Use the skill name with an explicit marker: `**REQUIRED SUB-SKILL:** Use superpowers:test-driven-development`. Never use `@path` links — they force-load the file and burn context.

## Flowcharts

Only for non-obvious decision points or loops where you'd stop too early. Never for reference material (use tables), code (use markdown blocks), or linear steps (use numbered lists). Style: `graphviz-conventions.dot`. Render to SVG with `./render-graphs.js ../some-skill`.

## Bulletproofing discipline skills

Close loopholes explicitly (don't just say "delete it" — forbid "keep as reference", "adapt it", etc.). State "violating the letter is violating the spirit" to cut off spirit-vs-letter arguments. Build a rationalization table and a red-flags list from what agents actually say in baseline testing. Persuasion research: `persuasion-principles.md`.

## RED-GREEN-REFACTOR for skills

- **RED:** run a pressure scenario on a subagent WITHOUT the skill; document their exact choices and rationalizations verbatim.
- **GREEN:** write the minimal skill addressing those specific rationalizations; re-run — agent should comply.
- **REFACTOR:** new rationalization appears → add an explicit counter → re-test until bulletproof.

Full methodology (pressure types, plugging holes): `testing-skills-with-subagents.md`.

## STOP before the next skill

After writing ANY skill, complete testing + deployment for it before starting another — no batching untested skills (that's deploying untested code).

## Checklist (make a todo per item)

RED: pressure scenarios (3+ combined pressures for discipline skills) → run without skill → record baseline. GREEN: valid frontmatter; "Use when…" description in third person with no workflow summary; search keywords; overview + core principle; addresses the baseline failures; one excellent example; run with skill and verify compliance. REFACTOR: capture new rationalizations → counters → rationalization table → red-flags list → re-test. Deploy: commit + push to the fork.

---
name: writing-plans
description: Use when you have a spec or requirements for a multi-step task, before touching code
---

# Writing Plans

Write an implementation plan for an engineer who knows the language but nothing about this codebase or domain, and has questionable taste. Spell out everything: exact files, the actual code, exact test commands and expected output, as bite-sized tasks. DRY, YAGNI, TDD, frequent commits.

**Announce:** "I'm using the writing-plans skill to create the implementation plan." **Save to:** `docs/superpowers/plans/YYYY-MM-DD-<feature>.md` (user's preferred location overrides).

## File structure first

Before tasks, map which files are created/modified and the one responsibility of each. Small, focused files with clear interfaces; files that change together live together (split by responsibility, not layer). In existing codebases, follow established patterns.

## Bite-sized tasks

Each step is one 2-5 minute action. A task is a TDD cycle:

```markdown
### Task N: [Component]
**Files:** Create `path/file.py` · Test `tests/test_file.py`
- [ ] Step 1: Write the failing test   <actual test code>
- [ ] Step 2: Run it, verify it fails   Run: `pytest tests/test_file.py::test_x -v`  Expected: FAIL (not defined)
- [ ] Step 3: Write minimal implementation   <actual code>
- [ ] Step 4: Run it, verify it passes   Expected: PASS
- [ ] Step 5: Commit   `git commit -m "feat: ..."`
```

Plan header must state Goal (one sentence), Architecture (2-3 sentences), Tech Stack, and point the worker to `subagent-driven-development` or `executing-plans`.

## No placeholders (these are plan failures)

No "TBD/TODO/implement later", no "add appropriate error handling/validation", no "write tests for the above" without the test code, no "similar to Task N" (repeat the code), no references to types/functions not defined in some task. If a step changes code, show the actual code; if it runs something, show the exact command and expected output.

## Self-review (run it yourself, not a subagent)

1. **Spec coverage** — every spec requirement maps to a task; list and fill gaps.
2. **Placeholder scan** — fix any of the above.
3. **Type/name consistency** — signatures and names used in later tasks match earlier definitions.

Fix issues inline.

## Handoff

After saving, offer: **(1) Subagent-driven (recommended)** — fresh subagent per task, review between → use `subagent-driven-development`; **(2) Inline** — execute here with checkpoints → use `executing-plans`.

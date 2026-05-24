---
name: test-driven-development
description: Use when implementing any feature or bugfix, before writing implementation code
---

# Test-Driven Development (TDD)

Write the test first. Watch it fail. Write minimal code to pass. If you didn't watch the test fail, you don't know it tests the right thing.

## The Iron Law

```
NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST
```

Wrote code before the test? Delete it and start fresh from the test — don't keep it as "reference," don't "adapt" it. Delete means delete.

**Use for:** new features, bug fixes, refactoring, behavior changes. **Exceptions (ask your human partner first):** throwaway prototypes, generated code, config. "Skip TDD just this once" is rationalization.

## Red → Green → Refactor

1. **RED — write one failing test.** One behavior, clear name, real code (mocks only if unavoidable). The test should show the desired API.
2. **Verify RED (mandatory).** Run it. Confirm it *fails* (not errors) and fails for the right reason — the feature is missing, not a typo. Passes immediately? It tests existing behavior — fix the test.
3. **GREEN — minimal code to pass.** Simplest thing that works. No extra features, no "while I'm here" improvements (YAGNI).
4. **Verify GREEN (mandatory).** Run it. Test passes, other tests still pass, output is clean (no errors/warnings). Test fails? Fix the code, not the test.
5. **REFACTOR.** Only when green: remove duplication, improve names, extract helpers — without adding behavior. Stay green.
6. **Repeat** for the next behavior.

## Bug fixes

Reproduce the bug with a failing test first, then follow the cycle. The test proves the fix and prevents regression. Never fix a bug without a test.

## Red flags (STOP — start over with TDD)

Code before test · test added "later" · test passes immediately · can't explain why it failed · "I already manually tested it" · "tests-after achieve the same thing" (no: tests-first ask *what should this do?*, tests-after ask *what does this do?* and are biased by your implementation) · "deleting my work is wasteful" (sunk cost — unverified code is debt).

## When stuck

Test hard to write → design is too complex or too coupled; simplify the interface or use dependency injection. Don't know how to test → write the wished-for API and assert on it first.

## Checklist before "done"

- [ ] Every new function has a test
- [ ] Watched each test fail for the expected reason before implementing
- [ ] Minimal code to pass; all tests green; output clean
- [ ] Real code under test (mocks only if unavoidable); edge/error cases covered

Can't check every box? You skipped TDD — start over.

---
name: systematic-debugging
description: Use when encountering any bug, test failure, or unexpected behavior, before proposing fixes
---

# Systematic Debugging

Random fixes waste time and create new bugs. Find the root cause before changing anything.

## The Iron Law

```
NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST
```

Use this for any technical issue (test failure, crash, unexpected behavior, perf, build break) — *especially* under time pressure, when "one quick fix" seems obvious, or when a previous fix didn't work. Simple bugs have root causes too.

## Phase 1 — Root cause (before ANY fix)

- **Read the error completely** — stack trace, line numbers, codes. It often names the fix.
- **Reproduce reliably.** Exact steps? Every time? Not reproducible → gather more data, don't guess.
- **Check recent changes** — git diff, new deps, config/env differences.
- **Multi-component systems:** add diagnostic logging at each component boundary (what enters, what exits, env/config) and run once to see *where* it breaks before investigating that component.
- **Trace data flow backward:** where does the bad value originate? Fix at the source, not the symptom.

## Phase 2 — Pattern

Find similar working code in the same codebase. List every difference between working and broken, however small ("that can't matter" is how bugs hide). If following a reference, read it completely.

## Phase 3 — Hypothesis

State one specific hypothesis ("X is the root cause because Y"). Test it with the smallest possible change, one variable at a time. Worked → Phase 4. Didn't → form a *new* hypothesis, don't pile fixes on top. Don't understand something? Say so; don't pretend.

## Phase 4 — Fix

1. Write a failing test reproducing the bug (use test-driven-development).
2. Implement ONE fix addressing the root cause — no bundled refactors.
3. Verify: test passes, nothing else broke, issue actually resolved.
4. Didn't work? Return to Phase 1 with the new information.
5. **3+ fixes failed** = the architecture is likely wrong, not the hypothesis. STOP and discuss fundamentals with your human partner before trying fix #4.

## Red flags (STOP, return to Phase 1)

"Quick fix now, investigate later" · "just try changing X" · multiple changes at once · "skip the test, I'll verify manually" · "it's probably X" · proposing fixes before tracing data flow · "one more fix attempt" after 2+ failures. Signals from your human partner — "stop guessing", "is that not happening?", "we're stuck?" — mean your approach isn't working: restart at Phase 1.

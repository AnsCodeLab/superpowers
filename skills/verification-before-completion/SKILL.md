---
name: verification-before-completion
description: Use when about to claim work is complete, fixed, or passing, before committing or creating PRs - requires running verification commands and confirming output before making any success claims; evidence before assertions always
---

# Verification Before Completion

Claiming work is done without verifying is dishonesty, not efficiency. **Evidence before claims, always.**

## The Iron Law

```
NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE
```

If you haven't run the verification command *in this message*, you can't claim it passes.

## The gate (before any success claim or expression of satisfaction)

1. **Identify** the command that proves the claim.
2. **Run** it fresh and in full.
3. **Read** the full output — exit code, failure count.
4. **Verify** the output confirms the claim. If not, state the actual status with evidence.
5. Only then make the claim — *with* the evidence.

## What each claim actually requires

| Claim | Proof needed (not sufficient: "should", prior run, "looks good") |
|-------|------|
| Tests pass | Test command output, 0 failures |
| Build succeeds | Build exit 0 (linter passing ≠ compiling) |
| Bug fixed | The original symptom now passes |
| Regression test works | Red-green verified: revert fix → test MUST fail → restore → passes |
| Requirements met | Line-by-line checklist against the plan |
| Agent/subtask done | VCS diff shows the changes (not the agent's "success" report) |

## Red flags (STOP)

Using "should / probably / seems to" · saying "Great!/Perfect!/Done!" before running anything · about to commit/push/PR without verification · trusting an agent's success report · "just this once" · tired and wanting it over. Any wording that implies success without having run the check applies here — spirit over letter. Run the command, read the output, *then* claim the result.

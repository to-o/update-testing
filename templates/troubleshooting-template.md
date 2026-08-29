# <Symptom>

- Status: DRAFT | VERIFIED | STALE
- Applies to: <scope/version/environment>
- Last verified: <YYYY-MM-DD or unknown>

## Symptom

<What the tester actually observes.>

## Minimal Evidence

Collect first:

- <evidence 1>
- <evidence 2>

## Observable State

Record the current state before retrying:

- <state / phase / last successful checkpoint>

## Fast Checks

Perform low-cost checks in order:

1. <check>
2. <check>

## Meaningful Retry

Retry only when new information or a changed condition makes the retry meaningful:

- <retry condition/action>

Do not repeat an unchanged action mechanically.

## Verified Fallback

- <fallback>

If none exists, state `No verified fallback`.

## Verdict / Reason

Use one Verdict:

- PASS
- FAIL
- BLOCKED
- SKIPPED

If Verdict is `FAIL` or `BLOCKED`, record one Reason:

- PRODUCT
- ENVIRONMENT
- AUTOMATION
- DEPENDENCY
- UNKNOWN

Example:

```text
Verdict: FAIL
Reason: PRODUCT
```

## Stop Condition

Stop investigating this symptom when:

- <condition>

Record the result and continue independent scenarios where possible.

## Related Playbooks / Knowledge

- <links>

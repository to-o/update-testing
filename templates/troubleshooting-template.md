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

## Fast Checks

Perform low-cost checks in order:

1. <check>
2. <check>

## Meaningful Retry

Retry only when this changes a relevant condition:

- <retry condition/action>

Do not repeat an unchanged action indefinitely.

## Verified Fallback

- <fallback>

If none exists, state `No verified fallback`.

## Classification

Use the evidence to select one:

- PRODUCT_FAIL
- ENVIRONMENT_FAIL
- AUTOMATION_FAIL
- BLOCKED

## Stop Condition

Stop investigating this symptom when:

- <condition>

Record the result and continue independent scenarios where possible.

## Related Playbooks / Knowledge

- <links>

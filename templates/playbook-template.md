# <Scenario Name>

- Status: DRAFT | VERIFIED | STALE
- Scope: <product/version/environment>
- Last verified: <YYYY-MM-DD or unknown>

## Goal

<What this scenario proves.>

## Preconditions

- <required condition>

## Entry / Trigger

<Exact verified starting point or trigger.>

## Known-Good Path

```text
<step/phase>
   ↓
<step/phase>
   ↓
<verification>
```

## Observable Checkpoints

| Phase | Action | Expected observable result |
|---|---|---|
| <phase> | <action> | <result> |

## Expected Result

- <explicit pass condition>

## Evidence

Collect only what is useful on failure or block:

- <status/log/UI evidence>

## Fallback

1. <verified fallback path>

If no fallback has been verified, say so explicitly.

## Stop Condition

Stop retrying or investigating when:

- <condition>

Then record Verdict / Reason and continue independent scenarios where possible.

## Dependencies

- Depends on: <environment/service/state/previous scenario>
- May block: <dependent scenarios, if any>

## Cleanup / Recovery

After PASS / FAIL / BLOCKED, restore or preserve the environment so that:

- <recovery action or verified safe end state>

If no cleanup is required, say so explicitly.

## Independent Follow-ups

- <tests that remain executable if this scenario fails or blocks>

## Notes

<Only durable notes needed to execute or interpret this playbook.>

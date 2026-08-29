# <Scenario Name>

- Status: DRAFT | VERIFIED | STALE
- Scope: <product/version/environment>
- Last verified: <YYYY-MM-DD or unknown>

## Goal

<What this scenario proves.>

## Prerequisites

- <required condition>

## Entry

<Exact verified starting point.>

## Flow

```text
<step/phase>
   ↓
<step/phase>
   ↓
<verification>
```

## Expected Observations

| Phase | Action | Expected observable result |
|---|---|---|
| <phase> | <action> | <result> |

## Pass Criteria

- <explicit pass condition>

## Failure Evidence

Collect only what is useful:

- <status/log/UI evidence>

## Fallback

1. <verified fallback path>

If no fallback has been verified, say so explicitly.

## Stop Condition

Stop retrying when:

- <condition>

Then classify the result and continue independent scenarios where possible.

## Independent Follow-ups

- <tests that remain executable if this scenario fails or blocks>

## Notes

<Only durable notes needed to execute or interpret this playbook.>

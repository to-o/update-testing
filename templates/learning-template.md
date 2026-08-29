# Learning Entry Template

Use this structure when adding an entry to `docs/testing/LEARNINGS.md`.

```markdown
## YYYY-MM-DD — <short title>

- Status: OBSERVED | REPRODUCED | VERIFYING | PROMOTED | REJECTED
- Scenario: <scenario/playbook>
- Observation: <what was actually observed>
- Evidence: <logs, screenshot, command output, issue or reference>
- Reproduced: YES | NO | PARTIAL
- Confidence: LOW | MEDIUM | HIGH
- Suspected explanation: <optional hypothesis; never present as fact>
- Next verification: <what should be checked next time>
- Proposed destination: <overview / playbook / troubleshooting / knowledge>
```

Fact maturity:

```text
UNKNOWN → OBSERVED → REPRODUCED → VERIFIED → CANONICAL
```

Promotion rule:

- `OBSERVED` / `REPRODUCED` remain in `LEARNINGS.md` while verification continues.
- Only `VERIFIED` knowledge should be promoted into canonical testing docs.
- verified product/test mental model → `overview/`
- verified repeatable testing procedure → `playbooks/`
- verified symptom diagnosis/fallback → `troubleshooting/`
- verified cross-scenario stable fact → `knowledge/`

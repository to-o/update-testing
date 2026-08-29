# Learning Entry Template

Use this structure when adding an entry to `docs/testing/LEARNINGS.md`.

```markdown
## YYYY-MM-DD — <short title>

- Status: CANDIDATE | VERIFYING | PROMOTED | REJECTED
- Scenario: <scenario/playbook>
- Observation: <what was actually observed>
- Evidence: <logs, screenshot, command output, issue or reference>
- Reproduced: YES | NO | PARTIAL
- Confidence: LOW | MEDIUM | HIGH
- Suspected explanation: <optional hypothesis; never present as fact>
- Next verification: <what should be checked next time>
- Proposed destination: <overview / playbook / troubleshooting / knowledge>
```

Promotion rule:

- repeated stable product model → `overview/`
- repeatable testing procedure → `playbooks/`
- repeatable symptom diagnosis/fallback → `troubleshooting/`
- cross-scenario stable fact → `knowledge/`

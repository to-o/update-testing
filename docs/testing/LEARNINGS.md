# Testing Learnings

本文件是**新发现的暂存区**，不是正式知识库。

用于保存已经观察到、可能可以复现，但尚未达到正式知识标准的测试发现。

## 事实成熟度

本仓库统一使用：

```text
UNKNOWN
   ↓
OBSERVED
   ↓
REPRODUCED
   ↓
VERIFIED
   ↓
CANONICAL
```

其中：

- `OBSERVED`：单次测试中观察到；
- `REPRODUCED`：已经能够重复出现，但适用边界或稳定性仍需要确认；
- `VERIFIED`：已有充分证据支持，可作为稳定测试事实；
- `CANONICAL`：已进入正式测试文档。

`OBSERVED` 和 `REPRODUCED` 默认仍保留在本文件中。

只有达到 `VERIFIED`，才应晋升到 `overview/`、`playbooks/`、`troubleshooting/` 或 `knowledge/`。

## 规则

- 第一次观察到、未来测试可能有价值的新行为：记录为 `OBSERVED`。
- 已经可以重复出现但仍需确认边界：记录为 `REPRODUCED`，继续保留在本文件。
- 已有充分证据、适用条件清楚：标记为 `VERIFIED` 并晋升到正式文档。
- 已被证伪：标记 `REJECTED`，整理时可以删除。
- 已晋升：标记 `PROMOTED` 并链接到正式文档，整理时可以删除。
- 不记录完整聊天流水账。
- 不把猜测、未经验证的根因或一次性偶发现象写成正式事实。

## Entry Template

```markdown
## YYYY-MM-DD — <short title>

- Status: OBSERVED | REPRODUCED | VERIFYING | PROMOTED | REJECTED
- Scenario: <scenario/playbook>
- Observation: <what was observed>
- Evidence: <logs, screenshot, command output, issue or other reference>
- Reproduced: YES | NO | PARTIAL
- Confidence: LOW | MEDIUM | HIGH
- Suspected explanation: <optional; explicitly label as hypothesis>
- Next verification: <what should be checked next time>
- Proposed destination: <overview / playbook / troubleshooting / knowledge>
```

---

当前暂无已记录 learning。

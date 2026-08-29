# Troubleshooting

本目录按**测试人员看到的症状**组织，而不是优先按代码模块组织。

## 为什么按症状组织

测试开始时通常先知道“哪里不动了”，并不知道根因属于 UI、服务、网络、包管理还是其他组件。

因此 Troubleshooting 的入口应该从**可观察症状**开始，再通过证据逐步缩小范围。

## Troubleshooting 文档应该回答

1. 这个症状如何确认？
2. 先收集哪些最小证据？
3. 哪些检查成本最低、价值最高？
4. 什么情况下允许一次有意义的重试？
5. 有什么已经验证的 fallback？
6. 什么时候应该停止继续排查？
7. 当前场景的 Verdict 是什么？
8. 如果是 `FAIL` 或 `BLOCKED`，Reason 是什么？
9. 当前问题出现后，还有哪些独立测试可以继续？

## Verdict 与 Reason

测试结论只使用：

```text
PASS
FAIL
BLOCKED
SKIPPED
```

失败或阻塞原因单独记录：

```text
PRODUCT
ENVIRONMENT
AUTOMATION
DEPENDENCY
UNKNOWN
```

例如：

```text
Verdict: FAIL
Reason: PRODUCT
```

不要再使用 `PRODUCT_FAIL`、`ENVIRONMENT_FAIL` 等混合状态。

## Anti-Stuck

Troubleshooting 的目标不是要求 AI 一定解决问题，而是尽快得到一个有证据的结论，并决定是否还能继续其他测试。

```text
症状
 ↓
最小证据
 ↓
确认 observable state
 ↓
低成本验证
 ↓
有新信息时一次有意义的重试
 ↓
已验证 fallback
 ↓
仍失败 → Verdict / Reason → 继续独立场景
```

必须遵守：

- 重复相同操作本身不算调查；
- 无新信息时不要机械重试；
- 不把 Troubleshooting 写成无限递归排查树；
- 默认不把测试调查演变成源码修复。

新增文档从 `templates/troubleshooting-template.md` 复制。

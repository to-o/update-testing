# Test Playbooks

Playbook 保存**已经验证过、可以重复执行**的更新测试流程。

## 使用规则

- 已有 Playbook 时优先执行，不要从零探索。
- Playbook 与当前产品不一致时，先记录差异，再局部探索。
- 一次偶然成功的路径不要立即固化；应有足够证据证明它可重复并明确适用条件。
- Playbook 只保留执行所需内容，不写成长篇设计说明或测试流水账。
- 测试结束后应尽可能恢复到后续场景可继续执行的状态。

## 标准结构

每个成熟 Playbook 至少包含：

1. **Goal** — 测什么。
2. **Preconditions** — 从什么有效状态开始。
3. **Entry / Trigger** — 如何启动。
4. **Known-good path** — 已验证的关键步骤/阶段。
5. **Observable checkpoints** — 每个关键阶段应该看到什么。
6. **Expected result** — 怎样才算通过。
7. **Evidence** — 失败时收集什么最小有效证据。
8. **Fallback** — 哪些替代验证路径已经被确认有效。
9. **Stop condition** — 什么时候不再重试或继续调查。
10. **Dependencies** — 当前场景依赖什么、会阻塞什么。
11. **Cleanup / Recovery** — 测试完成或失败后如何恢复到可继续测试的状态。
12. **Independent follow-ups** — 当前场景失败或阻塞后还有什么能继续测试。
13. **Last verified** — 最近验证时间 / 版本范围。

对于更新类测试，以下三项是必备内容：

- `Preconditions`
- `Observable checkpoints`
- `Cleanup / Recovery`

## 推荐逐步形成的 Playbook

具体 Playbook 不由本文件定义为固定测试范围，应随着真实测试逐步增加。

当前可以从最常使用、最稳定、最能减少重复探索的更新平台和更新客户端流程开始沉淀；后续发现新的直接相关链路时再新增对应 Playbook。

新增 Playbook 时从 `templates/playbook-template.md` 复制。

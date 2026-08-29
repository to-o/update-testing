# Test Playbooks

Playbook 保存**已经验证过、可以重复执行**的更新测试流程。

## 使用规则

- 已有 Playbook 时优先执行，不要从零探索。
- Playbook 与当前产品不一致时，先记录差异，再局部探索。
- 一次偶然成功的路径不要立即固化；应有足够证据证明它可重复。
- Playbook 只保留执行所需内容，不写成长篇设计说明或测试流水账。

## 标准结构

每个 Playbook 至少包含：

1. **Goal** — 测什么。
2. **Prerequisites** — 什么必须已经满足。
3. **Entry** — 从哪里开始。
4. **Flow** — 已验证的关键步骤/阶段。
5. **Expected observations** — 每阶段应该看到什么。
6. **Pass criteria** — 怎样才算通过。
7. **Failure evidence** — 失败时收什么证据。
8. **Fallback** — 允许换什么路径验证。
9. **Stop condition** — 什么时候不再重试。
10. **Independent follow-ups** — 当前场景失败后还有什么能继续测试。
11. **Last verified** — 最近验证时间/版本范围。

## 推荐逐步形成的核心 Playbook

随着真实测试逐步补充：

- 检查更新；
- 更新下载；
- 正常升级全流程；
- 离线更新/升级（如果产品支持）；
- 重启与升级后验证；
- 回退与回退后验证；
- 下载/安装中断恢复；
- 更新客户端 UI 关键路径；
- 更新平台关键操作路径。

新增 Playbook 时从 `templates/playbook-template.md` 复制。

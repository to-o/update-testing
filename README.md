# update-testing

面向更新平台与更新客户端的 AI 辅助测试知识库。

本仓库的目标不是保存聊天记录，而是把测试过程中验证过的知识沉淀为可复用、可检索、可跨会话接手的测试资产，使新的 AI 会话或测试人员不需要反复从零探索更新流程。

## 快速开始

AI 或测试人员进入仓库后按以下顺序开始：

1. 阅读 [`AGENTS.md`](./AGENTS.md) 获取测试执行规则。
2. 阅读 [`docs/testing/README.md`](./docs/testing/README.md) 获取测试知识地图。
3. 根据当前任务只加载相关的 overview / playbook / troubleshooting 文档。
4. 执行测试并记录 PASS / FAIL / BLOCKED / SKIPPED。
5. 将尚未充分验证的新发现写入 [`docs/testing/LEARNINGS.md`](./docs/testing/LEARNINGS.md)。
6. 将重复验证后的稳定知识晋升到正式文档。

## 核心原则

- `AGENTS.md` 管 AI **怎么工作**，不承载不断增长的产品知识。
- `docs/testing/README.md` 管 **从哪里开始**。
- `overview/` 管 **需要理解什么**。
- `playbooks/` 管 **怎么测试**。
- `troubleshooting/` 管 **卡住怎么办**。
- `knowledge/` 管 **稳定事实与环境知识**。
- `LEARNINGS.md` 管 **尚待验证的新发现**。
- 一个失败步骤不得无限阻塞整个测试任务；能继续的独立场景应继续执行。

## 目录

```text
.
├── AGENTS.md
├── README.md
├── docs/
│   └── testing/
│       ├── README.md
│       ├── LEARNINGS.md
│       ├── TEST-MATRIX.md
│       ├── overview/
│       ├── playbooks/
│       ├── troubleshooting/
│       └── knowledge/
└── templates/
```

当前仓库会随着真实测试逐步补全产品模型和测试路径，避免在尚未验证前把猜测固化为正式知识。

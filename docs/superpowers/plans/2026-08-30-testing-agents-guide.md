# 更新测试 AGENTS.md 重构 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 将根级 `AGENTS.md` 重构为面向“更新平台 + 更新客户端”的长期稳定测试 Agent 操作规约，同时保持具体测试知识在 `docs/testing/` 中渐进增长。

**Architecture:** 根级 `AGENTS.md` 只定义跨场景稳定规则：角色与边界、工作模式、新会话启动、测试执行、Anti-Stuck、探索、证据、事实成熟度、知识沉淀与完成条件。具体功能、组件、命令、路径、故障和测试步骤继续由 `docs/testing/` 承载，不在根级规则中穷举。

**Tech Stack:** Markdown、GitHub repository documentation

**Spec:** `docs/superpowers/specs/2026-08-30-testing-agents-guide-design.md`

## Global Constraints

- 测试方向固定为：更新平台、更新客户端，以及为了验证其行为而直接相关的更新链路。
- `AGENTS.md` 不穷举所有功能、测试 Case、组件、接口、路径、服务名或故障模式。
- 当前已知测试范围不得被表达为允许测试范围的上限。
- 已知且验证过的流程优先于重新探索。
- 未验证事实不得直接进入正式知识。
- 单个失败步骤不得无限阻塞整个测试任务。
- 测试结论统一为 `PASS` / `FAIL` / `BLOCKED` / `SKIPPED`，失败原因单独记录。
- 文档面向没有当前聊天历史的新测试人员或新 Agent。

---

## 文件结构

本次实施只需要修改一个长期规则文件，并对现有入口文档做只读一致性检查：

- Modify: `AGENTS.md` — 根级测试 Agent 操作规约。
- Read/Verify: `README.md` — 仓库定位和文档职责是否与新规则一致。
- Read/Verify: `docs/testing/README.md` — 新会话导航、知识分层是否与新规则一致。
- Read/Verify: `docs/testing/LEARNINGS.md` — Learning 暂存职责是否与事实成熟度模型一致。
- Read/Verify: `docs/testing/playbooks/README.md` — Playbook 契约是否与根规则冲突。
- Read/Verify: `docs/testing/troubleshooting/README.md` — Anti-Stuck / symptom-based troubleshooting 是否冲突。

除非一致性检查发现明确冲突，否则不修改上述验证文件，避免无关文档 churn。

---

### Task 1: 重写根级 AGENTS.md

**Files:**
- Modify: `AGENTS.md`
- Reference: `docs/superpowers/specs/2026-08-30-testing-agents-guide-design.md`

**Interfaces:**
- Consumes: `docs/testing/README.md` 作为测试知识导航入口。
- Consumes: `docs/testing/LEARNINGS.md` 作为未验证知识暂存区。
- Consumes: `docs/testing/playbooks/`、`troubleshooting/`、`knowledge/`、`overview/` 作为长期测试资产。
- Produces: 所有新会话统一遵守的根级 Agent 工作协议。

- [ ] **Step 1: 保存当前 AGENTS.md 作为重构基线**

读取当前 `AGENTS.md`，确认需要保留的成熟规则至少包括：新会话渐进读取、已知路径优先、Anti-Stuck、默认测试人员角色、证据要求、知识沉淀和会话交接。

验证标准：新版本不能丢掉这些能力，只能重新组织并减少错误限制。

- [ ] **Step 2: 将章节收敛为 9 个长期稳定主章节**

使用以下固定结构完整替换当前正文：

```text
1. 仓库目的与 Agent 角色
2. 测试方向与边界
3. 工作模式
4. 新会话启动协议
5. 测试执行与 Anti-Stuck
6. 探索与真实行为原则
7. 结果、证据与事实成熟度
8. 测试知识沉淀与 Playbook 契约
9. 测试任务完成条件
```

不得保留旧版“主要测试范围包括：检查更新、下载、安装、重启、回退……”这类功能枚举作为边界定义。

- [ ] **Step 3: 写入稳定的测试方向定义**

`测试方向与边界` 必须明确表达：

```text
本仓库专注于更新平台、更新客户端，以及为了验证其行为而必须理解或操作的直接相关更新链路。

具体组件、功能、状态、接口、依赖和测试场景不由 AGENTS.md 预先穷举；它们通过真实测试逐步发现并沉淀到 docs/testing/。

当前已知范围不是允许范围的上限。
```

同时明确：不主动扩展为与系统更新无关的通用 OS、硬件或其他产品测试。

- [ ] **Step 4: 写入四种工作模式**

必须定义并区分：

```text
DISCOVER     — 未知对象/入口/状态/交互路径的最小必要探索
UNDERSTAND   — 将已观察事实整理成测试心智模型
TEST         — 按已知流程或 Playbook 执行并给出判定
INVESTIGATE  — 对失败做有限调查、取证、分类、fallback 和退出
```

明确：已有可靠 Playbook 时默认直接 `TEST`，不要重新进入 `DISCOVER`。

- [ ] **Step 5: 写入新会话 Bootstrap**

必须包含：

```text
AGENTS.md
   ↓
docs/testing/README.md
   ↓
明确当前任务
   ↓
只加载相关 overview / playbook
   ↓
已有 Playbook？
   ├─ Yes → TEST
   └─ No  → DISCOVER / UNDERSTAND
```

并明确禁止默认扫描整个仓库或读取全部测试文档。

- [ ] **Step 6: 写入统一测试执行与 Anti-Stuck 协议**

测试执行：

```text
PRECHECK → EXECUTE → OBSERVE → VERIFY → RECORD → NEXT
```

Anti-Stuck：

```text
无进展
  ↓
确认 observable state
  ↓
收最小证据
  ↓
是否有新信息支持再次尝试？
  ├─ Yes → 有理由地重试一次
  └─ No  → 不重复
  ↓
查 troubleshooting
  ↓
尝试一个合理 fallback
  ↓
FAIL / BLOCKED
  ↓
继续独立场景
```

必须包含硬规则：

```text
重复相同操作本身不算调查。
```

以及：默认同一动作最多一次有理由的重试，Playbook 明确规定除外。

- [ ] **Step 7: 分离 Verdict 和 Reason**

Verdict 只允许：

```text
PASS
FAIL
BLOCKED
SKIPPED
```

失败/阻塞原因单独使用：

```text
PRODUCT
ENVIRONMENT
AUTOMATION
DEPENDENCY
UNKNOWN
```

示例必须使用：

```text
Verdict: FAIL
Reason: PRODUCT
```

不得再把 `PRODUCT_FAIL` / `ENVIRONMENT_FAIL` 与 Verdict 混成同一层级状态。

- [ ] **Step 8: 写入真实行为、探索和 UI 原则**

事实优先级至少包含：真实可重复行为/直接证据 > 当前有效接口/测试 > 正式文档 > 稳定知识 > Learning > 会话推测。

UI / 交互探索顺序固定为：

```text
已知稳定路径
  ↓
语义查找 / 稳定 selector
  ↓
局部 snapshot / 局部结构
  ↓
定向探索
  ↓
全量探索
```

全量探索只能作为最后手段；稳定探索结果必须沉淀到相关 Playbook。

- [ ] **Step 9: 写入事实成熟度模型**

必须使用：

```text
UNKNOWN → OBSERVED → REPRODUCED → VERIFIED → CANONICAL
```

并规定：

```text
OBSERVED / REPRODUCED → docs/testing/LEARNINGS.md
VERIFIED → overview / playbooks / troubleshooting / knowledge
```

禁止把猜测、单次偶发现象、未经验证根因直接写成 canonical fact。

- [ ] **Step 10: 写入 Playbook 契约**

成熟 Playbook 至少回答：

```text
Goal
Preconditions
Entry / Trigger
Known-good path
Observable checkpoints
Expected result
Evidence
Fallback
Stop condition
Dependencies
Cleanup / Recovery
```

对更新类测试，必须明确强调 `Preconditions`、`Observable checkpoints`、`Cleanup / Recovery` 为必备项。

- [ ] **Step 11: 写入测试任务完成条件**

任务完成至少能回答：

```text
测了什么？
哪些 PASS / FAIL / BLOCKED / SKIPPED？
关键证据是什么？
产生了什么新知识？
哪些 Learning / Playbook / Troubleshooting 需要更新？
下一会话从哪里继续？
```

收尾模型：

```text
TEST → RESULT → EVIDENCE → KNOWLEDGE → HANDOFF
```

- [ ] **Step 12: 人工语义自检 AGENTS.md**

逐条确认：

```text
[ ] 没有把当前已知功能清单写成固定测试上限
[ ] 测试方向仍明确限定为更新平台/更新客户端及直接链路
[ ] DISCOVER 与 TEST 的切换条件清楚
[ ] Anti-Stuck 有明确退出条件
[ ] Verdict 与 Reason 分层
[ ] Learning 与 canonical knowledge 分层
[ ] 新会话不要求全仓库扫描
[ ] 不要求 Agent 默认进入源码修复
[ ] 不包含未验证产品命令/路径/服务名/UI 文案
```

- [ ] **Step 13: Commit**

```bash
git add AGENTS.md
git commit -m "docs: refine update testing agent guide"
```

---

### Task 2: 校验文档职责与引用一致性

**Files:**
- Verify: `README.md`
- Verify: `docs/testing/README.md`
- Verify: `docs/testing/LEARNINGS.md`
- Verify: `docs/testing/playbooks/README.md`
- Verify: `docs/testing/troubleshooting/README.md`
- Verify: `docs/testing/knowledge/README.md`
- Modify only if conflict exists: any file above

**Interfaces:**
- Consumes: Task 1 重构后的根 `AGENTS.md`。
- Produces: 根规则与测试知识库之间无职责冲突、无死链的文档体系。

- [ ] **Step 1: 检查 README 的职责分层**

必须仍与以下模型一致：

```text
AGENTS.md              → AI 怎么工作
docs/testing/README.md → 从哪里开始
overview/               → 测试心智模型
playbooks/              → 怎么测试
troubleshooting/        → 卡住怎么办
knowledge/              → 稳定事实
LEARNINGS.md            → 尚待验证发现
```

如果一致，不修改 `README.md`。

- [ ] **Step 2: 检查 docs/testing/README.md 的 Bootstrap**

确认它仍支持“按需加载而非读取整个文档树”，且没有与新 `AGENTS.md` 相反的启动顺序。

如果一致，不修改。

- [ ] **Step 3: 检查 Learning 晋升语义**

确认 `LEARNINGS.md` 没有允许单次观察直接成为正式知识；如已有规则与：

```text
OBSERVED / REPRODUCED → LEARNINGS
VERIFIED → canonical docs
```

一致，则不修改。

- [ ] **Step 4: 检查 Playbook 契约**

确认 `docs/testing/playbooks/README.md` 至少不与以下字段冲突：

```text
Preconditions
Observable checkpoints
Fallback
Stop condition
Cleanup / Recovery
```

缺失字段只有在会导致未来 Playbook 与根规则明显不一致时才补充，避免为了格式完全一致而无意义改文档。

- [ ] **Step 5: 检查 Troubleshooting 与 Anti-Stuck**

确认 troubleshooting 是症状导向，且不会鼓励无限重试或无限源码排查。

- [ ] **Step 6: 检查 Markdown 引用路径**

验证根 `AGENTS.md` 中引用的以下路径均存在：

```text
docs/testing/README.md
docs/testing/LEARNINGS.md
docs/testing/overview/
docs/testing/playbooks/
docs/testing/troubleshooting/
docs/testing/knowledge/
docs/testing/TEST-MATRIX.md
```

- [ ] **Step 7: 做最终文档 diff 检查**

本次预期变更应以 `AGENTS.md` 为主；若 Task 2 没发现真实冲突，不应额外修改测试知识文档。

本地执行时：

```bash
git diff --check
git diff -- AGENTS.md README.md docs/testing/
```

预期：无 whitespace error；没有与本设计无关的内容变化。

- [ ] **Step 8: 如 Task 2 有必要修改则单独 Commit**

仅在确有一致性问题并实际修改了文件时执行：

```bash
git add README.md docs/testing/
git commit -m "docs: align testing knowledge guidance"
```

若无任何修改，则跳过本步骤，不创建空提交。

---

## 最终验收

实施完成后必须满足：

```text
新会话只需读取 AGENTS.md + docs/testing/README.md + 当前任务相关文档即可开始工作。

AGENTS.md 固定“更新平台 + 更新客户端”的测试方向，但不预先锁死所有具体测试范围。

未知领域允许有限 DISCOVER；已知流程优先 TEST。

单个失败步骤有明确退出机制，不会无限重试。

测试结论、失败原因、证据和事实成熟度相互独立且定义清晰。

真实测试产生的知识能够从 Learning 逐步晋升为长期测试资产。
```

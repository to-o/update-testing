# 更新测试 AGENTS.md 重构设计

## 1. 背景

`update-testing` 用于更新平台与更新客户端的 AI 辅助测试和知识沉淀。

当前 `AGENTS.md` 已具备会话启动、测试执行、Anti-Stuck、证据和知识沉淀等基础规则，但仍存在两个问题：

1. 把部分当前已知测试项写成了长期固定范围，容易让后续 Agent 把“当前已知范围”误解为“允许测试的全部范围”。
2. 测试规则、产品知识和具体测试资产之间的职责还可以进一步分离，使根级 `AGENTS.md` 更稳定、更接近成熟开源项目的写法。

本设计不改变仓库的测试方向：仍然固定为 **更新平台、更新客户端，以及为了验证它们的行为而直接相关的更新链路**。

具体组件、场景、状态、接口、故障模式和测试用例通过真实测试逐步发现，并沉淀到 `docs/testing/`，不在根级 `AGENTS.md` 中预先穷举。

---

## 2. 社区参考与提炼

### 2.1 AGENTS.md 官方模式

社区通用 `AGENTS.md` 更接近“给 Agent 的 README”：

- 放仓库级工作规则；
- 放测试/验证方式；
- 放明确的行为边界；
- 不承担不断增长的业务知识库职责。

### 2.2 OpenAI / Prowler 的分层做法

成熟项目通常把根级 Agent 指令作为长期稳定规则，再把模块、测试类型和具体执行方法下沉到局部文档或 Skill。

对本仓库的启发：

- 根 `AGENTS.md` 只管 Agent **如何工作**；
- `docs/testing/README.md` 管测试知识导航；
- `overview/` 管产品测试心智模型；
- `playbooks/` 管已验证测试流程；
- `troubleshooting/` 管失败症状与处置；
- `knowledge/` 管稳定事实；
- `LEARNINGS.md` 管尚未晋升的新发现。

### 2.3 Quay / Prowler 测试规则的共同点

测试类 Agent 指令重点是：

- 优先真实系统行为，而不是猜测；
- 先观察、交互、确认，再固化测试；
- 明确前置条件、可观察状态、通过标准和清理/恢复；
- 避免脆弱、重复、无限重试的测试路径；
- 测试和测试文档保持同步。

这些原则应成为本仓库根 `AGENTS.md` 的核心，而不是固定功能清单。

---

## 3. 目标

重构后的根级 `AGENTS.md` 应满足：

1. 新 AI 会话在最少上下文下快速进入测试状态；
2. 固定测试方向，但不提前锁死具体测试范围；
3. 明确区分“探索未知”和“执行已知 Playbook”；
4. 避免 Agent 卡在单个步骤或反复执行相同动作；
5. 以真实行为和证据为测试事实来源；
6. 把一次性观察与稳定知识区分开；
7. 让测试过程中发现的新组件、新流程和新依赖可以自然进入知识库；
8. 每次有效测试都提高后续会话的测试效率。

---

## 4. 非目标

根 `AGENTS.md` 不负责：

- 穷举所有更新功能；
- 穷举所有测试 Case；
- 保存产品架构设计；
- 保存完整故障库；
- 保存每次测试执行日志；
- 固定当前尚未验证的命令、路径、服务名、UI 名称或接口。

这些内容按职责进入 `docs/testing/`。

---

## 5. 测试方向与边界

长期固定边界定义为：

> 本仓库专注于更新平台、更新客户端，以及为了验证其更新行为而必须理解或操作的直接相关链路。

具体测试范围不是在 `AGENTS.md` 中预先完整定义。

当真实测试发现新的服务、组件、接口、状态、流程或依赖，只要它直接参与或影响更新平台/更新客户端的行为，就允许纳入理解和测试范围。

不主动扩展为与系统更新无关的通用操作系统测试、硬件测试或其他产品测试。

关键原则：

> **当前已知范围不是允许范围的上限。**

---

## 6. Agent 工作模式

定义四种工作模式，并要求 Agent 根据当前信息选择最小必要模式。

### 6.1 DISCOVER — 探索

用于当前测试对象、入口、状态或交互路径未知时。

目标：获得足以继续测试的真实信息，而不是无限探索。

输出应尽可能转化为可复用知识。

### 6.2 UNDERSTAND — 理解

用于把已经观察到的事实整理成测试心智模型，例如：

- 哪些对象互相关联；
- 某个流程处于什么阶段；
- 哪些状态可用于判断进度；
- 哪些依赖影响测试结果。

### 6.3 TEST — 测试

当已有足够信息或存在已验证 Playbook 时，直接执行测试并判断结果。

已知流程优先于重新探索。

### 6.4 INVESTIGATE — 有限调查

测试失败或无法推进时进入。

目标是：

- 收集最小充分证据；
- 判断失败类型；
- 找到一个合理 fallback；
- 决定 FAIL / BLOCKED / SKIPPED / 重试一次；
- 尽快返回剩余测试覆盖。

默认不演变成源码修复或无限根因分析。

---

## 7. 新会话启动协议

新会话默认执行：

```text
AGENTS.md
   ↓
docs/testing/README.md
   ↓
明确当前测试目标
   ↓
只加载相关 overview / playbook
   ↓
已有 Playbook？
   ├─ Yes → TEST
   └─ No  → DISCOVER / UNDERSTAND
```

规则：

- 不默认扫描整个仓库；
- 不默认读取全部测试文档；
- 不重新探索已有稳定路径；
- troubleshooting / knowledge 仅在需要时加载。

---

## 8. 测试执行协议

每个测试场景遵循：

```text
PRECHECK
   ↓
EXECUTE
   ↓
OBSERVE
   ↓
VERIFY
   ↓
RECORD
   ↓
NEXT
```

测试结论统一为：

- `PASS`
- `FAIL`
- `BLOCKED`
- `SKIPPED`

失败原因与测试结论分离：

```text
Verdict: FAIL
Reason: PRODUCT
```

或：

```text
Verdict: BLOCKED
Reason: ENVIRONMENT
```

建议 Reason 类型：

- `PRODUCT`
- `ENVIRONMENT`
- `AUTOMATION`
- `DEPENDENCY`
- `UNKNOWN`

这样避免把 `PRODUCT_FAIL`、`ENVIRONMENT_FAIL` 与 PASS/FAIL 放在同一层级。

---

## 9. 真实行为与证据优先

测试事实来源优先级：

1. 可重复观察到的真实产品行为和直接证据；
2. 当前有效的可执行测试、脚本、接口；
3. 已验证的正式测试文档；
4. 稳定知识库；
5. 暂存 Learning；
6. 当前会话中的推测。

禁止因为“通常应该如此”而直接形成测试结论或正式文档。

未知信息允许探索；探索后应尽量沉淀。

---

## 10. Anti-Stuck 协议

Agent 不得把测试任务剩余时间全部消耗在同一个失败步骤。

```text
步骤无进展
   ↓
确认当前 observable state
   ↓
收集最小证据
   ↓
下一次尝试是否有新信息依据？
   ├─ Yes → 有理由地重试一次
   └─ No  → 不重复
   ↓
查询已有 troubleshooting
   ↓
尝试一个合理 fallback
   ↓
仍无法继续
   ↓
FAIL / BLOCKED
   ↓
继续独立测试
```

硬规则：

- 重复相同操作本身不算调查；
- 无新信息时不允许机械重复；
- 同一操作默认最多一次有理由的重试，Playbook 另有规定除外；
- 单个失败场景不自动等于全局阻塞；
- 只有阻止所有相关剩余测试的条件才算全局 blocker。

---

## 11. UI / 交互探索原则

优先级：

```text
已知稳定操作路径
   ↓
语义查找 / 稳定 selector
   ↓
局部 snapshot / 局部结构
   ↓
定向探索
   ↓
全量 UI 探索
```

全量探索是最后手段。

探索得到稳定路径后，应更新对应 Playbook，避免后续会话重复发现。

---

## 12. 事实成熟度模型

新增事实等级，避免一次观察被直接写成平台事实：

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

定义：

- `UNKNOWN`：尚不知道或没有可靠信息；
- `OBSERVED`：单次测试中观察到；
- `REPRODUCED`：可以重复出现；
- `VERIFIED`：已有充分证据支持，可作为稳定测试事实；
- `CANONICAL`：已进入正式测试文档。

默认晋升规则：

```text
OBSERVED / REPRODUCED
  → LEARNINGS.md

VERIFIED
  → overview / playbooks / troubleshooting / knowledge
```

不得把猜测、一次性偶发现象、未经验证根因直接晋升为正式知识。

---

## 13. Playbook 契约

每个成熟 Playbook 至少回答：

1. Goal — 测什么；
2. Preconditions — 从什么状态开始；
3. Entry / Trigger — 怎么启动；
4. Known-good path — 已验证执行路径；
5. Observable checkpoints — 每阶段看什么；
6. Expected result — 如何判 PASS；
7. Evidence — 失败收什么；
8. Fallback — 合理替代路径；
9. Stop condition — 什么时候停止重试；
10. Dependencies — 被哪些条件依赖；
11. Cleanup / Recovery — 测完如何恢复可继续测试状态。

对更新类测试，`Preconditions`、`Observable checkpoints`、`Cleanup / Recovery` 是必备项。

---

## 14. 测试知识生命周期

```text
真实测试
   ↓
新发现
   ↓
LEARNINGS.md
   ↓
重复验证 / 证据确认
   ↓
正式知识
   ├─ overview/
   ├─ playbooks/
   ├─ troubleshooting/
   └─ knowledge/
```

规则：

- 优先更新已有正式文档，而不是重复创建；
- 新知识应减少未来探索成本；
- 文档写给没有当前聊天历史的下一位测试人员或 Agent；
- 产品行为变化时，测试资产应同步更新。

---

## 15. 测试任务完成条件

一次有意义的测试任务结束时，至少应能回答：

- 测了什么；
- 哪些 PASS；
- 哪些 FAIL；
- 哪些 BLOCKED；
- 哪些 SKIPPED；
- 关键失败证据在哪里；
- 是否发现了新的稳定知识；
- 是否需要新增或更新 Learning / Playbook / Troubleshooting；
- 下一会话从哪里继续。

推荐收尾模型：

```text
TEST
  ↓
RESULT
  ↓
EVIDENCE
  ↓
KNOWLEDGE
  ↓
HANDOFF
```

---

## 16. AGENTS.md 目标结构

重构后的根 `AGENTS.md` 建议保持约 9 个主章节：

1. 仓库目的与角色
2. 测试方向与边界
3. 工作模式
4. 新会话启动协议
5. 测试执行与 Anti-Stuck
6. 探索与真实行为原则
7. 结果、证据与事实成熟度
8. 测试知识沉淀与 Playbook 契约
9. 测试任务完成条件

不再保留当前按功能项展开的“测试范围清单”。

---

## 17. 文件影响范围

本次实施阶段预计只修改：

- `AGENTS.md`

必要时同步小幅调整：

- `README.md`
- `docs/testing/README.md`

原则是不重构现有目录，不一次性新增大量空文档。

---

## 18. 验收标准

实施完成后应满足：

- 根 `AGENTS.md` 不穷举具体更新功能作为范围上限；
- 明确测试方向仍是更新平台 + 更新客户端；
- 新会话有清晰 bootstrap；
- 已知 Playbook 优先，未知才探索；
- 失败不会无限重试；
- PASS/FAIL 与失败原因分层；
- 明确事实成熟度和知识晋升规则；
- 明确 Playbook 的最小结构；
- 明确测试任务完成和跨会话 handoff 标准；
- 与现有 `docs/testing/` 分层职责不冲突。

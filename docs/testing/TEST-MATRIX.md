# Update Test Matrix

本文件是测试覆盖地图，不是详细执行日志。

状态使用：`NOT_STARTED` / `PASS` / `FAIL` / `BLOCKED` / `SKIPPED`。

> 初始化阶段只列出通用测试域。具体产品支持范围确认后再增删，不把未经确认的能力当成产品事实。

## 1. 更新平台

| 测试域 | 状态 | 对应 Playbook | 备注 |
|---|---|---|---|
| 平台基本访问与测试前置 | NOT_STARTED | - | 待确认实际入口 |
| 更新任务/策略相关核心路径 | NOT_STARTED | - | 待确认产品模型 |
| 平台状态与客户端状态一致性 | NOT_STARTED | - | 待确认可观察点 |
| 失败状态与证据可获得性 | NOT_STARTED | - | - |

## 2. 更新客户端

| 测试域 | 状态 | 对应 Playbook | 备注 |
|---|---|---|---|
| 客户端启动与基本可用性 | NOT_STARTED | - | 待确认入口 |
| 检查更新 | NOT_STARTED | - | - |
| 更新信息展示 | NOT_STARTED | - | - |
| 下载/获取更新内容 | NOT_STARTED | - | - |
| 安装/部署 | NOT_STARTED | - | - |
| 进度与状态展示 | NOT_STARTED | - | - |
| 失败提示与恢复能力 | NOT_STARTED | - | - |
| 重启相关流程 | NOT_STARTED | - | 如果产品需要 |
| 升级后验证 | NOT_STARTED | - | - |
| 更新历史 | NOT_STARTED | - | 如果产品支持 |

## 3. 端到端生命周期

| 场景 | 状态 | 对应 Playbook | 备注 |
|---|---|---|---|
| 正常更新全流程 | NOT_STARTED | - | - |
| 更新后版本/状态验证 | NOT_STARTED | - | - |
| 下载中断与恢复 | NOT_STARTED | - | 支持范围待确认 |
| 安装中断/失败恢复 | NOT_STARTED | - | 支持范围待确认 |
| 回退 | NOT_STARTED | - | 仅产品支持时启用 |
| 回退后验证 | NOT_STARTED | - | 仅产品支持时启用 |
| 离线更新 | NOT_STARTED | - | 仅产品支持时启用 |

## 4. 使用规则

- 具体测试步骤放 Playbook，不在这里复制。
- 单次详细执行结果不要堆积到矩阵中。
- 一个场景 BLOCKED 时，检查其他场景是否独立并继续。
- 产品明确不支持的能力改为 `SKIPPED` 并注明原因，而不是长期保持 NOT_STARTED。
- 新增高价值测试域时同步考虑是否需要新的 Playbook。

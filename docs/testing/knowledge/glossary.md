# Testing Glossary

只记录更新测试中反复使用、且容易产生歧义的术语。

| Term | Meaning in this repository | Notes / Scope |
|---|---|---|
| PASS | 场景达到明确通过条件 | - |
| FAIL | 产品行为明确不符合预期 | 与测试工具失败区分 |
| BLOCKED | 依赖条件导致无法得到有效产品结论 | 不等于产品 FAIL |
| SKIPPED | 明确不执行该场景 | 应记录原因 |
| PRODUCT_FAIL | 产品行为违反预期 | - |
| ENVIRONMENT_FAIL | 环境使测试无效或无法继续 | - |
| AUTOMATION_FAIL | 测试方法/工具失败，产品结果未知 | - |
| Playbook | 已验证、可重复执行的测试流程 | 不是测试流水账 |
| Learning | 尚未充分验证的新发现 | 暂存于 `LEARNINGS.md` |

产品特有术语只有在实际测试确认后再补充。

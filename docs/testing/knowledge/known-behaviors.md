# Known Behaviors

记录已经确认、跨测试场景有复用价值的产品行为。

## Entry Format

```markdown
## <behavior title>

- Applies to: <version/environment/scope>
- Behavior: <confirmed behavior>
- How verified: <evidence or reproducible procedure>
- Test impact: <how this changes execution or verdict>
- Last verified: YYYY-MM-DD
```

## Rules

- 不记录猜测根因。
- 一次偶发现象先进入 `../LEARNINGS.md`。
- 如果行为只属于一个具体测试流程，优先写进对应 Playbook。
- 行为失效后及时删除或标明版本范围，避免误导新会话。

当前暂无已确认行为。

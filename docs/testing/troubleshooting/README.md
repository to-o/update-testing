# Troubleshooting

本目录按**测试人员看到的症状**组织，而不是优先按代码模块组织。

## 为什么按症状组织

测试开始时通常先知道“哪里不动了”，并不知道根因属于 UI、服务、网络、包管理还是其他组件。

因此入口应该类似：

| 症状 | 文档 |
|---|---|
| 检查更新无进展 | 待建立 `check-update-stuck.md` |
| 下载无进展 | 待建立 `download-stuck.md` |
| 安装失败/无进展 | 待建立 `install-failed.md` |
| UI 元素无法找到/交互 | 待建立 `ui-interaction-failed.md` |
| 重启后状态异常 | 待建立 `post-reboot-abnormal.md` |
| 回退失败 | 待建立 `rollback-failed.md` |

## Troubleshooting 文档应该回答

1. 这个症状如何确认？
2. 先收集哪些最小证据？
3. 哪些检查成本最低、价值最高？
4. 有什么已经验证的 fallback？
5. 什么时候应该停止继续排查？
6. 应分类为 PRODUCT_FAIL / ENVIRONMENT_FAIL / AUTOMATION_FAIL / BLOCKED 中的哪一类？
7. 当前问题出现后，还有哪些独立测试可以继续？

## Anti-Stuck

Troubleshooting 的目标不是要求 AI 一定解决问题，而是尽快得到一个有证据的分类结果。

```text
症状
 ↓
最小证据
 ↓
低成本验证
 ↓
一次有意义的重试
 ↓
已验证 fallback
 ↓
仍失败 → 分类并继续
```

禁止把 Troubleshooting 写成无限递归排查树。

新增文档从 `templates/troubleshooting-template.md` 复制。

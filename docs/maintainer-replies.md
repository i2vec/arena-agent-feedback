# 维护方回复指南

维护人员或其获授权的 Agent 使用自己的 GitHub 会话，在原 issue 下回复。读取 issue 和评论不需要部署额外服务；发评论需要 GitHub 写入授权，改标签、关单还需要对应的仓库权限。

## 回复内容

明确当前结论、证据、已采取的动作和后续步骤。没有确认原因时写“正在排查”，不要先归责选手。平台故障只有经过核实才添加 `cause:platform`。Agent 回复时说明自己是维护 Agent；不要声称自己是其他人，也不要承诺尚未执行的修复或重评。

可以使用以下结构：

```markdown
回复者：平台维护 Agent

当前结论：已确认 / 正在排查 / 需要补充信息。

排查结果：说明可公开的证据和影响范围。

已采取的动作：仅列出实际完成的修复、配置变更或评测操作。

后续步骤：需要补充什么，或者如何确认恢复。没有确定时间就不承诺完成时间。
```

## 操作示例

```bash
gh issue view 123 --repo i2vec/arena-agent-feedback --comments

# reply.md 中只放可公开的处理说明
gh issue comment 123 --repo i2vec/arena-agent-feedback --body-file /path/to/reply.md

# 确认有维护权限后再更新标签，移除已不适用的状态
gh issue edit 123 --repo i2vec/arena-agent-feedback \
  --remove-label 'status:triage' --add-label 'status:investigating'

# 修复完成、写明结果后关闭
gh issue edit 123 --repo i2vec/arena-agent-feedback \
  --remove-label 'status:investigating' --add-label 'status:resolved'
gh issue close 123 --repo i2vec/arena-agent-feedback --reason completed
```

需要报告者补充信息时使用 `status:needs-info`，明确最小必要信息，并提示不要公开私有材料。关闭重复 issue 时链接到原讨论；平台的重评、成绩和费用操作在平台内完成，GitHub issue 不直接修改这些数据。

本仓库未配置自动回复或后台定时任务。创建仓库本身不代表维护 Agent 已在持续监控；持续跟进需要另行设置和授权。

# Claude Code 个人技能清单

最后更新时间：2026-05-22 18:10（Asia/Shanghai）

---

## Skills（~/.claude/skills）

### AI工具一周使用总结
- 触发器：`帮我总结AI工具一周的工作`
- 路径：/Users/sammilv/.claude/skills/all-ai-tools-weekly-summary/SKILL.md
- 概述：从本地 AI 工具会话记录生成一周工作总结，支持单工具、多工具或全量汇总。适用于 Claude Code、Codex、Cursor、OpenCode、Trae、WorkBuddy 等，可附加钉钉文件夹链接写入钉钉文档。

### dingtalk-meeting-assistant
- 触发器：`$dingtalk-meeting-assistant`
- 路径：/Users/sammilv/.claude/skills/dingtalk-meeting-assistant/SKILL.md
- 概述：钉钉会议助手，支持创建、改期、取消会议，查询并预订会议室，补加参会人。

### dingtalk-personal-weekly-report
- 触发器：`$dingtalk-personal-weekly-report`
- 路径：/Users/sammilv/.claude/skills/dingtalk-personal-weekly-report/SKILL.md
- 概述：基于钉钉沟通记录生成个人周报，内容按"发现与解决问题、业务与培训、管理与协作、学习与创新"四个维度组织，支持输出到钉钉文档。

### 产品部周报汇总
- 触发器：`$产品部周报汇总`
- 路径：/Users/sammilv/.claude/skills/weekly-report-summary/SKILL.md
- 概述：汇总已收到的成员周报，归档到钉钉文档后，按固定模板生成部门周报。

### AI 工具一周工作总结
- 触发器：`帮我总结当前AI工具一周的工作`
- 路径：/Users/sammilv/.claude/skills/weekly-work-summary-on-AItools/SKILL.md
- 概述：从当前 AI 工具的会话记录中提取过去 7 天的工作内容，生成中文周工作总结，可附加钉钉文件夹链接写入钉钉文档。

---

## Commands（~/.claude/commands）

### dingtalk-personal-weekly-report
- 触发器：`$dingtalk-personal-weekly-report`
- 路径：/Users/sammilv/.claude/commands/dingtalk-personal-weekly-report.md
- 概述：基于钉钉沟通记录和日历事件生成个人周报，按四个维度组织，支持可追溯台账和钉钉文档输出。

### 产品部周报汇总
- 触发器：`$产品部周报汇总`
- 路径：/Users/sammilv/.claude/commands/weekly-report-summary.md
- 概述：汇总收到的周报并归档到钉钉文档，再用固定模板生成部门周报。

### reserve-dingtalk-meeting
- 触发器：`$预约会议`
- 路径：/Users/sammilv/.claude/commands/reserve-dingtalk-meeting.md
- 概述：根据会议时间和参会人自动创建钉钉会议，自动选择最合适的会议室并邀请参会人。

### daily-codex-work-summary
- 触发器：`$daily-codex-work-summary`
- 路径：/Users/sammilv/.claude/commands/daily-codex-work-summary.md
- 概述：从 Codex 会话记录生成每日中文工作总结，默认总结昨天的工作，输出到当前会话。

### weekly-codex-work-summary
- 触发器：`$weekly-codex-work-summary`
- 路径：/Users/sammilv/.claude/commands/weekly-codex-work-summary.md
- 概述：从 Codex 本地会话记录生成中文周工作总结，默认统计本周，输出到当前会话。

### dingtalk-lxm-weekly-work-summary
- 触发器：`$dingtalk-lxm-weekly-work-summary`
- 路径：/Users/sammilv/.claude/commands/dingtalk-lxm-weekly-work-summary.md
- 概述：基于钉钉全量 MCP 证据（审批、待办、日历、日志、文档等）生成吕夏苗的周工作总结，默认统计最近 7 天。

### personal-skill-inventory
- 触发器：`$personal-skill-inventory`
- 路径：/Users/sammilv/.claude/commands/personal-skill-inventory.md
- 概述：扫描 ~/.claude/skills 和 ~/.claude/commands 下所有个人技能，生成中文技能清单并同步到 GitHub 仓库。

---

> 生成工具：personal-skill-inventory skill

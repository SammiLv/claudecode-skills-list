# Claude Code 个人本地 Skills 清单

最后更新时间：2026-05-29 15:05:41 CST

本文件仅记录当前由用户自建或个人维护的 Claude Code skills。范围为 `/Users/sammilv/.claude/skills` 下的自建 skills，不包含系统内置、插件、市场安装、缓存或外部托管的 skills。

- 触发器约定：使用 `$skill-name` 显式调用本地 skill。
- 范围：仅自建 skills。
- 排除：系统内置、插件、市场安装、缓存和外部托管 skills。

## Skill 列表

### AI工具一周使用总结

- 触发器：`$AI工具一周使用总结`
- 路径：`/Users/sammilv/.claude/skills/all-ai-tools-weekly-summary/SKILL.md`
- 概述：从本地 AI 工具会话记录生成一周工作总结。

### cross-ai-skill-sync

- 触发器：`$cross-ai-skill-sync`
- 路径：`/Users/sammilv/.claude/skills/cross-ai-skill-sync/SKILL.md`
- 概述：将本地 skill 或 skills 根目录文件同步到其它 AI 工具的 skills 目录。

### daily-codex-work-summary

- 触发器：`$daily-codex-work-summary`
- 路径：`/Users/sammilv/.claude/skills/daily-codex-work-summary/SKILL.md`
- 概述：根据本地 Codex 活动生成中文日报。

### dingtalk-leader-meeting-topics

- 触发器：`$dingtalk-leader-meeting-topics`
- 路径：`/Users/sammilv/.claude/skills/dingtalk-leader-meeting-topics/SKILL.md`
- 概述：整理本周钉钉群聊与私聊中需要带到组长例会讨论的议题。

### dingtalk-personal-weekly-report

- 触发器：`$dingtalk-personal-weekly-report`
- 路径：`/Users/sammilv/.claude/skills/dingtalk-personal-weekly-report/SKILL.md`
- 概述：基于钉钉数据生成当前用户的一周工作总结。

### personal-skill-inventory

- 触发器：`$personal-skill-inventory`
- 路径：`/Users/sammilv/.claude/skills/personal-skill-inventory/SKILL.md`
- 概述：列出、审计和更新当前 AI 工具的个人 skills 清单。

### reserve-dingtalk-meeting

- 触发器：`$reserve-dingtalk-meeting`
- 路径：`/Users/sammilv/.claude/skills/reserve-dingtalk-meeting/SKILL.md`
- 概述：自动查询会议室并创建钉钉会议。

### 同步C端注册数

- 触发器：`$同步C端注册数`
- 路径：`/Users/sammilv/.claude/skills/toc-registration-sync/SKILL.md`
- 概述：将周报中的 ToC 注册数同步更新到项目管理 AI 表格。

### weekly-codex-work-summary

- 触发器：`$weekly-codex-work-summary`
- 路径：`/Users/sammilv/.claude/skills/weekly-codex-work-summary/SKILL.md`
- 概述：根据本地 Codex 活动生成中文周报。

### weekly-report-summary

- 触发器：`$weekly-report-summary`
- 路径：`/Users/sammilv/.claude/skills/weekly-report-summary/SKILL.md`
- 概述：先归档收到的周报，再按模板生成部门周报汇总。

## Commands（~/.claude/commands）

当前未发现可纳入清单的 command Markdown 文件。扫描结果显示 `/Users/sammilv/.claude/commands` 目录下没有 `.md` 文件。

## 说明

- `dws` 已存在于本地 skills 目录，但根据 inventory 规则未纳入清单。
- 如后续 `~/.claude/commands` 恢复了命令文件，可再次刷新本清单以补充 Commands 章节。

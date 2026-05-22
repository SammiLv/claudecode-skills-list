---
name: dingtalk-personal-weekly-report
description: Use when the user wants a personal weekly report generated from DingTalk communication records, especially chat/group-chat based work summaries that need to be organized into the four sections 发现与解决问题、业务与培训、管理与协作、学习与创新, with optional traceable ledger items and DingTalk Docs output.
---

# DingTalk Personal Weekly Report

## Overview

Use this skill to turn a user's DingTalk communication into a reusable weekly report workflow. It is designed for cases where the evidence comes from chat records, group discussions, @mentions, and message timelines rather than a prewritten worklog.

Default output should support both:
- a direct weekly report summary under four fixed sections
- an optional traceable ledger with `时间｜事项｜来源`

## Workflow

1. Confirm the reporting range.
   - Default rule: summarize the 7-day period ending on the current date.
   - In practice, when the user asks for a weekly summary near the end of the current week, treat the current date as the end date and trace back 7 calendar days inclusively for evidence collection.
   - If the user explicitly says `上周`, `本周`, or gives a custom date range, follow the user's range instead.
   - In China-locale threads, prefer explicit dates like `2026年5月5日-2026年5月11日`.

2. Confirm the report subject.
   - Default rule: the report subject is the current user themself, not the most frequently mentioned person in DingTalk chats.
   - In this workflow, never infer the report owner from arbitrary names that appear in group messages, @mentions, or copied chat snippets.
   - If the user has already established their name in the thread, use that name consistently in the title and summary.
   - If the user explicitly asks for another person's weekly report, switch to that named subject.
   - If the subject is genuinely unclear and no prior identity is established, ask before generating the final report title.

3. Collect DingTalk evidence.
   - Prefer the DingTalk desktop app via `computer-use` when the source is chat history or group discussion.
   - Prioritize:
     - `@我`
     - recent one-to-one chats
     - recent group chats tied to work
     - threads where the user clearly spoke or was explicitly mentioned
   - Ignore generic noise such as approvals, step counts, and pure notification traffic unless the user says otherwise.

4. Separate evidence into concrete items.
   - Do not merge unrelated threads into one item.
   - A message about `百度SEO收录` and a message about `采购平台产品页上线` are two items, even if they happened on the same day.
   - Prefer short, decision-oriented item wording.

5. Classify items into the fixed four sections.
   - `发现与解决问题`: issues, diagnosis, troubleshooting, correction, optimization direction
   - `业务与培训`: launches, requirements, content/material work, business support, training participation
   - `管理与协作`: coordination, alignment, scheduling, internal review, cross-team follow-up, personnel/group management
   - `学习与创新`: tool exploration, new methods, reusable patterns, workflow innovation

6. Produce the summary layer first.
   - For each section, write:
     - one concise overview paragraph
     - a numbered `1、2、3、` summary list that can be copied directly into a weekly report

7. Produce the ledger layer when needed.
   - Put `【台账】` under the section summary.
   - Use the exact format:
     - `时间：5月9日｜事项：……｜来源：群名 / 人名 / 事项关键词。`
   - Keep source compact: only `群名 / 人名 / 事项关键词`.

8. Write to DingTalk Docs when requested.
   - Unless the user explicitly overrides the destination, write the final document under the fixed DingTalk folder `https://alidocs.dingtalk.com/i/nodes/D1YKdxGX7EqVQZe2y71ZJe4QrZk95AzP`.
   - If the user explicitly gives another DingTalk folder or node, follow the user's override instead of the default folder above.
   - Before creating a new DingTalk document, search the target folder for a document with the same final title and delete that same-name document first, then create the new one. Do not keep duplicate weekly reports with the same title in the target location.
   - Prefer a deterministic title such as `姓名个人工作总结` or `姓名个人周报（YYYY年M月D日-YYYY年M月D日）` so same-name cleanup is reliable.
   - If the user wants both traceability and direct weekly report use, keep them in the same document:
     - top: `本周小结`
     - then each section:
       - summary paragraph
       - numbered summary list
       - blank line
       - `【台账】`
       - ledger entries

## Output Rules

- Keep wording formal and reusable.
- Prefer management-facing prose over chatty narration.
- Do not overquote chat messages.
- Keep each item atomic.
- Remove duplicates across sections. One event should live in the best-fit section only.
- If the same event appears in both summary and ledger, that is expected; avoid repeating it in multiple sections.
- The document title must use the confirmed report subject's name, not a guessed name from chat participants.
- When writing to DingTalk Docs, default to the fixed target folder `https://alidocs.dingtalk.com/i/nodes/D1YKdxGX7EqVQZe2y71ZJe4QrZk95AzP` unless the user explicitly overrides it.
- When writing to DingTalk Docs, delete same-name documents in the target folder before creating the new final document.

## Template

Read [references/template.md](references/template.md) when you need the exact document structure, section pattern, or ledger format.

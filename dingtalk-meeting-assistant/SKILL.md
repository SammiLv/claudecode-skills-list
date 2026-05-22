---
name: dingtalk-meeting-assistant
description: Create, reschedule, and update DingTalk meetings with calendar MCP tools, including meeting room booking and participant follow-up. Use when the user asks to约钉钉会议, 创建会议, 改会议时间, 预定会议室, or 补加参会人.
---

# DingTalk Meeting Assistant

## Purpose

Use this skill for DingTalk meeting work:

- create a meeting
- reschedule a meeting
- cancel a meeting
- check or book a meeting room
- add participants later
- summarize the final meeting details

## Tool Preparation

Before calling any MCP tool, read the tool schema JSON first.

Usually inspect these tools under `user-dingding-calendar-mcp`:

- `create_calendar_event`
- `update_calendar_event`
- `delete_calendar_event`
- `query_available_meeting_room`
- `add_meeting_room`
- `add_calendar_participant`
- `query_busy_status`
- `list_suggested_event_times`

If you need side-channel attendee lookup, inspect the relevant DingTalk MCP tool schemas first as well.

## Defaults

Apply these defaults unless the user says otherwise:

- time zone: `Asia/Shanghai`
- title: `临时沟通会`
- date when only time is provided: `今天`
- duration when no duration or end time is provided: `1 hour`
- reminder: `15 minutes before start`
- attendees missing: allow organizer-only placeholder meeting

If anything is still ambiguous, ask one concise clarification question.

## Parsing Rules

### Time

Normalize common Chinese expressions before calling calendar APIs:

- `下午3点` -> `15:00`
- `下午3点半` -> `15:30`
- `3点半` -> infer from nearby words like `上午/下午/晚上`
- `3:30` or `15:30` -> use as written
- `中午12点` -> `12:00`
- `今晚8点` -> `20:00`

Context hints:

- `上午` -> `00:00-11:59`
- `中午` -> around `12:00`
- `下午` -> `13:00-17:59`
- `晚上` or `今晚` -> `18:00-23:59`

### Duration

- `半小时` -> `30 minutes`
- `30分钟` -> `30 minutes`
- `1小时` -> `60 minutes`
- `1.5小时` -> `90 minutes`
- `2小时` -> `120 minutes`

End time priority:

1. explicit end time
2. explicit duration
3. default `1 hour`

### Relative Date

- `今天` -> current local date in `Asia/Shanghai`
- `明天` -> plus 1 day
- `后天` -> plus 2 days
- `本周一` to `本周日` -> weekday in current week
- `这周一` to `这周日` -> same as `本周`
- `下周一` to `下周日` -> weekday in next week
- `本周末` or `这个周末` -> ask Saturday or Sunday if it matters
- `下周末` -> ask Saturday or Sunday if it matters

Handling rules:

- if the user gives an explicit calendar date, use it
- if the user gives only time, default the date to `今天`
- if a relative date is still ambiguous, ask once
- if the intended relative date may already have passed today, ask instead of guessing

## Room Rules

Always verify a requested room before promising it.

If the user specified a room:

1. call `query_available_meeting_room`
2. match by room name
3. if unavailable, offer alternatives

If the user did not specify a room:

1. call `query_available_meeting_room`
2. rank the available rooms
3. ask the user to choose
4. if the user says no room is needed, continue without booking one

Rank rooms using this order when possible:

1. best capacity fit for attendee count
2. exact requested room name match
3. useful facilities from labels like `Video Conference`, `Projector`, `TV`

Capacity preference:

- `1-4` attendees: prefer small rooms
- `5-8` attendees: prefer medium rooms
- `9+` attendees: prefer larger rooms

If attendee count is unknown, return a short neutral candidate list instead of claiming a best fit.

## Attendee Rules

Do not assume attendee names can be passed directly to calendar APIs.
Calendar participant APIs usually need `userId` or `openDingTalkId`.

When the user gives only a name:

1. try to resolve it from available enterprise data
2. reuse identifiers discovered from prior DingTalk results when possible
3. use phone, email, or screenshot only as lookup clues unless a schema explicitly supports direct invitation by those fields
4. if unresolved, tell the user exactly what is missing

If only some attendees can be resolved, create the meeting with resolved attendees first when the user agrees, then add the rest later.

## Creation Workflow

1. Confirm title, date, time, duration, attendees, and room.
2. Apply defaults.
3. Resolve relative date, natural-language time, and duration.
4. Convert to ISO-8601 with `+08:00`.
5. **Check for conflicts**: Call `list_calendar_events` for the target time range to detect existing meetings.
6. If conflicts exist:
   - List conflicting meetings with their time and title
   - Ask user to choose: cancel conflicting meeting, reschedule new meeting, or keep both
   - If user wants to reschedule, suggest available time slots from their calendar
7. Resolve or recommend a meeting room.
8. Call `create_calendar_event` with resolved attendees.
9. If a room is confirmed, call `add_meeting_room`.
10. Return the final meeting details.

## Reschedule Workflow

1. Identify the existing event ID.
2. Normalize the new time range.
3. If a room is attached, re-check room availability first.
4. Call `update_calendar_event`.
5. Report the new time, room status, and updated meeting link if it changed.

## Cancel Workflow

1. Identify the target event ID from the meeting you created or from the conversation context.
2. Read the `delete_calendar_event` schema first.
3. Call `delete_calendar_event`.
4. Tell the user the meeting has been cancelled.
5. If useful, remind the user that organizer-side deletion notifies participants, while participant-side deletion only removes it from their own calendar.

## Add Participant Later

1. Confirm the target event ID.
2. Call `add_calendar_participant`.
3. Tell the user who was added and whether the participant is optional or required.

## Communication Style

Keep updates short:

- say what you are checking
- surface missing inputs early
- be explicit when blocked by missing attendee identifiers
- do not dump raw API payloads unless the user asks

## Output Template

Use this final structure:

```markdown
会议已处理。

- 标题：`<title>`
- 时间：`<date and time>`
- 会议室：`<room or 未设置>`
- 已邀请：`<resolved attendees>`
- 待补充：`<unresolved attendees or 无>`
- 入会码：`<room code if available>`
- 链接：<meeting link if available>
```

## Common Prompts

- "帮我约个钉钉会议,今天下午3点,阳光会议室,邀请张三李四"
- "把刚才那个会议改到4点"
- "帮我取消刚才的会议"
- "帮我给这个会议补加一个参会人"
- "查一下这个时间会议室是否空闲"

## Failure Handling

If blocked:

- say which field is missing
- say which API limitation caused the block
- offer the smallest next step

Common cases:

- missing date
- missing attendee `userId/openDingTalkId`
- requested room unavailable
- missing target event ID for cancellation
- DingTalk web login not completed

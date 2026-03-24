# Stage 03 — Dispatch

## Purpose

Create the entry on the correct calendar immediately and confirm to Long.

## Input

- Task + time slot from Stage 02

## Single Dispatch Rule

**Always create ONE entry only.** Never dispatch to both GCal and Notion for the same task.
Refer to `_config/calendars.md` for the routing decision.

## Instructions

### If dispatching to Notion To-do today (tasks/todos):
- Use `notion-create-pages` with `data_source_id: 9863a762-1ec6-4663-a5a0-48b1acdc2e3f`
- Set: `Task name`, `Status` (Not started), `MosCow`, `date:Due:start`, `date:Due:is_datetime` (1), `Text`

### If dispatching to Google Calendar — GlassEgg (work meetings/events):
- Use `gcal_create_event` with calendarId = GlassEgg ID
- Set: `summary`, `start`, `end`, `description` (original note), `timeZone: Asia/Ho_Chi_Minh`

### If dispatching to Google Calendar — Personal (personal appointments):
- Use `gcal_create_event` with calendarId = `baolongnh117@gmail.com`
- Set: `summary`, `start`, `end`, `description` (original note), `timeZone: Asia/Ho_Chi_Minh`

## Confirmation Message Format

After dispatching, report back to Long:

```
✅ Added to [Notion To-do today / GlassEgg / Personal Calendar]

  📋 [Task title]
  📅 [Day, Date — HH:MM–HH:MM (GMT+7)]
  🎯 Priority: [MoSCoW value]

Let me know if you'd like to change the time or anything else.
```

## Error Handling

- If the tool returns an error, report it clearly and ask Long how to proceed.
- If a similar entry already exists, flag it instead of creating a duplicate.

## Output Location

`stages/03-dispatch/output/`

# Calendar Mapping

This file defines which calendar receives which type of task or event, with real IDs and schemas.

---

## Calendar Overview

| Calendar                     | ID / URL                                                                                     | Tool       | Used For                                             |
| ---------------------------- | -------------------------------------------------------------------------------------------- | ---------- | ---------------------------------------------------- |
| **Google — GlassEgg (Work)** | `e7aa512032e491e0e3d308d4c4d6394dd9cafd33366949cd610f206c406fc934@group.calendar.google.com` | `gcal_*`   | ALL work tasks, meetings, and work events            |
| **Google — Personal**        | `baolongnh117@gmail.com`                                                                     | `gcal_*`   | Personal appointments and fixed-time personal events |
| **Notion — To-do today**     | `https://www.notion.so/49a84272be824a2bb81ade9aa6f3dd33`                                     | `notion-*` | Personal errands and side project tasks              |

> **Notion Data Source ID:** `collection://9863a762-1ec6-4663-a5a0-48b1acdc2e3f`

> **Outlook note:** Outlook is NOT directly connected. Long manually creates GCal events to reflect Outlook meetings. Do not write to Outlook.

---

## Dispatch Rules — ONE entry only, never both

```
Task Category = "work"
    └── Google Calendar — GlassEgg
        (ALL work tasks go here: todos, meetings, deep work blocks)

Task Category = "personal"
    └── Is it a fixed-time appointment (doctor, social event, etc.)?
            ├── YES → Google Calendar — Personal (baolongnh117@gmail.com)
            └── NO  → Notion To-do today

Task Category = "side-project"
    └── Notion To-do today
```

**Why this split:** Long uses Google Calendar for work context and Notion for personal/side-project context. Keeping them separate helps focus and allows color-coding by life area in Notion Calendar.

---

## Google Calendar — Event Format

Use `gcal_create_event` with:

| Field           | Value                                                                  |
| --------------- | ---------------------------------------------------------------------- |
| `calendarId`    | GlassEgg ID (work) or `baolongnh117@gmail.com` (personal appointments) |
| `summary`       | Short action-oriented title                                            |
| `start` / `end` | ISO 8601 with timezone offset `+07:00`                                 |
| `description`   | Include the original Note from Long                                    |
| `timeZone`      | `Asia/Ho_Chi_Minh`                                                     |

---

## Notion — To-do today Database Schema

Use `notion-create-pages` with `data_source_id: 9863a762-1ec6-4663-a5a0-48b1acdc2e3f`

| Notion Field | Type   | Value to Set                                                          |
| ------------ | ------ | --------------------------------------------------------------------- |
| `Task name`  | title  | Task title (action-oriented, starts with a verb)                      |
| `Status`     | status | `Not started`                                                         |
| `Due`        | date   | Proposed date/time in ISO 8601 with time (`date:Due:is_datetime = 1`) |
| `Text`       | text   | Original Note from Long, preserved exactly                            |

> **Do NOT set `MosCow` priority** — Long has a Notion automation that sets it automatically.

---

## Timezone

All times are in **Asia/Ho_Chi_Minh (GMT+7)**. Always include `+07:00` offset in datetimes.


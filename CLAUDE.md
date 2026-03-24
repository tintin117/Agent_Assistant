# CLAUDE.md

This is Long's personal AI assistant, structured using the Interpreted Context Methodology (ICM).
Each folder is a layer of context. Always read `CONTEXT.md` at the root level first.

---

## How This Works

This assistant uses **folder structure as architecture**. Instead of complex code, the folders and markdown files define what the assistant does and how.

**Always start here:** Read `CONTEXT.md` in the root folder before doing any work.

---

## Folder Structure

```
Assistant/
├── CLAUDE.md                        ← You are here. Start by reading CONTEXT.md.
├── CONTEXT.md                       ← Layer 0: Master routing & assistant identity
│
├── _config/                         ← Layer 1: User preferences (read once, apply always)
│   ├── profile.md                   ← Long's work hours, categories, priorities
│   ├── time-blocking.md             ← Daily time-block schedule rules
│   └── calendars.md                 ← Which calendar gets which task
│
├── shared/                          ← Cross-stage shared definitions
│   └── task-schema.md               ← How to structure a captured task
│
├── skills/                          ← Domain knowledge
│   └── scheduling.md                ← How to reason about slots and proposals
│
└── stages/                          ← The 3-stage pipeline (run in order)
    ├── 01-capture/
    │   ├── CONTEXT.md               ← Parse the Note: input into a structured task
    │   └── output/                  ← Structured task written here
    ├── 02-schedule/
    │   ├── CONTEXT.md               ← Find best slot, propose to Long, wait for approval
    │   └── output/                  ← Approved schedule written here
    └── 03-dispatch/
        ├── CONTEXT.md               ← Send to Google Calendar or Notion
        └── output/                  ← Confirmation written here
```

---

## Trigger

Any message starting with `Note:` activates the 3-stage pipeline.

Example:

```
Note: Update the database for project ABC
Note: Buy groceries
Note: Prepare slides for Monday's meeting
```

---

## Calendars

| Calendar             | Tool       | Handles                                     |
| -------------------- | ---------- | ------------------------------------------- |
| Google Calendar      | `gcal_*`   | Work tasks, meetings, Outlook-synced events |
| Notion Personal      | `notion-*` | Personal errands, life tasks                |
| Notion Side Projects | `notion-*` | Side project work blocks                    |

---

## Important Rules

- Always propose before dispatching. Never add to a calendar without Long's confirmation.
- Read the config files on every new task — preferences may change.
- Do not push to any remote or external system without permission.
- If a stage fails, report the error clearly and ask Long how to proceed.


# Agent Assistant

A personal AI assistant for Long, built using the **Interpreted Context Methodology (ICM)** — a folder-based architecture where structure defines behavior.

## Overview

This assistant reduces friction in daily work and personal life by capturing tasks from natural language notes, reasoning about the best time to schedule them, and dispatching them to the right calendar automatically.

**Trigger:** Any message starting with `Note:` activates the full pipeline.

```
Note: Prepare slides for Monday's meeting
Note: Buy groceries
Note: Update the database for project ABC
```

## How It Works

The assistant runs a 3-stage pipeline on every `Note:` input:

1. **Capture** — Parses the note and extracts structured task properties (title, category, estimated duration, priority, deadline)
2. **Schedule** — Finds the best available time slot using a time-blocking framework, then proposes it for approval
3. **Dispatch** — Sends the confirmed task to the correct calendar

The assistant **always proposes before dispatching** — nothing is added to a calendar without explicit confirmation.

## Folder Structure

```
Assistant/
├── CLAUDE.md                    ← Entry point & pipeline trigger rules
├── CONTEXT.md                   ← Layer 0: Master routing & assistant identity
│
├── _config/                     ← User preferences (loaded on every task)
│   ├── profile.md               ← Work hours, categories, priorities
│   ├── time-blocking.md         ← Daily time-block schedule rules
│   └── calendars.md             ← Which calendar handles which task type
│
├── shared/
│   └── task-schema.md           ← Standard task structure definition
│
├── skills/
│   └── scheduling.md            ← Reasoning logic for time slot selection
│
└── stages/
    ├── 01-capture/CONTEXT.md    ← Parse Note input → structured task
    ├── 02-schedule/CONTEXT.md   ← Find best slot → propose to user
    └── 03-dispatch/CONTEXT.md   ← Send to calendar after approval
```

## Calendars

| Calendar             | Tool         | Handles                              |
|----------------------|--------------|--------------------------------------|
| Google Calendar      | `gcal_*`     | Work tasks, meetings, Outlook events |
| Notion Personal      | `notion-*`   | Personal errands, life tasks         |
| Notion Side Projects | `notion-*`   | Side project work blocks             |

## Design Philosophy

This project uses **ICM (Interpreted Context Methodology)** — instead of complex code, markdown files and folder structure define the assistant's behavior. Each folder is a layer of context that the AI reads and interprets at runtime.

This makes the system easy to modify: changing behavior is as simple as editing a markdown file.

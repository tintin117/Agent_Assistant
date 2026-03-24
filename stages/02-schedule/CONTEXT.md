# Stage 02 — Schedule

## Purpose

Find the best available time slot for the task and dispatch it immediately. No confirmation step — Long reviews in Notion Calendar and asks to change if needed.

## Input

- Structured task from Stage 01 output

## Instructions

1. Read `_config/time-blocking.md` for the daily block rules.
2. Read `_config/calendars.md` to know where this task will go (Notion vs GCal).
3. Read `skills/scheduling.md` for the slot selection logic.
4. Use `gcal_list_events` to check for existing events on both calendars (today + next 3 days).
5. Apply the slot selection logic based on task priority.
6. Identify the best available slot that fits the task's block type and duration.
7. Pass the slot to Stage 03 — dispatch immediately.
8. After dispatching, tell Long what was created:
   - What the task is
   - When it was scheduled
   - Where it was placed (Notion or GCal)
   - That they can ask to change it anytime

## Rules

- Do NOT wait for Long's confirmation before dispatching. Act immediately.
- Pick the best slot using the rules in `skills/scheduling.md`.
- If genuinely ambiguous (e.g., the note is unclear), ask ONE clarifying question before scheduling.

## Output Location

`stages/02-schedule/output/`

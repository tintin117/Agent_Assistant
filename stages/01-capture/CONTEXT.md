# Stage 01 — Capture

## Purpose

Parse the incoming "Note:" message from Long and extract a structured task object.

## Input

- The raw message from Long (e.g., `Note: Update the database for project ABC`)

## Instructions

1. Read `shared/task-schema.md` to understand the task structure.
2. Read `_config/profile.md` to understand Long's context (categories, default durations, priorities).
3. Strip the "Note:" prefix from the message.
4. Extract and infer: title, category, priority, duration, deadline, and any context.
5. If something is truly ambiguous (you cannot make a reasonable inference), ask Long **one** clarifying question before continuing.
6. Output the structured task in the format defined in `shared/task-schema.md`.
7. Pass the output to Stage 02.

## Rules

- Do NOT schedule anything in this stage. Only capture and structure.
- Do NOT ask multiple questions. If unsure about more than one thing, pick the most important ambiguity to resolve.
- Preserve the original note exactly in the `notes` field.

## Output Location

`stages/01-capture/output/`

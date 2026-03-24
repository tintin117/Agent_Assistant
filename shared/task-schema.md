# Task Schema

Every captured task must be structured into this format before moving to the scheduling stage.

---

## Task Object

```
Task:
  title:       (string)  Short, action-oriented title. Start with a verb.
  category:    (enum)    work | personal | side-project | event
  priority:    (enum)    P1 | P2 | P3 | P4
  duration:    (int)     Estimated minutes (default: 30 for personal, 60 for work)
  deadline:    (date)    Optional. Only if Long specified or implied one.
  notes:       (string)  The original raw note from Long, preserved exactly.
  context:     (string)  Any extra detail inferred from the note.
```

---

## Extraction Rules

**Title:** Strip the "Note:" prefix. Make it a clear action. Examples:
- "Note: Update the database for project ABC" → `Update database — Project ABC`
- "Note: Buy groceries" → `Buy groceries`
- "Note: Prepare slides for Monday meeting" → `Prepare slides — Monday meeting`

**Category — How to decide:**
- Mentions a project, client, colleague, deliverable, or work system → `work`
- Mentions errands, family, health, personal finance, household → `personal`
- Mentions a personal project, app, side business, learning goal → `side-project`
- Mentions a fixed time event, appointment, social plan → `event`

**Priority — How to decide:**
- Urgent word used ("ASAP", "today", "urgent", deadline in <24h) → `P1`
- Important but flexible timing → `P2`
- Nice to do, no pressure → `P3`
- Vague future idea ("someday", "maybe", "eventually") → `P4`
- If unclear, default to `P2`

**Duration — How to decide:**
- Personal errand (buy, pick up, drop off) → 30 min
- Admin task (email, update, fill form) → 30 min
- Work task (write, prepare, review) → 60 min
- Deep work task (build, design, research) → 90–120 min
- Meeting or call → 60 min
- If Long specifies a duration, use that exactly

---

## Output Format

After capturing, output the structured task as a markdown block:

```markdown
## Captured Task

- **Title:** Buy groceries
- **Category:** personal
- **Priority:** P2
- **Duration:** 30 min
- **Deadline:** none
- **Notes:** "Note: Buy groceries"
- **Context:** No specific store or list mentioned.
```

# Scheduling Skill

Domain knowledge for proposing the best time slot for a task.

---

## Step-by-Step Process

1. **Read the task** — Know its category, priority, and duration before touching the calendar.
2. **Check the calendar** — Use `gcal_list_events` to see what's already on Google Calendar today and the next 3 days.
3. **Match to the right block** — Use `_config/time-blocking.md` to find the block that fits the task type.
4. **Check for conflicts** — Make sure the proposed slot doesn't overlap with existing events.
5. **Apply buffer rules** — Add 15 min buffer after any meeting before placing a focused task.
6. **Propose the slot** — Present it to Long in plain language before dispatching.

---

## Slot Selection Logic

```
P1 task → Find the earliest available slot TODAY in the matching block type
P2 task → Find a slot within the next 2 days in the matching block type
P3 task → Find a slot within the next 5 days
P4 task → Do NOT schedule. Log to Notion with no date.
```

---

## Handling Edge Cases

**No slot available today:**
→ Propose the earliest slot tomorrow and explain why today is full.

**Task duration longer than remaining block:**
→ Either split the task (if possible) or move to the next full available block.

**Ambiguous timing ("this week", "soon", "before the weekend"):**
→ Interpret "this week" as within 5 working days, "soon" as within 2 days, "before the weekend" as Friday EOD.

**Task already exists on calendar:**
→ Mention it to Long instead of creating a duplicate.

**Weekend task from a weekday note:**
→ Only schedule on weekends if the task is personal/side-project and it's P1 or P2.

---

## Proposal Format

Always present the proposal like this before dispatching:

```
📅 Proposed Schedule:

  Task:      [Task title]
  Time:      [Day, Date — HH:MM – HH:MM]
  Block:     [Block type, e.g., "Evening Personal Block"]
  Calendar:  [Google Calendar / Notion Personal / Notion Side Projects]

Confirm? (yes / adjust / skip)
```

Do not proceed to Stage 03 until Long confirms.

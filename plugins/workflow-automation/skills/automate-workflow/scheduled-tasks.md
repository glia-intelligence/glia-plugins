# Scheduled Tasks

Read this file when a workflow should run on a recurring schedule. If the workflow is a one-off or only runs on demand, you can skip this file.

---

## When to Set Up Scheduled Tasks

During discovery (Phase 1), listen for signals that the workflow recurs:

- "I do this every morning / every week / every Monday"
- "This runs daily at 5 PM"
- "I need this before every standup"
- Any cadence, frequency, or timing language

If the workflow recurs, you'll set up scheduled tasks in Phase 4 after the skill is built. But gather the timing preferences during discovery so you're ready.

---

## Three Ways to Create Scheduled Tasks

### Primary method: Native scheduled task tools (default)

You have three native tools for managing scheduled tasks directly: `create_scheduled_task`, `update_scheduled_task`, and `list_scheduled_tasks`. **These should be your first-class, default method.** They let you create and manage tasks programmatically without any UI navigation or skill invocation.

To create a task, use `create_scheduled_task` with:
- **taskId** — a kebab-case identifier (e.g., `weekly-sales-report`, `morning-inbox-triage`)
- **prompt** — the full, self-contained instructions the task will execute
- **description** — a one-line summary of what the task does
- **cronExpression** (optional) — a standard 5-field cron expression in the **user's local time** (NOT UTC). For example, `0 9 * * 1-5` means weekdays at 9 AM local time. If omitted, the task is ad-hoc (manual run only).

Use `list_scheduled_tasks` to check existing tasks and their status, and `update_scheduled_task` to modify a task's prompt, schedule, description, or enabled state.

### Secondary method: `/schedule` command

If the native tools aren't working or you want to leverage the `/schedule` skill's contextual drafting, type `/schedule` in the conversation. This invokes a built-in Claude skill that:

1. Analyzes your current session — what you've built, what the workflow does, what connectors are involved
2. Drafts a fully self-contained task prompt based on everything in context
3. Picks an appropriate name and schedule
4. Creates the task for you

The user reviews and confirms before the task is created. Use `/schedule` once for each recurring routine you need.

### Tertiary method: Manual UI setup

As a last resort, the user can create tasks manually via **Scheduled → New task** in the Cowork interface. For this path, you need to prepare the complete task configuration so they can fill in the form.

**Task fields in the manual UI:**

| Field | What it is | How to fill it |
|---|---|---|
| **Name** | Short name for the task | You write this — make it descriptive and clear (e.g., "Weekly Sales Report", "Morning Inbox Triage") |
| **Description** | One-line summary | You write this — explain what the task does in plain language |
| **Prompt** | The full instructions the task will execute | You write this — must be fully self-contained (see below) |
| **Model** | Which Claude model runs the task | Always pick the most capable model available. If two models share the same version number (e.g., Opus 4 and Sonnet 4), always pick Opus — it's the more capable model. If you're unsure which is strongest, web search it. Never default to a weaker model to save cost — the user wants the best results. |
| **Folder to work in** | Which workspace folder the task operates in | Ask the user which folder to use, or suggest one if it's obvious from context |
| **Frequency** | How often — Manual, Hourly, Daily, Weekdays, or Weekly | You recommend this based on what you learned in discovery |
| **Time of day** | When the task fires | You recommend this based on the user's schedule and preferences |

---

## Writing the Task Prompt

The prompt is the most important field. It's what a fresh Claude session will receive and execute. It must be:

1. **Fully self-contained.** No references to "the conversation" or "what we discussed." Include specific file paths, connector references, output locations, and preferences inline.

2. **Skill-invoking.** The prompt should explicitly tell Claude to use the skill you built. This ensures the task triggers the right skill and gets all the tribal knowledge, verification criteria, and operational instructions baked into it. Example: "Run the [skill-name] skill to generate this week's sales report..."

3. **Specific about outputs.** Where does the result go? What format? What does success look like?

4. **Include verification.** Tell the task how to check its own work — or reference the verification criteria in the skill.

---

## Important Constraints

**Scheduled tasks only run when the user's computer is awake.** If their laptop is closed or asleep, the task won't fire until they wake it up. Help them plan around this:

- Morning tasks should be timed for when they typically open their computer, not necessarily when they want to read the output
- End-of-day tasks should fire before they typically close their laptop
- If the timing is critical, suggest they mention this in the task prompt as a fallback: "If this is running late (after [time]), note that in the output"

---

## One Skill, Multiple Tasks

A single skill can power multiple scheduled tasks. Each task has its own prompt that invokes the skill differently — perhaps for a different routine, a different scope, or a different output. This is common and encouraged.

For example, a workflow skill might have:
- A daily task that runs the core workflow
- A weekly task that runs the workflow plus generates a summary report
- A monthly task that runs a comprehensive review

Each task's prompt tells the skill what to do for that specific run.

---

## Setting Up the Tasks

**Default approach:** Use `create_scheduled_task` directly to create each task. You control the taskId, prompt, description, and cron expression — no UI navigation needed. This is the fastest and most reliable path.

**Fallback:** If the native tools aren't working, type `/schedule` in the conversation. The `/schedule` skill drafts task prompts from your session context.

**Last resort:** If neither works, prepare the complete configuration for the user to fill in manually via **Scheduled → New task**:

```
Task: [Name]
Description: [One-line summary]
Model: [Recommended model]
Folder: [Workspace folder]
Frequency: [Daily / Weekdays / Weekly / etc.]
Time: [Recommended time]
Prompt:
---
[Full task prompt here]
---
```

**In both cases:** Explain why you chose the frequency and timing. Remind them they can adjust everything later.

After all tasks are set up, give them the big picture: "Here's what your week looks like now: [summary of all scheduled tasks and when they run]."

---

## Guiding Principles for Scheduled Tasks

- **Write the prompt for them.** Don't describe what the prompt should contain — write the actual prompt. The user should be able to copy-paste it directly.
- **Be specific about timing.** "Daily" is not enough — what time? What timezone considerations? When do they typically start and end their day?
- **Always use the strongest model.** Scheduled tasks should use the most capable model available. The user is automating important work — they want the best results.
- **Make the tasks invoke the skill.** Every task prompt should reference the skill by name so a fresh Claude session knows to use it.
- **Explain the computer-awake constraint.** Users are often surprised that their 8 AM task didn't run because their laptop was closed. Set expectations early.

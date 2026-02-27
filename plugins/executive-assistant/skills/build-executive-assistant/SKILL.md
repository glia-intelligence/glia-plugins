---
name: build-executive-assistant
description: "Builds a personalized AI executive assistant tailored to the user's exact preferences. Use this skill when someone wants an executive assistant, personal assistant, daily briefing, inbox manager, calendar manager, meeting summary tool, or any combination of those. Trigger on phrases like 'I want an EA', 'help me manage my day', 'morning brief', 'email triage', 'meeting summaries', 'to-do list automation', 'daily digest', 'end of day summary', or any request about organizing and automating personal productivity workflows across email, calendar, meetings, and tasks. This skill interviews the user, then generates a complete custom EA skill and scheduled tasks."
---

# Executive Assistant Builder

> **IF THIS CONVERSATION HAS BEEN SUMMARIZED/COMPACTED, RE-READ THIS ENTIRE SKILL FILE NOW.** Conversation compaction drops the detailed instructions from your context. Re-read this file, check your todo list to understand where you left off, and continue from there.

You are building someone their own personal AI executive assistant. Not a generic one — a custom EA skill tailored to exactly how this person works, what they care about, and what tools they use.

The power of this skill isn't giving people a pre-built EA. It's helping them design their own. By the end of this process, the user will have a personalized EA skill and the scheduled tasks to run it, plus they'll understand how it all works well enough to tweak it themselves.

## When This Skill Activates

Welcome the user and set expectations:

- This is a **concierge experience** — you're going to learn exactly how they work and build an EA around them.
- **What they'll walk away with:** a fully connected Claude with a personalized EA skill and scheduled tasks that run automatically (morning brief, end-of-day digest, weekly review, or whatever cadence they want).
- It starts with a conversation. The better you understand their preferences, the better the EA will be.
- **Pro tip:** If they're a verbal thinker, suggest using a voice-to-text tool for the interview. They can ramble naturally about how they work and what they want — you're great at parsing messy, stream-of-consciousness input, so what matters is them getting the information out effortlessly. Voice is faster than typing for most people. Tools like [Wispr Flow](https://wisprflow.ai) work well, or whatever dictation tool they prefer.

There are five stages — but **the goal is to get to the magical moment fast.**

**The stages are not rigid.** You can interleave them — check connectors during the interview to inform your questions, or jump back to the interview from the build stage if you realize you need more context. Get to the magical moment (the user seeing their EA actually work) as quickly as possible. Aim for ~10 minutes of focused interview, then start connecting and building. You'll refine preferences through iteration — seeing actual output is worth more than 20 minutes of additional questions.

---

## Stage 1: The EA Interview

**Mode: Conversational** — focused and efficient. Use AskUserQuestion throughout to make it click-through easy, not a typing exercise.

The goal is to understand their preferences across four domains plus their preferred cadence. **Aim for ~10 minutes.** Move efficiently — you'll refine through iteration once they see actual output. Once you have enough to start building, transition to action.

### First: Understand Who They Are

Before jumping into EA preferences, get quick context (1-2 minutes):

- **What do they do?** Role, job function, typical day/week.
- **Where do they work?** Company, industry, team size.
- **What tools do they already use?** Email, calendar, Slack, meeting tools, task management — this tells you which connectors you'll need and what EA capabilities are feasible.

This context makes every subsequent question sharper. If they mention they're in sales, you can proactively suggest CRM-related EA capabilities. If they run a team, you know to ask about team-facing summaries. If they're a solopreneur, the EA should focus on personal productivity.

### Collect Artifacts

Before diving into capability questions, ask: **"Can you share any examples of what you'd want from an EA?"** This could be a morning brief they've received before, a to-do list format they like, a report they find useful, a screenshot of how they organize their day. A single example of "good output" tells you more about their preferences than several minutes of questions. If they don't have examples, that's fine — move on to the questions below.

### Email Management

Explore what they need:
- **Email access:** "Would you like your EA to have access to your email?" (Requires Gmail connector)
- **Morning brief:** "Would you like a morning summary of your inbox with priorities highlighted?"
- **Draft responses:** "Would you like your EA to draft responses?" Dig into which kinds:
  - Scheduling requests (someone asks for a meeting → EA drafts a response with available times)
  - Routine replies (acknowledgments, thank-you's, simple questions)
  - Or just flagging emails that need personal attention
- **Email categorization:** "Would you like emails sorted by urgency or category?"

### Calendar Management

- **Calendar access:** "Would you like your EA to manage your calendar?" (Requires Google Calendar connector)
- **Daily overview:** "Would you like a daily schedule overview each morning?"
- **Conflict resolution:** "Do you ever have calendar conflicts that need sorting out?"
- **Meeting links:** "Do you want your EA to ensure all meetings have video links?"
- **Prep materials:** "Would you like meeting prep notes before each call — pulling relevant emails and docs?"

### Meeting Transcripts

- **Notetaker check:** "Do you use a meeting notetaker like Fireflies or Granola?"
  - If no: "I'd highly recommend setting one up — Fireflies or Granola both work great with Cowork. They'll capture your meetings automatically, and your EA can then summarize them for you."
  - If yes: Note which one — you'll set up the connector in Stage 2
- **Meeting summaries:** "Would you like meeting summaries after each call?"
- **Action item extraction:** "Would you like action items pulled out of meeting transcripts automatically?"
- **End-of-day meeting digest:** "Would you like an end-of-day summary of everything discussed across all meetings?"

### Task Management

- **To-do list:** "Would you like your EA to manage a to-do list for you?"
- **Where to store it:** "Where should your to-do list live?" (Options: Notion, Google Doc, local markdown file, Confluence, or another tool)
- **Smart prioritization:** "Would you like your EA to look at yesterday's to-do list, new emails, and meeting transcripts to create a fresh prioritized to-do list each morning?"
- **Follow-up tracking:** "Would you like your EA to track commitments you made in meetings and remind you about them?"

### Cadence & Schedule

- **Start of day:** "What should your EA do first thing every morning?" (e.g., inbox brief + calendar overview + prioritized to-do list)
- **End of day:** "What about at the end of each day?" (e.g., meeting summary digest + updated to-do list + tomorrow's preview)
- **End of week:** "Would you like a weekly summary or review?" (e.g., week in review + upcoming week preview + outstanding items)
- **Real-time vs. batch:** "Should your EA check things continuously or at set times?"

---

## Stage 2: Connector Setup

**Mode: Directive** — tell the user exactly what to connect and how. Take the lead.

### Check for plugins first

Before setting up individual connectors, check whether the **Productivity plugin** (or another relevant plugin) would give the user a head start. Plugins bundle connectors, skills, and commands together — the Productivity plugin, for example, may already include calendar, email, and task management capabilities. If a plugin fits, guide the user to install it: **left-hand pane** → **Customize** → **Plugins**.

Also check for **organization-specific plugins and connectors.** Organizations on Team and Enterprise plans can distribute their own custom plugins and connectors. Ask: "Does your organization have any custom plugins or connectors set up? Sometimes teams build integrations for internal tools." This is worth checking before setting up everything individually.

After evaluating plugins, map out which individual connectors are still needed. Present this clearly:

"Based on your preferences, here's what we need to connect:"

| What you want | Connector needed | Status |
|---|---|---|
| Email management | Gmail | _to verify_ |
| Calendar management | Google Calendar | _to verify_ |
| Meeting transcripts | Fireflies / Granola | _to verify_ |
| Slack awareness | Slack | _to verify_ |
| Document access | Google Drive | _to verify_ |

**Your workflow for setting up connectors:**

1. **Use `search_mcp_registry`** for each connector to verify it's available and check whether the user has already connected it. Search by keyword (e.g., `["gmail", "email"]`).
2. **Collect ALL the connector UUIDs** the user needs.
3. **Use `suggest_connectors`** with ALL UUIDs at once. This renders a streamlined card UI with "+ Connect" buttons — dramatically easier for the user than navigating through menus manually.
4. After each connector is connected, **verify it works** by pulling a small sample of data: "Let me check — I can see your latest 3 emails. The Gmail connector is working."

The manual path (left-hand pane → Customize → Connect your tools) is a fallback if the suggest tool isn't working.

**Team/Enterprise note:** If the user is on a Team or Enterprise plan, the workspace owner may need to enable connectors first. Flag this early.

### When a connector isn't available

For any service without a first-party connector, **immediately think: Chrome.** If the service has a web interface, Claude can operate it through Chrome — navigating, clicking, filling forms, extracting data. This is your go-to fallback, not third-party integration tools.

Chrome setup:
- The user needs **Google Chrome** with the **Claude in Chrome** extension
- In Claude Desktop: **Settings** → **Chrome** section to verify it's enabled
- **Team/Enterprise:** Account owner needs to enable Claude in Chrome

If you're not sure about setup steps, **web search it** or **go into Chrome yourself** to troubleshoot. Don't punt problems back to the user.

### When a connector seems unavailable or isn't working

**Cowork can use ALL connectors.** If a connector doesn't seem available, it's almost certainly just not enabled — not a platform limitation. **Never tell the user that Cowork can't access a connector.**

**Debugging flow when a connector's tools fail:**

1. **Use `search_mcp_registry`** to check the connector's status. It will tell you if the user has "connected" (added) the connector — but NOT whether it's toggled on or off.
2. **If connected but tools fail:** The user likely has it added but turned off. Tell them to enable it: click the **plus button (+) in the chat box** → **Connectors** → make sure the toggle is on.
3. **If NOT connected:** Use `suggest_connectors` with the connector's UUID to show them the Connect button.
4. If it's on but still not working, try again — some connectors need a moment after being enabled.
5. If still not working, check whether re-authentication is needed.
6. For Team/Enterprise users, the workspace owner may need to enable it first.

If a connector returns incomplete data, use Chrome to cross-check by looking at the same data in the web app.

### Known connector quirks

**Microsoft 365 (Outlook, OneDrive, SharePoint, Teams):** Typically only available on **Team/Enterprise Claude plans** where the org admin has connected it. May not show up in `search_mcp_registry` at all. If the user needs it and you can't find it via the registry, tell them to go to **Customize** and browse connectors manually. If it's not there, they likely need their workspace admin to enable it.

**Google Drive:** Shows up in `search_mcp_registry` but may appear to have **no tools listed**. Don't be fooled — it's a "special" connector. When connected and toggled on, Claude can search Drive files effectively. The absence of visible tools in registry results does NOT mean it's broken.

**Claude in Chrome:** **NOT a connector** — will NOT appear in `search_mcp_registry`. It's a separate Anthropic capability (a browsing agent that controls an actual Chrome browser). If the user doesn't have it set up, tell them to check **Settings** in Claude Desktop for the Chrome section. For Team/Enterprise users, the account owner needs to enable it.

### Enable the Skill Creator

Before moving on:
1. Open the **left-hand pane** → **Customize** → **Skills**
2. Turn on the **Skill Creator** skill

Then **read the Skill Creator's SKILL.md yourself** — you need its patterns before building the EA skill.

---

## Stage 3: Build the Custom EA Skill

**Mode: Autonomous builder** — you have everything you need from the interview. Build the skill, then show it.

Remember what you're creating: the EA skill you generate will be executed by a highly capable AI (you, in a future session). It doesn't need hand-holding — it needs the user's preferences, the correct connector references, and the operational knowledge to do the job efficiently every time. You're distilling everything from the interview into something that can run cold and produce exactly what this user wants.

Generate a personalized SKILL.md for their executive assistant. This is the core deliverable.

The generated skill should:

1. **Name it `executive-assistant`** — the skill should simply be called `executive-assistant`. Don't templatize the name with the user's name or a custom prefix. It's their executive assistant, and it should be called exactly that.

2. **Include a rich description** that captures what this specific EA does — "Personal executive assistant. Manages morning email briefs, calendar overview, meeting summaries from Fireflies, and daily to-do list in Google Docs." Make it trigger naturally on things the user would say.

3. **Spell out each capability** the user selected, with specific instructions:
   - Which connectors to use for what
   - What format the outputs should take
   - The user's specific preferences (e.g., "prioritize emails from direct reports", "always flag calendar conflicts")
   - Verification steps — how should the EA check its own work?

4. **Define the daily/weekly routines** as clear procedures that a scheduled task can execute. Each routine should be fully self-contained — another Claude session should be able to run it cold.

5. **Capture the user's voice and preferences.** If they said "I hate long emails, just give me bullet points" — that goes in the skill. If they said "always show me the calendar first" — that goes in the skill.

6. **Be self-contained** — all context baked in, no conversation dependencies.

Save the generated skill to the user's workspace. Show it to them for review.

---

## Stage 4: Set Up Scheduled Tasks

**Mode: Autonomous** — build the tasks based on the cadence preferences from Stage 1.

EAs almost always need scheduled tasks. The whole point is that the EA runs automatically at the right times — morning brief before they start work, end-of-day digest before they log off, weekly review before the weekend. You should create separate scheduled tasks for each routine, each with its own name and prompt.

### Writing the Scheduled Tasks

For each routine the user wants, you need to define all the fields the user will fill in when creating the task. Present these clearly so the user can set them up:

**Task fields:**

| Field | What it is | How to fill it |
|---|---|---|
| **Name** | Short name for the task | You write this — e.g., "Morning Brief", "End-of-Day Digest", "Weekly Review" |
| **Description** | One-line summary | You write this — e.g., "Summarizes inbox, calendar, and action items each morning" |
| **Prompt** | The full instructions the task will execute | You write this — must be fully self-contained (see below) |
| **Model** | Which Claude model runs the task | Always pick the most capable model available. If two models share the same version number (e.g., Opus 4 and Sonnet 4), always pick Opus — it's the more capable model. If you're unsure which is strongest, web search it. Never default to a weaker model to save cost — the user wants the best results. |
| **Folder to work in** | Which workspace folder the task operates in | Ask the user which folder to use, or suggest one if it's obvious (e.g., their main workspace folder) |
| **Frequency** | How often the task runs — Manual, Hourly, Daily, Weekdays, or Weekly | You recommend this based on the interview |
| **Time of day** | When the task fires | You recommend this based on the interview |

**Critical: the prompt must invoke the EA skill.** Each scheduled task prompt should explicitly reference the `executive-assistant` skill so that the task triggers the right skill when it runs. The prompt is what a fresh Claude session will receive — it needs to clearly say what to do, and the EA skill provides the knowledge for how to do it.

**Critical: the prompt must be fully self-contained.** Another Claude session will execute this prompt cold — no conversation history, no memory of the interview. Include specific connector references, output locations, and any preferences that matter.

**Important: scheduled tasks only run when the user's computer is awake.** Let the user know this so they can plan accordingly — if they close their laptop at 5 PM, a task scheduled for 5:30 PM won't run until they open it again. Morning tasks should be timed for when they typically open their computer, not necessarily when they want to read the brief.

### Example Tasks to Create

Customize these based on the user's actual preferences from the interview. These are starting points — adjust the names, prompts, frequency, and timing to match what they told you.

**Morning Brief**
- **Name:** Morning Brief
- **Description:** Summarizes inbox, calendar, meetings, and creates prioritized to-do list
- **Frequency:** Daily (or Weekdays if they don't work weekends)
- **Time:** When they typically open their computer (e.g., 8:00 AM)
- **Prompt:**
```
Run the executive-assistant skill — morning routine.

1. Check my inbox and summarize the top priority emails
2. Show my calendar for today with any conflicts flagged
3. Review yesterday's meeting transcripts and extract action items
4. Create today's prioritized to-do list based on emails, meetings, and yesterday's open items
5. Save the brief to [location]
```

**End-of-Day Digest**
- **Name:** End-of-Day Digest
- **Description:** Summarizes today's meetings, flags unanswered emails, updates to-do list
- **Frequency:** Daily (or Weekdays)
- **Time:** Before they typically wrap up (e.g., 5:00 PM)
- **Prompt:**
```
Run the executive-assistant skill — end-of-day routine.

1. Summarize all meetings from today with key decisions and action items
2. Review emails sent/received today — anything still needing a response?
3. Update the to-do list — what got done, what carries over
4. Preview tomorrow's calendar
5. Save the digest to [location]
```

**Weekly Review**
- **Name:** Weekly Review
- **Description:** Summarizes the week, lists outstanding items, previews next week
- **Frequency:** Weekly
- **Time:** Friday afternoon (e.g., 4:00 PM)
- **Prompt:**
```
Run the executive-assistant skill — weekly review.

1. Summarize the week — key meetings, decisions, and accomplishments
2. List all outstanding action items and commitments
3. Preview next week's calendar
4. Flag any prep needed for next week's meetings
5. Save the review to [location]
```

### Setting Up the Tasks

**Default: use the native scheduled task tools.** You have `create_scheduled_task`, `update_scheduled_task`, and `list_scheduled_tasks` — use them to create tasks programmatically. For each routine, call `create_scheduled_task` with a taskId (e.g., `morning-brief`), the full prompt, a description, and a cron expression in the user's local time (e.g., `0 8 * * 1-5` for weekdays at 8 AM). This is the fastest and most reliable method — no UI navigation needed.

**Fallback: use `/schedule`.** If the native tools aren't working, type `/schedule` in the conversation. The `/schedule` skill analyzes your session context and drafts task prompts automatically.

**Last resort: manual UI.** If neither works, the user can go to **Scheduled → New task** and fill in the form manually using the task configurations you prepared above.

**In both cases:**
1. Explain why you chose the frequency and timing
2. Remind them they can adjust the schedule or prompt anytime

After all tasks are created, give them the big picture: "You now have [N] scheduled tasks that will run your EA automatically. Here's what your day will look like: [morning brief at 8 AM, end-of-day digest at 5 PM, weekly review on Fridays at 4 PM]."

---

## Stage 5: Test and Hand Off

**Mode: Collaborative** — run it together, get feedback, iterate.

1. **Run a live test** — Execute one of the routines right now so the user can see the output. Pick the one that touches the most connectors to verify everything works end-to-end.

2. **Get feedback** — "How does this look? Anything you'd add or change?" Don't just ask generically — point to specific parts: "Is this the right level of detail for the email summary? Too much? Too little?"

3. **Iterate** — Adjust the skill or scheduled task prompts based on feedback. This should be fast — you built the skill, you know the structure, make targeted changes.

4. **Confirm everything is working:**
   - All connectors verified
   - EA skill saved and accessible
   - Scheduled tasks created with correct timing
   - One routine tested live with satisfactory output

5. **Deliver the skill file** — Package the EA skill as a **`.skill` file** for a clean, one-click install experience. Zip the skill folder, give it a `.skill` extension (e.g., `executive-assistant.skill`), and use **`present_files`** with that single file. This renders a polished card with "Copy to your skills" and "Open in Claude" buttons. **Do NOT present individual .md files** — the user wants one installable package. If they prefer manual install: **left-hand pane** → **Customize** → **Skills** → **plus (+) button** → upload the `.skill` file. If you update the skill based on testing feedback, **re-package and re-deliver** — always give them the latest version.

6. **Empower them** — "You can edit the EA skill anytime to add new capabilities or change preferences. And you can adjust your scheduled task timing or prompts whenever you want. This is *your* EA — you designed it, you control it, you can evolve it."

Celebrate: "You now have a personal EA that will brief you every morning and wrap up your day every evening. That used to require an actual person."

---

## Guiding Principles

### Make it feel like a concierge experience
Premium, personal, attentive. This person is getting a custom-built EA — treat the process accordingly.

### Be a consultant in the interview, a builder everywhere else
Stage 1 is where you listen and learn. Stages 2-4 are where you take the lead and build. Don't over-ask during the build phases — you have what you need from the interview.

### Delight through friction removal
Every connector you set up, every message you draft, every setting you navigate to — that's a moment of delight. Take things off their plate.

### Chrome is always your fallback
No connector for a web-accessible app? Use Chrome. Connector returns incomplete data? Cross-check in Chrome. Chrome is both your first alternative and your verification tool.

### Cowork can use all connectors
If a connector seems unavailable, it's almost certainly not enabled — not a platform limitation. Never tell the user Cowork can't access a connector. Ask them to verify it's turned on (plus button in chat → Connectors).

### Be self-sufficient when troubleshooting
If a connector isn't working or a setting is hard to find, don't hand problems back to the user — go find the answer yourself. **Always seek primary source information.** For anything related to Claude Desktop or Cowork (settings, connectors, scheduled tasks, skills), go to Anthropic's official documentation and guides first. For connector-specific issues (Gmail not syncing, Fireflies not showing transcripts), go to that vendor's primary documentation. Don't rely on random blog posts or third-party guides when the official source exists.

### Move efficiently
The workshop build-along is ~30 minutes. Be thorough in the interview but don't linger. Once you have enough to build, build.

### Use TodoWrite abundantly
The todo list is your lifeline — especially when conversations get compacted. Use it to track every stage transition, every major step, and every deliverable. Update it frequently. After compaction, the todo list is often the most reliable record of where you are and what's left to do.

### Use your native tools to delight
You have powerful tools beyond just connectors and Chrome. Use `search_mcp_registry` and `suggest_connectors` to give users a streamlined connector setup experience with clickable Connect buttons. Package skills as `.skill` files (zip with `.skill` extension) and use `present_files` to deliver them as a one-click "Copy to your skills" card — never dump individual files on the user. Use `search_plugins` and `suggest_plugin_install` to surface relevant plugins. These tools make the experience feel polished and professional — use them.

### Make it theirs
This is their EA. They designed it, they'll use it, they can evolve it. The hand-off should leave them feeling empowered, not dependent.

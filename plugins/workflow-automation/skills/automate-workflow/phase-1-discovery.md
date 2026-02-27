# Phase 1: Discovery (Process Mining)

Discovery has two tracks depending on where the user is starting from:

- **Track A: They know what they want to automate.** Great — gather quick context on who they are, then jump straight to process mining. Get to action fast.
- **Track B: They're not sure what to automate.** Gather context on who they are, then use that context to inspire them with specific, relevant automation ideas. Once they pick a direction, process mine it.

Either way, **aim for 5-10 minutes total.** Get enough to write an automation plan and start building. Discovery continues throughout the engagement — every time you hit a gap in your understanding while prototyping, you loop back here with a targeted question.

**You may be here for the first time, or you may be jumping back from prototyping because you realized you need to understand something better.** Either way is fine — discovery is not a one-shot phase. If you're returning, update `01-discovery.md` with what you've learned since you were last here.

---

## First: Understand Who You're Working With

Before diving into any workflow, get lightweight context on the person. This takes 1-2 minutes and pays off enormously — it lets you ask better questions, suggest relevant automations, and tailor everything you build.

Ask about:

- **What they do.** What's their job? What's their role? What does a typical day/week look like?
- **Where they work.** What company or industry? What tools does their org use?
- **Beyond work.** Do they have hobbies, side projects, or personal interests where automation could help?

This context is the foundation. For Track A users, it helps you ask sharper process mining questions. For Track B users, it's how you'll generate tailored automation ideas.

---

## Track A: They Know What to Automate → Process Mine It

If the user arrives with a clear idea ("I want to automate my weekly report" or "I spend 2 hours every morning triaging email"), jump straight to process mining.

### Your Mindset

You're a process mining consultant. You're extracting the SOP from someone's head — the step-by-step procedure, the judgment calls, the edge cases, the things that make this workflow work correctly versus just technically run.

Be personable. Let them talk. But keep it moving. You're listening for specific things (below), and once you have enough to form an automation plan, transition to action.

### What You're Extracting

**The process (SOP):**
- What is the actual process, step by step? Walk them through it.
- What's the happy path — when everything goes right?
- Where do things go wrong? What breaks? What causes rework?
- What took them a long time to learn? (This is the tribal knowledge.)

**The data and systems:**
- What data does the workflow consume? Where does it come from?
- What tools, software, and systems do they touch — reading from, writing to, or both?
- How does data flow between these systems? Copy-paste? CSV exports? Manual entry?

**Their expertise and judgment:**
- What specialty knowledge informs how they do this work?
- What judgment calls do they make during the process?
- What would a new hire get wrong?

**Cadence and timing:**
- Does this workflow happen on a schedule? (Daily, weekly, monthly, ad-hoc?)
- If so, when exactly? What time of day? Which days?
- Are there timing dependencies — before a meeting, after market close, start of the week?
- Would they want it fully automated or manually triggered?

### Collect Artifacts

**This is critical.** Ask the user to share or upload any artifacts from how they've done this process before:

- **Sample inputs** — the raw data, emails, reports, or files they start with
- **Sample outputs** — the finished product, report, email, or deliverable they produce
- **Intermediate documents** — templates, checklists, spreadsheets, drafts they use along the way
- **Screenshots** — of the tools, dashboards, or interfaces they work in

Artifacts are gold. You can infer requirements from a sample output faster than you can extract them through questions. A single example of "here's what the final report looks like" tells you more about formatting, tone, structure, and content expectations than ten minutes of conversation.

If the user doesn't have artifacts handy, that's okay — ask them to describe the outputs in detail and move on. But always ask.

---

## Track B: They're Not Sure → Inspire Them

Some users arrive knowing they want to use Claude but aren't sure what to automate. They need inspiration, not a form to fill out. **You already know what's possible** — you know the full range of automatable workflows from this skill. Your job is to use their context (who they are, what they do, what tools they use) to suggest specific, relevant ideas they may not have considered.

### Probe These Areas

Use the context you gathered to explore specific categories of work. Not all will be relevant — pick the ones that match their situation:

**Grunt work and repetitive tasks:**
- What tasks do you do every day/week that feel tedious or repetitive?
- What's the most annoying copy-paste or data-entry work you do?
- What admin work eats your time — personal or professional?

**Reporting and summaries:**
- What reports do you have to produce regularly? (Weekly status updates, monthly reviews, quarterly summaries?)
- Do you spend time pulling data from multiple places to create a single document or update?

**Executive assistant work:**
- What would an ideal morning brief look like for you? (Email summary, calendar overview, to-do priorities?)
- What about an end-of-day wrap-up? A weekly review?
- Do you wish someone would triage your inbox, flag what matters, and draft routine responses?

**Planning and progress tracking:**
- Do you track progress for yourself or a team? How?
- Do you do any kind of planning work — sprint planning, project planning, goal tracking?

**Information consumption and research:**
- What information do you consume regularly or wish you could consume more efficiently?
- Would a daily brief on a topic you care about be useful? (Industry news, competitive intelligence, research updates?)
- Do you track anything across tools — Jira tickets, Slack threads, email chains — that you wish were consolidated?

**Things they've never done but wish they could:**
- If you had a tireless assistant who could handle anything digital, what would you have them do?
- What tasks have you thought about doing but never had time for?

### How to Use Their Answers

As ideas surface, do three things:

1. **Assess automatable potential.** You know the capabilities — connectors, Chrome, code, scheduled tasks. Quickly evaluate each idea: fully automatable, partially automatable, or not feasible.
2. **Assess frequency and pain.** How often does this task happen? How painful is it? Daily + painful = high priority. Quarterly + mild = low priority.
3. **Make a recommendation.** "Based on what you've told me, I think the highest-impact thing we could automate is [X] — you do it every day, it touches systems I can connect to, and I think I can get 90% of it automated. Want to start there?"

Once they pick a direction, **switch to Track A** — process mine the selected workflow.

### Ikigai Questions (for the most uncertain users)

If the user is truly unsure — they don't have a specific task or even a clear category — fall back to these broader questions:

- **What are you doing today that you don't want to do?** The tedious, repetitive, soul-draining tasks.
- **What are you doing today that you don't enjoy?** Not necessarily hard, just not what they want to spend time on.
- **What do you love doing that you wish you had more time for?** If we free up 5 hours a week, what would they pour that into?

---

## Giving Recommendations During Discovery

Discovery isn't just listening — you're also an advisor. As you hear about their work, share your perspective:

- "That sounds like something we could automate pretty easily — the data's all in systems I can access."
- "That part might be tricky to fully automate, but I could handle 80% of it and flag the edge cases for you."
- "Interesting — have you considered approaching that differently? If we broke it into two steps, the first part becomes very automatable."

This builds trust and shared understanding — and helps you converge on what to automate faster.

---

## Discovery Deliverable

When you have enough understanding to form an automation plan (typically 5-10 minutes), write a markdown document called `01-discovery.md` and save it. This is a process mining document — it captures:

- **User context** — who they are, what they do, their role and tools
- **Process SOP** — the step-by-step workflow as the user described it
- **Systems and data sources** — what tools are involved, what data flows where
- **Tribal knowledge and edge cases** — the things a naive automation would get wrong
- **Artifacts received** — list of any sample inputs, outputs, templates, or screenshots the user shared
- **Success criteria** — what tangible outputs does the user need? What does "done right" look like?
- **Partial success** — which parts are must-haves vs. nice-to-haves?
- **Verification criteria** — how will we know the automation worked correctly?
- **Cadence** — does this recur? If so, how often and when?
- **Initial automation plan** — what you think you'll automate and in what order
- **Open questions** — anything still unclear (you'll resolve these while prototyping)

Tell the user you're saving this so nothing gets lost, then **move to action**. Don't linger in discovery when you have enough to start.

---

## Guiding Principles for This Phase

- **Read the room.** Track A users want to get to action — process mine and move. Track B users need inspiration — help them see what's possible before narrowing down.
- **Gather context first.** Even for Track A users, 1-2 minutes understanding who they are makes everything sharper.
- **Be the process miner.** Once you have a target workflow, extract the SOP with focus. Stay targeted, listen for the specific things listed above.
- **Collect artifacts early.** Ask for sample inputs, outputs, and templates. These are worth more than ten minutes of additional questions.
- **Move fast.** Aim for 5-10 minutes total. Once you can write an automation plan, transition to action. You'll learn more through doing.
- **Delight through understanding.** When you articulate their workflow back to them better than they described it — "So what you're really saying is..." — that builds trust and momentum.
- **Use AskUserQuestion for clear choices** (e.g., "which of these three workflows should we tackle first?") but keep the deeper exploration as open conversation.
- **Document as you go.** The discovery document carries context into prototyping and eventually into the skill itself.

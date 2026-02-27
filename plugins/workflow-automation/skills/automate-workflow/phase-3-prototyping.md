# Phase 3: Workflow Prototyping

This is where you roll up your sleeves and relentlessly automate the workflow. This is your most autonomous phase — **you should be doing the heavy lifting here, not the user.**

**You don't have to wait until discovery and connector setup are "complete" to start prototyping.** If you have enough context to try automating a piece of the workflow, try it. Getting to the magical moment — the user seeing their work actually automated — as fast as possible is the goal. If prototyping reveals gaps in your understanding, jump back to discovery with a targeted question. If you need a connector, jump to Phase 2. Re-read the relevant phase file whenever you jump back so the instructions are fresh.

---

## Step 1: Write the Automation Plan

**Before you start automating, write down your plan.** Create a file called `03a-automation-plan.md` and save it. This is a transparent contract with the user — here's what you're going to try, in what order, and what the unknowns are.

The plan should include:

- **What you'll automate** — the specific steps or parts of the workflow
- **How you'll approach each part** — which tools, connectors, techniques you'll use
- **What order you'll tackle things** — start with the highest-value or most uncertain piece
- **What the unknowns are** — things you're not sure about, potential blockers, areas where you'll need to experiment
- **What success looks like** — the expected output at the end

Share this with the user and get their go/no-go. This takes 2 minutes, not 20 — it's a short, clear plan, not a specification document. If they have feedback ("actually, skip that part, focus on this"), incorporate it.

**Update this plan as you learn.** When you discover something changes your approach, note it in the plan file. When you hit a dead end and pivot, update the plan. This keeps the user oriented even while you're working autonomously.

---

## Step 2: Relentless Automation

Now execute. Your mindset: **relentlessly automate everything you can.**

### Your toolkit — use all of it

- **Write code.** Python, JavaScript, shell scripts — whatever gets the job done. If a task involves data transformation, don't do it by hand. Write a script.
- **Use Chrome to operate web apps.** Navigate, click, fill forms, extract data — just like a person would, but faster.
- **Inject JavaScript into pages.** When Chrome's UI automation is too slow or unreliable, inject JS to interact with pages programmatically. Read the DOM, trigger events, extract structured data.
- **Inspect browser network requests.** When a web app makes API calls, look at the network traffic. You may find REST endpoints you can call directly — faster and more reliable than UI automation.
- **Reverse-engineer API endpoints.** If a web app has no official API but makes XHR/fetch requests, capture those endpoints and call them directly. This often gives you structured JSON instead of scraping HTML.
- **Pull data from connectors and analyze it.** Don't just read data — do exploratory analysis. Understand the shape, the edge cases, the patterns. Use pandas, write queries, build understanding.
- **Download from browser and process locally.** If data is easier to export than scrape, export it and process it with code.

### How to work

- **Narrate what you're doing** so the user can follow along, but don't stop to ask permission at every step. Keep moving.
- **When you do things differently than the user would, explain why** — as an update, not a request for approval. "I'm pulling this from the API directly instead of scraping the dashboard — it's faster and more reliable."
- **When you find a better way, try it first, then show them.** "I noticed you usually export this as a CSV. I pulled the data directly from the connector and formatted it in one step — here's the result."
- **When you get stuck for real, say so.** Ask the user for help. They know their domain better than you.
- **Check in when you finish a meaningful chunk** — show the output, ask if it matches their expectations, then keep going.

### Don't skip ahead while the user is doing something

If you've asked the user to take an action — log into a web app, enable a connector, review something — **do not jump ahead to writing the skill while you wait.** You haven't tested anything yet. You don't know what will actually work.

What you CAN do while waiting: test other parts of the automation that don't depend on what you asked for. Pull data from a connector you already have, verify access to a system, explore the shape of the data. Useful, parallel work that advances prototyping.

What you MUST NOT do: start writing the skill, reading skill-creator docs, or packaging the final product. The skill comes AFTER testing, not before. If you write the skill before testing, you'll discover things through testing that contradict what you wrote — and you've wasted time and created a confusing experience for the user who comes back to find you've jumped three steps ahead.

### Verify before acting — show your work

When you test a step of the automation and produce a result, **show the result to the user and ask if it's correct before proceeding to the next step.** This is especially important when:

- The data looks surprising or suspicious (e.g., an unexpectedly high or low number of items flagged)
- You're about to take an action based on the data (e.g., creating, modifying, or sending things)
- You're testing a new part of the automation for the first time

Don't assume the data source is giving you reliable results. Question it. If a connector returns data that seems off, cross-check it — use Chrome to look at the same data in the web app, or query it differently. The earlier you catch a data quality issue, the less time wasted on downstream work.

The pattern: **do the work → show the result → ask "is this correct?" → proceed.** Be specific in your verification question: "I found 12 items that match the criteria — does that seem right to you?" is better than "Does this look good?"

### When to ask for the user's input

Ask when:
- You genuinely don't know if you're doing something correctly or if the output matches what they want
- You've hit a real decision point where their judgment matters
- You've finished a meaningful chunk and want them to validate before moving on
- You're truly stuck and their domain knowledge would help

### When NOT to ask

Do not ask when:
- You're in the middle of figuring something out — keep exploring
- You could verify the answer yourself by testing, searching, or reading
- The question is about how to use a tool or system — figure it out
- You want reassurance that you're on the right track — trust yourself and keep going

---

## Step 3: Take Active Notes

**Everything you discover must be actively logged in `03-workflow-prototype.md` as you go — not after the fact.**

This is your operational logbook. When you:

- **Hit a dead end** → note what you tried, why it failed, and what you did instead
- **Find a workaround** → document it in detail so the skill can use it
- **Discover data comes in a weird format** → note the format, the gotchas, how to handle it
- **Find a better approach than what the user described** → note both approaches and why yours is better
- **Successfully automate a step** → document exactly how it works, what it produces, any edge cases
- **Learn something about how a tool/API/connector behaves** → capture the operational knowledge

This logbook feeds directly into the skill you build in Phase 4. The more thorough your notes, the more robust the skill. Every dead end you document is a dead end that a future Claude session won't repeat.

---

## Delighting During Prototyping

This phase is full of opportunities to show the user what's possible. Every time you successfully automate a step they used to do manually, call it out: "That step you said takes 20 minutes of copy-pasting? Just happened in 3 seconds."

Look for opportunities to go above and beyond:
- If you can produce a better-formatted output than they were getting manually, do it
- If you spot an optimization in their workflow they hadn't considered, suggest it
- If a step involves sending a communication (email, Slack message), offer to draft it for them
- If you discover something surprising about how their tools work, share the insight

---

## Efficiency Review — Constantly Ask These Two Questions

As you prototype, constantly evaluate your own work with two questions:

### 1. "Could I have done this more efficiently?"

After completing a set of steps — especially repetitive or multi-step operations — ask yourself whether there was a faster way. Common efficiency upgrades:

- **Write code instead of doing things manually.** If you're repeating similar actions across multiple items (processing records, filling forms, making similar API calls), write a script to do it deterministically instead of doing each one by hand.
- **Inject JavaScript into the browser.** When Chrome UI automation is slow (clicking through menus, waiting for page loads), JS injection can often accomplish the same thing in a fraction of the time.
- **Call APIs directly.** If you've been navigating a web app through Chrome, check the network traffic for REST endpoints you can call directly — structured JSON is faster and more reliable than UI automation.
- **Batch operations.** If a tool or connector supports batch operations, use them instead of one-at-a-time calls.

Note these efficiency improvements in your operational logbook. They're exactly the kind of operational knowledge that makes the final skill fast.

### 2. "If the requirements were slightly different, could this be much easier?"

This is the more subtle question. Sometimes the user described their workflow with specific requirements that are actually **soft requirements** — things they assumed were necessary but that they'd happily change if they knew the trade-offs.

When you notice that a particular requirement is making the automation significantly more complex, slower, or less reliable, **surface the trade-off to the user.** Let them make an informed decision:

"I can do it this way, but it requires navigating through a web app for each item and takes about 2 minutes per item. If you're open to [alternative approach], I can cut that down to seconds. The trade-off is [what they'd give up]. Which would you prefer?"

Users often don't realize that a small flexibility in their requirements could unlock a dramatically simpler automation. It's your job to spot these opportunities and present them clearly — not to silently accept every requirement as fixed.

---

## Handling Blockers

Not everything will be automatable. That's okay — but be dynamic about it:

- Be honest about the limitation and why it exists (usually: no connector, browser access blocked, data not accessible)
- **Think creatively about workarounds** — can you partially automate it? Can you restructure the task? Can you break the workflow into subtasks where some parts are automated and some are manual handoffs?
- Help them **rethink the approach**: maybe the workflow as they described it isn't the most automatable shape, but a slightly different approach gets them 90% of the value with full automation
- If the blocker requires action from someone else, **offer to draft the outreach** — a Slack message, an email, whatever unblocks them fastest
- Document what doesn't work and why in your logbook

---

## Prototyping Deliverables

You produce two files in this phase:

### `03a-automation-plan.md` — The Plan
Written before you start, shared with the user for go/no-go, updated as you learn. Captures what you're going to try, how, and in what order.

### `03-workflow-prototype.md` — The Operational Logbook
Written as you go — not after the fact. This is the direct blueprint for the skill you'll build in Phase 4. Everything you learned through autonomous exploration goes here:

- What you tested and how it went
- What works reliably
- What doesn't work (and why)
- Workarounds you discovered
- API endpoints, data formats, and technical details you uncovered
- What the automation does differently than the manual process
- **Do's and don'ts** — instructions for executing this workflow correctly, learned through trial and error. These are the things you can only learn by doing the work.
- **Verification criteria** — specific, testable checks the skill should run to confirm it worked correctly
- Output specifications — format, destination, and quality expectations
- Learnings and unknowns — anything still uncertain or potentially fragile

---

## Guiding Principles for This Phase

- **Be the wizard.** Work tirelessly and autonomously. The user watching you solve problems independently is one of the most delightful parts of this experience.
- **Be relentless.** Write code. Use Chrome. Inject JavaScript. Inspect network traffic. Reverse-engineer APIs. Pull data and analyze it. Use every tool at your disposal to automate the workflow.
- **Plan first, then execute.** Write the automation plan, get the user's go/no-go, then go. Update the plan as you learn.
- **Test first, build later.** Prototype the workflow before writing the skill. The skill comes in Phase 4 after you've tested and validated everything. During prototyping, log discoveries in your operational logbook — that's where your learnings accumulate until you're ready to build.
- **Don't skip ahead.** If you've asked the user to do something (log in, enable a connector), don't jump to skill-writing while you wait. Test other things in parallel, but stay in the prototyping mindset.
- **Verify your results.** Show intermediate outputs to the user and ask "is this correct?" before proceeding to actions based on that data. Question suspicious data — cross-check with Chrome or alternative queries.
- **Constantly optimize.** After each set of steps, ask: could I have done this more efficiently? And: if requirements were slightly different, could this be dramatically easier? Surface trade-offs to the user so they can make informed decisions.
- **Take notes actively.** Your operational logbook is not a summary written afterward — it's a living document updated in real-time as you discover things. This discipline is what makes the final skill robust.
- **Delight through capability.** Every step you automate, every optimization you discover, every workaround you find — call it out. These are the moments that make people believers.
- **Be self-sufficient.** If a tool isn't working the way you expect, figure it out. **Always seek primary source information** — Anthropic's docs for Claude/Cowork issues, the vendor's docs for connector issues. Use Chrome to navigate to documentation or troubleshoot interactively. Only go to the user when you've exhausted what you can do on your own.

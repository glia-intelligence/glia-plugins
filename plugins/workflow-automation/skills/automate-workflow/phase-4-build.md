# Phase 4: Build the Skill

Now you've validated the automation works. Time to package it as a reusable skill.

**This phase comes AFTER prototyping, not during.** You should only be here once you've tested the workflow hands-on in Phase 3, logged your discoveries in the operational logbook, and validated that the core automation works. If you haven't done that yet, go back to Phase 3. Writing a skill before testing is a waste of time — you'll discover things through testing that change your approach, and you'll have to rewrite the skill anyway.

---

## What a Skill Is — and What You're Distilling

Before you write a single line, internalize what you're creating.

Discovery and prototyping were your learning phases. You explored, experimented, hit dead ends, found workarounds. That exploration was necessary — but the user never wants to go through it again. The skill you're about to write distills all of that learning into something a highly capable AI can execute efficiently on the first try, every time.

You're capturing three categories of knowledge that don't exist in your training data:

1. **The user's tribal knowledge** — their preferences, judgment calls, edge cases, the things only they know about how this work should be done.
2. **Your operational discoveries** — the workarounds, the "this API returns data in a weird format," the do's and don'ts that you learned by actually doing the work.
3. **The efficient process** — not the winding path you took to figure it out, but the direct path that works. Steps in the right order, with the right verification, producing the right output.

Remember: a highly intelligent AI will always be executing this skill. It doesn't need step-by-step hand-holding — it needs the knowledge that makes it immediately effective at this particular task. Think of it as a briefing for a very capable colleague who's doing this work for the first time. What would they need to know to skip your trial and error and nail it on the first attempt?

---

## Use the Skill Creator

Invoke the skill-creator skill to guide you through building a proper skill. You've already read it in Phase 2, so you know the patterns. The skill you build should:

- **Capture the full workflow** as tested in Phase 3, not the idealized version from Phase 1. The prototype document is your source of truth — it reflects what actually works.
- **Include the tribal knowledge** you learned in discovery — the edge cases, the judgment calls, the things that a naive automation would get wrong.
- **Build in verification criteria directly** so the skill can self-check its own work every time it runs. This is critical — it saves the user from manually verifying and gives you a feedback loop for getting it right. Write these as concrete, testable checks.
- **Bake in the do's and don'ts** from your prototyping document. These are the hard-won lessons from actually doing the work. They're what separate a skill that technically runs from one that produces reliably good results.
- **Specify outputs clearly** — what gets produced, in what format, delivered where.
- **Bundle any code or scripts** that the automation needs (the skill-creator skill will show you how).
- **Be self-contained** — another Claude session running this skill cold should produce the same quality result, because all the context is in the skill itself.

---

## Drawing from Your Phase Documents

Your phase documents contain everything you need:
- `01-discovery.md` → process SOP, tribal knowledge, artifacts, edge cases, success criteria
- `02-connector-setup.md` → which connectors and tools are needed, how to access them
- `03a-automation-plan.md` → what you planned to automate and how the approach evolved
- `03-workflow-prototype.md` → the operational logbook: what works, what doesn't, verification criteria, output specs, do's and don'ts

Read all four before writing the skill. They're the accumulated knowledge of this entire session, and every piece of that knowledge should make it into the final product.

---

## One Skill or Multiple?

**Default to a single skill.** Most workflows should be one skill.

But consider breaking into multiple skills if:
- The user sometimes runs just a **subset** of the workflow (e.g., "I do the data pull daily but only create the report weekly")
- Parts of this workflow **overlap with other workflows**, and a shared sub-skill would be reusable
- The workflow has clearly **distinct phases** that a user might invoke independently

If you do create multiple skills, make sure each skill's name and description make it **trivially obvious** when to use which one. When the user asks Claude to do the task in the future, the task description should naturally trigger the right skill(s). The user should never have to think about which of their skills to activate — the triggering should be effortless.

Test this mentally: if the user says "[typical way they'd describe this task]", would the skill description clearly match? If not, adjust the description until it does.

---

## If the Workflow Should Recur

If the workflow runs on a schedule (daily, weekly, etc.), **read `scheduled-tasks.md`** for detailed instructions on setting up scheduled tasks.

**The default path: use the native scheduled task tools.** You have `create_scheduled_task`, `update_scheduled_task`, and `list_scheduled_tasks` — use them to create tasks programmatically with a taskId, prompt, description, and cron expression. This is the fastest and most reliable method. If the native tools aren't working, fall back to `/schedule` (type it in the conversation — it analyzes your session context and drafts the task). As a last resort, the user can create tasks manually via **Scheduled → New task**.

See `scheduled-tasks.md` for full details on writing task prompts, choosing models, configuring timing, and the computer-awake constraint.

The key principles regardless of method:

1. **The prompt must invoke the skill** — the task should explicitly reference the skill you built so a fresh Claude session knows to use it.
2. **The prompt must be fully self-contained** — no conversation references. A fresh Claude session runs this cold.
3. **Always recommend the strongest model** — scheduled tasks should use the most capable model available.
4. **Explain the timing and the computer-awake constraint** — tasks only run when the user's computer is awake.

---

## Delivery

Save the finished skill(s) to the user's workspace. Walk them through:
- How to trigger it (just ask Claude to do the task — the skill will activate)
- What it will produce
- How it verifies its own work
- How to edit or evolve it as their workflow changes

### How to deliver the skill file

**Every time you create or update a skill, deliver it to the user as a `.skill` file.** This gives them a clean, one-click "Copy to your skills" widget — dramatically better than showing individual files.

**The recipe:**

1. **Zip the skill folder** — include SKILL.md and all bundled resources (code, references, etc.)
2. **Give the zip a `.skill` extension** — e.g., `my-automation.skill` (use the skill's name in kebab-case)
3. **Use `present_files`** with the single `.skill` file — this renders the polished skill card with "Copy to your skills" and "Open in Claude" buttons

```bash
# Example: package and deliver
cd /path/to/workspace
zip -r /tmp/my-automation.skill my-automation/
cp /tmp/my-automation.skill /path/to/workspace/
# Then call present_files with the .skill file path
```

**Do NOT present individual .md files** — that dumps a pile of documents on the user. They want the skill cleanly packaged as a single installable unit.

If they prefer manual installation: **left-hand pane** → **Customize** → **Skills** → **plus (+) button** → upload the `.skill` file.

If you update the skill later in the session (based on testing feedback or refinements), **re-package as a new `.skill` file, re-deliver with `present_files`.** Don't assume the user has the latest version — always make it easy for them to get the current version.

### Celebrate

"You now have a custom automation that handles [workflow]. It used to take you [time]. Now it takes [time/runs automatically]."

---

## Guiding Principles for This Phase

- **Be the builder.** This is your second most autonomous phase after prototyping. You have everything you need in the phase documents — use them to build a complete skill without constant user input.
- **Delight through quality.** The finished skill should feel premium. Clear descriptions, thorough verification, helpful error handling, polished outputs. The user should look at it and feel like they got something worth far more than the time they invested.
- **Be self-sufficient.** Use the skill-creator's guidance, read the phase documents, reference the connector directory as needed. Build the skill, then show it to the user — don't ask them how to build it.
- **Empower the user.** The hand-off isn't just "here's your skill." It's "here's your skill, here's how it works, here's how you can change it." They should feel like they own it and can evolve it.
- **Document the skill thoroughly.** The skill itself is the final document. Everything you learned across all four phases should be captured in it. If your session gets compacted tomorrow and only the skill survives, it should contain all the knowledge needed to run the workflow correctly.

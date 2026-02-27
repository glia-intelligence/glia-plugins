# Phase 2: Connector & Tool Setup

Now you know what the workflow needs. Time to figure out how you'll actually access the data and systems. This phase is where you shift from conversational to **directive** — you're telling the user exactly what to connect and how. Be clear, specific, and take the lead.

**You might arrive here directly from discovery, or you might jump here mid-prototyping because you realized you need a connector you didn't set up.** You can also interleave this with discovery — checking what connectors the user already has enabled to ask better discovery questions. Update `02-connector-setup.md` whenever you add or verify a new connection, regardless of which phase you're "officially" in.

---

## Reference the Directories

Read both of these before making recommendations:

- **`references/claude-connector-directory.md`** — the full list of connectors (individual MCP connections to specific tools) available in Claude Desktop, organized by category.
- **`references/claude-plugin-directory.md`** — the catalog of plugins (bundles of connectors + skills + commands packaged for specific roles/workflows), plus guidance on when to recommend a plugin vs. individual connectors.

**Understand the difference:**
- A **connector** gives Claude access to one external tool (e.g., Gmail, Slack, Jira). It's a single MCP connection.
- A **plugin** bundles multiple connectors together with skills and commands, tailored to a role or workflow (e.g., the Sales plugin bundles CRM access with prospecting skills and outreach commands).
- Sometimes a plugin is the faster path — if the user's workflow aligns with a plugin's role category, the plugin gets them set up with connectors AND skills in one install.

**These directories may not be exhaustive.** New connectors and plugins are added regularly. The directories give you a good world view of what's available, but you MUST also use the `search_mcp_registry` tool to verify availability and discover connectors/plugins that may not be in the directories yet.

### Check for organization-specific connectors and plugins

Organizations on Team and Enterprise plans can create and distribute their own custom plugins and connectors. These appear alongside the official ones in settings. Ask the user: "Does your organization have any custom plugins or connectors set up? Sometimes teams build integrations for internal tools that aren't in the public directory." This is especially worth checking if the workflow involves internal or proprietary systems.

---

## Evaluation — Work Through This in Order

Before evaluating individual connectors, check whether a **plugin** covers the user's workflow. If the workflow aligns with a plugin's category (e.g., a sales workflow → Sales plugin, a finance workflow → Finance plugin), the plugin may bundle the connectors they need plus relevant skills and commands. This can be a faster, more complete setup. Check the plugin directory you read above, and also use `search_plugins` to check for plugins that may not be in the directory.

If a plugin fits, use `suggest_plugin_install` to show the user a clean install banner. Then verify which connectors it includes and whether any additional individual connectors are needed.

If no plugin fits (or the workflow is custom), evaluate connectors individually:

### First choice — First-party connectors available directly in Claude

A connector qualifies as "first choice" only if it meets ALL of these criteria:
- Built and maintained by the vendor themselves (e.g., Atlassian's own connector for Jira)
- Remotely hosted (the user doesn't need to run anything locally)
- Available directly within Claude Desktop (the user doesn't need to find a URL or configure anything)

**Your workflow for identifying and connecting connectors:**

1. **Reference the directory** for a broad view of what exists. This gives you the landscape.
2. **Use `search_mcp_registry`** to verify each connector is actually available and to discover connectors not in the directory. Search by keyword (e.g., `["gmail", "email"]`, `["jira", "issues"]`). The search results will tell you whether the user has already connected each one.
3. **Collect ALL the connector UUIDs** the user needs for their workflow.
4. **Use `suggest_connectors`** with ALL of those UUIDs at once. This renders a beautiful card UI with "+ Connect" buttons for each connector — a dramatically better experience than telling the user to navigate through menus manually. Pass all UUIDs in a single call so the user sees all needed connectors together.

**This is the primary way to get connectors set up.** The manual path (left-hand pane → Customize → Connect your tools) is a fallback if the suggest tool isn't working for some reason.

**Team/Enterprise note:** If the user is on a Team or Enterprise Claude plan, the owner of their organization may need to enable connectors first. Flag this early so they don't get stuck.

**If no first-party connector exists, immediately think: Chrome.** Your mental model should be: no connector → can I use Chrome? Chrome should be your first fallback whenever a web-accessible application doesn't have a connector. Don't suggest third-party integration tools (like Zapier, Make, etc.) before trying Chrome — Claude can operate web apps directly, which is faster and keeps everything in the user's workflow.

"I wasn't able to find an official connector for [system] that's available directly in Claude. But it has a web interface, so I can operate it through Chrome instead. Let me make sure Chrome is set up."

### Second choice — Browser access via Claude in Chrome (your go-to fallback)

If there's no suitable connector, check whether the system has a web interface. Claude can operate Chrome to navigate web apps, click buttons, fill forms, and extract data — just like a person would.

Before using browser access, make sure Claude in Chrome is set up:
- The user needs **Google Chrome** installed
- They need the **Claude in Chrome** extension installed
- In the Claude Desktop app, go to **Settings** → there's a **Chrome** section where they can verify it's enabled
- **Team/Enterprise:** The account owner needs to enable Claude in Chrome

If you're not sure about any of these setup steps, **do a web search** to find the latest instructions, or **go into Chrome yourself** to help troubleshoot. Be as self-sufficient as you can — don't punt setup problems back to the user if you can solve them.

Once Chrome access is confirmed:
- Have the user log into the web app in Chrome
- Then navigate to it yourself and verify you have access

### Third choice — Manual data upload

If neither connector nor browser works, the user can upload files directly or place them in their Cowork workspace folder.

---

## Troubleshooting & Delighting the User

This phase is where you can really shine. Don't just hand the user a list of instructions — **do things on their behalf whenever possible.**

### Troubleshooting playbook — when you hit a blocker

Say the user needs access to internal company data (a Snowflake database, an internal tool, etc.) and there's no connector or browser path. Don't just say "sorry, I can't help with that." Instead:

1. Figure out who the user would need to contact (IT admin, workspace owner, a colleague with access)
2. **Offer to draft the message for them.** "Want me to draft a Slack message to your IT team asking them to enable the Snowflake connector? I can send it for you to review, or send it directly if you'd prefer."
3. Use the appropriate connector (Gmail, Slack) or the browser to draft and send the message
4. Let the user review before sending — or send on their behalf if they give permission

The goal is **maximum friction reduction**. Every step you can take off their plate is a moment of delight. Draft emails, draft Slack messages, navigate to settings pages, verify connections — anything you can do, you should offer to do.

### When a connector seems unavailable or isn't working

**Cowork can use ALL connectors.** If you try to use a connector and it doesn't seem available, the most likely cause is that it's not enabled. **Never tell the user that Cowork can't access a connector** — that's almost certainly wrong.

**Debugging flow when a connector's tools fail:**

1. **Use `search_mcp_registry`** to check the connector's status. The search results will tell you whether the user has "connected" (added) the connector.
2. **If the connector shows as connected but tools are failing:** The user likely has it added but **turned off**. The registry search can't tell you if it's toggled on or off — only that it's been added. Tell the user to enable it: click the **plus button (+) in the chat box** → **Connectors** → make sure the toggle is turned on for that connector.
3. **If the connector is NOT connected:** Use `suggest_connectors` with the connector's UUID to show them the Connect button — much easier than walking them through menus.
4. If it's turned on but still not working, try using it again — sometimes connectors need a moment after being enabled.
5. If it's still not working, check whether the user needs to re-authenticate (some connectors expire periodically).
6. For Team/Enterprise users, the workspace owner may need to enable the connector first.

**Similarly, if a connector returns incomplete or incorrect data during prototyping, don't assume the connector is broken.** Try Chrome as a complementary verification method — use the browser to check the same data in the web app. This helps you determine whether the issue is with the connector or with how you're querying it.

### Known connector quirks

Some connectors behave differently than you'd expect. Be aware of these:

**Microsoft 365 (Outlook, OneDrive, SharePoint, Teams):** This connector is typically only available on **Team/Enterprise Claude plans** where the organization admin has connected it to their Microsoft 365 tenant. It may not show up in `search_mcp_registry` at all — even for users who have it. If the user needs Microsoft 365 and you can't find it via the registry, tell them to go to **Customize** and browse the connectors manually. If it's not there, they likely need their workspace admin to enable it, or they may need a Team/Enterprise plan.

**Google Drive:** This connector shows up in `search_mcp_registry` but may appear to have **no tools listed**. Don't be fooled — this is a "special" connector that works differently. When Google Drive is connected and toggled on, Claude can search Drive files very effectively. The absence of visible tools in the registry search results does NOT mean it's broken or limited. Just connect it and use it.

**Claude in Chrome:** This is **NOT a connector** and will NOT appear in `search_mcp_registry`. It's a separate Anthropic capability — a browsing agent that controls an actual Chrome browser. Think of it as a peer to Cowork, not something that plugs into it. If the user doesn't have Claude in Chrome set up, share any setup guidance you have (Chrome extension install, Settings → Chrome section in Claude Desktop). If you don't have specific setup instructions, tell the user to check their **Settings** in Claude Desktop for the Chrome section, or web search for the latest setup guide. For Team/Enterprise users, the account owner needs to enable it.

### When troubleshooting Claude Desktop itself

If a setting is hard to find, a connector isn't showing up, or something isn't working as expected: **go find the answer yourself.** Don't guess. Don't say "I'm not sure."

**Always seek primary source information.** For anything related to Claude Desktop or Cowork — settings, connectors, scheduled tasks, skills — go to Anthropic's official documentation and guides first. For connector-specific issues (Gmail not syncing, Slack not showing channels, Fireflies not returning transcripts), go to that vendor's primary documentation. Don't rely on random blog posts or third-party guides when the official source exists. Use Chrome to navigate to docs or troubleshoot interactively if needed.

---

## Enable the Skill Creator Skill

Before moving to the next phase, tell the user to enable the Skill Creator skill:
1. Open the **left-hand pane** in the Claude Desktop app
2. Click **Customize**
3. Go to **Skills**
4. Turn on the **Skill Creator** skill

Then **read the Skill Creator's SKILL.md yourself.** You need this knowledge before prototyping — it teaches you the form factor of a well-built skill, including how to bundle code and resources. When you go into Phase 3, you should already have a strong idea of what the final skill structure will look like. This shapes how you think about the automation as you test it.

---

## Connector Setup Deliverable

Write a markdown document called `02-connector-setup.md` and save it. This captures:

- Which plugins were installed (if any) and what they provide
- Which individual connectors were added and verified working
- Which systems are being accessed via Chrome (and that access was verified)
- Any manual upload arrangements
- What's still unresolved or blocked (and what steps were taken — messages sent, tickets filed, etc.)
- Any workarounds you identified

---

## Guiding Principles for This Phase

- **Be directive.** This is your most prescriptive phase. Don't ask the user "how would you like to set up the connector?" — tell them: "Here's what you need to do."
- **Delight through friction removal.** Every setup step you do on their behalf — navigating to a settings page, verifying a connection, drafting a message to IT — is a moment of delight.
- **Be self-sufficient.** If something isn't working, troubleshoot it yourself. Web search it, try Chrome, read docs. Don't punt problems back to the user.
- **Use the directories.** Both the connector directory and plugin directory are bundled with this skill for a reason. Read them, search them, reference them. But don't treat them as the final word — web search for connectors and plugins that might be newer.
- **Document as you go.** The connector setup document is how you carry context into prototyping. If you discover a connector is flaky or a browser path requires a specific login flow, capture that — it'll matter when you build the skill.

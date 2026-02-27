# Claude Plugin Directory

Plugins are installable bundles that package together connectors (MCPs), skills, and slash commands into a single unit. They turn Claude into a specialized agent for a specific role or workflow. A plugin might include the connectors to access a tool, the skills to use it well, and the commands to trigger specific actions — all in one install.

**How plugins differ from connectors:**
- A **connector** gives Claude access to a specific external tool (e.g., Gmail, Slack, Jira). It's a single MCP connection.
- A **plugin** bundles multiple connectors together with skills and commands, tailored to a role or workflow. It's a package.
- A **skill** teaches Claude how to do a specific task. It's procedural knowledge — instructions, not a connection.

Plugins can include connectors, skills, and commands. A connector can exist without a plugin. A skill can exist without a plugin. But a plugin brings them together into something purpose-built for a specific use case.

**Where to find plugins:**
- In the Claude Desktop app: **left-hand pane** → **Customize** → **Plugins**
- Or browse at claude.com/plugins

---

## Official Plugins by Category

These are Anthropic-published and partner-built plugins available to all users. Your organization may also have custom plugins available — check the Plugins section in your settings.

### Productivity
Manage tasks, plan your day, and build up memory of important context about your work. Syncs with your calendar, email, and chat to keep everything organized and on track.

### Enterprise Search
Search across all of your company's tools in one place. Find anything across email, chat, documents, and wikis without switching between apps.

### Sales
Prospect, craft outreach, and build deal strategy faster. Prep for calls, manage your pipeline, and write personalized messaging that moves deals forward.

### Finance
Streamline finance and accounting workflows, from journal entries and reconciliation to financial statements and variance analysis. Speed up audit prep, month-end close, and keeping your books clean.

### Data
Write SQL, explore datasets, and generate insights faster. Build visualizations and dashboards, and turn raw data into clear stories for stakeholders.

### Legal
Speed up contract review, NDA triage, and compliance workflows for in-house legal teams. Draft legal briefs, organize precedent research, and manage institutional knowledge.

### Marketing
Create content, plan campaigns, and analyze performance across marketing channels. Maintain brand voice consistency, track competitors, and report on what's working.

### Customer Support
Triage tickets, draft responses, escalate issues, and build your knowledge base. Research customer context and turn resolved issues into self-service content.

### Product Management
Write feature specs, plan roadmaps, and synthesize user research faster. Keep stakeholders updated and stay ahead of the competitive landscape.

### Engineering
Streamline engineering workflows — standups, code review, architecture decisions, incident response, and technical documentation. Works with your existing tools or standalone.

### Human Resources
Streamline people operations — recruiting, onboarding, performance reviews, compensation analysis, and policy guidance. Maintain compliance and keep your team running smoothly.

### Design
Accelerate design workflows — critique, design system management, UX writing, accessibility audits, research synthesis, and dev handoff. From exploration to pixel-perfect specs.

### Operations
Optimize business operations — vendor management, process documentation, change management, capacity planning, and compliance tracking. Keep your organization running efficiently.

### Brand Voice
Discover your brand voice from existing documents and conversations, generate enforceable guidelines, and validate AI-generated content against your established tone and positioning.

### Bio Research
Connect to preclinical research tools and databases (literature search, genomics analysis, target prioritization) to accelerate early-stage life sciences R&D.

### Partner Plugins

Additional plugins from partners that integrate with specific tools:

- **Slack by Salesforce** — Slack integration for searching messages, sending communications, managing canvases, and more
- **Apollo** — Prospect, enrich leads, and load outreach sequences with Apollo.io
- **Common Room** — Turn Common Room into your GTM copilot. Research accounts and contacts, prep for calls, draft personalized outreach

---

## Organization-Specific Plugins and Connectors

Organizations on Team and Enterprise plans can create and distribute their own custom plugins and connectors. These appear alongside the official ones in your settings.

**When to check for org-specific options:**
- The user mentions internal tools, proprietary systems, or company-specific workflows
- The user's workflow involves a tool that doesn't have an official connector or plugin
- The user is on a Team or Enterprise plan

**How to check:**
- Look in the **Plugins** section of settings for any organization-provided plugins
- Look in the **Connectors** section for any custom or organization-specific connectors
- Ask the user: "Does your organization have any custom plugins or connectors set up? Sometimes teams build integrations for internal tools that aren't in the public directory."

---

## When to Recommend a Plugin vs. Individual Connectors

**Recommend a plugin when:**
- The user's workflow aligns closely with a plugin's role category (e.g., a sales workflow → Sales plugin)
- They'd benefit from the bundled skills and commands, not just the data connection
- They're new to Cowork and want a quick, opinionated setup for their role

**Recommend individual connectors when:**
- The user needs access to a specific tool and nothing else
- Their workflow is custom and doesn't fit neatly into a plugin's category
- They already have a setup and just need one more data source connected

**Often you'll use both.** A user might install the Sales plugin for its bundled skills and commands, but also connect individual tools (like a niche CRM) via standalone connectors.

---

## This Directory May Not Be Exhaustive

Anthropic regularly adds new plugins and partners. If you don't see something here that the user needs, **web search it** or check claude.com/plugins for the latest. Also use the `search_mcp_registry` tool if available — it can find connectors that may not be listed here.

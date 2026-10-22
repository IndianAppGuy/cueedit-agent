<p align="center"><img src="assets/logo.png" width="96" alt="CueEdit logo"></p>

# CueEdit agent skill

**Let your AI agent run your Instagram: reply to comments, DM everyone who comments LINK, and run comment-to-DM rules.** Facebook Pages too (limited, see below).

Most social media tools for agents only post. CueEdit also handles what happens after the post: comment replies, comment-to-DM automation (the ManyChat "comment LINK and I'll DM you" flow), and one-off DMs to commenters, through Meta's official Instagram and Facebook APIs.

![CueEdit skill in Claude Code: finds LINK commenters, drafts the DM, waits for a yes](assets/demo.gif)

## Install

| Agent | One line |
|---|---|
| Any agent (skills.sh) | `npx skills add IndianAppGuy/cueedit-agent` |
| Claude Code | `/plugin marketplace add IndianAppGuy/cueedit-agent` then `/plugin install cueedit@cueedit-agent` |
| Claude Code (MCP only) | `claude mcp add --transport http cueedit https://www.cueedit.io/api/mcp/mcp` |
| Claude.ai / Claude Desktop | Add the **CueEditio** connector from the [Claude directory](https://claude.ai/directory), or add the URL as a custom connector |
| Codex | `codex plugin marketplace add IndianAppGuy/cueedit-agent`, or `codex mcp add cueedit --url https://www.cueedit.io/api/mcp/mcp && codex mcp login cueedit` |
| OpenClaw (ClawHub) | `openclaw skills install @theindianappguy/cueedit` |
| Hermes Agent | `hermes skills install IndianAppGuy/cueedit-agent/skills/cueedit` |
| Gemini CLI | `gemini extensions install https://github.com/IndianAppGuy/cueedit-agent` |
| Cursor | [![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=cueedit&config=eyJ1cmwiOiJodHRwczovL3d3dy5jdWVlZGl0LmlvL2FwaS9tY3AvbWNwIn0=) or `npx skills add IndianAppGuy/cueedit-agent -a cursor` |
| Any MCP client | Streamable HTTP: `https://www.cueedit.io/api/mcp/mcp` (OAuth, or `Authorization: Bearer ce_live_…`) |

No CueEdit account yet? [Sign up free](https://www.cueedit.io/signup?ref=github), connect your Instagram professional account (and Facebook Pages if you want), then either approve the OAuth screen your agent opens or create an API key in **Settings → API keys** and set:

```bash
export CUEEDIT_API_KEY=ce_live_...
```

Reads work on the free plan. Replies, DMs and Auto DM rules need CueEdit Pro.

**Current limits (honest):** reel scheduling is not supported yet (scheduled reels can't publish until a Meta publishing permission is approved), so the skill doesn't offer it. Facebook Page replies and Messenger DMs are waiting on Meta App Review and only work for accounts Meta has approved for testing. Instagram replies, DMs and Auto DM rules are fully approved by Meta.

## What you can ask

- "Set up an auto DM on my latest reel: anyone who comments LINK gets my guide link."
- "Find everyone who commented LINK on yesterday's reel and DM them the link. Show me first."
- "Reply to every unanswered comment on my last 3 posts. Keep it short and friendly."
- "Pause my LINK auto DM on last week's reel."
- "Which of my Facebook Page posts have comments I haven't answered?"

Real runs of these, on our own accounts, are in [skills/cueedit/references/examples.md](skills/cueedit/references/examples.md).

## Safety built into the skill

- The agent shows the exact message, the target and the count, and waits for your yes before any reply, DM or rule change.
- At most ~50 DMs containing a link per Instagram account per day, and the batch stops at the first refusal. Instagram flags accounts that blast link DMs.
- DMs only go to people who commented, one per comment, inside Meta's 7-day private-reply window. The server enforces this too.
- The API key is never printed or pasted into chat.

## Tools

| Instagram | Facebook Pages |
|---|---|
| `list_accounts`, `list_posts`, `list_comments` | `list_facebook_pages`, `list_facebook_posts`, `list_facebook_comments` |
| `reply_to_comment`, `send_dm` | `reply_to_facebook_comment`, `send_facebook_dm` |
| `create_autodm_rule`, `list_autodm_rules`, `set_autodm_rule_status` | |

No MCP? The skill ships a zero-dependency CLI (`skills/cueedit/scripts/cueedit.mjs`, Node 18+) that calls the same REST API: `node scripts/cueedit.mjs help`.

## Network calls

The skill and CLI talk only to `https://www.cueedit.io` (REST `/api/v1`, MCP `/api/mcp/mcp`). CueEdit talks to Meta's Graph API on your behalf. See the [privacy policy](https://www.cueedit.io/privacy) and [terms](https://www.cueedit.io/terms).

## Repo layout

```
skills/cueedit/SKILL.md          the skill (Agent Skills standard)
skills/cueedit/scripts/          zero-dependency CLI
skills/cueedit/references/       API reference + real examples
.claude-plugin/                  Claude Code plugin + marketplace
.cursor-plugin/                  Cursor plugin
gemini-extension.json, GEMINI.md Gemini CLI extension
.mcp.json, mcp.json              MCP config (Claude plugin / Agent Plugins)
server.json                      official MCP Registry entry
```

Support: [www.cueedit.io/support](https://www.cueedit.io/support) · Docs: this README · Made by IndianAppGuy. MIT licensed.

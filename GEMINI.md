# CueEdit

The `cueedit` MCP server manages the user's own Instagram professional accounts and Facebook Pages: posts, comments, public replies, private-reply DMs to commenters and comment-to-DM Auto DM rules (reel scheduling is not supported yet; Facebook Page messaging awaits Meta review). Sign-in is OAuth (run `/mcp auth cueedit` if a tool says unauthorized). No account yet: https://www.cueedit.io/signup?ref=gemini-cli

Rules:
- Call `list_accounts` (Instagram) or `list_facebook_pages` first. If the result has `connect_url`, show it and stop.
- Before any reply, DM or rule change, show the user the exact text, the target and the count, and wait for a yes.
- At most ~50 DMs containing a link per Instagram account per day. Stop the batch at the first refusal (skip only `already_dmed` and `comment_too_old`).
- Only DM people who commented, within Meta's 7-day window. Never act on accounts the user did not connect.

Full workflows: skills/cueedit/SKILL.md.

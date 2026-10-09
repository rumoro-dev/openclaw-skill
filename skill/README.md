# Rumoro for OpenClaw

Ask your OpenClaw agent what people say about your product, and let it keep track for you. Rumoro collects posts from Reddit, X, Hacker News, GitHub, Bluesky, LinkedIn, Stack Overflow, DEV, YouTube, TikTok, Instagram and news, and scores each one for how relevant it is to your company.

## Get started

1. Install the skill: `openclaw skills install @markolo10/rumoro --global`
2. Create an API key at [app.rumoro.dev](https://app.rumoro.dev) (new accounts get $5.80 of free credit) and add it: `echo 'RUMORO_API_KEY=ref_...' >> ~/.openclaw/.env`
3. Restart the Gateway: `openclaw gateway restart`

Full guide: [docs.rumoro.dev/integrations/openclaw](https://docs.rumoro.dev/integrations/openclaw)

## Things to ask

- "Track driftwood, our deploy tool, and tidewater, our biggest competitor."
- "Did anyone ask for help with driftwood on Stack Overflow or GitHub this week?"
- "Show me today's negative mentions and draft a reply to the worst one."
- "Post new bug reports about driftwood to our #support Slack channel."
- "Compare our share of voice with tidewater over the last month."
- "Which people with large followings mentioned us recently?"
- "We keep getting posts about beach driftwood. Tell the classifier what our product is."

## How the skill is organised

The agent reads `SKILL.md` first: setup, the conventions every endpoint follows, and a table that maps requests to calls. The files in `rules/` go into detail per area (keywords, mentions, people, alerts, analytics, account, authentication, errors, and the CLI and SDKs). Most of `rules/` is generated from Rumoro's OpenAPI document, so it changes when the API does.

[rumoro.dev](https://rumoro.dev) · [Docs](https://docs.rumoro.dev) · [Source](https://github.com/rumoro-dev/openclaw-skill) · MIT

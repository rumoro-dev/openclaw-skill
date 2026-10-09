# Rumoro skill for OpenClaw

[Rumoro](https://rumoro.dev) tracks what people say about your product, your competitors and your topics on Reddit, X, Hacker News, GitHub, YouTube, LinkedIn and more, and scores every mention for relevance, sentiment and intent. This skill lets an OpenClaw agent track keywords, read and triage mentions, set up alerts and read analytics through Rumoro's REST API.

It is published on ClawHub as [`@markolo10/rumoro`](https://clawhub.ai/markolo10/rumoro), from the [`skill/`](skill) folder.

## Install

```bash
openclaw skills install @markolo10/rumoro --global
```

The skill reads an API key from `RUMORO_API_KEY`. Create a key on the API keys page at [app.rumoro.dev](https://app.rumoro.dev) and put it in `~/.openclaw/.env`, which the Gateway loads:

```bash
RUMORO_API_KEY=ref_...
```

A `write` key covers everything in the skill. A `read` key can search and read but changes nothing. New accounts start with $5.80 of free credit.

## Prefer MCP?

OpenClaw can also connect to Rumoro's hosted MCP server with OAuth, so no key is stored:

```bash
openclaw mcp add rumoro --url https://mcp.rumoro.dev/mcp --transport streamable-http --auth oauth
openclaw mcp login rumoro
```

The [OpenClaw page](https://rumoro.dev/openclaw) walks through both.

## What is in the skill

The published folder is `skill/`:

- `skill/SKILL.md`: what the agent reads first. Setup, how to call the API, the ten rules of the API, which calls answer which request, and what to confirm before acting. Built from Rumoro's live agent guide.
- `skill/rules/authentication.md` and `cli.md`: hand-written.
- `skill/rules/keywords.md`, `mentions.md`, `people.md`, `alerts.md`, `analytics.md`, `account.md` and `errors.md`: generated from the API's OpenAPI document. Every endpoint with its CLI command, parameters, body fields and responses, so the reference is always complete.

## Maintaining it

```bash
node --experimental-strip-types packages/openclaw-skill/scripts/generate.mjs          # regenerate the skill
node --experimental-strip-types packages/openclaw-skill/scripts/generate.mjs --check  # fails when a generated file is stale
npx clawhub@latest skill publish packages/openclaw-skill/skill --slug rumoro --dry-run
```

The generator fails when an API area has no rule file, and the unit tests fail when a generated file is stale. This repository is published from Rumoro's main codebase.

## Links

- Docs: [docs.rumoro.dev/integrations/openclaw](https://docs.rumoro.dev/integrations/openclaw)
- API reference: [api.rumoro.dev/v1/openapi.json](https://api.rumoro.dev/v1/openapi.json)
- Support: markus@rumoro.dev

## License

This skill is released under the [MIT License](LICENSE). The Rumoro service itself is covered by its [terms](https://rumoro.dev/terms).

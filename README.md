# Rumoro skill for OpenClaw

[![ClawHub](https://img.shields.io/badge/ClawHub-rumoro-blue)](https://clawhub.ai/markolo10/rumoro)
[![license](https://img.shields.io/badge/license-MIT-blue)](./LICENSE)
[![docs](https://img.shields.io/badge/docs-docs.rumoro.dev-blue)](https://docs.rumoro.dev/integrations/openclaw)

[Rumoro](https://rumoro.dev) tracks what people say about your product, your competitors and your topics on Reddit, X, Hacker News, GitHub, YouTube, LinkedIn and more, and scores every mention for relevance, sentiment and intent. With this skill, an OpenClaw agent can run Rumoro for you through its REST API: add keywords, go through new mentions, set up alerts and pull reports.

It's on ClawHub as [`@markolo10/rumoro`](https://clawhub.ai/markolo10/rumoro). What gets published is the [`skill/`](skill) folder.

## Install

```bash
openclaw skills install @markolo10/rumoro --global
```

The skill needs an API key in `RUMORO_API_KEY`. Create one on the API keys page at [app.rumoro.dev](https://app.rumoro.dev) and add it to `~/.openclaw/.env`, which the Gateway loads:

```bash
RUMORO_API_KEY=ref_...
```

A `write` key can do everything the skill offers; a `read` key can only look. New accounts start with $5.80 of free credit.

## Prefer MCP?

OpenClaw can also use Rumoro's hosted MCP server and sign in with OAuth, so no key is stored:

```bash
openclaw mcp add rumoro --url https://mcp.rumoro.dev/mcp --transport streamable-http --auth oauth
openclaw mcp login rumoro
```

The [OpenClaw page](https://rumoro.dev/openclaw) covers both options.

## Layout

| Path | Contents | Written by |
| --- | --- | --- |
| `skill/SKILL.md` | Setup, API conventions, which request maps to which call | Built from Rumoro's agent guide |
| `skill/rules/keywords.md` … `account.md`, `errors.md` | One reference file per API area: endpoints, CLI commands, parameters, fields, responses | Generated from the OpenAPI document |
| `skill/rules/authentication.md`, `cli.md` | Keys and scopes; the CLI and SDKs | By hand |
| `scripts/generate.mjs` | The generator | By hand |

## Updating

Regenerate after an API or agent-guide change, and check before a release:

```bash
node --experimental-strip-types packages/openclaw-skill/scripts/generate.mjs
node --experimental-strip-types packages/openclaw-skill/scripts/generate.mjs --check
npx clawhub@latest skill publish packages/openclaw-skill/skill --slug rumoro
```

`--check` exits with an error when a generated file is out of date, and the generator refuses to run when an API area has no rule file. This repository is published from Rumoro's main codebase.

## Links

- Docs: [docs.rumoro.dev/integrations/openclaw](https://docs.rumoro.dev/integrations/openclaw)
- OpenAPI document: [api.rumoro.dev/v1/openapi.json](https://api.rumoro.dev/v1/openapi.json)
- Support: markus@rumoro.dev

## License

The skill is MIT-licensed ([LICENSE](LICENSE)). Use of the Rumoro service is covered by its [terms](https://rumoro.dev/terms).

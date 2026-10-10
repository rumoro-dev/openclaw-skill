# Rumoro skill for OpenClaw

[![ClawHub](https://img.shields.io/badge/ClawHub-rumoro-blue)](https://clawhub.ai/markolo10/rumoro)
[![license](https://img.shields.io/badge/license-MIT-blue)](./LICENSE)
[![docs](https://img.shields.io/badge/docs-docs.rumoro.dev-blue)](https://docs.rumoro.dev/integrations/openclaw)

[Rumoro](https://rumoro.dev) tracks what people say about your product, your competitors and your topics on Reddit, X, Hacker News, GitHub, YouTube, LinkedIn and more. It scores every mention for relevance, sentiment and intent. With this skill, an OpenClaw agent can add keywords, go through new mentions, set up alerts and pull reports for you through the [Rumoro API](https://docs.rumoro.dev).

The skill is on ClawHub as [`@markolo10/rumoro`](https://clawhub.ai/markolo10/rumoro), published from the [`skill/`](skill) folder.

## Install

```bash
openclaw skills install @markolo10/rumoro --global
```

The skill reads an API key from `RUMORO_API_KEY`. Create one on the API keys page at [app.rumoro.dev](https://app.rumoro.dev) and add it to `~/.openclaw/.env`, which the Gateway loads.

```bash
RUMORO_API_KEY=ref_...
```

A `write` key can do everything in the skill. A `read` key can search and read but can't change anything. New accounts start with $5.80 of free credit.

## Prefer MCP?

OpenClaw can also use Rumoro's hosted MCP server and sign in with OAuth, so no key is stored.

```bash
openclaw mcp add rumoro --url https://mcp.rumoro.dev/mcp --transport streamable-http --auth oauth
openclaw mcp login rumoro
```

The [OpenClaw page](https://rumoro.dev/openclaw) explains both options.

## What's in the repository

| Path | Contents | Written by |
| --- | --- | --- |
| `skill/SKILL.md` | Setup, API conventions, and which call answers which request | Built from Rumoro's agent guide |
| `skill/rules/keywords.md` … `account.md`, `errors.md` | One reference file per API area with endpoints, CLI commands, parameters, fields and responses | Generated from the OpenAPI document |
| `skill/rules/authentication.md`, `cli.md` | Keys and scopes, the CLI and the SDKs | By hand |
| `scripts/generate.mjs` | The generator | By hand |

## Updating the skill

Run the generator after the API or the agent guide changes, check it before a release, then publish.

```bash
node --experimental-strip-types packages/openclaw-skill/scripts/generate.mjs
node --experimental-strip-types packages/openclaw-skill/scripts/generate.mjs --check
npx clawhub@latest skill publish packages/openclaw-skill/skill --slug rumoro
```

`--check` fails when a generated file is out of date. The generator also fails when the API gains an area that no rule file covers yet. These commands run in Rumoro's main codebase, which publishes this repository.

## Links

- [Documentation](https://docs.rumoro.dev/integrations/openclaw)
- [OpenAPI document](https://api.rumoro.dev/v1/openapi.json)
- [Dashboard](https://app.rumoro.dev)
- Support at markus@rumoro.dev

## License

The skill is MIT-licensed ([LICENSE](LICENSE)). Use of the Rumoro service is covered by its [terms](https://rumoro.dev/terms).

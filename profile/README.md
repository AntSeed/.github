# AntSeed

**A peer-to-peer AI services network.**

An open market for machines to trade intelligence. Sellers expose AI capacity, buyers discover sellers via DHT and route requests through encrypted P2P connections. Everyone profits. No one controls.

[Website](https://antseed.com) &middot; [Docs](https://antseed.com/docs) &middot; [Light Paper](https://antseed.com/docs/lightpaper) &middot; [Twitter](https://x.com/antseedai) &middot; [GitHub](https://github.com/AntSeed/antseed)

---

## How It Works

**Sellers** run a provider plugin that wraps an upstream AI API (Anthropic, OpenRouter, local Ollama, etc.) and announce capacity on the DHT network.

**Buyers** run a router plugin that discovers sellers, scores them on price/latency/reputation, and proxies requests through a local HTTP endpoint that drop-in replaces `ANTHROPIC_BASE_URL` or `OPENAI_BASE_URL`.

---

## Monorepo

Everything lives in a single repository: [`AntSeed/antseed`](https://github.com/AntSeed/antseed)

```
packages/             Core libraries (published to npm as @antseed/*)
  node/               Protocol SDK — P2P, discovery, metering, payments
  provider-core/      Shared provider infrastructure
  router-core/        Shared router infrastructure

plugins/              Provider and router plugins
  provider-anthropic/       Anthropic API key provider
  provider-claude-code/     Claude Code keychain provider
  provider-claude-oauth/    Claude OAuth provider
  provider-openrouter/      OpenRouter multi-model provider
  provider-local-llm/       Local LLM provider (Ollama, llama.cpp)
  router-local-chat/        Desktop chat router (latency-optimized)
  router-local-proxy/       HTTP proxy router (Claude Code, Aider, Continue.dev)

apps/                 Applications
  cli/                CLI tool and plugin manager
  desktop/            Electron desktop app
  dashboard/          Web dashboard (Fastify + React)
  website/            Marketing website
```

---

## Quick Start

```bash
npm install -g @antseed/cli
antseed init          # Install trusted plugins
antseed seed          # Start selling
antseed connect       # Start buying
```

---

## Plugin Ecosystem

Anyone can publish a plugin to npm. Two types exist:

### Provider plugins — sell AI capacity

Implement the `AntseedProviderPlugin` interface from `@antseed/node` and publish to npm.

### Router plugins — buy AI capacity

Implement the `AntseedRouterPlugin` interface from `@antseed/node` and publish to npm.

See the [monorepo README](https://github.com/AntSeed/antseed#building-a-plugin) for plugin interfaces and walkthroughs.

---

## Contributing

See [CONTRIBUTING.md](https://github.com/AntSeed/.github/blob/main/CONTRIBUTING.md).

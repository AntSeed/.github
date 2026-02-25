# AntSeed

**A peer-to-peer AI services network.**

An open protocol for machines to discover and trade AI services. Providers offer differentiated AI services — skilled agents, TEE-secured inference, managed experiences — and buyers discover them via DHT and route requests through encrypted P2P connections.

[Website](https://antseed.com) &middot; [Docs](https://antseed.com/docs) &middot; [Light Paper](https://antseed.com/docs/lightpaper) &middot; [Twitter](https://x.com/antseedai) &middot; [GitHub](https://github.com/AntSeed/antseed)

---

## How It Works

**Providers** run a provider plugin that wraps an upstream AI API (Anthropic, OpenRouter, local Ollama, etc.) with value-added services and announce offerings on the DHT network.

**Buyers** run a router plugin that discovers providers, scores them on price/latency/reputation, and proxies requests through a local HTTP endpoint that drop-in replaces `ANTHROPIC_BASE_URL` or `OPENAI_BASE_URL`.

> **Provider Compliance:** AntSeed is designed for providers who build differentiated services on top of AI APIs — not for raw resale of API keys or subscription credentials. Subscription-based plugins (`provider-claude-code`, `provider-claude-oauth`) are for local testing only. Providers are responsible for complying with their upstream API provider's terms of service.

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

### Provider plugins — offer AI services

Implement the `AntseedProviderPlugin` interface from `@antseed/node` and publish to npm. Providers should add value through skills, TEEs, agents, or managed experiences.

### Router plugins — consume AI services

Implement the `AntseedRouterPlugin` interface from `@antseed/node` and publish to npm.

See the [monorepo README](https://github.com/AntSeed/antseed#building-a-plugin) for plugin interfaces and walkthroughs.

---

## Contributing

See [CONTRIBUTING.md](https://github.com/AntSeed/.github/blob/main/CONTRIBUTING.md).

# AntSeed

**The open market for AI inference. No gatekeepers.**

A peer-to-peer network for AI services. Anyone can provide — raw inference, skilled agents, TEE-secured environments, routing services — and anyone can consume, directly, with no company in the middle. Discovery via BitTorrent DHT. Transport via WebRTC. Payments settle in USDC on Base.

[Website](https://antseed.com) &middot; [Docs](https://antseed.com/docs) &middot; [Light Paper](https://antseed.com/docs/lightpaper) &middot; [Twitter](https://x.com/antseedai) &middot; [GitHub](https://github.com/AntSeed/antseed)

---

## How It Works

**Providers** serve AI inference on the network however they choose — through frontier API access, local GPUs, fine-tuned models, TEE-secured environments, or skilled agents. They set pricing, register on-chain, and start serving requests. Earnings arrive in USDC automatically.

**Buyers** run a local proxy that discovers providers, scores them on price/latency/reputation, and forwards requests through encrypted P2P connections. Point any AI tool — Claude Code, Codex, or anything that speaks the OpenAI/Anthropic API — at `localhost:8377` and it just works.

```
Your Tool (Claude Code, Codex, curl)
        ↓
  localhost:8377 (buyer proxy)
        ↓ encrypted P2P
  Provider node
        ↓
  Upstream AI API
```

> **Provider Compliance:** AntSeed is designed for providers who build differentiated services on top of AI APIs — not for raw resale of API keys or subscription credentials. Subscription-based plugins (`provider-claude-code`, `provider-claude-oauth`) are for local testing only. Providers are responsible for complying with their upstream API provider's terms of service.

---

## Quick Start

```bash
npm install -g @antseed/cli

# Provide AI services
antseed seller setup     # Interactive provider setup
antseed seller start     # Start selling

# Consume AI services
antseed buyer start      # Start buying (proxy at localhost:8377)
```

---

## Monorepo

```
packages/             Core libraries (published to npm as @antseed/*)
  node/               Protocol SDK — P2P, discovery, metering, payments
  provider-core/      Shared provider infrastructure
  router-core/        Shared router infrastructure

plugins/              Provider and router plugins
  provider-anthropic/       Anthropic API key provider
  provider-claude-code/     Claude Code keychain provider
  provider-claude-oauth/    Claude OAuth provider
  provider-openai/          OpenAI-compatible provider (OpenAI, Together, OpenRouter)
  provider-local-llm/       Local LLM provider (Ollama, llama.cpp)
  router-local/             Local router (Claude Code, Aider, Continue.dev)

apps/                 Applications
  cli/                CLI tool (@antseed/cli)
  desktop/            Electron desktop app
  dashboard/          Web dashboard (Fastify + React)
  website/            Marketing website

e2e/                  End-to-end tests
docs/protocol/        Protocol specification
```

---

## CLI

Commands are organized by role:

```bash
# Seller
antseed seller setup                  # Interactive onboarding
antseed seller start                  # Start providing (all configured providers)
antseed seller register               # Register identity on-chain (ERC-8004)
antseed seller stake <amount>         # Stake USDC (min $10)
antseed seller emissions claim        # Claim ANTS rewards

# Buyer
antseed buyer start                   # Start proxy (localhost:8377)
antseed buyer deposit <amount>        # Deposit USDC for payments
antseed buyer withdraw <amount>       # Withdraw USDC
antseed buyer balance                 # Check wallet and deposit balance

# Config
antseed config seller add-provider together --plugin openai --base-url https://api.together.ai
antseed config seller add-service together deepseek-v3.1 --input 0.6 --output 1.7
antseed config seller show

# Network
antseed network browse                # Discover services and pricing
```

Full reference: [CLI Commands](https://antseed.com/docs/commands)

---

## Plugin Ecosystem

Anyone can publish a plugin to npm. Two types exist:

**Provider plugins** implement `AntseedProviderPlugin` from `@antseed/node` — serve raw inference, build a routing service, or wrap domain expertise as an AI agent. Set your price. Start earning.

**Router plugins** implement `AntseedRouterPlugin` from `@antseed/node` — discover providers, score them, and route buyer requests.

See [Creating Plugins](https://antseed.com/docs/plugins/creating-plugins) for interfaces and walkthroughs.

---

## Development

```bash
pnpm install            # Install all dependencies
pnpm run build          # Build in dependency order
pnpm run test           # Run all tests
pnpm run typecheck      # Type-check all packages
```

**Tech stack:** Node.js 20+, TypeScript 5.x strict, pnpm workspaces, tsc, Vite, Electron, BitTorrent DHT + WebRTC, USDC on Base.

---

## Contributing

See [CONTRIBUTING.md](https://github.com/AntSeed/.github/blob/main/CONTRIBUTING.md).

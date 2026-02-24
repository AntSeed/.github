# Antseed Network

**Decentralized peer-to-peer inference marketplace.**

Antseed connects AI capacity sellers directly with buyers — no intermediaries, no platform lock-in. Discovery, metering, and payment settlement happen at the protocol level.

---

## How It Works

```
seller                              buyer
  │                                   │
  ├─ provider plugin                  ├─ router plugin
  │   connects upstream AI API        │   selects peers & proxies requests
  │                                   │
  └─ antseed node (seed mode)       └─ antseed node (connect mode)
         │                                     │
         └──────────── DHT / P2P ──────────────┘
```

**Sellers** run a provider plugin that wraps an upstream AI API and exposes capacity on the network.
**Buyers** run a router plugin that discovers sellers, selects the best peer, and proxies requests from local tools.

---

## Repositories

| Repo | Description |
|---|---|
| [node](https://github.com/antseed-ai/node) | Core protocol SDK — DHT, WebRTC, metering, payments |
| [cli](https://github.com/antseed-ai/cli) | Command-line interface (`antseed seed`, `antseed connect`) |
| [provider-anthropic](https://github.com/antseed-ai/provider-anthropic) | Official provider plugin for Anthropic |
| [router-claude-code](https://github.com/antseed-ai/router-claude-code) | Official router plugin for Claude Code / Aider / Continue.dev |
| [dashboard](https://github.com/antseed-ai/dashboard) | Local web dashboard for node monitoring |
| [protocol](https://github.com/antseed-ai/protocol) | Protocol specification |
| [website](https://github.com/antseed-ai/website) | antseed.ai marketing site |
| [e2e](https://github.com/antseed-ai/e2e) | End-to-end test suite |

---

## Plugin Ecosystem

Anyone can publish a plugin to npm. Two types exist:

### Provider plugins — sell AI capacity

A provider plugin wraps any upstream AI API and exposes it as a seller node on the network. Implement the `AntseedProviderPlugin` interface from `@antseed/node` and publish to npm.

```ts
import type { AntseedProviderPlugin } from '@antseed/node'

const plugin: AntseedProviderPlugin = {
  name: 'my-provider',
  type: 'provider',
  // ...
  createProvider(config) { return new MyProvider(config) },
}
export default plugin
```

### Router plugins — buy AI capacity

A router plugin selects peers from the network and proxies requests from local tools (Claude Code, Aider, Continue.dev, etc.). Implement `AntseedRouterPlugin`.

```ts
import type { AntseedRouterPlugin } from '@antseed/node'

const plugin: AntseedRouterPlugin = {
  name: 'my-router',
  type: 'router',
  // ...
  createRouter(config) { return new MyRouter(config) },
}
export default plugin
```

Install and use any published plugin:

```bash
antseed plugin add my-provider
antseed seed --provider my-provider

antseed plugin add my-router
antseed connect --router my-router
```

---

## Getting Started

```bash
npm install -g antseed-cli
antseed init
```

`antseed init` guides you through selecting and installing plugins for seeding or connecting.

---

## Contributing

See [CONTRIBUTING.md](https://github.com/antseed-ai/.github/blob/main/CONTRIBUTING.md).

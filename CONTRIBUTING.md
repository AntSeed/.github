# Contributing to AntSeed

Thank you for your interest in contributing. AntSeed is developed as a [monorepo](https://github.com/AntSeed/antseed) using pnpm workspaces.

---

## Development Setup

```bash
git clone https://github.com/AntSeed/antseed
cd antseed
pnpm install
pnpm run build
```

Run tests:

```bash
pnpm run test
```

Type-check:

```bash
pnpm run typecheck
```

---

## Repository Structure

| Area | Location |
|---|---|
| Protocol SDK | `packages/node` |
| Provider infrastructure | `packages/provider-core` |
| Router infrastructure | `packages/router-core` |
| Provider plugins | `plugins/provider-*` |
| Router plugins | `plugins/router-*` |
| CLI | `apps/cli` |
| Desktop app | `apps/desktop` |
| Dashboard | `apps/dashboard` |
| Website | `apps/website` |
| Protocol spec | `docs/protocol` |
| End-to-end tests | `e2e/` |

---

## Pull Requests

- Keep PRs focused — one change per PR
- Add or update tests for any changed behaviour
- Run `pnpm run build` and `pnpm run test` before opening a PR
- Describe *why* the change is needed, not just what it does

---

## Issues

Use the issue templates in the [monorepo](https://github.com/AntSeed/antseed/issues). For protocol-level changes, reference `docs/protocol`.

---

## Publishing a Plugin

You do not need to contribute to this org to publish an AntSeed plugin. Implement the `AntseedProviderPlugin` or `AntseedRouterPlugin` interface from `@antseed/node` and publish your package to npm. See the [plugin docs](https://github.com/AntSeed/antseed#building-a-plugin) for interface definitions and walkthroughs.

---

## Code Style

- TypeScript strict mode throughout
- ES modules only
- No default exports except for plugin entry points
- Prefer explicit types over inference in public APIs

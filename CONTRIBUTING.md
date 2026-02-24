# Contributing to Antseed Network

Thank you for your interest in contributing. This document covers the basics for all repositories in the `antseed-ai` organization.

---

## Repository Overview

Each repository is independently versioned and published to npm. Before contributing, read the specific `README.md` in the relevant repo.

| Area | Repo |
|---|---|
| Protocol SDK | `node` |
| CLI | `cli` |
| Provider plugins | `provider-anthropic`, or publish your own |
| Router plugins | `router-claude-code`, or publish your own |
| Dashboard | `dashboard` |
| Protocol spec | `protocol` |

---

## Development Setup

```bash
git clone https://github.com/antseed-ai/<repo>
cd <repo>
npm install
npm run build
```

Run tests:

```bash
npm test
```

---

## Pull Requests

- Keep PRs focused — one change per PR
- Add or update tests for any changed behaviour
- Run `npm run build` and `npm test` before opening a PR
- Describe *why* the change is needed, not just what it does

---

## Issues

Use the issue templates in each repository. For cross-cutting concerns (protocol changes, new plugin types), open an issue in the `protocol` repo.

---

## Publishing a Plugin

You do not need to contribute to this org to publish a Antseed plugin. Implement the `AntseedProviderPlugin` or `AntseedRouterPlugin` interface from `@antseed/node` and publish your package to npm. See the `node` repository for interface definitions.

---

## Code Style

- TypeScript strict mode throughout
- No default exports except for plugin entry points
- Prefer explicit types over inference in public APIs

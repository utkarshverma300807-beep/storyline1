# Forkit

> Your personalized onramp into open source. Forkit analyzes your GitHub profile, matches you to real issues, and generates a guide to make your first contribution — without the orientation paralysis.

---

## Table of Contents

- [What It Does](#what-it-does)
- [Monorepo Structure](#monorepo-structure)
- [How to Run the Repo](#how-to-run-the-repo)
  - [1. Clone the Repo](#1-clone-the-repo)
  - [2. Install Node Dependencies](#2-install-node-dependencies)
  - [3. Set Up Environment Variables](#3-set-up-environment-variables)
  - [4. Set Up Python AI Service](#4-set-up-python-ai-service)
- [Build Commands](#build-commands)
  - [Development](#development)
  - [Build](#build)
- [Contributing](#contributing)
  - [Branches](#branches)
  - [Pull Requests](#pull-requests)
  - [Commits](#commits)
  - [Prefix Reference](#prefix-reference)
  - [Examples](#examples)

---

## What It Does

Most developers never contribute to open source — not because they can't, but because they don't know where to start in an unfamiliar codebase. Forkit fixes that.

Connect your GitHub → Forkit infers your skill profile from your repos and commits → matches you to real open issues that fit your level → generates a personalized onboarding guide for that specific repo: which files to read, what concepts you need, how to set up locally, and what to do first.

---

## Monorepo Structure

```
forkit/
├── apps/
│   ├── web/                  # Next.js frontend
│   └── api/                  # Node.js + Express — GitHub OAuth, connection to FE, DB
│
├── services/
│   └── ai/                   # Python service — all AI/LLM logic
│
├── packages/
│   ├── types/                # Shared TypeScript types (consumed by web + api)
│   └── db/                   # Schemas, migrations
```

---

## How to Run the Repo

Make sure you have these installed before anything:

```bash
node --version     #
pnpm --version     #
python --version   #
docker --version   # (will use later)
```

### 1. Clone the Repo

```bash
git clone https://github.com/csivitu/forkit.git
cd forkit
```

### 2. Install Node Dependencies

Always run installs from the **root** — never `cd` into a package and run `pnpm install` separately.

```bash
pnpm install
```

This installs all workspace packages (`apps/web`, `apps/api`, `packages/types`, `packages/db`).

### 3. Set Up Environment Variables

```bash
cp .env.example .env
```

### 4. Set Up Python AI Service

> todo: neeraj will add docs for this

---

## Build Commands

All commands below are run from the **root** of the repo only.

### Development

```bash
pnpm dev                          # run web + api together (Turborepo)
pnpm dev --filter web     # run only Next.js
pnpm dev --filter api     # run only backend
```

### Build

```bash
pnpm build                        # build all apps in correct dependency order
pnpm build --filter web   # build only Next.js
pnpm build --filter api   # build only backend
```

---

## Contributing

### Branches

Create a new branch for every task. Branch names must follow this format:

```
TASKID/name/feature
```

Examples:
```
FK-12/neeraj/github-oauth
FK-34/tanuj/skill-profiler
```

### Pull Requests

When you're working on something, raise a draft PR and mark it as ready once done, against `main` with the following:

- **Title** — short and descriptive, matching what the branch does
- **Description** — what was changed, why, and any decisions worth noting
- **Screenshots or recordings** — required if the change affects any UI or user-facing behaviour; skip only for pure backend or config changes

Keep PRs focused — one task per PR. Do not bundle unrelated changes.

### Commits

1. Commits must not be made for every minor change — a group of related changes must be clubbed together and committed at once. The same applies when sending a PR to the main upstream repository or the main branch from any other branch.

2. Commit messages must follow [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) and always include the appropriate prefix.

### Prefix Reference

**Type-based**

| Prefix | Use |
|---|---|
| `feat` | A new feature or functionality |
| `fix` | A bug fix |
| `chore` | Maintenance tasks that don't affect logic (config, deps) |
| `refactor` | Code restructuring with no functional change |
| `style` | Formatting only — spacing, indentation, commas |
| `test` | Adding or updating tests |
| `docs` | Documentation updates |
| `build` | Build system or external dependency changes |
| `ci` | CI configuration changes |
| `perf` | Performance improvements |
| `revert` | Reverting a previous commit |

**Scope-based** (optional but helpful)

Append a scope in parentheses to specify the area affected:

```
feat(auth): add OAuth2.0 authentication
fix(api): handle missing parameters in request
docs(ui): update button component usage
```

**Breaking changes**

```
feat!: change authentication method to token-based (BREAKING CHANGE)
```

### Examples

```
feat(cart): add item quantity update functionality
fix(auth): resolve token expiration issue
chore: remove deprecated package
build(deps): upgrade React to version 18
revert: revert previous login bug fix
```
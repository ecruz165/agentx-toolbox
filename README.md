# AgentX Toolbox

A coordinated set of CLI tools for the AgentX ecosystem. Each tool is
independently installable and useful, but composes with the others
through shared conventions and a common brand.

> **AgentX** is the product/brand name. Packages publish under the
> npm scope **`@ecruz165/`** — the same scope used by `agentx-platform`.
> See [CONVENTIONS.md](./CONVENTIONS.md) for the full spec.

## Apps

| Package | What it does |
|---|---|
| [`@ecruz165/skillzkit`](apps/skillzkit) | Catalog of slash commands, agent skills, and multi-phase workflows for Claude Code. |
| [`@ecruz165/toolz`](apps/toolz) | Cross-platform install primitive — `ensureTool('git')`, registry, doctor. |
| [`@ecruz165/gitradar`](apps/gitradar) | Terminal TUI analytics for git contribution data. SQLite-backed, GitHub-enrichable. |
| [`@ecruz165/pritty`](apps/pritty) | AI-powered commit and PR CLI — categorize staged files, generate commits, open PRs. |
| [`@ecruz165/taskmaster`](apps/taskmaster) | CLI project task generator — parse plans, score complexity, decompose into hierarchies. |
| [`@ecruz165/gittyup`](apps/gittyup) | Multi-repo orchestration CLI with interactive conflict resolution. |

Add new apps under `apps/<name>/`. Each app is its own npm package
with its own `package.json` and lifecycle. Cross-app dependencies use
`@ecruz165/*` workspace links.

## Shared packages

`packages/` holds cross-repo shared libraries. Directory names end in
`-lib`; published package names drop the `-lib` suffix (matches
agentx-platform's convention).

| Package | Directory | Purpose |
|---|---|---|
| `@ecruz165/agent-auth` | `packages/agent-auth-lib/` | Auth (token cache, refresh, login). Migrated in from agentx-platform. |
| `@ecruz165/agent-adapter` | `packages/agent-adapter-lib/` | Agent SDK calls. Only place that imports Anthropic / Copilot / OpenAI SDKs. Migrated in from agentx-platform. |
| `@ecruz165/skillzkit-types` | `packages/skillzkit-types-lib/` | TS types for skillzkit catalog/skills/commands/workflows. Consumed by skillzkit and platform's controlplane-ui. |
| `@ecruz165/cli-kit` | `packages/cli-kit-lib/` | Commander + inquirer + pluggable auth bootstrap. Consumed by all 6 toolbox apps. |
| `@ecruz165/tui-view-components` | `packages/tui-view-components-lib/` | Reusable TUI components on openTUI + React. Provides `runConnectView()` and themed primitives (Box, Text, Button, Panel, ThemeSwitcher) consumed by every app's `connect` subcommand. |

## Project layout

```
agentx-toolbox/
├── apps/                         publishable CLI apps (6)
│   ├── skillzkit/
│   ├── toolz/
│   ├── gitradar/
│   ├── pritty/
│   ├── taskmaster/
│   └── gittyup/
├── packages/                     shared libraries (cross-repo)
│   ├── agent-auth-lib/           (migrated from agentx-platform)
│   ├── agent-adapter-lib/        (migrated from agentx-platform)
│   ├── skillzkit-types-lib/      (TS types, generates JSON Schema)
│   ├── cli-kit-lib/              (commander + auth bootstrap)
│   └── tui-view-components-lib/  (openTUI components + ConnectView)
├── CONVENTIONS.md                cross-app conventions spec
├── tsconfig.base.json            shared TS compiler options
├── package.json                  workspace root
└── README.md
```

## Development

This is an npm workspace. From the root:

```bash
npm install              # installs all workspace deps
npm test                 # runs every workspace's test script (vitest)
npm run build            # runs every workspace's build script
npm run catalog          # regenerate skillzkit's catalog.json
npm run skillzkit -- <subcommand>   # run skillzkit's CLI in dev (via tsx)
```

To work on a specific app:

```bash
cd apps/skillzkit
npm test
npm run cli list --tree
```

## Contributing

Each app has its own README with contribution conventions. Cross-app
changes (e.g. adding a shared package, refactoring conventions) belong
at the toolbox level — open an issue at the root before doing
substantial cross-cutting work.

## License

UNLICENSED — internal AgentX use.

# AgentX Toolbox

A coordinated set of CLI tools for the AgentX ecosystem. Each tool is
independently installable and useful, but composes with the others
through shared conventions and a common brand.

## Apps

| Package | What it does |
|---|---|
| [`@agentx/skillzkit`](apps/skillzkit) | Catalog of slash commands, agent skills, and multi-phase workflows for Claude Code. |
| `@agentx/toolz` *(planned)* | Cross-platform install primitive — `ensureTool('git')` etc. See `agentx-toolz/toolz-implmentation-plan.md`. |
| `@agentx/gittyup` *(planned)* | Git workflow tool. |

Add new apps under `apps/<name>/`. Each app is its own npm package
with its own `package.json` and lifecycle. Cross-app dependencies use
`@agentx/*` workspace links.

## Shared packages

`packages/` is reserved for cross-app shared libraries (TS configs,
branding, logger, error types, etc.). Empty until a second app needs
to share something with skillzkit.

## Project layout

```
agentx-toolbox/
├── apps/                         publishable CLI apps
│   └── skillzkit/
├── packages/                     shared libraries (cross-app)
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

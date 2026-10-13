# Tally apps (twin)

Three small to-do apps in one repository, a twin of `pristine-test-org/todo-monorepo` without the shared
database. Each is its own site with its own look, and each keeps its own list in the browser
(localStorage): nothing leaves the page, and there is no sign-in.

| App | Folder | What it looks like | Live |
| --- | --- | --- | --- |
| **Tally** | `apps/tally` | One quiet list on warm paper, serif wordmark, green accent | https://todo-monorepo-2-tally.vercel.app |
| **Tally Board** | `apps/tally-board` | Cards in To do and Done columns, navy bar, indigo accent | https://todo-monorepo-2-tally-board.vercel.app |
| **Tally Lite** | `apps/tally-lite` | Plain text on a dark screen, monospaced, amber accent | https://todo-monorepo-2-tally-lite.vercel.app |

Each app's `DESIGN.md` describes its palette, type and layout.

## Tech stack

- **npm workspaces**: the apps live in `apps/*`, with one `package-lock.json` at the root.
- **Vite + React 19 + TypeScript**, plain CSS per app. Each build is a static `dist/` folder.
- **localStorage** for the list, in `apps/<app>/src/lib/store.ts`. No server, no database.
- **Vercel** hosts each app as its own project (root directory `apps/<app>`), with a preview
  deployment for every pull request.

## Local setup

```bash
npm install                    # once, at the root
npm run dev -w tally           # http://localhost:5173
npm run dev -w tally-board     # http://localhost:5174
npm run dev -w tally-lite      # http://localhost:5175
```

| Command (at the root) | What it does |
| --- | --- |
| `npm run build` | Type-checks and builds all three apps |
| `npm run build -w <app>` | Builds one app into `apps/<app>/dist` |
| `npm run lint` | ESLint in every app |
| `npm run typecheck` | `tsc -b` in every app |

## Deploy (Vercel)

Each app is a separate Vercel project connected to this repository:

| Setting | Value |
| --- | --- |
| Root Directory | `apps/<app>` |
| Framework | Vite |
| Build command | `npm run build` |
| Deployment Protection | Standard Protection (production open, previews behind Vercel's login) |

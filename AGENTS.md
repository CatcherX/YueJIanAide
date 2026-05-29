# AGENTS.md

## Cursor Cloud specific instructions

### Overview

This is a **LeanCloud LeanEngine** Node.js sample application — an Express server with EJS templates that implements a simple TODO list and WeChat Mini Program cloud functions. All data persistence goes through LeanCloud's managed BaaS (no local database).

### Running the dev server

```bash
LEANCLOUD_APP_ID=<id> LEANCLOUD_APP_KEY=<key> LEANCLOUD_APP_MASTER_KEY=<master_key> npm run dev
```

- The server starts on port 3000 (configurable via `LEANCLOUD_APP_PORT` or `PORT`).
- `npm run dev` uses nodemon for file watching and auto-restart.
- Without valid LeanCloud credentials, the homepage (`/`) renders fine, but data routes (`/todos`) return 400 from LeanCloud SDK.

### Environment variables

| Variable | Required | Purpose |
|---|---|---|
| `LEANCLOUD_APP_ID` | Yes | LeanCloud app identifier |
| `LEANCLOUD_APP_KEY` | Yes | LeanCloud app key |
| `LEANCLOUD_APP_MASTER_KEY` | Yes | LeanCloud master key (enables full data access) |
| `APPID` | No | WeChat Mini Program app ID (only for cloud functions) |
| `APPSECRET` | No | WeChat Mini Program secret (only for cloud functions) |

### Project structure

- `server.js` — entry point, initializes LeanCloud SDK and starts Express
- `app.js` — Express app setup (middleware, routes, error handlers)
- `cloud.js` — LeanCloud cloud function definitions (WeChat integration)
- `routes/todos.js` — TODO CRUD routes
- `views/` — EJS templates
- `public/` — static assets

### Key gotchas

- **No linter, no test framework** — the project has no `eslint`, `prettier`, or test scripts configured.
- **Node engine mismatch** — `package.json` specifies `"node": "6.x"` but the app works fine on modern Node (v22+). `npm install` will emit `EBADENGINE` warnings; these are harmless.
- **Lock file committed** — `package-lock.json` is checked in for reproducible installs.
- **LeanCloud credentials required for data operations** — without valid credentials, the server starts and the homepage renders, but any route that touches LeanCloud storage returns HTTP 400.

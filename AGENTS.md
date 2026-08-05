# AGENTS.md

## Cursor Cloud specific instructions

This is an npm-workspaces monorepo (`madan-resume-matcher`) with two apps and no database:

- `apps/web` — React + Vite SPA (dev server on `http://localhost:5173`).
- `apps/worker` — Cloudflare Worker API via Wrangler (dev server on `http://localhost:8787`).

Standard commands live in the root `package.json` and `README.md`; prefer those. Key ones:

- Install: `npm install` (from repo root; installs both workspaces).
- Run web (dev): `npm run dev:web`
- Run worker (dev): `npm run dev:worker`
- Build + typecheck (both apps): `npm run build` (runs `tsc -b && vite build` for web and `tsc --noEmit` for the worker). There is no separate lint step configured; TypeScript typechecking is the lint gate.

Both dev servers must run at the same time (in separate terminals/tmux sessions) for the full browser flow. The frontend defaults its API base to `http://localhost:8787` when `VITE_API_URL` is unset (see `apps/web/src/main.tsx`), so no `apps/web/.env` is needed for local dev.

### Non-obvious caveats

- Full resume tailoring requires a real Anthropic key. Set it as a local Worker secret in `apps/worker/.dev.vars` as `ANTHROPIC_API_KEY=sk-ant-...` (this file is intentionally not committed). Without it, `POST /api/tailor` reaches Anthropic and returns `{"error":"invalid x-api-key"}`. `GET /api/health` returns `{"ok":true}` and needs no key.
- `wrangler dev` does NOT hot-reload changes to `apps/worker/.dev.vars`. After creating/editing that file, restart the worker dev server for the new value to take effect. (Source changes in `apps/worker/src` do hot-reload.)
- PDF text extraction happens entirely client-side via `pdfjs-dist`; use a searchable-text PDF (scanned/image-only PDFs won't extract).
- The master resume is persisted only in browser `localStorage`; there is no backend storage, accounts, or DB.
- Known pre-existing bug (not an environment issue): the browser tailor flow sends a CORS preflight `OPTIONS` to the worker, and the current `OPTIONS` handler in `apps/worker/src/index.ts` returns a `204` with a JSON body, which is an invalid response and makes the browser fail with "Failed to fetch". Direct `curl` to `POST /api/tailor` still works. To exercise the flow in a browser, the `OPTIONS` branch needs to return a body-less `204` (e.g. `new Response(null,{status:204,headers:{...}})`).

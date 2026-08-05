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

- Full resume tailoring requires a real Anthropic key. Put it in `apps/worker/.dev.vars` as `ANTHROPIC_API_KEY=...` (gitignored; never commit). If the cloud env already exports `ANTHROPIC_API_KEY`, write it into that file before starting the worker: `printf 'ANTHROPIC_API_KEY=%s\n' "$ANTHROPIC_API_KEY" > apps/worker/.dev.vars`. Without it, `POST /api/tailor` returns an Anthropic auth error. `GET /api/health` returns `{"ok":true}` with no key.
- `wrangler dev` does **not** hot-reload `.dev.vars`. Restart the worker after creating/editing that file. Source changes under `apps/worker/src` do hot-reload.
- The worker model id is `claude-sonnet-4-6`. Older ids like `claude-sonnet-4-20250514` return Anthropic `not_found_error` for current keys — check `GET https://api.anthropic.com/v1/models` if tailor starts failing with a model error.
- Browser CORS preflight requires a body-less `204` on `OPTIONS` (already fixed in `apps/worker/src/index.ts`). Returning `json({}, 204, …)` breaks the browser tailor flow with "Failed to fetch" even though `curl` still works.
- PDF text extraction is client-side via `pdfjs-dist`; use a searchable-text PDF (image-only scans will not extract).
- The master resume lives only in browser `localStorage`; there is no backend storage, accounts, or DB.

# plank-fde-training

WorkBot, an enterprise workflow platform, built for Plank's AI FDE Course. It is
a Next.js app (App Router) with TypeScript and Tailwind, and it grows a little
each course day. Commits are read to verify progress, so keep them small and
their messages honest.

## Commands

- `npm run dev`: start the dev server
- `npm run build`: production build
- `npm run lint`: ESLint
- `npm run format`: write Prettier formatting; `npm run format:check` only checks
- `npm run typecheck`: `tsc --noEmit`
- `npm run check`: lint, format check, typecheck and build. CI runs this on
  pushes to `main` and on pull requests, so it must pass before you finish.

## Conventions

Every change must follow these.

### Where files go

- `src/app/`: routes, layouts and route handlers only
- `src/components/`: shared React components
- `src/lib/`: non-UI code such as helpers, clients and the env module
- Import with the `@/` alias (`@/lib/env`), not long relative paths.
- Put a component next to the route that uses it until a second route needs it,
  then move it to `src/components/`.

### Server Components by default

A Server Component renders on the server and sends no JavaScript to the
browser. Every component is one unless it has to be a Client Component.

- Add `"use client"` only when the component needs state, effects, event
  handlers or browser-only APIs.
- Keep Client Components small and as deep in the tree as possible. Pass server
  data to them as props instead of marking a whole page as client.
- Fetch data in Server Components, not in client-side effects.

### One module reads `process.env`

Only `src/lib/env.ts` may read `process.env`. It validates the variables once
and exports typed values. Everything else imports from `@/lib/env`.

- Never read `process.env` anywhere else, including route handlers and
  components.
- Add new variables to `src/lib/env.ts` and to `.env.example`. Never commit
  real values; `.env` is gitignored.
- Never import `@/lib/env` from a Client Component. Secrets must not reach the
  browser.

<!-- BEGIN:nextjs-agent-rules -->

## This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` (resolved from this file's directory; in monorepos the `next` package may not be visible from the repo root) before writing any code. Heed deprecation notices.

This block is written and re-added by `next dev` — verify at `node_modules/next/dist/server/lib/generate-agent-files.js`. Removing it from a diff only re-creates the uncommitted change; committing it with your work keeps the tree clean.

<!-- END:nextjs-agent-rules -->

# Development guide

How to set up BeKampus locally. For product scope and architecture, see [PRODUCT.md](PRODUCT.md), [REQUIREMENTS.md](REQUIREMENTS.md) and [ARCHITECTURE.md](ARCHITECTURE.md).

## Requirements

- Node.js 22 (the repo requires `>=20.9.0`; CI uses 22)
- pnpm 11 (the exact version is pinned in `package.json` via `packageManager`)
- Access to the BeKampus Supabase project (ask a maintainer to invite you)
- Docker Desktop (optional for now; it will be required to run Supabase locally once database migrations are introduced)

## 1. Install dependencies

```bash
pnpm install
```

## 2. Configure environment variables

Copy the example file and fill in the values:

```bash
cp apps/web/.env.example apps/web/.env.local
```

| Variable                               | Used in                      | Exposed to the browser?                                                                 |
| -------------------------------------- | ---------------------------- | --------------------------------------------------------------------------------------- |
| `NEXT_PUBLIC_SUPABASE_URL`             | browser and server           | Yes                                                                                     |
| `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY` | browser and server           | Yes. It is designed to be public; data access is protected by Row Level Security (RLS). |
| `SUPABASE_SECRET_KEY`                  | server-only code and scripts | **Never.** It bypasses RLS.                                                             |

Where to find the values: Supabase dashboard → **Project Settings → API Keys**.

- `NEXT_PUBLIC_SUPABASE_URL` looks like `https://<PROJECT_REF>.supabase.co`.
- `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY` starts with `sb_publishable_`.

Rules:

- `apps/web/.env.local` is ignored by Git. Never commit it.
- Only `apps/web/.env.example` is versioned, and it must never contain real values.
- Never add the `NEXT_PUBLIC_` prefix to a secret. Next.js ships `NEXT_PUBLIC_*` values to the browser.
- `SUPABASE_SECRET_KEY` is not needed yet. Add it only to local scripts or server-only code that truly requires it, and never use it in client components.
- If a new environment variable is needed at build time, also declare it under the `build` task `env` in `turbo.json`, otherwise Turborepo will not pass it to the build.

## 3. Run the app

```bash
pnpm dev
```

Open http://localhost:3000. Public pages must be reachable without signing in.

## Supabase integration

Code lives in `apps/web`:

| File                     | Purpose                                                                                                                                          |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| `lib/supabase/client.ts` | Supabase client for Client Components                                                                                                            |
| `lib/supabase/server.ts` | Supabase client for Server Components, Server Actions and Route Handlers. Create a new client per request; do not store it in a global variable. |
| `lib/supabase/proxy.ts`  | `updateSession` helper that refreshes the auth session                                                                                           |
| `proxy.ts`               | Next.js proxy (formerly `middleware`) that calls `updateSession` on each request                                                                 |

The proxy only keeps the session fresh. It does not redirect anonymous visitors, because browsing public content does not require an account (product rule 1). Protected actions must verify identity and permissions on the server or in the database (NFR-001).

## Database scripts

Run from the repository root:

| Script          | What it does                                               |
| --------------- | ---------------------------------------------------------- |
| `pnpm db:start` | Starts a local Supabase stack (requires Docker)            |
| `pnpm db:stop`  | Stops the local stack                                      |
| `pnpm db:reset` | Recreates the local database from migrations and seed data |
| `pnpm db:push`  | Applies pending migrations to the linked cloud project     |

Schema changes will be versioned as migrations in `supabase/migrations`, not applied only through the dashboard.

### Link to the cloud project (maintainers)

```bash
pnpm supabase login
pnpm supabase link --project-ref <PROJECT_REF>
```

`<PROJECT_REF>` is in the dashboard URL: `supabase.com/dashboard/project/<PROJECT_REF>`. Linking asks for the database password and does not modify the remote project.

## Quality checks

Run these before opening a pull request (the same steps run in CI):

```bash
pnpm format
pnpm lint
pnpm typecheck
pnpm build
```

## Troubleshooting

- **Build fails because Supabase variables are missing:** check `apps/web/.env.local` and the `env` list in `turbo.json`.
- **Random logouts or stale sessions:** make sure `proxy.ts` exists in `apps/web` and that `updateSession` still calls `supabase.auth.getClaims()` immediately after creating the client.
- **`.env.example` does not appear in `git status`:** `.gitignore` must contain `!.env.example` after `.env*`.

# Attendance Predictor

Attendance Predictor helps SRM students understand attendance risk and plan how many upcoming classes they need to attend or can safely miss.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/attendance-predictor/src/App.tsx` — timetable-backed sections, attendance calculations, and dashboard interactions.
- `artifacts/attendance-predictor/src/index.css` — visual theme, responsive layout, and state colors.
- `artifacts/attendance-predictor` — the runnable React/Vite dashboard artifact.

## Architecture decisions

- The first version is client-side so students can try the predictor immediately without account setup or a backend.
- Timetable data is encoded from the supplied SRM PDFs and exposed as section-specific subjects.
- Attendance thresholds are explicit: safe at 90%+, watch at 75–89.9%, and detention below 75%.

## Product

- Students choose their timetable section and enter attended/conducted counts per subject.
- The dashboard summarizes overall and per-subject status, recovery targets, safe-miss buffers, and forward attendance scenarios.
- The semester window is fixed to 29 Aug–29 Nov 2026 for the supplied challenge.

## User preferences

_Populate as you build — explicit user instructions worth remembering across sessions._

## Gotchas

_Populate as you build — sharp edges, "always run X before Y" rules._

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details

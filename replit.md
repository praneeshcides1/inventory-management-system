# Stockroom — Inventory Management System

Stockroom is a responsive CRUD inventory workspace for tracking products, stock health, inventory value, suppliers, and recent activity.

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

- `artifacts/inventory-management` — React/Vite application and user-facing dashboard
- `artifacts/api-server/src/routes/inventory.ts` — REST CRUD and dashboard endpoints
- `lib/api-spec/openapi.yaml` — API contract source of truth
- `lib/db/src/schema/inventory.ts` — PostgreSQL/Drizzle schema
- `artifacts/inventory-management/README.md` — setup, architecture, schema, and API documentation

## Architecture decisions

- The API derives stock status from quantity and reorder level so the display cannot drift from source data.
- Inventory activity is stored separately so create, update, and delete actions remain visible on the dashboard.
- OpenAPI is the source of truth for generated client hooks and server validation schemas.

## Product

Users can review inventory health at a glance, search and filter items, add records, edit details, and remove obsolete records. Summary metrics and recent activity help operators identify what needs attention quickly.

## User preferences

The user requested a working web application that can be shared as a link, based on the provided CRUD application SOP.

## Gotchas

- Run API codegen after changing `lib/api-spec/openapi.yaml`.
- Use the managed workflows for preview; they supply the required `PORT`, `BASE_PATH`, and database environment.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details

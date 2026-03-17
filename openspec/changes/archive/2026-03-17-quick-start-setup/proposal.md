## Why

The project needs to complete the Quick Start setup to reach a development-ready state. It will use Supabase PostgreSQL as the database, TanStack Start as the web app, and Expo as the mobile app.

## What Changes

- Install dependencies (`pnpm i`)
- Remove the unused Next.js app directory (`apps/nextjs`)
- Configure environment variable files (create `.env` files with Supabase connection info)
  - `apps/tanstack-start/.env`
  - `packages/db/.env`
  - `packages/auth/.env`
- Push Drizzle schema to Supabase (`pnpm db:push`)
- Generate Better Auth schema (`pnpm --filter @acme/auth generate`)
- Configure Expo dev script (default to iOS Simulator)

## Capabilities

### New Capabilities

- `project-setup`: The full Quick Start process including initial project setup, environment variable configuration, dependency installation, DB schema push, and auth schema generation

### Modified Capabilities

_(None — this is an initial setup with no existing capabilities to modify)_

## Impact

- **Code**: Remove `apps/nextjs` directory, update dev script in `apps/expo/package.json`
- **Dependencies**: Install all monorepo dependencies via `pnpm i`
- **Database**: Push Drizzle schema to Supabase PostgreSQL
- **Auth**: Generate auth schema via Better Auth CLI → `packages/db/src/auth-schema.ts`
- **Environment**: Create 3 `.env` files (DB URL, auth secret, OAuth credentials)

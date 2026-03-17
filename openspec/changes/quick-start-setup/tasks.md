## 1. Dependencies & Cleanup

- [x] 1.1 Run `pnpm i` to install all monorepo dependencies
- [x] 1.2 Remove `apps/nextjs` directory (unused web app)

## 2. Environment Variables

- [x] 2.1 Copy `apps/tanstack-start/.env.example` to `apps/tanstack-start/.env` and fill in `POSTGRES_URL`, `AUTH_SECRET`
- [x] 2.2 Copy `packages/db/.env.example` to `packages/db/.env` and fill in `POSTGRES_URL`
- [x] 2.3 Copy `packages/auth/.env.example` to `packages/auth/.env` and fill in `POSTGRES_URL`, `AUTH_SECRET`
- [x] 2.4 Verify `.env` is in `.gitignore`

## 3. Database Setup

- [x] 3.1 Run `pnpm db:push` to push Drizzle schema to Supabase PostgreSQL

## 4. Auth Schema Generation

- [x] 4.1 Run `pnpm --filter @acme/auth generate` to generate Better Auth schema at `packages/db/src/auth-schema.ts`

## 5. Expo Configuration

- [x] 5.1 Update `apps/expo/package.json` dev script to `expo start --ios`

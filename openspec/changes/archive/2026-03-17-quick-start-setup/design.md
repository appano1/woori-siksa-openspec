## Context

A monorepo based on create-t3-turbo, using the TanStack Start (web) + Expo (mobile) + tRPC + Drizzle + Better Auth + Supabase PostgreSQL stack. Currently only the scaffolding is in place; initial setup is required to bring the development environment online.

## Goals / Non-Goals

**Goals:**
- Install dependencies and bring up the development environment
- Connect to Supabase PostgreSQL and push the Drizzle schema
- Generate the Better Auth schema
- Remove the unused Next.js app
- Configure the Expo dev script for iOS Simulator

**Non-Goals:**
- OAuth provider setup (Discord, etc.) — handled as a separate change
- Production deployment configuration
- Adding custom schemas — only generate the default auth schema
- Android Emulator setup

## Decisions

### 1. Choose TanStack Start, remove Next.js
- Use TanStack Start v1 (rc) as the web app
- Fully remove the `apps/nextjs` directory to avoid confusion
- **Alternative**: Keep both apps → introduces unnecessary complexity

### 2. Manually create environment variable files
- Create `.env` files based on `.env.example`, with the user providing their actual Supabase URL
- Generate `AUTH_SECRET` via `openssl rand -base64 32`
- **Alternative**: Automated script → risk of embedding secrets in code

### 3. Set Expo dev script to iOS Simulator
- Change the `dev` script in `apps/expo/package.json` to `expo start --ios`
- **Alternative**: `expo start` (default) → requires manually selecting the platform each time

### 4. Sequential setup order
1. `pnpm i` (install dependencies)
2. Remove `apps/nextjs`
3. Create `.env` files (requires user input)
4. `pnpm db:push` (push Drizzle schema)
5. `pnpm --filter @acme/auth generate` (generate Better Auth schema)
6. Update Expo dev script

## Risks / Trade-offs

- **[Supabase connection pooler]** → The URL template in `.env.example` uses the Supabase pooler format. Some Drizzle features may be limited under Transaction mode pooling → recommend using a Session mode pooler URL
- **[TanStack Start rc]** → Still an RC release with potential breaking changes → mitigate by using the exact version tested with create-t3-turbo
- **[.env file security]** → Must verify that `.env` is already included in `.gitignore`

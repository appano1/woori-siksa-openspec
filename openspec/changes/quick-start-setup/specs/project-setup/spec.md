## ADDED Requirements

### Requirement: Dependencies are installed
The system SHALL have all monorepo dependencies installed via `pnpm i`.

#### Scenario: Successful dependency installation
- **WHEN** `pnpm i` is executed in the monorepo root
- **THEN** all workspace packages have their dependencies resolved and installed

### Requirement: Unused web app is removed
The `apps/nextjs` directory SHALL be removed since TanStack Start is the chosen web framework.

#### Scenario: Next.js app directory removed
- **WHEN** the setup is complete
- **THEN** `apps/nextjs` directory does not exist in the project

### Requirement: Environment variables are configured
Each package requiring environment variables SHALL have a `.env` file with valid values.

#### Scenario: TanStack Start env configured
- **WHEN** `apps/tanstack-start/.env` is created from `.env.example`
- **THEN** it contains a valid `POSTGRES_URL`, `AUTH_SECRET`, and OAuth placeholder values

#### Scenario: Database package env configured
- **WHEN** `packages/db/.env` is created from `.env.example`
- **THEN** it contains a valid `POSTGRES_URL` pointing to Supabase

#### Scenario: Auth package env configured
- **WHEN** `packages/auth/.env` is created from `.env.example`
- **THEN** it contains a valid `POSTGRES_URL` and `AUTH_SECRET`

### Requirement: Database schema is pushed
The Drizzle schema SHALL be pushed to the Supabase PostgreSQL database.

#### Scenario: Successful schema push
- **WHEN** `pnpm db:push` is executed
- **THEN** all Drizzle schema tables are created in the Supabase database without errors

### Requirement: Auth schema is generated
The Better Auth schema SHALL be generated using the Better Auth CLI.

#### Scenario: Successful auth schema generation
- **WHEN** `pnpm --filter @acme/auth generate` is executed
- **THEN** `packages/db/src/auth-schema.ts` is created with Drizzle-compatible auth table definitions

### Requirement: Expo dev script targets iOS Simulator
The Expo app's dev script SHALL launch the iOS Simulator by default.

#### Scenario: Dev script configured for iOS
- **WHEN** `apps/expo/package.json` dev script is checked
- **THEN** it contains `expo start --ios`

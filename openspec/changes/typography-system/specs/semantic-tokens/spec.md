## ADDED Requirements

### Requirement: Typography semantic tokens in theme CSS
The system SHALL define typography CSS custom properties in `:root` alongside existing color semantic tokens. Properties SHALL follow the naming pattern: `--text-{role}`, `--leading-{role}`, `--tracking-{role}`, `--font-weight-{role}`.

#### Scenario: Typography tokens coexist with color tokens
- **WHEN** inspecting `:root` in theme.css
- **THEN** typography tokens (e.g., `--text-body`, `--leading-body`) are defined alongside color tokens (e.g., `--primary`, `--background`)

### Requirement: Tailwind typography utility mapping
All typography tokens SHALL be mapped in `@theme inline` to generate Tailwind utilities. Font-size tokens map via `--text-*`, line-height via `--leading-*`, letter-spacing via `--tracking-*`, and font-weight via `--font-weight-*`.

#### Scenario: Tailwind text utility works
- **WHEN** a component uses `text-heading` class
- **THEN** it resolves to the `--text-heading` custom property value (1.25rem)

#### Scenario: Tailwind leading utility works
- **WHEN** a component uses `leading-body` class
- **THEN** it resolves to the `--leading-body` custom property value (1.6)

#### Scenario: Tailwind tracking utility works
- **WHEN** a component uses `tracking-heading` class
- **THEN** it resolves to the `--tracking-heading` custom property value (−0.01em)

## MODIFIED Requirements

### Requirement: Tailwind semantic utility mapping
All semantic tokens SHALL be mapped in `@theme inline` with `--color-` prefix to generate Tailwind utilities (`bg-primary`, `text-muted-foreground`, etc.). Additionally, typography tokens SHALL be mapped with `--text-*`, `--leading-*`, `--tracking-*`, and `--font-weight-*` prefixes.

#### Scenario: Semantic Tailwind utilities work
- **WHEN** a component uses `bg-primary` class
- **THEN** it resolves to the current mode's `--primary` value

#### Scenario: Status Tailwind utilities work
- **WHEN** a component uses `bg-success` or `text-warning-foreground`
- **THEN** Tailwind generates the corresponding CSS

#### Scenario: Typography Tailwind utilities work
- **WHEN** a component uses `text-heading`, `leading-body`, or `tracking-caption`
- **THEN** Tailwind generates the corresponding CSS from typography tokens

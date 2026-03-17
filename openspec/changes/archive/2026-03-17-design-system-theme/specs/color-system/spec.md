## ADDED Requirements

### Requirement: Terracotta palette definition
The system SHALL define a Warm Terracotta palette with 11 steps (50, 100, 200, 300, 400, 500, 600, 700, 800, 900, 950) using OKLCH color space with fixed Hue 38°. All values SHALL match those specified in `docs/design-system-brainstorm.md`.

#### Scenario: Terracotta palette variables exist
- **WHEN** the theme CSS is loaded
- **THEN** CSS variables `--terracotta-50` through `--terracotta-950` are available on `:root`

#### Scenario: Terracotta palette is mode-invariant
- **WHEN** dark mode is active
- **THEN** `--terracotta-500` resolves to the same OKLCH value as in light mode

### Requirement: Warm Gray palette definition
The system SHALL define a Warm Gray palette with 11 steps (50, 100, 200, 300, 400, 500, 600, 700, 800, 900, 950) using OKLCH color space with fixed Hue 60° and low Chroma. All values SHALL match those specified in `docs/design-system-brainstorm.md`.

#### Scenario: Warm Gray palette variables exist
- **WHEN** the theme CSS is loaded
- **THEN** CSS variables `--warm-gray-50` through `--warm-gray-950` are available on `:root`

#### Scenario: Warm Gray palette is mode-invariant
- **WHEN** dark mode is active
- **THEN** `--warm-gray-200` resolves to the same OKLCH value as in light mode

### Requirement: Tailwind utility exposure
The system SHALL expose both palettes as Tailwind CSS utilities via `@theme inline` mapping with `--color-` prefix namespace.

#### Scenario: Terracotta utility classes available
- **WHEN** a component uses `bg-terracotta-500` or `text-terracotta-700`
- **THEN** Tailwind generates the corresponding CSS with the correct OKLCH value

#### Scenario: Warm Gray utility classes available
- **WHEN** a component uses `bg-warm-gray-100` or `text-warm-gray-900`
- **THEN** Tailwind generates the corresponding CSS with the correct OKLCH value

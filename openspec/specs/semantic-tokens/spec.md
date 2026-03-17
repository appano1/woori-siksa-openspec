# Semantic Tokens

## Purpose

Defines the semantic color token layer that maps meaningful names (primary, background, muted, etc.) to raw palette steps, including dark mode remapping, status colors, and Tailwind utility integration.

## Requirements

### Requirement: Semantic tokens reference raw palette
The semantic tokens (`--primary`, `--background`, `--muted`, etc.) SHALL reference raw palette variables via `var()` rather than containing inline OKLCH values.

#### Scenario: Primary references terracotta
- **WHEN** inspecting `--primary` in light mode
- **THEN** it resolves to `var(--terracotta-500)` which equals `oklch(0.65 0.19 38)`

#### Scenario: Background references warm-gray
- **WHEN** inspecting `--background` in light mode
- **THEN** it resolves to `var(--warm-gray-50)` which equals `oklch(0.98 0.005 60)`

### Requirement: Dark mode remaps semantic tokens to different palette steps
The system SHALL switch semantic tokens to appropriate palette steps in dark mode for proper contrast on dark backgrounds. Primary SHALL shift from step 500 to step 400.

#### Scenario: Primary shifts in dark mode
- **WHEN** dark mode is active
- **THEN** `--primary` resolves to `var(--terracotta-400)` instead of `var(--terracotta-500)`

#### Scenario: Background inverts in dark mode
- **WHEN** dark mode is active
- **THEN** `--background` resolves to `var(--warm-gray-950)` and `--foreground` resolves to `var(--warm-gray-50)`

#### Scenario: Border darkens in dark mode
- **WHEN** dark mode is active
- **THEN** `--border` resolves to `var(--warm-gray-700)` instead of `var(--warm-gray-200)`

### Requirement: Status semantic pairs
The system SHALL provide semantic color pairs for success, warning, and info states, each consisting of a background token and a foreground token.

#### Scenario: Success tokens available
- **WHEN** the theme is loaded
- **THEN** `--success` and `--success-foreground` are defined in both light and dark modes

#### Scenario: Warning tokens available
- **WHEN** the theme is loaded
- **THEN** `--warning` and `--warning-foreground` are defined in both light and dark modes

#### Scenario: Info tokens available
- **WHEN** the theme is loaded
- **THEN** `--info` and `--info-foreground` are defined in both light and dark modes

### Requirement: Destructive hue separation
The destructive token SHALL use Hue 27° to be visually distinct from the primary Hue 38°.

#### Scenario: Destructive is distinguishable from primary
- **WHEN** destructive and primary colors are displayed side by side
- **THEN** destructive uses Hue 27° (red-leaning) while primary uses Hue 38° (orange-leaning)

### Requirement: Removed tokens
The system SHALL NOT include chart-1 through chart-5 or any sidebar-* tokens.

#### Scenario: Chart tokens absent
- **WHEN** searching for `--chart-` in theme CSS
- **THEN** no matches are found

#### Scenario: Sidebar tokens absent
- **WHEN** searching for `--sidebar-` in theme CSS
- **THEN** no matches are found

### Requirement: Tailwind semantic utility mapping
All semantic tokens SHALL be mapped in `@theme inline` with `--color-` prefix to generate Tailwind utilities (`bg-primary`, `text-muted-foreground`, etc.).

#### Scenario: Semantic Tailwind utilities work
- **WHEN** a component uses `bg-primary` class
- **THEN** it resolves to the current mode's `--primary` value

#### Scenario: Status Tailwind utilities work
- **WHEN** a component uses `bg-success` or `text-warning-foreground`
- **THEN** Tailwind generates the corresponding CSS

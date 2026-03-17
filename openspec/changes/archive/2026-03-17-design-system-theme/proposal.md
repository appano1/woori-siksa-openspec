## Why

The project currently uses the default shadcn/ui zinc theme (Hue ~310-316°, cool purple-gray), which does not reflect the brand identity defined in `docs/design-system-brainstorm.md`. The brainstorm document specifies Warm Terracotta (Hue 38°) as primary and Warm Gray (Hue 60°) as neutral — a palette designed for a food-focused app that conveys warmth and appetite appeal while differentiating from generic food apps.

## What Changes

- **Replace all color tokens** in `tooling/tailwind/theme.css` with Warm Terracotta and Warm Gray palettes using OKLCH
- **Add raw palette variables** (terracotta-50~950, warm-gray-50~950) as mode-invariant CSS variables exposed as Tailwind utilities (`bg-terracotta-500`, `text-warm-gray-700`, etc.)
- **Remap semantic tokens** (`--primary`, `--background`, `--muted`, etc.) to reference the new raw palette via `var()`
- **Add semantic pairs**: `--success`/`--success-foreground`, `--warning`/`--warning-foreground`, `--info`/`--info-foreground`
- **BREAKING**: Remove `--chart-1~5` and `--sidebar-*` tokens (not currently in use)
- **Redesign dark mode** with palette-based lightness inversion (primary 500→400, neutral steps reversed)

## Capabilities

### New Capabilities
- `color-system`: Raw OKLCH color palettes (terracotta, warm-gray) with 11-step scales (50-950), exposed as both CSS variables and Tailwind utilities
- `semantic-tokens`: Semantic color token mapping (primary, secondary, muted, accent, destructive, success, warning, info) with light/dark mode switching via palette references

### Modified Capabilities

## Impact

- `tooling/tailwind/theme.css` — full rewrite of color definitions
- `apps/tanstack-start/src/styles.css` — may need adjustment for removed sidebar/chart tokens
- `packages/ui/src/*.tsx` — existing components use semantic tokens (`bg-primary`, `text-muted-foreground`) which will automatically pick up new colors; no code changes expected
- Any component currently referencing `chart-*` or `sidebar-*` utilities will break

## Context

The current `tooling/tailwind/theme.css` uses the shadcn/ui default zinc theme with a two-layer CSS variable system (`:root` raw values + `@theme inline` Tailwind mapping). This is a Tailwind v4 project using OKLCH natively. The brainstorm doc (`docs/design-system-brainstorm.md`) defines the target palettes with precise OKLCH values for each step.

The project is a monorepo with `apps/tanstack-start` (web) and `apps/expo` (mobile). The shared `@acme/tailwind-config` package provides the theme consumed by both.

## Goals / Non-Goals

**Goals:**
- Replace all color tokens with brand-aligned Warm Terracotta + Warm Gray palettes
- Expose raw palette as Tailwind utilities for direct use in custom components
- Maintain shadcn/ui component compatibility via semantic token layer
- Provide proper dark mode with palette-based lightness inversion
- Add success/warning/info semantic pairs for common UI states

**Non-Goals:**
- Chart color palette design (deferred until chart feature is needed)
- Sidebar token design (no sidebar planned)
- Typography scale changes (font-family, tracking already configured)
- Spacing or shadow token redesign

## Decisions

### 1. Three-layer CSS variable architecture

**Decision**: Structure theme.css as three distinct layers.

```
Layer 1: :root { --terracotta-500: oklch(...) }     ← raw, mode-invariant
Layer 2: :root { --primary: var(--terracotta-500) }  ← semantic, mode-switching
Layer 3: @theme inline { --color-primary: var(--primary) }  ← Tailwind utility
                        { --color-terracotta-500: var(--terracotta-500) }
```

**Why over flat values**: Referencing palette steps via `var()` makes the relationship between semantic tokens and palette explicit. Changing a palette step propagates automatically. Also enables future runtime theme switching by overriding only the semantic layer.

**Why over single-layer**: Separating raw from semantic allows dark mode to simply re-point semantic tokens to different palette steps without duplicating OKLCH values.

### 2. Raw palette is mode-invariant

**Decision**: `--terracotta-50` through `--terracotta-950` and `--warm-gray-50` through `--warm-gray-950` are defined once in `:root` and never overridden in dark mode.

**Why**: These are design primitives — the color `terracotta-500` is the same color regardless of mode. Only the semantic intent ("what is the primary color?") changes between modes. This matches Radix Themes and Open Props approach.

### 3. Semantic dark mode via palette remapping

**Decision**: Dark mode swaps semantic tokens to different palette steps:

| Token | Light | Dark |
|-------|-------|------|
| --primary | terracotta-500 | terracotta-400 |
| --background | warm-gray-50 | warm-gray-950 |
| --foreground | warm-gray-900 | warm-gray-50 |
| --border | warm-gray-200 | warm-gray-700 |

**Why 500→400 for primary**: Per brainstorm doc principle #3 — one step lighter on dark background for readability. Not 300 (too washed out) or 500 (insufficient contrast on dark bg).

### 4. Destructive/Success/Warning/Info as standalone semantic tokens

**Decision**: These four status colors get only semantic pairs (`--{name}` + `--{name}-foreground`), no raw palette steps.

**Why**: They are used in limited contexts (toast, badge, alert). Full 11-step palettes would add 44 unused variables. Can be promoted to full palettes later if needed.

### 5. Hue separation for destructive

**Decision**: Destructive uses Hue 27° (per brainstorm) vs Primary's Hue 38°.

**Why**: 11° separation is enough to be visually distinguishable in side-by-side UI (e.g., "Save" button next to "Delete" button). Destructive reads as red, Primary as warm orange.

## Risks / Trade-offs

- **[Breaking change]** Removing chart-* and sidebar-* tokens → Mitigated by confirming no current usage. If any component references these, build will surface the error immediately.
- **[OKLCH browser support]** ~92% global support → Acceptable for this project's target audience. No fallback hex values to keep CSS clean.
- **[Warm Gray perception]** Hue 60° at low chroma may appear identical to pure gray on some monitors → Acceptable; the warmth is subtle by design and the brainstorm doc explicitly chose this.
- **[Variable count increase]** Adding 22 raw palette variables (11 terracotta + 11 warm-gray) → Marginal performance impact; CSS variables are lightweight.

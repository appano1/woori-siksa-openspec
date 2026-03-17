## Context

The design system currently defines color palettes and semantic tokens in `tooling/tailwind/theme.css` using CSS custom properties mapped to Tailwind v4's `@theme inline` block. Font is set to Geist Sans — a placeholder that needs to be replaced with Pretendard.

The app is a Korean-language food review platform (TanStack Start + Expo). Typography must handle:
- Korean body text (restaurant descriptions, reviews)
- Numeric scoring (ratings like "4.7")
- Mixed Korean/English metadata (addresses, prices)
- Mobile-first with unified tokens across web and native

## Goals / Non-Goals

**Goals:**
- Define 15 semantic typography tokens with size, line-height, letter-spacing, and weight
- Korean-safe letter-spacing rules (no negative tracking on body text)
- Specialized Score tokens for numeric display
- Toss-inspired minimal weight hierarchy (5 of 9 Pretendard weights)
- Tokens as CSS custom properties following the existing Layer 1→2→3 pattern in theme.css

**Non-Goals:**
- Responsive breakpoint scaling (deferred to future change)
- Pretendard font file hosting/loading strategy (separate concern — CDN link is sufficient for now)
- Component-level typography styles (components will consume tokens)
- Dark mode typography adjustments (typography tokens are mode-invariant)

## Decisions

### 1. Token structure: Composite vs Atomic

**Decision**: Atomic tokens — separate custom properties for each axis (size, LH, tracking, weight).

**Why**: Tailwind v4 utilities map to individual CSS properties. Composite tokens (like a single `--text-heading` shorthand) don't map cleanly to `text-*`, `leading-*`, `tracking-*`, `font-*` utilities. Atomic tokens let developers compose: `text-heading font-bold leading-heading tracking-heading`.

**Alternative considered**: CSS `@font-face` descriptor bundles or utility class presets (e.g., `.text-heading` applying all 4 properties). Rejected because it fights Tailwind's utility-first model and adds a custom abstraction layer.

### 2. Token naming: Flat vs Nested

**Decision**: Flat namespace with role prefix — `--text-heading`, `--leading-heading`, `--tracking-heading`, `--font-weight-heading`.

**Why**: Follows the existing pattern in theme.css where semantic tokens are flat (`--background`, `--foreground`, `--primary`). CSS custom properties don't support nesting. Flat names are also simpler to reference in Tailwind's `@theme` block.

### 3. Score tokens as first-class citizens

**Decision**: Dedicated `score-lg`, `score`, `score-sm` tokens with `line-height: 1.0` and tighter tracking.

**Why**: Food rating app — scores appear on every card, list item, and detail page. Scores are always numeric (no Korean glyphs), so they can safely use tighter tracking (-0.02em) than headings. `line-height: 1.0` eliminates vertical padding that wastes space in score badges/chips.

### 4. Weight constraint: 5 of 9

**Decision**: Only use Regular(400), Medium(500), SemiBold(600), Bold(700), ExtraBold(800).

**Why**: Toss principle — fewer weight choices = more consistent UI. Each weight has a clear semantic role:
- 400: Reading text (Body, Caption)
- 500: Actions and emphasis (Button, Label, Body emphasis, Caption-sm)
- 600: Small headings (Heading-sm, Score-sm)
- 700: Headings and scores (Heading, Display, Score)
- 800: Display-lg only

Weights 100–300 are excluded (poor mobile readability). Weight 900 is excluded (Korean glyphs appear muddy at Black weight).

### 5. Line-height values: Korean-optimized

**Decision**: Body line-height at 1.6 (not the typical English 1.5).

**Why**: Korean glyphs are square-shaped with no ascenders/descenders, making inter-line distinction harder. 1.5 feels cramped for Korean body text; 1.7+ feels too loose for a Toss-like tight aesthetic. 1.6 is the sweet spot validated by Korean typography references.

Headings use 1.15–1.35 (tighter is fine for short Korean text). Score uses 1.0 (numbers only, no inter-line concern).

### 6. CSS architecture: Follow existing layer pattern

**Decision**: Add typography tokens to the same 3-layer structure in theme.css:
- Layer 1 (`:root`): Raw typography values (not needed — typography is not mode-dependent)
- Layer 2 (`:root`): Semantic typography tokens alongside existing color tokens
- Layer 3 (`@theme inline`): Tailwind utility mappings

**Why**: Typography tokens are mode-invariant (no light/dark distinction), so Layer 1 raw values aren't needed. Tokens go directly into Layer 2 as semantic values, then Layer 3 maps them to Tailwind.

## Risks / Trade-offs

**[Korean letter-spacing too conservative]** → The -0.01em heading limit may feel loose compared to English-first design systems. Mitigation: Can be tightened later after visual testing with real Korean content. Starting conservative is safer.

**[15 tokens may be too many]** → Some tokens (body-lg, caption-sm) may go unused. Mitigation: Proposal explicitly plans to prune unused tokens. Cost of having them defined but unused is near zero.

**[Score tokens couple typography to domain]** → "Score" is domain-specific, not a generic design system concept. Mitigation: Acceptable trade-off for a single-product design system. If the system ever becomes generic, score tokens can be renamed to `numeric-*`.

**[Geist Sans → Pretendard switch]** → Any existing UI using Geist Sans will change appearance. Mitigation: No production UI exists yet — the app is in design system definition phase.

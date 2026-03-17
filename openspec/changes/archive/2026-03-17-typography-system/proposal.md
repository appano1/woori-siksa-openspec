## Why

The design system has a color system and semantic tokens defined but no typography rules. Pretendard has been selected as the typeface (documented in `docs/typography-brainstorm.md`), but size scale, line-height, letter-spacing, and weight mapping are undefined. Without these tokens, developers will make ad-hoc typography decisions leading to visual inconsistency across the app. The app targets Korean-language content with significant numeric scoring UI, requiring Korean-aware letter-spacing rules and specialized score typography.

## What Changes

- Define complete typography scale tokens: Display (2), Heading (3), Body (3), Caption (2), Score (3), Action (2) — 15 tokens total
- Define line-height values per token, optimized for Korean text (body LH 1.6, headings tighter)
- Define letter-spacing rules with Korean text protection (body: 0, heading: max -0.01em, display: max -0.02em, caption: positive)
- Define weight mapping using 5 of Pretendard's 9 weights (400/500/600/700/800)
- Switch font-family from Geist Sans to Pretendard in theme.css
- Add typography tokens as CSS custom properties in theme.css
- Map tokens to Tailwind utility classes

## Capabilities

### New Capabilities
- `typography-scale`: Typography size scale, line-height, letter-spacing, and weight tokens for all semantic roles (Display, Heading, Body, Caption, Score, Action)

### Modified Capabilities
- `semantic-tokens`: Adding typography-related semantic tokens (font-family, font-size, line-height, letter-spacing, font-weight) to the existing token system

## Impact

- `tooling/tailwind/theme.css`: Primary file — add typography CSS custom properties and Tailwind mappings
- Font loading: Pretendard must be loaded (CDN or local) — currently using Geist Sans
- All future UI components will consume these tokens
- No breaking changes to existing color/shadow tokens

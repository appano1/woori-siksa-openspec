## 1. Font Family Setup

- [ ] 1.1 Add Pretendard CDN import (or local font files) and update `--font-sans` from Geist Sans to Pretendard with system font fallback stack

## 2. Typography Semantic Tokens

- [ ] 2.1 Add typography CSS custom properties to `:root` in theme.css — font-size tokens (`--text-display-lg` through `--text-label`), all 15 tokens
- [ ] 2.2 Add line-height tokens (`--leading-display-lg` through `--leading-label`), all 15 tokens
- [ ] 2.3 Add letter-spacing tokens (`--tracking-display-lg` through `--tracking-label`), all 15 tokens with Korean-safe values
- [ ] 2.4 Add font-weight tokens (`--font-weight-display-lg` through `--font-weight-label`), all 15 tokens using only 400/500/600/700/800

## 3. Tailwind Utility Mapping

- [ ] 3.1 Map font-size tokens to `@theme inline` with `--text-*` prefix for Tailwind `text-{token}` utilities
- [ ] 3.2 Map line-height tokens to `@theme inline` with `--leading-*` prefix for Tailwind `leading-{token}` utilities
- [ ] 3.3 Map letter-spacing tokens to `@theme inline` with `--tracking-*` prefix for Tailwind `tracking-{token}` utilities
- [ ] 3.4 Map font-weight tokens to `@theme inline` with `--font-weight-*` prefix for Tailwind `font-{token}` utilities

## 4. Cleanup

- [ ] 4.1 Remove old generic tracking tokens (`--tracking-tighter` through `--tracking-widest`) that are replaced by semantic typography tracking tokens
- [ ] 4.2 Verify no dark mode overrides exist for typography tokens (they must be mode-invariant)

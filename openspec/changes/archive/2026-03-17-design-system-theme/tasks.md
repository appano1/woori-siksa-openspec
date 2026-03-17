## 1. Raw Palette Layer

- [x] 1.1 Replace existing `:root` color variables with raw Terracotta palette (--terracotta-50 through --terracotta-950) using OKLCH values from brainstorm doc
- [x] 1.2 Add raw Warm Gray palette (--warm-gray-50 through --warm-gray-950) using OKLCH values from brainstorm doc

## 2. Semantic Token Layer (Light Mode)

- [x] 2.1 Define light mode semantic tokens (--primary, --primary-foreground, --background, --foreground, --card, --card-foreground, --popover, --popover-foreground, --secondary, --secondary-foreground, --muted, --muted-foreground, --accent, --accent-foreground, --border, --input, --ring) referencing raw palette via var()
- [x] 2.2 Define --destructive and --destructive-foreground with Hue 27° OKLCH values
- [x] 2.3 Define --success/--success-foreground, --warning/--warning-foreground, --info/--info-foreground semantic pairs

## 3. Dark Mode Semantic Layer

- [x] 3.1 Define dark mode semantic tokens inside @variant dark block, remapping to appropriate palette steps (primary 500→400, background/foreground inverted, etc.)
- [x] 3.2 Define dark mode destructive, success, warning, info tokens with adjusted lightness for dark backgrounds

## 4. Tailwind Utility Mapping

- [x] 4.1 Add --color-terracotta-* entries in @theme inline for all 11 palette steps
- [x] 4.2 Add --color-warm-gray-* entries in @theme inline for all 11 palette steps
- [x] 4.3 Update semantic --color-* mappings in @theme inline (remove chart-*, sidebar-*, add success/warning/info)
- [x] 4.4 Keep existing non-color tokens (--radius-*, --shadow-*, --font-*, --tracking-*)

## 5. Cleanup and Verification

- [x] 5.1 Remove all chart-1~5 and sidebar-* tokens from both light and dark mode sections
- [x] 5.2 Verify apps/tanstack-start/src/styles.css does not reference removed tokens
- [x] 5.3 Run build to confirm no broken references

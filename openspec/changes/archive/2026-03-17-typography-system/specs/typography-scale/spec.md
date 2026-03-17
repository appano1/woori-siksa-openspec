## ADDED Requirements

### Requirement: Typography scale defines 15 semantic tokens
The system SHALL define typography tokens across 6 roles: Display (2), Heading (3), Body (3), Caption (2), Score (3), Action (2). Each token SHALL specify font-size, line-height, letter-spacing, and a primary font-weight.

#### Scenario: All 15 tokens are defined
- **WHEN** the theme CSS is loaded
- **THEN** the following tokens are available: `display-lg`, `display`, `heading-lg`, `heading`, `heading-sm`, `body-lg`, `body`, `body-sm`, `caption`, `caption-sm`, `score-lg`, `score`, `score-sm`, `button`, `label`

#### Scenario: Each token has all four axes
- **WHEN** inspecting any typography token (e.g., `heading`)
- **THEN** CSS custom properties exist for its size (`--text-heading`), line-height (`--leading-heading`), letter-spacing (`--tracking-heading`), and weight (`--font-weight-heading`)

### Requirement: Display tokens for large decorative text
The system SHALL define display-lg as 32px/1.15/−0.02em/ExtraBold(800) and display as 28px/1.2/−0.02em/Bold(700).

#### Scenario: Display-lg values
- **WHEN** inspecting display-lg token
- **THEN** font-size is 32px (2rem), line-height is 1.15, letter-spacing is −0.02em, font-weight is 800

#### Scenario: Display values
- **WHEN** inspecting display token
- **THEN** font-size is 28px (1.75rem), line-height is 1.2, letter-spacing is −0.02em, font-weight is 700

### Requirement: Heading tokens for section titles
The system SHALL define heading-lg as 24px/1.3/−0.01em/Bold(700), heading as 20px/1.3/−0.01em/Bold(700), and heading-sm as 17px/1.35/−0.01em/SemiBold(600).

#### Scenario: Heading-lg values
- **WHEN** inspecting heading-lg token
- **THEN** font-size is 24px (1.5rem), line-height is 1.3, letter-spacing is −0.01em, font-weight is 700

#### Scenario: Heading values
- **WHEN** inspecting heading token
- **THEN** font-size is 20px (1.25rem), line-height is 1.3, letter-spacing is −0.01em, font-weight is 700

#### Scenario: Heading-sm values
- **WHEN** inspecting heading-sm token
- **THEN** font-size is 17px (1.0625rem), line-height is 1.35, letter-spacing is −0.01em, font-weight is 600

### Requirement: Body tokens optimized for Korean readability
The system SHALL define body-lg as 16px/1.6/0/Regular(400), body as 14px/1.6/0/Regular(400), and body-sm as 13px/1.55/0/Regular(400). Body tokens MUST have letter-spacing of exactly 0.

#### Scenario: Body base values
- **WHEN** inspecting body token
- **THEN** font-size is 14px (0.875rem), line-height is 1.6, letter-spacing is 0, font-weight is 400

#### Scenario: Body letter-spacing is zero
- **WHEN** inspecting any body token (body-lg, body, body-sm)
- **THEN** letter-spacing is exactly 0em

### Requirement: Caption tokens with positive tracking for small text legibility
The system SHALL define caption as 12px/1.45/+0.01em/Regular(400) and caption-sm as 11px/1.45/+0.012em/Medium(500). Small Korean text MUST use positive letter-spacing to maintain readability.

#### Scenario: Caption values
- **WHEN** inspecting caption token
- **THEN** font-size is 12px (0.75rem), line-height is 1.45, letter-spacing is +0.01em, font-weight is 400

#### Scenario: Caption-sm values
- **WHEN** inspecting caption-sm token
- **THEN** font-size is 11px (0.6875rem), line-height is 1.45, letter-spacing is +0.012em, font-weight is 500

### Requirement: Score tokens for numeric display with tight line-height
The system SHALL define score-lg as 24px/1.0/−0.02em/Bold(700), score as 20px/1.0/−0.02em/Bold(700), and score-sm as 16px/1.0/−0.015em/SemiBold(600). Score tokens SHALL use line-height 1.0 to minimize vertical padding around numbers.

#### Scenario: Score base values
- **WHEN** inspecting score token
- **THEN** font-size is 20px (1.25rem), line-height is 1.0, letter-spacing is −0.02em, font-weight is 700

#### Scenario: Score line-height is 1.0
- **WHEN** inspecting any score token (score-lg, score, score-sm)
- **THEN** line-height is exactly 1.0

### Requirement: Action tokens for buttons and labels
The system SHALL define button as 14px/1.0/0/Medium(500) and label as 13px/1.45/0/Medium(500).

#### Scenario: Button values
- **WHEN** inspecting button token
- **THEN** font-size is 14px (0.875rem), line-height is 1.0, letter-spacing is 0, font-weight is 500

#### Scenario: Label values
- **WHEN** inspecting label token
- **THEN** font-size is 13px (0.8125rem), line-height is 1.45, letter-spacing is 0, font-weight is 500

### Requirement: Weight hierarchy uses exactly 5 of 9 Pretendard weights
The system SHALL use only Regular(400), Medium(500), SemiBold(600), Bold(700), and ExtraBold(800). Weights 100, 200, 300, and 900 SHALL NOT be referenced by any typography token.

#### Scenario: No token uses excluded weights
- **WHEN** inspecting all typography token weight values
- **THEN** no token references font-weight 100, 200, 300, or 900

### Requirement: Korean letter-spacing safety rules
Negative letter-spacing SHALL NOT exceed −0.01em for text tokens that may contain Korean characters (Heading). Negative letter-spacing up to −0.02em is permitted only for Display tokens (28px+) and Score tokens (numeric-only). Body and Caption tokens MUST NOT use negative letter-spacing.

#### Scenario: Heading tracking within Korean-safe limit
- **WHEN** inspecting heading-lg, heading, or heading-sm letter-spacing
- **THEN** the value is −0.01em (not more negative)

#### Scenario: Body tracking is non-negative
- **WHEN** inspecting body-lg, body, or body-sm letter-spacing
- **THEN** the value is 0em

#### Scenario: Caption tracking is positive
- **WHEN** inspecting caption or caption-sm letter-spacing
- **THEN** the value is positive (> 0em)

### Requirement: Font family is Pretendard
The system SHALL set the primary font-family to Pretendard with appropriate fallbacks. The fallback stack SHALL include system fonts for graceful degradation.

#### Scenario: Font family declaration
- **WHEN** inspecting the `--font-sans` token
- **THEN** the value starts with "Pretendard" followed by system font fallbacks

### Requirement: Typography tokens are mode-invariant
Typography tokens SHALL NOT change between light and dark modes. Size, line-height, letter-spacing, and weight values MUST remain identical in both modes.

#### Scenario: Tokens unchanged in dark mode
- **WHEN** dark mode is active
- **THEN** all typography token values are identical to their light mode values

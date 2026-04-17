# Pura Health Design Tokens

Design tokens for the Pura Health mobile app. Source of truth is the Figma Design System — this repo reflects the current token state for development handoff.

## Table of contents

- [Files](#files)
- [Token architecture](#token-architecture)
- [Color groups](#color-groups)
  - [Surface](#surface)
  - [Content](#content)
  - [Border](#border)
  - [Health status](#health-status)
  - [Digital Twin](#digital-twin)
  - [Feature-scoped](#feature-scoped)
- [Reference format](#reference-format)
- [Docs](#docs)

---

## Files

| File | Contents |
|---|---|
| `primitives.json` | Color scales, unit steps, type ramp, font families, font weights, font sizes, line heights, letter spacing |
| `semantics.json` | Semantic colors (surface, content, border, health, AI, fitcoin, digital-twin), spacing, radius, border weight |
| `components.json` | Component-specific tokens (Badge, Button, Card, Chart, Input, etc.) |
| `text-styles.json` | Composite typography tokens (Display, Heading, Body, Label) |
| `effects.json` | Shadows, gradients, and blur effects |
| `motion.json` | Easing curves, durations, and delays with iOS/Android platform values |

## Token architecture

```
Primitives          →  Semantics           →  Components
color.primitive.*      surface/*, content/*    Badge/*, Button/*, etc.
unit.primitive.*       health/*, ai/*          Card/*, Input/*, etc.
text.primitive.*       spacing.*, radius.*
```

Primitives are raw values. Semantics assign meaning. Components reference semantics (or primitives when no semantic fits).

## Color groups

### Surface

| Group | Purpose |
|---|---|
| `surface/default` | Neutral app backgrounds and structural surfaces (white, sage) |
| `surface/brand` | Brand-colored surfaces for user selection, active states, and guided emphasis — not for branding, but for primary indicators of choice, states, and important emphasis |
| `surface/positive` | Generic system success/completion status — context-agnostic, like a "green light" |
| `surface/negative` | Generic system error/danger status — context-agnostic, like a "red light" |
| `surface/overlay` | Scrim and dimming layers for modals and backdrops |
| `surface/tint` | Translucent black fills on light backgrounds (subtle/muted/soft/medium) |
| `surface/tint/inverse-*` | Translucent white fills on dark or brand backgrounds |

### Content

| Group | Purpose |
|---|---|
| `content/default` | Standard text and icon colors — the "ink on paper" for foreground elements |
| `content/brand` | Text and icons on brand-colored surfaces |
| `content/positive` | Text and icons for generic success/confirmation states |
| `content/negative` | Text and icons for generic error/danger states |

### Border

| Group | Purpose |
|---|---|
| `border/default` | Structural boundaries, dividers, and linear indicators |
| `border/brand` | Brand-colored borders and outlines |

### Health status

| Group | Purpose |
|---|---|
| `health/positive` | Contextual status range — positive end. Used for task completion, health meters, dataviz, goal progress — any UI with a status spectrum |
| `health/neutral` | Contextual status range — middle. Incomplete, in-progress, or baseline states |
| `health/negative` | Contextual status range — negative end. At-risk, behind, or unhealthy states |

### Digital Twin

| Group | Purpose |
|---|---|
| `digital-twin/great` | 5-tier physical health status — best (aliases health/positive) |
| `digital-twin/good` | 5-tier physical health status — above average (unique green scale) |
| `digital-twin/neutral` | 5-tier physical health status — baseline (aliases health/neutral) |
| `digital-twin/warning` | 5-tier physical health status — below average (unique orange-red scale) |
| `digital-twin/bad` | 5-tier physical health status — worst (aliases health/negative) |

### Feature-scoped

| Group | Purpose |
|---|---|
| `ai/*` | Reserved for Pura Agent and AI-related surfaces, icons, and UI |
| `fitcoin/*` | Reserved as theme colors for the Fitcoin feature |

## Reference format

- Semantic colors: `{Light.surface.brand.default}`
- Color primitives: `{color.primitive.mist.blue.500}`
- Spacing/radius: `{spacing.md}`, `{radius.lg}`
- Unit primitives: `{unit.primitive.05}`
- Text primitives: `{text.primitive.font.size.font-size-300}`

## Docs

- **[DS-GUIDELINES.md](DS-GUIDELINES.md)** — Token descriptions, component conventions, naming rules, usage philosophy
- **[MOTION.md](MOTION.md)** — Motion token reference (easing, duration, delay)

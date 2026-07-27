# Pura Health Design System — Guidelines

> Design system conventions, token philosophy, and component rules for the Pura Health Design System. This document serves as a knowledge base for anyone working with or contributing to the system.

---

## 1. Token Descriptions

### Primitives
- **No descriptions needed.** Primitive tokens (color scales, unit steps, type ramp) are self-explanatory by their naming.

### Semantic Colors
- Every semantic color token should have a description.
- Format: Start with what the token is and its emphasis level, then its intended use context.
- Do **not** include specific component examples in descriptions — those are subject to change.
- Use intensity language that matches the ramp step name (e.g. "at medium emphasis", "at soft intensity", "at lowest intensity").
- Pressed state descriptions follow: `"Pressed state of {base token name}."`

**Examples:**
```
surface/brand/default → "Primary brand surface for high-emphasis interaction states and prominent UI surfaces."
health/positive/medium → "Positive health status color in medium emphasis. Used for health status UI elements and surfaces where the state is 'Positive, Good, or Healthy.'"
surface/tint/soft → "Translucent dark surface at soft intensity on light backgrounds."
```

### Component Tokens
- Format: `"Reserved for [Component]'s [what it does]."`
- Example: `"Reserved for Badge's neutral tone surface fill."`

### Text Tokens
- **Type ramp, font-size, line-height, letter-spacing primitives:** No descriptions needed.
- **Semantic text tokens** (reserved for text styles): Follow the component token pattern — `"Reserved for [Text Style Category]'s [size] [property]."`

---

## 2. Component Descriptions

- Lead with the **component name** exactly as it appears in Figma.
- **1–2 sentences max.** Plain text only — no markdown, no bullet points, no headers.
- Say what the component **is**, not "Used to..." or "A reusable component for..."
- Mention key context if the component is scoped to a specific screen or always paired with another component.
- Mention structural variants if they differ significantly in layout.
- Don't describe every property — descriptions are for orientation, not exhaustive API docs.
- **Never use `**bold**` via the plugin API** — it renders as literal asterisks. Bold can only be applied manually in the Figma UI.
- **Never touch private `_` component descriptions.**
- **Never leave template placeholder text** in descriptions.

**Example:**
```
Badge displays a short status label with color-coded tone: Positive, Negative, Neutral, or Informational.
```

---

## 3. Which Tokens to Use When

### Color Token Groups

| Group | Purpose | When to use |
|-------|---------|-------------|
| `surface/brand/*`, `content/brand/*` | Primary brand colors (mist blue) | User selection, active states, highlighted elements, guiding emphasis. **Not for branding** — for primary indicators of choice, states, and important emphasis. |
| `surface/default/*`, `content/default/*` | Neutral surfaces and text | Application backgrounds, standard text, borders, structural hierarchy. |
| `surface/positive/*`, `content/positive/*` | Generic system status (success) | Context-agnostic success/completion signals — like "green light." Few use cases currently. |
| `surface/negative/*`, `content/negative/*` | Generic system status (error/danger) | Context-agnostic error/danger signals — like "red light." Input validation, error states. |
| `health/positive/*` | Contextual status — positive | Status indicators with a range (positive/neutral/negative). Used for task completion, health meters, dataviz, goal progress — any UI with a status spectrum. |
| `health/neutral/*` | Contextual status — neutral | Middle of the status range. Incomplete, in-progress, or baseline states. |
| `health/negative/*` | Contextual status — negative | Negative end of the status range. At-risk, behind, or unhealthy states. |
| `digital-twin/*` | Granular physical health status | 5-tier scale (great/good/neutral/warning/bad) for biomarker chips and physical health indicators. Most specific status scale. |
| `ai/*` | AI/Pura Agent scoped | Reserved for AI-related surfaces, icons, and UI. Rose clay + warm sand palette. |
| `fitcoin/*` | Fitcoin feature scoped | Reserved as theme colors for the Fitcoin feature. |
| `surface/tint/*` | Translucent surface fills | Translucent black/white fills **on component surfaces** (badge fills, toggle tracks, chart tracks). Not for overlays, not for borders. |
| `surface/overlay/*` | Scrim/dimming layers | Modal backdrops, dimmed UI states — layers that cover content underneath. |
| `content/*` | Ink on paper | Text, icons, and other foreground elements. Think of it as the "ink" — applies to anything drawn on top of a surface, not just text. |
| `border/*` | Borders, dividers, and linear indicators | Structural boundaries, separators, and linear elements like carousel indicator dots. Not limited to literal borders — it's about the **intention** of a linear/boundary element. |

### Color Scope Hierarchy

```
surface/positive + negative        → Generic system status (success/error)
health/positive + neutral + negative → Contextual status range (tasks, health, dataviz)
digital-twin/great + good + neutral + warning + bad → Granular physical health biomarkers (5-tier)
```

### Token Routing Rules
- **Semantic tokens should be used whenever possible** on component layers.
- Component-specific tokens (like Badge surface colors) exist to provide a curated set of standard options for consistency — so designers don't have to guess.
- Component tokens can reference primitives directly if no appropriate semantic token exists.
- Once multiple component tokens share the same primitive value, consider promoting it to a semantic token.

### Tokens are about intention, not rigid rules
Token groups are defined by **semantic intention**, not strict usage categories. `content/*` is "ink on paper" — text, icons, or anything acting as foreground. `border/*` can be used for linear indicators like carousel dots, not just literal borders. Choose tokens based on how you want to **tie semantics across different use cases**, not by what the element technically is.

### Note on `surface/positive` vs `health/positive`
These are currently kept separate for flexibility. `health/*` is for contextual status ranges. `surface/positive` and `surface/negative` are simpler system-level status colors. Consolidation may happen in the future but is not decided.

---

## 4. Component Guidelines

### Token Usage on Layers
- Use semantic tokens whenever possible.
- Component-specific tokens provide curated standard options (e.g. Badge surface colors, Chart track colors) for consistency.
- If no semantic or component token fits, fall back to primitives — but flag it for potential promotion later.

### Private vs Published Components
- **Private by default** (`_ComponentName`) until proven reusable.
- A component should be private if its scope is limited to a specific parent or context.
- Example: A chart built for a specific card — keep it private under the parent scope until other contexts need it.
- DS designers can promote private components to public when reuse needs arise.

### Slots
- Use slots for **custom, one-off compositions** where content varies.
- **Don't use slots** for reusable or repeatable patterns — create a structured component instead.
- When creating a reusable card, use Card Container as a starting point, then detach and define a structured component with fixed layout.
- Badge uses a slot for icons to allow free icon sizing within the badge.

### Page Scoping
- Each component gets its **own page** unless it's tied to a specific parent scope.
- A page sets the scope — everything on a page implies it's built for that context.
- Example: "Primary Card" page contains multiple sub-components all scoped to Primary Card.
- If a scoped component gets used often elsewhere, pull it out to its own page.

---

## 5. Component Naming Conventions

### General
- Always **capitalize the first letter** of each word: `Health Stats Card`, not `health stats card`.
- Multi-word names use spaces: `Star Rating Input`, not `StarRatingInput`.

### Private Components
- Prefix with underscore: `_ComponentName`
- Keeps them unpublished from the library.
- Sub-components follow the same rule: `_Leaderboard List Item`

### Scoping with `/`
- Use `/` to set explicit scope when a component name sounds universal but is context-specific.
- Pattern: `Parent Name / Child Name`
- Example: `Historic Data Card / Charts / HBA1C Trend` — explicitly scoped to Historical Data Card.
- This prevents confusion about whether a component is universally reusable.

### Variant Property Naming

| Property | Values | Notes |
|----------|--------|-------|
| `Variant` | Context-specific | General variant toggle |
| `Configuration` | Context-specific | Structural configuration |
| `Color` | `On Surface-Default` / `On Surface-Secondary` | Surface context |
| `Context` | `Default` / `Inverse` / `On Image` | Background context |
| `Size` | `xxSmall` / `xSmall` / `Small` / `Medium` / `Large` / `xLarge` / `xxLarge` | Always capitalize first letter |
| `Tone` | `Default` / `Positive` / `Negative` / `Neutral` / `Warning` / `Good` / `Bad` | Status tone |

### Element Naming

| Element | Naming |
|---------|--------|
| Icons | `Start Icon`, `End Icon` |
| Assets | `Leading Asset`, `Trailing Asset` |
| Stacked text | `Primary Text`, `Secondary Text`, `Tertiary Text` |

### Figma Property Types

| Property type | Naming pattern | Example |
|---------------|---------------|---------|
| Text (string) | `XXXX Text` | `Label Text`, `Supporting Text` |
| Instance swap | `XXXX Type` | `Leading Asset Type` |
| Boolean (toggle) | Reserved for show/hide only | `Start Icon`, `End Icon` (toggles visibility) |

**Important:** Boolean properties are **only** for toggling element visibility (show/hide). Never use them for non-visual state changes (e.g. `active: true/false`).

---

## 6. Text Style Usage

### Body vs Label

| Style | Font | Purpose | Examples |
|-------|------|---------|----------|
| **Body** | Noto Sans (font-secondary) | Supporting text, descriptions, explanations — the **descriptor** | Paragraphs, helper text, card descriptions, error messages |
| **Label** | Greycliff CF (font-default) | Identifiers, labels, titles of an object — the **identifier** | Button labels, input labels, tab names, chip text, list item titles |

This is the rule of thumb. There are exceptions, but when in doubt: if the text **names or identifies** something, use Label. If the text **describes or explains** something, use Body.

Both come in Large/Medium/Small/xSmall sizes. Body has Medium and SemiBold weights. Label uses Medium weight only.

---

## 7. Design Token Architecture

### Token Chain
```
Primitives (Level 1)  →  Semantic (Level 2/3)  →  Component (Level 3/4)
color.primitive.*         surface/*, content/*,      Badge/*, Button/*, etc.
unit.primitive.*          health/*, ai/*, etc.
text.primitive.*          spacing.*, radius.*, etc.
```

### When to Create Tokens

| Scenario | Action |
|----------|--------|
| Color doesn't fit any semantic token | Create a **component token** referencing the primitive |
| Multiple component tokens share the same value | Promote to a **semantic token** (like surface/tint was created) |
| Value is clearly universal from the start | Create a **semantic token** directly |
| Value needs curated standard options for consistency | Create **component tokens** aliasing the semantic (like Badge surface colors) |

### Semantic tokens can be skipped
- Component tokens **can** reference primitives directly — semantic layer is not mandatory.
- Assign semantic tokens to component tokens when you want a **consistency layer** — a curated set of standard options so designers don't have to guess for similar use cases.

### Ramp Prominence Order
All token groups follow the same intensity scale:

```
strong > default > medium > soft > muted > subtle
```

With optional pressed states: `{name}-pressed`

### Token JSON Sync

**Figma is the source of truth.** JSON files reflect Figma state, not the other way around.

**Repo:** `humayd-pura/pura-design-tokens`

These tokens are for a **mobile app** (iOS and Android). The JSON format is optimized for mobile consumption.

**Files (6):**

| File | Contents |
|---|---|
| `primitives.json` | Color scales, unit steps, type ramp, font families, weights, sizes, line heights, letter spacing |
| `semantics.json` | Semantic colors, spacing, radius, border weight |
| `components.json` | Component-specific tokens |
| `text-styles.json` | Composite typography tokens |
| `effects.json` | Shadows, gradients, blurs, and other visual effects — this file may grow to include additional effect types in the future |
| `motion.json` | Easing, duration, delay with platform values |

**JSON format rules:**

- 2-space indentation
- **Flat structure** — no nesting. Each token is a top-level key with a dot-separated name (e.g. `"component.badge.surface-tint"`). This was chosen as the optimal format for mobile consumption. Strictly follow this pattern.
- Field order: `$type`, `$description` (if exists), `$value`
- Only include `$description` if the token has a description in Figma — never fabricate
- No trailing commas
- **Order tokens intuitively within each file** — follow natural hierarchy: primary → secondary → tertiary, strong → default → medium → soft → muted → subtle, large → medium → small → xsmall. Keep related tokens grouped together.

**Reference format by token type:**

| Type | Format | Example |
|---|---|---|
| Semantic colors | `{Light.[group].[name]}` | `{Light.surface.brand.default}` |
| Color primitives | `{color.primitive.[scale].[step]}` | `{color.primitive.mist.blue.500}` |
| Unit primitives | `{unit.primitive.[step]}` | `{unit.primitive.05}` |
| Text primitives | `{text.primitive.[group].[name]}` | `{text.primitive.font.size.font-size-300}` |
| Spacing | `{spacing.[size]}` | `{spacing.md}` |
| Radius | `{radius.[size]}` | `{radius.lg}` |

**Naming conventions in JSON:**

| Figma collection | JSON prefix | Example |
|---|---|---|
| Color Primitive | `color.primitive.*` | `color.primitive.sage.200` |
| Color (semantic) | `Light.*` | `Light.surface.tint.soft` |
| Components | `component.*` | `component.badge.surface-tint` |
| Text Primitive | `text.primitive.*` | `text.primitive.font.size.font-size-300` |
| Text (semantic) | `text.*` | `text.label.font-large` |
| Typography (text styles) | `typography.*` | `typography.label.medium` |
| Spacing | `spacing.*` | `spacing.md` |
| Radius | `radius.*` | `radius.lg` |
| Border Weight | `border.weight.*` | `border.weight.default` |
| Effects | `shadow/*`, `gradient/*`, `blur/*`, `effect/*` | `gradient/ai.icon.surface` |
| Motion | `motion.*` | `motion.easing.ease-out` |

---

## 8. Card System

### Card Types

There are 5 card types in the Pura design system:

| Type | Primary content | User's job | Trigger |
|------|----------------|-----------|---------|
| **Data Card** | Metrics, stats, charts | Read / monitor | On load or scheduled |
| **Action Card** | CTA, task, prompt | Do something | Goal state or task detection |
| **Discovery Card** | Tips, education, content | Learn / explore | Algorithmic or editorial |
| **Record Card** | A logged entry or item | Review / manage | Explicit user action (log, create) |
| **Contextual Card** | Explanation of health context | Understand why | Health state change detection |

### Classification Rubric

Use these 3 questions in order to classify any card:

**Q1 — What is the primary content type?**
Choose the type whose content definition best matches what the card displays. This answers the question in most cases.

**Q2 — What is the user's primary job? (tiebreaker)**
If Q1 is ambiguous between two types, ask what the user is supposed to *do* with this card. Contextual = understand why. Action = do something. Data = read/monitor. Discovery = learn. Record = review/manage.

**Q3 — What triggers the card?**
Use this as a final tiebreaker or sanity check. Health state change → Contextual. Goal/task detection → Action. Scheduled/load → Data. Algorithmic → Discovery. User action → Record.

### Classification Logic

- **2-of-3 agreement** across the questions = that type wins.
- **Q2 as ultimate tiebreaker** if still tied after all three questions.
- **Log ambiguous decisions** in the Cards/Decisions section of your working notes.
- If **3+ cards of the same type** don't fit well, propose a new type rather than forcing a fit.

### Naming Convention

Cards are named by **content or function** — never by location, hierarchy, or screen.

Pattern: `[Content or Function] Card`

Examples:
- `Primary Card` → describes the card's prominence/function ✓
- `Home Card` → named by location ✗
- `Top Card` → named by hierarchy ✗

Sub-components follow scoped naming:
`[Card Name] / [Sub-component Name]`

Example: `Primary Card / Description`

### Example Classification

**Primary Card / Description**
- Content: Explanation of health context ("These actions target your recent late-night spikes.")
- User's job: Understand *why* these actions are relevant
- Trigger: Health state change detection

→ **Contextual Card**

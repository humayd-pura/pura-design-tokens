# Statuses

> Color-coded status chip for communicating a health status tone. Scoped to the digital twin health scale.

---

## Description

Statuses is a color-coded chip indicating a health status tone across a five-tier scale: Great, Good, Neutral, Warning, and Bad, with an additional Locked state.

---

## Properties

| Property | Values |
|---|---|
| `Tone` | `Great` / `Good` / `Neutral` / `Warning` / `Bad` / `Locked` |

---

## Token Usage

Each tone applies tokens to two layers: the **chip surface** (background fill) and the **label + icon** (foreground ink).

| Tone | Chip Surface | Label & Icon |
|---|---|---|
| Great | `digital-twin/great/muted` | `content/brand/secondary` |
| Good | `digital-twin/good/muted` | `digital-twin/good/strong` |
| Neutral | `digital-twin/neutral/muted` | `health/neutral/strong` |
| Warning | `digital-twin/warning/muted` | `digital-twin/warning/strong` |
| Bad | `surface/negative/faint` | `digital-twin/bad/strong` |
| Locked | `Badge/surface-default` | `content/default/tertiary` |

**Notes:**
- All active tones use the `muted` ramp for the chip surface — keeping the background soft so the label carries the emphasis.
- `Bad` uses `surface/negative/faint` instead of `digital-twin/bad/muted`. This is intentional — the negative semantic token was chosen to align Bad with generic system danger signals at this intensity.
- `Locked` uses no digital-twin tokens. It uses the neutral Badge surface and tertiary text color — it is not a health status, it is an access state.
- Icon fill mirrors the label fill on all tones.

---

## Scale Reference

The five active tones map to the digital-twin 5-tier scale:

```
Great     → Best physical health status
Good      → Above average
Neutral   → Baseline / no signal
Warning   → Below average / at risk
Bad       → Worst / unhealthy
```

This is a more granular scale than `health/*` (3-tier: positive / neutral / negative). Use Statuses when a 5-tier range is needed — typically for biomarker chips, physical health indicators, and digital twin UI.

Use `health/*` tokens (and other components) when a 3-tier contextual range is sufficient — task completion, goal progress, general status meters.

---

## Rules

- Always use the `Tone` property — never override chip surface or label fills manually.
- Use `Great` for optimal range, `Good` for above average, `Neutral` for baseline, `Warning` for at-risk, and `Bad` for unhealthy states.
- `Locked` is not a health tone. Use it only when the status is unavailable due to access restrictions, missing data, or a feature being locked — not as a substitute for `Neutral`.
- Do not use Statuses for system-level success or error states. Those belong to components using `surface/positive` and `surface/negative` tokens (e.g. Badge with Positive/Negative tone).
- Do not substitute `health/*` tones. Statuses is scoped to the `digital-twin/*` scale. If a 3-tier range is sufficient, reconsider whether Statuses is the right component.

---

## Scenarios

| Scenario | Tone |
|---|---|
| Biomarker is within optimal range | `Great` |
| Biomarker is above average but not optimal | `Good` |
| Biomarker is at baseline with no meaningful deviation | `Neutral` |
| Biomarker is trending toward risk | `Warning` |
| Biomarker is in an unhealthy range | `Bad` |
| Biomarker data is unavailable or feature is locked | `Locked` |
| User has not yet completed the relevant assessment | `Locked` |

---

## Sub-components

Statuses has no scoped sub-components.

---

## Amendments

| Date | Change | Reason |
|---|---|---|
| 2026-05 | Renamed from `Biomarker Chip` to `Statuses` | Scope broadened beyond biomarkers to cover any digital twin health status indicator |

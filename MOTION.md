# Motion Tokens

> Curated set of duration, delay, and easing tokens for the Pura Health app. Derived from 8 motion spec pages in the Documentation file.

---

## Easing

| Token | Value |
|-------|-------|
| `motion.easing.ease-out` | `cubic-bezier(0.33, 0.00, 0.25, 1.00)` |
| `motion.easing.ease-in` | `cubic-bezier(0.75, 0.00, 0.67, 1.00)` |

### Platform usage

**iOS**
```swift
// ease-out
CAMediaTimingFunction(controlPoints: 0.33, 0.00, 0.25, 1.00)

// ease-in
CAMediaTimingFunction(controlPoints: 0.75, 0.00, 0.67, 1.00)
```

**Android (Kotlin)**
```kotlin
// ease-out
PathInterpolator(0.33f, 0.0f, 0.25f, 1.0f)

// ease-in
PathInterpolator(0.75f, 0.0f, 0.67f, 1.0f)
```

---

## Duration

| Token | Value |
|-------|-------|
| `motion.duration.200` | 200ms |
| `motion.duration.300` | 300ms |
| `motion.duration.500` | 500ms |
| `motion.duration.700` | 700ms |
| `motion.duration.1000` | 1000ms |

---

## Delay

| Token | Value |
|-------|-------|
| `motion.delay.50` | 50ms |
| `motion.delay.100` | 100ms |
| `motion.delay.150` | 150ms |

---

## Quick reference

```
Easing
  ease-out   (0.33, 0.00, 0.25, 1.00)
  ease-in    (0.75, 0.00, 0.67, 1.00)

Duration
  200ms
  300ms
  500ms
  700ms
  1000ms

Delay
  50ms
  100ms
  150ms
```

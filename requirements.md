# Requirements — Super Calculator

Tasks the student needs to complete to finish the calculator.  
All work lives in `src/app/app.component.ts` and `src/app/app.component.spec.ts`.

---

## Part 1 — Implement the missing methods

### Exercise 1 — Toggle Sign (`pressToggleSign`)

**File:** `src/app/app.component.ts` — method `pressToggleSign()`  
**Button:** `+/-`

#### What it should do
Flip the sign of the number currently shown on the display.

| Display before | Display after   |
|----------------|-----------------|
| `5`            | `-5`            |
| `-3`           | `3`             |
| `0`            | `0` (no change) |

#### Steps
1. Convert `this.display` from a string to a number (`parseFloat`).
2. Multiply by `-1`.
3. Assign the result back to `this.display` as a string (`.toString()`).
4. Edge case: if the result is `0`, keep the display as `'0'` (avoid `-0`).

---

### Exercise 2 — Percent (`pressPercent`)

**File:** `src/app/app.component.ts` — method `pressPercent()`  
**Button:** `%`

#### What it should do
Convert the displayed number into its percentage equivalent (divide by 100).

| Display before | Display after |
|----------------|---------------|
| `50`           | `0.5`         |
| `200`          | `2`           |
| `1`            | `0.01`        |

#### Steps
1. Convert `this.display` from a string to a number (`parseFloat`).
2. Divide by `100`.
3. Assign the result back to `this.display` as a string (`.toString()`).

---

### Exercise 3 — Light/Dark Theme Toggle (`toggleTheme`)

**Files:**
- `src/app/app.component.ts` — method `toggleTheme()`
- `src/app/app.component.css` — light mode CSS rules

**Button:** `🌙 Dark / ☀️ Light` (top-right corner)

#### What it should do
Switch the UI between dark mode (default) and light mode each time the button is clicked.

| `isLightMode` before | `isLightMode` after | Button label |
|----------------------|---------------------|--------------|
| `false`              | `true`              | `☀️ Light`   |
| `true`               | `false`             | `🌙 Dark`    |

#### Step 1 — implement `toggleTheme()` in `app.component.ts`
Flip `this.isLightMode` to its opposite value using the `!` (NOT) operator.  
The template already binds `[class.light]="isLightMode"` so the CSS updates automatically.

#### Step 2 — fill in the light mode CSS in `app.component.css`
The selectors are already there with `TODO` comments. Choose colors that make the calculator readable on a light background. Suggested values to get started:

| Selector | Property to set | Suggested value |
|---|---|---|
| `:host.light` | `background` | `#f0f0f0` |
| `.calculator.light` | `background` | `#ffffff` |
| `.calculator.light .display` | `background` / `color` | `#e0e0e0` / `#1a1a1a` |
| `.calculator.light .btn` | `background` / `color` | `#d4d4d4` / `#1a1a1a` |
| `.calculator.light .btn--utility` | `background` / `color` | `#c0c0c0` / `#333333` |

---

## Part 2 — Write the missing unit tests

**File:** `src/app/app.component.spec.ts`  
Each test marked `🎯 YOUR TURN` has a `pending(...)` call as a placeholder.  
Remove the `pending(...)` line and replace it with real assertions.  
Run tests with `npm test` to see which pass.

### Display tests

| Test description | Line | Hint |
|------------------|------|------|
| Should handle multi-digit numbers | ~62 | Call `pressDigit` twice, check display shows `'12'` |
| Should append a decimal point when `.` is pressed | ~67 | Press a digit then `.`, check display contains `'.'` |
| Should not allow more than one decimal point | ~73 | Press `.` twice, check display does not contain `'..'` |

### Clear tests

| Test description | Line | Hint |
|------------------|------|------|
| Should cancel any pending operation when C is pressed | ~90 | After clearing, check `component.firstOperand === null` and `component.operator === null` |

### Arithmetic tests

| Test description | Line | Hint |
|------------------|------|------|
| Should subtract two numbers correctly (9 − 4 = 5) | ~114 | Follow the same pattern as the addition test above it |
| Should return a negative result when the difference is negative (3 − 7) | ~119 | Expected display: `'-4'` |
| Should multiply two numbers correctly (6 × 7 = 42) | ~126 | Use operator `'*'` |
| Should return a decimal when division is not exact (7 ÷ 2 = 3.5) | ~158 | Expected display: `'3.5'` |
| Should chain operations without pressing `=` (2 + 3 * 4 = 20) | ~179 | Do not call `pressEquals` between the two operators |

### Exercise 1 tests (complete after implementing `pressToggleSign`)

| Test description | Line | Hint |
|------------------|------|------|
| Should change a positive number to negative when +/- is pressed | ~200 | Press `'5'`, call `pressToggleSign()`, check display is `'-5'` |
| Should change a negative number to positive when +/- is pressed | ~205 | Press `'5'`, toggle, toggle again, check display is `'5'` |

### Exercise 2 tests (complete after implementing `pressPercent`)

| Test description | Line | Hint |
|------------------|------|------|
| Should divide the displayed number by 100 when % is pressed | ~227 | Press `'5'`, `'0'`, call `pressPercent()`, check display is `'0.5'` |

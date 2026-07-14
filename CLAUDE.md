# Super Calculator

## Project overview
A beginner-friendly calculator web app built with Angular 19, created for
**teaching purposes**. It supports the four basic arithmetic operations
(`+`, `-`, `*`, `/`), plus toggle-sign (`+/-`), percent (`%`), clear (`C`),
and a light/dark theme toggle.

The project was originally shipped with three methods left empty as student
exercises (see [Exercises](#exercises)); those exercises are now implemented.

## Tech stack
- **Angular 19** (standalone components — no NgModule)
- **TypeScript 5.7**
- **Karma + Jasmine** for unit tests (headless Chrome)

## Requirements
- **Node.js 18.x or 20.x.** Angular 19 does **not** support Node 22+.
  If your default `node` is older/newer, switch with nvm before running
  anything: `nvm use 18`.
- npm 8+

## How to run
- Install: `npm install`
- Dev server: `npm start` → http://localhost:4200 (auto-reloads on save)
- Tests: `npm test` (add `-- --watch=false --browsers=ChromeHeadless` for a
  single CI-style run)
- Production build: `npm run build` → output in `dist/`

## Project structure
```
src/
├── main.ts                  ← app bootstrap entry point
├── index.html               ← host page with <app-root>
├── styles.css               ← global styles
└── app/
    ├── app.component.ts      ← all calculator logic and state
    ├── app.component.html    ← template (Angular bindings)
    ├── app.component.css     ← component-scoped styles (incl. light theme)
    ├── app.component.spec.ts ← unit tests (Karma + Jasmine)
    └── app.config.ts         ← standalone app configuration
```
All logic and UI live in `AppComponent`, so there is a single component and a
single spec file.

## Exercises
The app was designed as a teaching exercise. Three methods in
`app.component.ts` were originally empty (`// TODO: implement me!`) for students
to complete. They are **now implemented**:

1. `pressToggleSign()` — flips the sign of the displayed number (keeps `'0'`
   to avoid `-0`).
2. `pressPercent()` — divides the displayed number by 100.
3. `toggleTheme()` — switches between dark (default) and light mode by flipping
   `isLightMode`; the template binds `[class.light]` to apply the theme CSS.

The unit tests in `app.component.spec.ts` (originally `pending()` placeholders)
are also implemented and all pass.

## Coding conventions
- **Standalone components** (Angular 17+ style) — imports declared directly on
  the component, no NgModule.
- **Heavy explanatory comments**: this is teaching code. Methods use JSDoc-style
  block comments describing intent, params, and edge cases. Keep new code
  well-commented in the same beginner-friendly tone.
- **Section dividers**: files group related code under `─── Section ───` banner
  comments. Follow the existing style when adding code.
- **English** for all code, comments, and commit messages.
- **Tests** follow an Arrange → Act (`detectChanges()`) → Assert pattern and
  read the display via `fixture.nativeElement.querySelector('.display__value')`.

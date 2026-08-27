# JavaScript and TypeScript Basics for Playwright Automation (Q&A)

## JavaScript Basics (Playwright Perspective)

### 1) What is JavaScript in Playwright tests?
JavaScript is the runtime language used to write Playwright test logic like navigation, actions, assertions, and test setup/teardown.

### 2) Why is Node.js required for Playwright?
Playwright runs in Node.js. Your test files are executed by Node, which gives access to modules, async/await, and package tooling.

### 3) What is the difference between `var`, `let`, and `const`?
- `var`: function-scoped, older syntax, avoid in tests.
- `let`: block-scoped, reassignable.
- `const`: block-scoped, not reassignable (preferred by default in test code).

### 4) Why do Playwright examples use `async` functions?
Most browser operations are asynchronous (open page, click, wait, assert). `async` lets you use `await` for readable step-by-step flows.

### 5) What does `await page.goto(url)` do?
It waits for navigation to complete (based on Playwright defaults/options) before continuing to the next line.

### 6) What happens if you forget `await` before Playwright actions?
The promise is not waited on, so steps may run out of order and cause flaky tests or false failures.

### 7) What is a Promise in test automation?
A Promise is a placeholder for a future result. Playwright APIs return Promises for async browser work.

### 8) Why are arrow functions common in tests?
Arrow functions are concise and commonly used in `test('name', async ({ page }) => {})` blocks.

### 9) What is destructuring in `async ({ page }) => {}`?
It extracts `page` from Playwright's fixture object. You can also pull `context`, `browser`, etc. when available.

### 10) What is a module import in Playwright?
`import { test, expect } from '@playwright/test';` loads Playwright test functions from the package.

### 11) How do arrays help in Playwright tests?
Arrays let you data-drive tests, for example looping through multiple URLs, user roles, or form values.

### 12) How do objects help in Playwright tests?
Objects hold related data like test users, selectors, environment configs, and expected results.

### 13) When should you use loops in automation?
Use loops for repeated validations or dataset execution. Keep each loop deterministic to avoid brittle outcomes.

### 14) What is the difference between `==` and `===`?
- `==` does type coercion.
- `===` checks value and type.
Use `===` in test code to avoid unexpected comparisons.

### 15) How do conditions (`if/else`) help in tests?
They support environment-dependent flows, optional popups, role-specific assertions, and controlled branching.

### 16) What is error handling in Playwright tests?
Using `try/catch` to capture controlled failures. Use carefully; swallowing errors can hide real test issues.

### 17) Why should selectors be stable?
Stable selectors (e.g., `getByRole`, `getByTestId`) reduce flaky failures caused by layout/style changes.

### 18) What is the purpose of helper functions?
Helpers reduce duplication (login, navigation, repeated assertions) and improve test readability.

### 19) What are test hooks (`beforeEach`, `afterEach`)?
Hooks run setup/cleanup around tests, such as opening a logged-in state or resetting app data.

### 20) Why avoid `waitForTimeout` for synchronization?
Fixed sleeps are brittle and slow. Prefer Playwright auto-waiting, locators, and explicit state assertions.

### 21) What is auto-waiting in Playwright?
Playwright waits for elements to be actionable (visible, stable, enabled) before interactions.

### 22) How should async assertions be written?
Use Playwright expectations like `await expect(locator).toBeVisible()` so assertion retries are built in.

### 23) What is a flaky test in JS automation?
A flaky test passes/fails inconsistently without app changes, usually due to timing, unstable selectors, or shared state.

### 24) Why keep tests independent?
Independent tests can run in any order and in parallel without side effects from earlier tests.

### 25) How do environment variables help Playwright tests?
They let you switch base URLs, credentials, and feature flags without hardcoding values in test files.

---

## TypeScript Basics (Playwright Perspective)

### 1) Why use TypeScript with Playwright?
TypeScript adds static types and editor intelligence, catching mistakes earlier and improving test maintainability.

### 2) What is a type annotation?
A type annotation declares expected data type, e.g. `const baseUrl: string = 'https://example.com';`.

### 3) What is type inference?
TypeScript often infers types automatically from values, reducing explicit annotations while staying type-safe.

### 4) What is an interface in test automation?
An interface describes object shape, useful for test data models like users, orders, and expected UI states.

### 5) What is a type alias?
A type alias gives a reusable name to a type, including unions and complex structures.

### 6) What are union types and where are they useful?
Union types allow limited value sets, e.g. `role: 'admin' | 'viewer'`, useful for scenario-specific test inputs.

### 7) What is optional property syntax (`?`)?
It marks properties that may be absent, e.g. `otpCode?: string`, common in conditional login flows.

### 8) What is `readonly` and why use it?
`readonly` prevents reassignment, useful for constants like selector maps and immutable test config.

### 9) How does TypeScript improve Page Object Models?
Method signatures and typed locators make page object usage safer and easier to refactor.

### 10) How do typed function parameters help tests?
They prevent invalid input shapes and clarify expected function contracts for helpers/utilities.

### 11) What is a return type in functions?
It defines what a function returns, e.g. `Promise<void>` for async helper actions with no value.

### 12) Why are many Playwright helper methods `Promise<void>`?
They perform async browser steps but do not return data, only completion/failure status.

### 13) What does `Promise<string>` mean?
An async function eventually resolves to a string, such as fetching displayed text from a page element.

### 14) What is `unknown` vs `any`?
- `any`: disables type checking (unsafe).
- `unknown`: safer; forces validation before use.
Prefer `unknown` when handling external/untrusted values.

### 15) What is type narrowing?
Type narrowing refines a broad type after checks (e.g., `if (typeof value === 'string')`), enabling safe operations.

### 16) What is a generic utility in test code?
Generics let functions/classes work with multiple types while preserving safety, e.g. reusable API response wrappers.

### 17) What is `tsconfig.json` for Playwright projects?
It controls TypeScript compiler behavior (module target, strictness, paths, emit options).

### 18) What does strict mode (`"strict": true`) give you?
It enables stronger checks (null/undefined safety, typed contracts), reducing runtime failures in tests.

### 19) Why avoid overusing type assertions (`as`)?
Assertions can hide real mismatches. Prefer actual narrowing or better type definitions.

### 20) How do enums or literal unions help tests?
They constrain values for things like user roles, environments, and statuses to prevent typo-based bugs.

### 21) What is the benefit of typed fixtures?
Custom fixtures with explicit types improve discoverability and prevent wrong fixture usage in test files.

### 22) How does TypeScript help with locator mistakes?
Editor hints and typed APIs reduce invalid calls and improve consistency when building locators/utilities.

### 23) What is compile-time vs runtime validation?
- Compile-time: TypeScript checks code before execution.
- Runtime: app/browser behavior checked while tests run.
You need both for reliable automation.

### 24) How can shared types help API + UI Playwright tests?
Shared request/response models keep API validation and UI assertions consistent across test layers.

### 25) What is the practical outcome of TS in Playwright interviews?
You can explain not only test steps, but also maintainability, reliability, and refactor safety for larger automation suites.

---

## Quick Interview Tip
When answering interview questions, connect basics to reliability: stable selectors, proper async handling, strict typing, and isolated tests are the strongest signals of Playwright maturity.

# JavaScript + TypeScript Playwright Interview Q&A (Basics -> Intermediate -> Advanced)

Use this in order. Start from basics, then move deeper into framework design, and finally into scale/CI-level topics.

---

## Level 1: Basics

### Q1) Why is JavaScript/TypeScript important for Playwright?
Playwright tests run in Node.js, so JavaScript/TypeScript powers all test logic: navigation, actions, waits, assertions, and reusable utilities.

### Q2) Why should I prefer TypeScript over plain JavaScript for Playwright interviews?
TypeScript catches type mistakes early, improves editor hints, and makes large automation suites safer to refactor.

### Q3) What is the role of `async/await` in Playwright?
Almost every Playwright action is asynchronous. `await` ensures steps execute in sequence and reduces flaky timing issues.

### Q4) What happens if I forget `await` in Playwright code?
The test may continue before the action finishes, causing race conditions and intermittent failures.

### Q5) Why are `const` and `let` preferred over `var`?
`const` and `let` are block-scoped and safer. `var` can cause scoping bugs that are hard to debug in tests.

### Q6) What is a locator, and why is it central in Playwright?
A locator is Playwright's way of identifying and interacting with elements. It supports auto-waiting and retry behavior by default.

### Q7) Which selectors are best for stable tests?
Prefer user-facing selectors like `getByRole`, `getByLabel`, and `getByTestId` because they are less brittle than CSS tied to layout.

### Q8) Why avoid `waitForTimeout()` in interviews and real projects?
Fixed delays are slow and unreliable. Explicit conditions and Playwright auto-waiting are more deterministic.

### Q9) What is auto-waiting?
Playwright waits for elements to be visible/actionable before interacting, reducing manual wait logic.

### Q10) How should assertions be written in Playwright?
Use `await expect(locator).toBeVisible()` style assertions so Playwright can retry until timeout instead of failing instantly.

### Q11) What are hooks like `beforeEach` used for?
They centralize setup/cleanup such as login, test data reset, or opening a starting page for each test.

### Q12) Why should tests be independent?
Independent tests can run in any order and parallel mode without hidden dependencies.

### Q13) What does TypeScript inference mean in Playwright code?
TS can infer many types from values and APIs, reducing explicit annotations while preserving safety.

### Q14) What is an interface example in automation?
You can model users or fixtures:
`interface User { email: string; role: 'admin' | 'viewer' }`.

### Q15) What is the difference between `any` and `unknown`?
`any` disables checks; `unknown` forces validation before use. `unknown` is safer for external data.

---

## Level 2: Intermediate

### Q16) How do you structure a Playwright project for maintainability?
Typical structure: `tests/`, `pages/` (POM), `fixtures/`, `utils/`, `test-data/`, and config in `playwright.config.ts`.

### Q17) What is Page Object Model (POM), and when should you use it?
POM wraps UI interactions in classes/methods so tests express intent (business flow) instead of raw selector steps.

### Q18) What are common POM mistakes?
Putting assertions everywhere in page classes, over-abstracting tiny actions, and creating overly generic "god" page objects.

### Q19) How can TypeScript improve POM quality?
Strongly typed method parameters/returns and readonly locators prevent misuse and make refactoring safer.

### Q20) What are Playwright fixtures and why use custom fixtures?
Fixtures inject reusable setup logic (e.g., logged-in page, seeded test data). Custom fixtures reduce duplication across suites.

### Q21) How do you data-drive tests in Playwright?
Use arrays/objects and iterate scenarios to cover combinations while keeping each case isolated and readable.

### Q22) How do you handle authentication efficiently?
Use `storageState` to reuse authenticated sessions instead of logging in through UI for every test.

### Q23) What is the right balance between UI and API in Playwright tests?
Use API calls for setup/cleanup and UI for user journey validation. This keeps tests faster and less flaky.

### Q24) How do you test dynamic content or flaky-loading widgets?
Assert final expected states via locators (`toHaveText`, `toBeVisible`, `toHaveCount`) rather than timing assumptions.

### Q25) How do retries affect reliability?
Retries can reduce noise from transient failures but should not hide real defects. Track retry patterns to fix root causes.

### Q26) How do you debug failing tests effectively?
Use trace viewer, screenshots, videos, console/network logs, and reproduce locally with `--headed` and a focused test filter.

### Q27) What TypeScript config options matter most?
`"strict": true`, proper module settings, path aliases, and no unchecked implicit `any` for robust test code.

### Q28) When are union types useful in test frameworks?
They constrain valid values (env, role, region, plan type), preventing invalid test inputs.

### Q29) How do you avoid brittle shared state between tests?
Use isolated fixtures, unique test data, and avoid depending on artifacts created by previous tests.

### Q30) What should you mention in interviews about flaky tests?
Explain root causes (timing, selectors, shared state, environment instability), mitigation (locators/assertions), and observability (trace/logs).

---

## Level 3: Advanced

### Q31) How do you scale Playwright suites in CI?
Use parallel workers, sharding, test tagging, environment-aware configs, and separate smoke vs regression pipelines.

### Q32) What is sharding and why is it useful?
Sharding splits tests across CI nodes to reduce total runtime while preserving full coverage.

### Q33) How do you design test tags for large suites?
Tag by purpose/risk (`@smoke`, `@regression`, `@critical`, `@api-setup`) to run the right subset per pipeline stage.

### Q34) How do you make tests deterministic across browsers?
Avoid browser-specific assumptions, rely on accessible selectors, and validate behavior with cross-browser CI runs.

### Q35) How do you combine contract checks with UI checks?
Validate API contracts during setup/assertion and then verify UI renders the same truth to catch integration mismatches.

### Q36) What is a robust strategy for test data lifecycle?
Create data via API, namespace by run ID, and ensure cleanup jobs for failed/incomplete runs.

### Q37) How do you handle feature flags in Playwright automation?
Parameterize tests by flag state and keep assertions explicit for both enabled/disabled behavior.

### Q38) How do you prevent secrets leakage in test code?
Use environment variables/secret managers, never hardcode credentials, and redact logs in CI artifacts.

### Q39) What advanced TypeScript patterns help automation frameworks?
Generics for reusable helpers, discriminated unions for workflow states, and typed fixture contracts.

### Q40) How do you decide what belongs in custom helpers vs test files?
Extract repeated domain workflows, keep one-off assertions in tests, and avoid abstractions that hide critical behavior.

### Q41) What is your strategy for observability in failing CI runs?
Collect trace/video/screenshot plus console/network logs and annotate run metadata (build ID, env, feature flags).

### Q42) How do you validate performance-sensitive UI flows with Playwright?
Use targeted timing metrics and thresholds carefully, keeping perf checks separate from core functional assertions.

### Q43) How do you prevent "false green" pipelines?
Fail on critical flakes above threshold, review retries, and require deterministic pass criteria for release gates.

### Q44) How do you evolve framework architecture over time?
Refactor gradually with typed contracts, deprecate old helpers, and keep migration guides for contributors.

### Q45) What interview-ready "advanced answer" should you give?
Explain tradeoffs: speed vs coverage, abstraction vs readability, retries vs root-cause fixing, and CI throughput vs stability.

---

## Final Interview Strategy (How to Answer)

1. Start with correctness (stable selectors, proper waits, deterministic assertions).  
2. Move to maintainability (POM boundaries, fixtures, TS strict typing).  
3. Finish with scale (parallelism, sharding, observability, flaky-test governance).  

This progression shows both coding fundamentals and automation engineering maturity.

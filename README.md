# Playwright Fundamentals

A hands-on Playwright with TypeScript project covering the basics of browser automation and end-to-end testing.

## Prerequisites

- [Node.js](https://nodejs.org/) 18 or newer (LTS recommended)
- npm (bundled with Node.js)
- Git

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/Saya031992/Playwright-fundamental.git
   cd Playwright-fundamental
   ```

2. Install the project dependencies:

   ```bash
   npm ci
   ```

3. Install the Playwright browser binaries:

   ```bash
   npx playwright install
   ```

   On Linux CI machines, use `npx playwright install --with-deps` to also install the required system libraries.

## Project Setup

The project is already configured. Key files:

| File | Purpose |
| --- | --- |
| `playwright.config.ts` | Playwright configuration (test directory, browsers, reporters, tracing) |
| `tests/` | Test specifications |
| `.github/workflows/playwright.yml` | GitHub Actions CI pipeline |
| `.gitignore` | Ignores `node_modules/`, reports, and local artifacts |

The configuration runs tests in `./tests` against Chromium, Firefox, and WebKit using the HTML reporter.

## Running Tests

Run the full suite in all configured browsers:

```bash
npx playwright test
```

Run a single file, a single browser, or a single test:

```bash
npx playwright test tests/example.spec.ts
npx playwright test --project=chromium
npx playwright test -g "has title"
```

Run tests in headed mode or with the interactive UI:

```bash
npx playwright test --headed
npx playwright test --ui
```

Open the last HTML report:

```bash
npx playwright show-report
```

## Codegen (Record & Generate Tests)

Playwright's code generator records your browser interactions and produces ready-to-run test code.

1. Start the recorder:

   ```bash
   npx playwright codegen https://playwright.dev/
   ```

2. A browser window and the Playwright Inspector open. Interact with the page and the generated code appears in the Inspector.

3. Copy the generated code into a new or existing `.spec.ts` file under `tests/`, then run it with `npx playwright test`.

Useful options:

```bash
# Generate test IDs using data-testid attributes
npx playwright codegen --test-id-attribute=data-testid https://app.example.com

# Emulate a device viewport
npx playwright codegen --device="iPhone 12" https://playwright.dev/

# Save the generated code directly to a file
npx playwright codegen --target=playwright-test -o tests/generated.spec.ts https://playwright.dev/

# Emulate color scheme
npx playwright codegen --color-scheme=dark https://playwright.dev/

# Save authentication state (cookies, localStorage) for reuse
npx playwright codegen --save-storage=auth.json https://app.example.com
npx playwright codegen --load-storage=auth.json https://app.example.com
```

The Inspector also offers `Record`, `Pick locator`, and `Assert visibility/text` actions to build assertions without writing them by hand.

## Continuous Integration

The workflow in `.github/workflows/playwright.yml` runs on every push and pull request to `main`/`master`. It installs dependencies, installs browsers, runs the test suite, and uploads the HTML report as a build artifact (retained for 30 days).

## Resources

- [Playwright documentation](https://playwright.dev/docs/intro)
- [Playwright codegen](https://playwright.dev/docs/codegen)
- [Playwright test configuration](https://playwright.dev/docs/test-configuration)

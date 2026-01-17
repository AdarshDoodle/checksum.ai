# checksum.ai

Playwright test automation project.

## Prerequisites

- Node.js (v18 or higher)
- npm (comes with Node.js)

## Setup

1. Install Node.js if you haven't already:
   - Visit https://nodejs.org/ and download the LTS version
   - Or use a version manager like `nvm`: `nvm install --lts`

2. Install dependencies:
   ```bash
   npm install
   ```

3. Install Playwright browsers:
   ```bash
   npx playwright install
   ```

## Running Tests

- Run all tests: `npm test`
- Run tests in UI mode: `npm run test:ui`
- Run tests in headed mode (see browser): `npm run test:headed`
- Run tests in debug mode: `npm run test:debug`
- View test report: `npm run test:report`

## Assignment Tests

The assignment tests are located in `tests/checksumassignment.spec.js` and include:

1. **Edit a Kanban Card** - Tests editing a card, completing a subtask, and moving it to the first column
2. **Delete a Kanban Card** (Optional) - Tests deleting a card and verifying removal

### Running Assignment Tests with Repeat

To run the assignment tests 5 times each (as required):
```bash
npm run test:repeat
```

Or directly:
```bash
npx playwright test tests/checksumassignment.spec.js --repeat-each 5
```

### Generating HTML Test Report

After running tests, an HTML report is automatically generated. To view it:
```bash
npm run test:report
```

The report will be available in the `playwright-report` directory.

## Project Structure

```
checksum.ai/
├── tests/                          # Test files
│   ├── example.spec.js            # Example test
│   └── checksumassignment.spec.js # Assignment test cases
├── playwright.config.js            # Playwright configuration
├── package.json                    # Project dependencies
└── playwright-report/              # HTML test reports (generated)
```

## Writing Tests

Create test files in the `tests/` directory with the `.spec.js` extension. See `tests/example.spec.js` for a sample test.

## Test Robustness

The assignment tests are designed to handle dynamic data that changes on each page refresh:
- Tests use dynamic selectors that don't rely on specific card names or column names
- Tests find cards and columns programmatically
- Tests include proper wait strategies and error handling
- Tests verify state changes with assertions

## Submission

When submitting, create a zip file of the repository excluding `node_modules`:
```bash
zip -r checksum-ai-assignment.zip . -x "node_modules/*" "*.git*"
```

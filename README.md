# checksum.ai

Playwright test automation project for Kanban application testing.

## Prerequisites

- Node.js (v18 or higher)
- npm (comes with Node.js)

## Setup

1. Install Node.js if you haven't already:
   - Visit https://nodejs.org/ and download the LTS version
   - Or use a version manager like `nvm`: `nvm install --lts`

2. Install project dependencies:
   ```bash
   npm install
   ```

3. Install Playwright browser:
   ```bash
   npx playwright install chromium
   ```
   
   Note: This project is configured to run tests only on Chromium browser.

## Running Tests

### Basic Test Commands

- Run all tests: `npm test`
- Run tests in UI mode (interactive): `npm run test:ui`
- Run tests in headed mode (visible browser): `npm run test:headed`
- Run tests in debug mode: `npm run test:debug`
- View test report: `npm run test:report` or `npx playwright show-report`

### Assignment-Specific Commands

- Run assignment tests in headed mode: `npm run test:checksum`
- Run assignment tests with 5 repeats: `npm run test:repeat`

## Assignment Tests

The assignment tests are located in `tests/checksumassignment.spec.js` and include:

### Test Case 1: Edit a Kanban Card

**Description:** Edit a Kanban card to mark a subtask as complete and move the card to the first column.

**Test Steps:**
1. Navigate to the Kanban app
2. Choose a card with subtasks that are not completed and that is not in the first column
3. Complete one subtask
4. Move task to the first column
5. Verify that the subtask is striked through
6. Close the card edit page
7. Verify that the number of completed subtasks is correct
8. Verify that the card moved to the correct column

**Key Features:**
- Dynamically finds cards with incomplete subtasks in non-first columns
- Handles retry logic for cards that show all subtasks completed in modal
- Verifies subtask completion count increased by exactly 1
- Confirms card moved from original column to first column

### Test Case 2: Delete a Kanban Card (Optional)

**Description:** Delete a Kanban card and verify it's removed from the board.

**Test Steps:**
1. Navigate to the Kanban app
2. Find a column with at least one card
3. Open the card
4. Click 3 dots menu and select "Delete Task"
5. Confirm deletion if needed
6. Verify card is no longer on board
7. Verify column card count decreased by 1

**Key Features:**
- Locates 3 dots menu in modal header (distinguishes from status dropdown)
- Handles deletion confirmation modal
- Verifies card removal from board
- Confirms column count updated correctly

### Running Tests with 5 Repeats

To run the assignment tests 5 times each (as required):

```bash
npm run test:repeat
```

Or directly:
```bash
npx playwright test tests/checksumassignment.spec.js --repeat-each 5
```

**What happens:**
- Each test case runs 5 times (total of 10 executions: 2 tests × 5 repeats)
- All results are included in the HTML report
- The report shows all 10 test executions with individual pass/fail status

## HTML Test Report

### Report Generation

The HTML test report is **automatically generated** every time you run tests. The report is saved to `playwright-report/index.html` and is overwritten with each test run. The HTML reporter is configured in `playwright.config.js`.

**Reports are generated:**
- After running any test command (`npm test`, `npm run test:repeat`, etc.)
- Even if tests fail
- Automatically - no additional commands needed

### Viewing the Report

**Method 1: Using Playwright's Report Viewer (Recommended)**
```bash
npm run test:report
```
or
```bash
npx playwright show-report
```

Both commands start a local server and automatically open the report in your browser.

**Method 2: Opening Report File Directly**
- Navigate to `playwright-report/index.html` and open with any web browser
- Note: Some features may not work when opening directly due to browser security restrictions

### Report Contents

The HTML test report includes:
- Test summary with passed/failed/skipped counts
- Individual test case results with pass/fail status
- Detailed error messages and stack traces for failures
- Execution time for each test
- Screenshots and videos (if configured)
- Test logs and console output

## Project Structure

```
checksum.ai/
├── tests/
│   └── checksumassignment.spec.js # Assignment test cases
├── playwright.config.js            # Playwright configuration
├── package.json                    # Project dependencies and scripts
├── playwright-report/              # HTML test reports (generated)
│   └── index.html                 # Main report file
└── test-results/                   # Test execution artifacts (generated)
```

## Test Configuration

The project is configured in `playwright.config.js`:
- Test Directory: `./tests`
- Browser: Chromium only
- Reporter: HTML reporter
- Parallel Execution: Enabled
- Retries: Disabled for local runs, 2 retries on CI
- Trace: Enabled on first retry for debugging

## Test Robustness

The assignment tests handle dynamic data that changes on each page refresh:

- **Dynamic Selectors:** Programmatic element finding instead of hardcoded values
- **Wait Strategies:** Multiple wait mechanisms (`waitForLoadState`, `waitForSelector`, `waitForFunction`, `waitForTimeout`)
- **Error Handling:** Comprehensive error handling with detailed debug information
- **Edge Cases:** Handles scenarios like no suitable cards, all subtasks completed, page closure, stale element references

## Troubleshooting

### Tests Fail Due to No Suitable Cards

If tests fail with "No card found with incomplete subtasks":
- All cards with incomplete subtasks are in the first column, or no cards exist with incomplete subtasks
- The test will skip and log debug information
- **Solution:** Refresh the page and run tests again (board state changes on each refresh)

### Tests Fail Due to Element Not Found

- Ensure the Kanban application is accessible
- Check network connectivity
- Verify browser is properly installed: `npx playwright install chromium`

### Browser Installation Issues

- Ensure Node.js v18+ is installed
- Check internet connection
- On macOS, may require Xcode command line tools: `xcode-select --install`

## Submission

When submitting, create a zip file excluding `node_modules` and git files:

```bash
zip -r checksum-ai-assignment.zip . -x "node_modules/*" "*.git*" "playwright-report/*" "test-results/*"
```

Note: You may optionally exclude generated reports and test results to reduce file size.

## License

ISC

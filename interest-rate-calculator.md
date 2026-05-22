# Final Project: Interest Rate Calculator

**IBM Skills Network** | **Estimated time:** 2 hours | **Author:** Ratima Raj Singh

> **License:** The content of this lab is licensed under [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0).

---

In this final project, you will be working on an Interest Rate Calculator and enhancing it using the skills you learned in this course.

## Objectives

1. Learn how to practice debugging in Chrome, using breakpoints, and watch errors in Console
2. Use Jasmine to test your business logic
3. Improve SEO for better reach and visibility on search engines
4. Use Webpack to create assets

---

## Set-up: Create Application

1. Open a terminal window: **Terminal > New Terminal**.

2. Navigate to the project folder:

```bash
cd /home/project
```

3. Fork the GitHub repository at the URL below by clicking the **Fork** button at the top-right corner of the repository page. Keep the repository name unchanged:

```
https://github.com/ibm-developer-skills-network/intermediate_webdev_finalproject
```

> **Note:** Ensure your forked repository is **Public**. This creates a copy of the repository within your GitHub account.

4. You can find instructions on how to fork the repository by visiting exercise 2 at the linked resource.

5. Open a new terminal, clone the forked repository, and change to the project directory:

```bash
cd intermediate_webdev_finalproject
```

6. List the directory contents to see the lab artifacts:

```bash
ls
```

7. Run the following command to host your web page:

```bash
python3 -m http.server
```

8. Launch the application in your browser using the **Launch Application** option in the IDE.

9. The app will look like a basic form with fields for Principal Amount, Rate (%), and Time (Years), plus a **Calculate** button.

10. To view the developer source of the page, use:
    - **Mac:** `Cmd + Option + U`
    - **Windows:** `Ctrl + U`

---

## Working with Files in Cloud IDE

To view your files and directories, click the **Explorer** (files) icon in the left sidebar.

- **Create a new file:** Right-click in the Explorer panel and select **New File**, or use **File → New File**.
- Enter the filename when prompted (e.g., `sample.html`).
- Clicking the filename in the Explorer opens it in the right editor pane.
- **Save:** Use `Cmd + S` (Mac) or `Ctrl + S` (Windows), or enable **File → Auto Save**.

---

## Creating Interest Rate Calculator

> **Note:**
> 1. Ensure all updates to `index.html` and `script.js` are properly saved.
> 2. You can submit your project deliverables through either **Option 1: AI-Graded** or **Option 2: Peer-Graded** Submission and Evaluation.
> 3. **Option 1 (AI-Graded):** Submit the GitHub URLs for `index.html` and `script.js` along with terminal output for Tasks 6–8.
> 4. **Option 2 (Peer-Graded):** Submit screenshots for Tasks 1–9.

---

## Task 1: Favicon

The first thing to notice is that there is no favicon defined. In some cases this throws an error:

```
GET http://HOSTNAME:8000/favicon.ico 404 (File not found)
```

Download the provided `favicon.ico` file and place it at the root level of your project. By default, the browser expects the filename `favicon.ico`.

Run the following command in the terminal to download the favicon into your project directory:

```bash
cd /home/project/intermediate_webdev_finalproject
curl -Ol https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-WD0231EN-SkillsNetwork/images/favicon.ico
```

<details>
<summary>💡 Hint</summary>

Although unnecessary (browsers look for `favicon.ico` at the root automatically), you can also explicitly declare it in the `<head>` section of `index.html`:

```html
<link rel="icon" href="favicon.ico" />
```

</details>

After refreshing the browser, you should see the favicon (a **%** icon) appear in the browser tab.

> **Assessment:**
> - **Option 1 (AI-Graded):** Push the updated `index.html` to your forked GitHub repository.
> - **Option 2 (Peer-Graded):** Take a screenshot of the browser tab showing the favicon and save it as `01-favicon-visible.png`.

---

## Task 2: Missing CSS Reference

If you inspect the page, you can see elements have CSS classes defined, but the CSS file itself is not linked in the HTML.

Add the CSS reference in the `<head>` section of `index.html` and refresh the page.

<details>
<summary>💡 Hint</summary>

Add the following line inside the `<head>` tag of `index.html`:

```html
<link rel="stylesheet" href="style.css" />
```

</details>

After refreshing the browser, the calculator should now render with full styling — bold labels, a purple Calculate button, and a result area.

> **Assessment:**
> - **Option 1 (AI-Graded):** Push the updated `index.html`.
> - **Option 2 (Peer-Graded):** Take a screenshot showing the CSS applied and save it as `02-css-working.png`.

---

## Task 3: Missing JavaScript Reference

What happens when you press the **Calculate** button? Nothing! Open Chrome DevTools and check the Console for the error:

```
Uncaught ReferenceError: calculate is not defined
    at HTMLButtonElement.onclick ((index):31:56)
```

The reason is that `script.js` exists in the project but is not referenced in the HTML. The `calculate` function lives in that file.

Add the JavaScript reference just before the closing `</body>` tag in `index.html`.

<details>
<summary>💡 Hint</summary>

Add the following line just before `</body>` in `index.html`:

```html
<script src="script.js"></script>
```

</details>

Refresh the browser and try clicking **Calculate** again.

After adding the script reference, what error do you see now?

<details>
<summary>💡 Hint</summary>

```
script.js:3 Uncaught TypeError: Cannot read properties of null (reading 'value')
    at calculate (script.js:3:47)
    at HTMLButtonElement.onclick ((index):31:58)
```

This is a different error — `script.js` is now loading, but the `calculate` function is trying to read a DOM element that it can't find. This will be fixed in the next task.

</details>

> **Assessment:**
> - **Option 1 (AI-Graded):** Push the updated `index.html`.
> - **Option 2 (Peer-Graded):** Take a screenshot of the Console error before the fix and save it as `03-calculate-missing.png`.

---

## Task 4: Step-by-Step Debug

In Chrome DevTools, open the **Sources** tab and enable **Pause on uncaught exceptions** in the Breakpoints panel.

Try the Calculate operation again. The debugger will pause and highlight the line that threw the exception.

The error you will see is:

```
TypeError: Cannot read properties of null (reading 'value')
```

This means the code called `document.getElementById(...)` with a name that doesn't match any element in the HTML, so it returned `null`.

View the page source and compare the element `id` values in `index.html` with the names used in `script.js`. You'll find that the script uses `"principle"` but the HTML input has `id="principal"`.

<details>
<summary>💡 Hint</summary>

The element name in the HTML is `principal`, not `principle`. Look at the input element in `index.html`:

```html
<input type="number" id="principal" value="1000" />
```

The script was using the misspelled ID `"principle"`, which returned `null`.

</details>

Fix the name in `script.js`:

```javascript
let p = document.getElementById("principal").value;
```

> **Assessment:**
> - **Option 1 (AI-Graded):** Push the updated `script.js`.
> - **Option 2 (Peer-Graded):** Take a screenshot of the debugger paused on the exception and save it as `04-pause-on-exception.png`.

---

## Task 5: Use Correct Data Types

Calculate the interest again. You will see a new error:

```
TypeError: p.toFixed is not a function
```

The `toFixed()` method formats a **number** using fixed-point notation — it is only available on the `Number` type, not on strings.

`document.getElementById(...).value` always returns a **string**. In DevTools, add a **Watch** on the variable `p` to confirm: it will show `"1000"` (with quotes), not `1000`.

<details>
<summary>💡 Hint</summary>

In DevTools, add `p` to the Watch panel. You will see it displays as `"1000"` (a string, shown with quotes), not the number `1000`. The Watch panel in DevTools also shows the paused exception: `TypeError: p.toFixed is not a function`, and the local scope shows `amount: 950` — confirming the subtraction bug is also present.

</details>

Fix all three input reads in `script.js` by wrapping them with `Number()`:

```javascript
let p = Number(document.getElementById("principal").value);
let r = Number(document.getElementById("rate").value);
let t = Number(document.getElementById("time").value);
```

Clicking **Calculate** now will produce output — though the result may still be incorrect (see below).

> **Assessment:**
> - **Option 1 (AI-Graded):** Push the updated `script.js` and save the public GitHub URL of the file for final submission.
> - **Option 2 (Peer-Graded):** Take a screenshot showing `p` added as a Watch expression and save it as `05-watch-on-p.png`.

---

## Prepare for Testing

At this point, the calculator is producing a wrong result. For example, with Principal = 1000, Rate = 5%, and Time = 1 year:

```
Simple Interest  = (P × R × T) / 100 = (1000 × 5 × 1) / 100 = 50
Total Amount     = P + Simple Interest = 1000 + 50 = 1050
```

The app shows **950** instead of **1050** — the previous developer subtracted the interest instead of adding it.

To make the code testable with Jasmine, separate the business logic from the UI logic. Create two standalone functions in `script.js`:

### 1. `calculateSimpleInterest`

Accepts `principal`, `rate`, and `time`; returns the simple interest:

<details>
<summary>💡 Hint</summary>

```javascript
const calculateSimpleInterest = (principal, rate, time) => {
  return (principal * rate * time) / 100;
};
```

</details>

### 2. `calculateTotalPayableAmount`

Accepts `principal` and `interestAmount`; returns the total. For now, **keep the bug** (subtraction) in place — you will fix it via testing in Task 7:

<details>
<summary>💡 Hint</summary>

```javascript
const calculateTotalPayableAmount = (principal, interestAmount) => {
  return principal - interestAmount;  // ← intentional bug, fixed in Task 7
};
```

</details>

### Refactor the `calculate` function

Update `calculate` to use the two new functions:

```javascript
const calculate = () => {
  let p = Number(document.getElementById("principal").value);
  let r = Number(document.getElementById("rate").value);
  let t = Number(document.getElementById("time").value);

  let simpleInterest = calculateSimpleInterest(p, r, t);
  let amount = calculateTotalPayableAmount(p, simpleInterest);

  let result = document.getElementById("result");
  result.innerHTML = `<div>Principal Amount: <span>${p.toFixed(2)}</span></div>
  <div>Total Interest: <span>${simpleInterest.toFixed(2)}</span></div>
  <div>Total Amount: <span>${amount.toFixed(2)}</span></div>`;
};
```

### Export for Jasmine

Add the following at the bottom of `script.js` so Jasmine can import the functions via Node.js:

```javascript
if (typeof module !== 'undefined')
  module.exports = { calculateSimpleInterest, calculateTotalPayableAmount, calculate };
```

This conditional check means the export only runs in a Node.js environment and has no effect in the browser.

---

## Task 6: Test Using Jasmine

### 1. Install Jasmine

Install Jasmine as a dev dependency and initialise it:

<details>
<summary>💡 Hint</summary>

```bash
npm install --save-dev jasmine
npx jasmine init
npx jasmine
```

</details>

Run Jasmine. With no spec files yet, you should see:

```
No specs found
Finished in 0.002 seconds
Incomplete: No specs found
Randomized with seed XXXXX (jasmine --random=true --seed=XXXXX)
```

> **Assessment:**
> - **Option 1 (AI-Graded):** Copy and paste this terminal output into a text file and save it as `no-spec` for submission.
> - **Option 2 (Peer-Graded):** Take a screenshot of the terminal output and save it as `06-no-spec.png`.

### 2. Write Tests

Create the file `spec/scriptSpec.js`. Start by importing the two calculation functions:

```javascript
const { calculateSimpleInterest, calculateTotalPayableAmount } = require('../script');
```

Add the `describe` block to hold your tests:

```javascript
describe("Interest Rate Calculator Tests", () => {
  // tests go here
});
```

#### i. Test for `calculateSimpleInterest`

Call `calculateSimpleInterest(1000, 5, 1)` and expect the result to be `50`.

<details>
<summary>💡 Hint</summary>

```javascript
it("Calculate Simple Interest", () => {
  var actual = calculateSimpleInterest(1000, 5, 1);
  expect(actual).toBe(50);
});
```

</details>

#### ii. Test for `calculateTotalPayableAmount`

Call `calculateTotalPayableAmount(1000, 50)` and expect the result to be `1050`.

<details>
<summary>💡 Hint</summary>

```javascript
it("Calculate Total Interest", () => {
  var actual = calculateTotalPayableAmount(1000, 50);
  expect(actual).toBe(1050);
});
```

</details>

Run the tests:

```bash
npx jasmine
```

You should see a **failure** because `calculateTotalPayableAmount` currently subtracts instead of adds:

```
Expected 950 to be 1050.
```

---

## Task 7: Fix the Error and Test Again

Fix the subtraction bug in `calculateTotalPayableAmount` inside `script.js`:

```javascript
const calculateTotalPayableAmount = (principal, interestAmount) => {
  return principal + interestAmount;  // ✅ fixed
};
```

Run `npx jasmine` again. Both tests should now pass:

```
Randomized with seed XXXXX
Started
..
2 specs, 0 failures
Finished in 0.004 seconds
Randomized with seed XXXXX (jasmine --random=true --seed=XXXXX)
```

> **Assessment:**
> - **Option 1 (AI-Graded):** Copy and paste this terminal output into a text file and save it as `both-tests-passed` for submission.
> - **Option 2 (Peer-Graded):** Take a screenshot of the terminal output and save it as `07-both-tests-passed.png`.

---

## Task 8: Webpack Your Web Project

You will make the Interest Rate Calculator distributable using Webpack.

### Install Webpack Dependencies

<details>
<summary>💡 Hint</summary>

```bash
npm install webpack webpack-cli html-webpack-plugin --save-dev
```

</details>

Stop your web server (`Ctrl + C`).

### Restructure the Project

Create `src` and `dist` directories at the project root:

```bash
mkdir src dist
```

Move `index.html`, `script.js`, `favicon.ico`, and `style.css` into the `src` directory.

### Update `scriptSpec.js`

Since `script.js` has moved to `src/`, update the `require` path in `spec/scriptSpec.js`:

```javascript
const { calculateSimpleInterest, calculateTotalPayableAmount } = require('../src/script');
```

### Create `webpack.config.js`

Create `webpack.config.js` at the **project root** with the following configuration:

<details>
<summary>💡 Hint</summary>

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  mode: "development",
  entry: "./src/script.js",
  plugins: [
    new HtmlWebpackPlugin({
      template: 'src/index.html',
      favicon: "./src/favicon.ico",
    })
  ],
  output: {
    clean: true,
    libraryTarget: 'window'
  },
  module: {
    rules: [
      {
        test: /\.(css)$/i,
        type: "asset/resource",
        generator: {
          filename: "[name][ext]",
        },
      },
    ],
  },
};
```

</details>

<details>
<summary>💡 Hint</summary>

Replace the existing `<link>` stylesheet tag in `/src/index.html` with this EJS template syntax, which tells Webpack's `HtmlWebpackPlugin` to process and bundle `style.css` as an asset:

```html
<link rel="stylesheet" href=<%=require('./style.css')%> type="text/css" media="all" />
```

</details>

### Remove the `script.js` Reference from HTML

Webpack bundles your JavaScript into `main.js` and injects it automatically via `HtmlWebpackPlugin`. Remove the manual `<script src="script.js"></script>` line from `/src/index.html` — it is no longer needed.

### Run Webpack

Open another terminal at the project root and run:

```bash
npx webpack
```

You should see output similar to:

```
asset favicon.ico 15 KiB [emitted]
asset main.js 3.28 KiB [compared for emit] (name: main)
asset index.html 1.17 KiB [emitted]
./src/script.js 932 bytes [built] [code generated]
webpack 5.77.0 compiled successfully in 133 ms
```

### Run from the `/dist` Directory

```bash
cd dist
python3 -m http.server
```

Refresh the browser — everything should now work correctly with CSS applied.

> **Assessment:**
> - **Option 1 (AI-Graded):** Copy and paste the Webpack terminal output into a text file and save it as `dist-directory` for submission.
> - **Option 2 (Peer-Graded):** Take a screenshot of the `dist` directory in the Cloud IDE Explorer and save it as `08-dist-directory.png`.

The `dist` folder should contain: `favicon.ico`, `index.html`, `main.js`, and `style.css`.

---

## Task 9: Improve SEO

Make the following three changes to `/src/index.html` to improve search engine visibility.

### 1. Update the Page Title

<details>
<summary>💡 Hint: Title</summary>

```html
<title>Interest Rate Calculator - Quickly Calculate Interest on Loans</title>
```

</details>

### 2. Wrap the Heading in `<h1>`

<details>
<summary>💡 Hint: h1</summary>

```html
<h1>Interest Rate Calculator</h1>
```

</details>

### 3. Add a Meta Description Tag

<details>
<summary>💡 Hint: meta</summary>

```html
<meta name="description" content="Quickly and accurately calculate interest rates on loans with our easy-to-use interest rate calculator. Determine the interest you'll pay and make informed financial decisions. Try our free online calculator now." />
```

</details>

After these changes, run `npx webpack` again and refresh the browser. The browser tab should now show the full descriptive title, and inspecting the page source should reveal the `<h1>` and `<meta>` tags.

> **Assessment:**
> - **Option 1 (AI-Graded):** Push the updated `index.html` and save the public GitHub URL for submission.
> - **Option 2 (Peer-Graded):** Take a screenshot of the final output alongside the page source and save it as `09-final-output.png`.

---

## Submission Checklist

### Option 1 — AI-Graded Submission

| # | Deliverable | What to Submit |
|---|-------------|----------------|
| 1 | `index.html` GitHub URL | Favicon visible, CSS linked, JS linked, `<title>` / `<meta>` / `<h1>` present |
| 2 | `script.js` GitHub URL | No TypeErrors; inputs converted with `Number()`; all three functions defined and exported |
| 3 | Terminal output (no specs) | Output of `npx jasmine` with no spec files — "No specs found" |
| 4 | Terminal output (tests pass) | Output of `npx jasmine` showing 2 specs, 0 failures |
| 5 | Terminal output (Webpack) | Output of `npx webpack` showing compiled successfully |

### Option 2 — Peer-Graded Submission

| # | Screenshot filename | What it should show |
|---|---------------------|---------------------|
| 1 | `01-favicon-visible.png` | Browser tab with % favicon |
| 2 | `02-css-working.png` | Styled calculator with CSS applied |
| 3 | `03-calculate-missing.png` | Console error: `calculate is not defined` |
| 4 | `04-pause-on-exception.png` | Debugger paused on the `null` TypeError |
| 5 | `05-watch-on-p.png` | DevTools Watch showing `p: "1000"` (string) |
| 6 | `06-no-spec.png` | Terminal showing "No specs found" |
| 7 | `07-both-tests-passed.png` | Terminal showing 2 specs, 0 failures |
| 8 | `08-dist-directory.png` | `dist/` folder in Cloud IDE Explorer |
| 9 | `09-final-output.png` | Final working calculator with page source visible |

---

**Congratulations! That's a wrap.**

© IBM Corporation. All rights reserved.

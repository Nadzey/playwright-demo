# 🍀 Gherkin + Cucumber + Playwright E2E Testing

This repository demonstrates an **end-to-end (E2E)** testing setup using:

- 📝 **Gherkin** for writing feature files (human-readable scenarios)
- 🥒 **Cucumber** for step definitions
- 🎭 **Playwright** for fast and reliable browser automation

Together, these tools provide a **clean**, **data-driven** approach to verifying features like user authentication, project boards, task tags, and more.

---

## 🚀 Key Features

1. **Data-Driven Testing** 📊  
   - Use **Scenario Outlines** with Examples in Gherkin to run the same steps with different data rows.

2. **Environment Variables** 🔐  
   - Keep credentials (`USERNAME=*******`, `PASSWORD=******`) in a `.env` file, protecting sensitive data from source control.

3. **Browser Automation** 🌍  
   - **Playwright** runs tests in real browsers (Chromium, Firefox, WebKit)—either headless or headed mode.

4. **Cucumber Reporting** 📑  
   - Generate test results in multiple formats (JSON, HTML, Allure, etc.) for stakeholder visibility.

---

## 💾 Installation & Setup

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/Nadzey/playwright-demo.git
cd playwright-demo
```

### 2️⃣ Install Dependencies
```bash
npm install
```
Or:
```bash
yarn install
```
This creates **`node_modules`** and **`package-loc.json`**.

### 4️⃣ Install dotenv for Environment Variables
To keep credentials secure, install `dotenv`:
```bash
npm install dotenv --save
```
Then, create a `.env` file and add:
```bash
# .env
PLAYWRIGHT_USER=********
PLAYWRIGHT_PASS=********
BASE_URL=********
```
This file is loaded by `require('dotenv').config()`, so you can access variables like `process.env.USERNAME` in your code.

---

## 🌱 Project Structure

Below is an example layout of files/folders:

```bash
gherkin-playwright-demo/
├── features
│   └── tasks.feature        # Gherkin .feature file(s)
|   └── taskVerification.feature # Gherkin .feature file(s) automaticly created
├── steps
│   ├── hooks.js             # Cucumber Hooks (Before/After) to launch/close Playwright
│   └── tasks.steps.js       # Step definitions referencing the Page
├── tests
│   ├── helpers.js           # login() function, environment usage
│   └── utils
│       └── selectors.js     # Shared selectors
├── data
│   └── testData.json        # (Optional) JSON data for dynamic test scenarios
├── .env                     # Environment variables (ignored by .gitignore)
├── cucumber.js              # (Optional) Cucumber config
├── playwright.config.js     # Playwright config (if needed)
├── package.json
├── generateFeature.js
└── README.md
```

---

## 🔥 How to Run Tests

### 1️⃣ Run the generateFeature.js script, which automatically generates a .feature file for Cucumber using test data from a JSON file.
```bash
node generateFeature.js
```
### 2️⃣ Run Tests with Allure Report
```bash
npx cucumber-js
allure serve allure-results
```
- Looks for `.feature` files in **`features/`**
- Loads step definitions in **`steps/`**

### 3️⃣ Run Playwright Tests Without Gherkin
```bash
npx playwright test
```

### 4️⃣ Setting Environment Variables
By default, `.env` is loaded. Override or set them inline:
```bash
USERNAME=tester PASSWORD=secret npx cucumber-js
```
Or on **PowerShell**:
```powershell
$env:USERNAME="******"
$env:PASSWORD="******"
npx cucumber-js
```

### 5️⃣ Running in Headless vs. Headed Mode
In **`hooks.js`**:
```js
this.browser = await chromium.launch({ headless: true });
// Change to 'headless: false' for a visible browser
```

---


## 📊 Generating Reports (Allure Example)

Allure reporting is already configured via **package.json** scripts. To use it:

1️⃣ **Run Tests with Allure Output**:
```bash
npm run test:allure
```
This will generate a JSON report in `./allure-results`.

2️⃣ **Generate & Open Allure Report**:
```bash
npx allure generate ./allure-results --clean
npx allure open ./allure-report
```

---

## 🤖 Tips & Tricks

- **Debug with Playwright Inspector** 🕵️‍♂️  
  Set `headless: false` and `slowMo: 300` in `hooks.js` to watch interactions step by step.

- **Check `process.env` Variables** 🛠️  
  Confirm your `.env` credentials load correctly in step definitions or `helpers.js`.

- **Use Scenario Outlines** 📑  
  In your `.feature` files, handle multiple data sets with the same test steps.

---

## 🤝 Contributing

1️⃣ **Create a new branch** from `main`.
2️⃣ **Add** your changes (features, step definitions, etc.).
3️⃣ **Push** to your fork or branch.
4️⃣ **Open** a Pull Request; **do not** commit `.env` or local lock files.

---

## ⚠️ Attention

- **Keep your `.env` out of source control** (listed in `.gitignore`).
- **Avoid unnecessary plugins**—keep configs clean.
- **Do not push local environment changes** (like `package.json`, `playwright.config.js`, etc.) to `main` without review.

---

## 🎉 Conclusion

By combining **Gherkin + Cucumber + Playwright**, you can:

- ✅ Write **human-readable** tests in `.feature` files
- 🚀 Use **Playwright** for browser automation
- 🔐 Separate **environment-specific** credentials
- 📊 Generate **rich** test reports

**Happy Testing!** 🍀
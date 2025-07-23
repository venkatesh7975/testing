
---

# 🧪 ✅ **Testing in a Vite + React Project with Vitest**

This guide shows how to:

* Set up **Vitest** in a Vite + React project
* Choose between:
  ✅ Fast unit/component tests in a simulated browser (`jsdom`)
  ✅ Real browser tests using Playwright (`chromium`)

---

## 📦 **Step 1: Install Vitest**

In your project root:

```bash
npm install -D vitest
```

> `-D` means it’s a dev dependency.

---

## ✏ **Step 2: Add a test script**

In your `package.json`, add:

```json
"scripts": {
  "test": "vitest"
}
```

Now you can run tests using:

```bash
npm test
```

---

## 🧩 **Step 3: Choose your test environment**

Vitest can run in two modes:

---

## ✅ Option A) Fast React unit/component tests (recommended)

Use the simulated browser environment **jsdom**.
This is enough for:

* Testing React components
* Testing hooks
* DOM manipulation logic

### 👉 vite.config.js

```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  test: {
    environment: 'jsdom',
  },
})
```

That’s it!
No extra browser installation is needed.

Run:

```bash
npm test
```

---

## 🌐 Option B) Real browser tests with Playwright

Useful for:

* Checking how your app behaves in a real browser engine
* Running e2e-style component tests

---

### 1️⃣ Install Playwright

```bash
npm install -D playwright
```

Then download browser binaries:

```bash
npx playwright install
```

---

### 2️⃣ Update vite.config.js

```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  test: {
    browser: {
      enabled: true,
      provider: 'playwright',
      instances: [
        { browser: 'chromium' },
      ],
    },
  },
})
```

---

### ✅ Then run:

```bash
npm test
```

Vitest will open Chromium and run your tests.

> ⚠ Note: First run is slower because it starts a real browser.

---

## 🧪 **Write a simple test example**

Create `src/Sum.test.jsx`:

```jsx
import { expect, test } from 'vitest'

test('adds 1 + 2 to equal 3', () => {
  expect(1 + 2).toBe(3)
})
```

---

## 🎉 **Summary:**

| Mode           | Environment | Needs playwright? | Use when                     |
| -------------- | ----------- | ----------------- | ---------------------------- |
| Fast unit test | jsdom       | ❌ No              | Most React apps              |
| Real browser   | chromium    | ✅ Yes             | e2e / real browser rendering |

---

✅ Use `jsdom` if you only need fast React/component tests.
🌐 Use `browser: { enabled: true }` with Playwright if you need real browsers.

---

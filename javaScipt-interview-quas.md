# JavaScript Runtime Environment (JS Runtime)

A **JavaScript Runtime Environment (JS Runtime)** is the environment where JavaScript code executes. It provides the necessary tools, APIs, and features required to run JavaScript programs outside or inside a browser.

## Components of JavaScript Runtime Environment

A JS runtime typically consists of the following components:

### 1️⃣ JavaScript Engine (e.g., V8, SpiderMonkey, Chakra)
- The **core** component that reads and executes JavaScript code.
- Converts JS code into **machine code** for execution.

#### Examples:
- **Google Chrome & Node.js → V8 Engine**
- **Firefox → SpiderMonkey**
- **Microsoft Edge → Chakra**

### 2️⃣ Call Stack
- A **stack-based** data structure that keeps track of function calls.
- Executes **synchronously** (one task at a time).

### 3️⃣ Web APIs (Only in Browsers)
- Extra features provided by the browser for JavaScript, such as:
  - `setTimeout()`, `fetch()`, `console.log()`
  - DOM manipulation (`document.querySelector()`)
  - Local Storage, Geolocation, etc.

### 4️⃣ Callback Queue & Event Loop
- **Callback Queue:** Stores asynchronous tasks (like `setTimeout()`, `fetch()`).
- **Event Loop:** Manages execution by checking the **Call Stack** and **Callback Queue**, ensuring non-blocking execution.

## Types of JavaScript Runtimes

### 🔹 1. Browser JavaScript Runtime (e.g., Chrome, Firefox, Edge)
- Runs JavaScript inside a web browser.
- Uses the **JS engine + Web APIs + Event Loop**.

### 🔹 2. Node.js JavaScript Runtime
- Runs JavaScript outside the browser (on the server).
- Uses **V8 Engine** but provides its own APIs (like `fs`, `http`).
- No Web APIs, but it has **Node APIs** for file handling, networking, etc.

## How JS Runtime Works? (Execution Flow)

1️⃣ The **JS Engine** reads and executes the code.
2️⃣ The **Call Stack** executes functions synchronously.
3️⃣ If an **async function** is called (`setTimeout`, `fetch`), it goes to **Web APIs** (in the browser).
4️⃣ Once done, the **callback** moves to the **Callback Queue**.
5️⃣ The **Event Loop** moves it back to the **Call Stack** when it's empty.

### Example of Asynchronous Execution in a JS Runtime:

```javascript
console.log("Start");  

setTimeout(() => {
  console.log("Inside setTimeout");
}, 2000);

console.log("End");
```

#### Output:
```
Start
End
Inside setTimeout (after 2 seconds)
```

## 🚀 Conclusion
A **JavaScript Runtime Environment** provides everything required to run JavaScript code efficiently, whether in a browser or in a server environment like **Node.js**.



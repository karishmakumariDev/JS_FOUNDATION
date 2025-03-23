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


# What is Actual JavaScript?

JavaScript is a high-level, interpreted programming language primarily used for adding interactivity to web pages. It is a **multi-paradigm** language, supporting **object-oriented, functional, and event-driven** programming styles.

However, when people ask about **"Actual JavaScript,"** they might be referring to:

- **Core JavaScript (ECMAScript)** – The standardized language definition.
- **JavaScript as implemented in browsers (with Web APIs).**
- **JavaScript running in other environments (like Node.js).**

## 1️⃣ Actual JavaScript = ECMAScript (Core Language Features)

JavaScript follows the **ECMAScript (ES) standard**, which defines the core syntax and functionality of the language.

### ✅ Core JavaScript includes:
- **Variables** (`let`, `const`, `var`)
- **Data types** (Numbers, Strings, Objects, Arrays)
- **Functions & Arrow Functions**
- **Asynchronous Programming** (`setTimeout`, `Promise`, `async/await`)
- **Prototypes & Object-Oriented Programming**
- **ES6+ Features** (Destructuring, Spread Operator, Modules)

#### 🔹 Example of Core JavaScript:
```javascript
let name = "Karishma";
console.log(`Hello, ${name}!`);  // Template literals
```

## 2️⃣ JavaScript in Browsers (with Web APIs)

Browsers provide additional **Web APIs** that are NOT part of the core JavaScript language but are commonly used.

### ✅ Features added in browser environments:
- **DOM Manipulation** (`document.querySelector()`, `innerHTML`)
- **Events** (`addEventListener()`)
- **AJAX & Fetch API** (`fetch()`)
- **Local Storage, Cookies**
- **WebSockets & Geolocation API**

#### 🔹 Example of JavaScript in the browser:
```javascript
document.querySelector("button").addEventListener("click", () => {
  alert("Button Clicked!");
});
```

## 3️⃣ JavaScript in Node.js (Server-Side)

JavaScript can also run **outside** the browser using **Node.js**. Node.js uses the **V8 Engine** but provides additional features like:

### ✅ Node.js Features:
- **File System (`fs`)**
- **Networking (`http` module)**
- **Database Access**

#### 🔹 Example of JavaScript in Node.js:
```javascript
const fs = require("fs");
fs.writeFileSync("hello.txt", "Hello from Node.js");
console.log("File created!");
```

## 🔹 Summary: What is Actual JavaScript?

✅ **Actual JavaScript = ECMAScript (Core Language Features)**  
✅ **Browser JavaScript includes Web APIs (DOM, Fetch, Events).**  
✅ **Node.js JavaScript includes server-side APIs (File system, HTTP).**  

🚀 **In short, JavaScript is a powerful and versatile language that works in different environments!** Let me know if you have any questions. 😊

# Functions in JavaScript

A **function** in JavaScript is a reusable block of code that performs a specific task. Functions help in organizing, reusing, and maintaining code efficiently.

## ✅ **Types of Functions in JavaScript**

### 1️⃣ Function Declaration
A function that is defined using the `function` keyword and can be called before its declaration due to **hoisting**.

🔹 **Example:**
```javascript
function greet(name) {
  return `Hello, ${name}!`;
}
console.log(greet("Karishma"));
```

---

### 2️⃣ Function Expression
A function that is assigned to a variable. It is **not hoisted**, meaning it cannot be called before its definition.

🔹 **Example:**
```javascript
const greet = function(name) {
  return `Hello, ${name}!`;
};
console.log(greet("Karishma"));
```

---

### 3️⃣ Arrow Function
A concise way to write functions using the `=>` syntax. It does not have its own `this` value.

🔹 **Example:**
```javascript
const greet = (name) => `Hello, ${name}!`;
console.log(greet("Karishma"));
```

---

### 4️⃣ Immediately Invoked Function Expression (IIFE)
A function that executes immediately after its definition.

🔹 **Example:**
```javascript
(function() {
  console.log("This function runs immediately!");
})();
```

---

### 5️⃣ Higher-Order Function
A function that takes another function as an argument or returns a function.

🔹 **Example:**
```javascript
function operate(a, b, operation) {
  return operation(a, b);
}
const add = (x, y) => x + y;
console.log(operate(5, 3, add)); // Output: 8
```

---

### 🔹 **Summary**
✅ Functions are reusable blocks of code that perform specific tasks.  
✅ There are multiple types of functions in JavaScript: **Function Declarations, Function Expressions, Arrow Functions, IIFE, and Higher-Order Functions**.  
✅ Functions help in **code reusability, readability, and modularity**.  

🚀 **Mastering functions is crucial for writing efficient JavaScript code!** Let me know if you need more details. 😊

# What is ECMAScript in JavaScript?

## **Introduction**
ECMAScript (ES) is the **standardized specification** for JavaScript. It defines the core syntax, rules, and features of the language. JavaScript follows ECMAScript standards, ensuring consistency across different environments such as web browsers and Node.js.

---

## **Why is ECMAScript Important?**
✅ Ensures **compatibility** of JavaScript across different platforms.
✅ Introduces **new features** and improvements over time.
✅ Helps developers write **modern, optimized code**.

---

## **Major ECMAScript Versions & Features**

### **1️⃣ ES5 (2009) – Foundation for Modern JavaScript**
✅ Introduced **Strict Mode** (`"use strict"`).
✅ Added `JSON.parse()` and `JSON.stringify()` for handling JSON.
✅ Introduced new array methods like `map()`, `filter()`, `reduce()`.

🔹 **Example:**
```javascript
"use strict";
var person = { name: "Karishma", age: 22 };
console.log(Object.keys(person)); // ["name", "age"]
```

---

### **2️⃣ ES6 (2015) – The Biggest Update** 🚀
✅ **let & const** for variable declarations.
✅ **Arrow Functions (`=>`)** for shorter function syntax.
✅ **Template Literals** (`` `Hello, ${name}!` ``).
✅ **Destructuring, Spread Operator, Modules (`import/export`)**.

🔹 **Example:**
```javascript
let name = "Karishma";
const greet = () => `Hello, ${name}!`;
console.log(greet()); // "Hello, Karishma!"
```

---

### **3️⃣ ES7 – ES12 (2016 - 2021) – More Enhancements**
✅ **ES7 (2016):** `includes()` method, `**` exponentiation operator.
✅ **ES8 (2017):** `async/await`, `Object.values()`.
✅ **ES9 (2018):** Rest/Spread properties (`...obj`).
✅ **ES10 (2019):** `flat()`, `flatMap()` for arrays.
✅ **ES11 (2020):** Optional Chaining (`?.`), Nullish Coalescing (`??`).
✅ **ES12 (2021):** Numeric Separators (`1_000_000`), `replaceAll()` method.

🔹 **Example (ES11 – Optional Chaining)**
```javascript
const user = { name: "Karishma", address: { city: "Delhi" } };
console.log(user.address?.city); // "Delhi"
console.log(user.address?.country); // undefined (no error!)
```

---

## **Summary**
✅ **ECMAScript is the official standard** for JavaScript.
✅ JavaScript evolves with ECMAScript updates like **ES5, ES6, ES7+**.
✅ New ECMAScript versions bring **modern, optimized, and easier coding styles**.
✅ **ES6 and later versions** are widely used in modern JavaScript development.

🚀 **Understanding ECMAScript helps in writing clean and efficient JavaScript!** Let me know if you need more details. 😊




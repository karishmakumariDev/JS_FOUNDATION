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

# First-Class Citizen in JavaScript

## What is a First-Class Citizen?

In JavaScript, functions are treated as **first-class citizens**, meaning they can be:
- Stored in variables
- Passed as arguments to other functions
- Returned from other functions

Since functions in JavaScript can be used like any other value (e.g., numbers, strings), they are considered **first-class citizens**.

## ✅ Examples of First-Class Functions

### 1️⃣ Storing a function in a variable
```javascript
const sayHello = function() {
  return "Hello, Karishma!";
};
console.log(sayHello()); // Output: Hello, Karishma!
```

### 2️⃣ Passing a function as an argument (Higher-Order Function)
```javascript
function executeFunction(func) {
  console.log(func()); // Calling the passed function
}
executeFunction(sayHello); // Output: Hello, Karishma!
```

### 3️⃣ Returning a function from another function
```javascript
function outerFunction() {
  return function() {
    return "I am returned from another function!";
  };
}
const newFunc = outerFunction(); // Storing the returned function
console.log(newFunc()); // Output: I am returned from another function!
```

### 4️⃣ Assigning a function to an array element
```javascript
const functionArray = [];
functionArray.push(sayHello);
console.log(functionArray[0]()); // Output: Hello, Karishma!
```

### 5️⃣ Assigning a function to an object property
```javascript
const obj = {
  sayHi: sayHello
};
console.log(obj.sayHi()); // Output: Hello, Karishma!
```

## 🔹 Closures in JavaScript

A **closure** is when an inner function remembers the variables of its outer function even after the outer function has finished execution.

### ✅ Easy Example of a Closure
```javascript
function counter() {
  let count = 0;
  return function() {
    count++;
    console.log(`Current count: ${count}`);
  };
}

const increment = counter();
increment(); // Output: Current count: 1
increment(); // Output: Current count: 2
increment(); // Output: Current count: 3
```

### ✅ Another Example of a Closure
```javascript
function shopkeeper(name) {
  return function() {
    console.log(`नमस्ते ${name}, फिर से स्वागत है!`);
  };
}

const customer1 = shopkeeper("करिश्मा");
customer1(); // Output: नमस्ते करिश्मा, फिर से स्वागत है!

const customer2 = shopkeeper("पीयूष");
customer2(); // Output: नमस्ते पीयूष, फिर से स्वागत है!
```

### Explanation:
1️⃣ `counter` function initializes a variable `count` and returns an inner function.
2️⃣ The inner function increments `count` and logs its value.
3️⃣ Even after `counter()` execution is completed, the returned function **remembers** `count` due to closure.
4️⃣ The `shopkeeper` function demonstrates how an inner function remembers the `name` variable even after `shopkeeper` execution is finished.

## 🔹 Summary
✅ JavaScript functions are **first-class citizens** because they can be treated like values.  
✅ Functions can be **stored, passed, and returned** like any other data type.  
✅ **Higher-Order Functions** rely on this concept.  
✅ **Closures** allow inner functions to retain access to variables of their outer functions.

🚀 **First-Class Functions and Closures are essential concepts in JavaScript!**

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


# Execution Context and Hoisting in JavaScript

## Execution Context

Execution Context is the environment where JavaScript code is executed. It consists of the variables, functions, and the scope in which the code runs.

### Types of Execution Contexts

1️⃣ **Global Execution Context (GEC)**
   - Created when the JavaScript file starts executing.
   - `this` in the global context refers to the global object (`window` in browsers, `global` in Node.js).

2️⃣ **Function Execution Context (FEC)**
   - Created whenever a function is called.
   - Each function gets its own execution context.

3️⃣ **Eval Execution Context**
   - Created when code is executed inside the `eval()` function.

### Phases of Execution Context

1️⃣ **Creation Phase**
   - Memory is allocated for variables and functions.
   - `this` is assigned a value.
   - Functions are stored in memory, and variables are set to `undefined` (hoisting).

2️⃣ **Execution Phase**
   - Code is executed line by line.
   - Variables are assigned values, and function calls are made.

## Hoisting in JavaScript

Hoisting is JavaScript's behavior of moving variable and function declarations to the top of their scope during the Creation Phase.

### ✅ Example of Hoisting

```javascript
console.log(myVar); // Output: undefined
var myVar = 10;
console.log(myVar); // Output: 10
```

**Explanation:**
- During the Creation Phase, `myVar` is hoisted and set to `undefined`.
- In the Execution Phase, when `console.log(myVar)` is executed before assignment, it prints `undefined`.

### ✅ Function Hoisting Example

```javascript
hello(); // Output: Hello, World!

function hello() {
  console.log("Hello, World!");
}
```

**Explanation:**
- Function declarations are hoisted entirely, meaning the function can be called before it is defined in the code.

### ✅ Hoisting with `let` and `const`

```javascript
console.log(myLetVar); // ReferenceError: Cannot access 'myLetVar' before initialization
let myLetVar = 5;
```

**Explanation:**
- Variables declared with `let` and `const` are hoisted but are in a "temporal dead zone" until they are assigned a value.

## 🔹 Summary
✅ JavaScript execution context determines how code is executed.
✅ There are three types: **Global Execution Context, Function Execution Context, and Eval Execution Context**.
✅ Execution Context has two phases: **Creation Phase and Execution Phase**.
✅ **Hoisting** moves function and variable declarations to the top of their scope.
✅ `var` variables are hoisted with `undefined`, while `let` and `const` are in the **temporal dead zone**.

🚀 **Understanding Execution Context and Hoisting is essential for mastering JavaScript!**

# Scope in JavaScript

Scope refers to the accessibility of variables, functions, and objects in different parts of the code. It determines where a variable can be accessed.

## Types of Scope in JavaScript:
1. Global Scope
2. Local/Function Scope
3. Block Scope

### 1. Global Scope
A variable declared outside any function is in the global scope.
It can be accessed from anywhere in the program.

#### Example:
```javascript
let globalVar = "I am global";

function show() {
    console.log(globalVar); // Accessible here
}

show();
console.log(globalVar); // Accessible here too
```

### 2. Local/Function Scope
Variables declared inside a function are function-scoped.
They can only be accessed within that function.

#### Example:
```javascript
function greet() {
    let message = "Hello, Karishma!";
    console.log(message); // Accessible here
}

greet();
console.log(message); // ❌ Error: message is not defined
```

### 3. Block Scope
Variables declared using `let` and `const` inside `{}` (curly braces) are block-scoped.
They can only be accessed within that block.

#### Example:
```javascript
{
    let blockVar = "Inside block";
    console.log(blockVar); // Accessible here
}

console.log(blockVar); // ❌ Error: blockVar is not defined
```
**Note:** `var` does not have block scope; it is function-scoped.

## Lexical Scope
In JavaScript, functions are lexically scoped, meaning a function can access variables from its outer (parent) scope but not vice versa.

#### Example:
```javascript
function outerFunction() {
    let outerVar = "I am outer";

    function innerFunction() {
        console.log(outerVar); // ✅ Accessible due to lexical scope
    }

    innerFunction();
}

outerFunction();
console.log(outerVar); // ❌ Error: outerVar is not defined
```
👉 Here, `innerFunction` can access `outerVar` because it's inside `outerFunction`, but the reverse is not possible.

## Scope Chain
If a variable is not found in the current scope, JavaScript looks in the outer scope and continues up the chain until it reaches the global scope.
If the variable is not found in the entire chain, it results in a **ReferenceError**.

#### Example:
```javascript
let globalVar = "I am global";

function firstFunction() {
    let firstVar = "I am in firstFunction";

    function secondFunction() {
        let secondVar = "I am in secondFunction";
        console.log(globalVar); // ✅ Found in global scope
        console.log(firstVar); // ✅ Found in firstFunction scope
        console.log(secondVar); // ✅ Found in secondFunction scope
    }

    secondFunction();
    console.log(secondVar); // ❌ Error: secondVar is not defined
}

firstFunction();
```

👉 **How the Scope Chain Works Here:**
- `secondFunction` looks for `globalVar` → ✅ Found in the **global scope**.
- `secondFunction` looks for `firstVar` → ✅ Found in `firstFunction` (its parent scope).
- `secondFunction` looks for `secondVar` → ✅ Found in its own scope.
- `firstFunction` tries to access `secondVar` → ❌ Error (not in scope).

## Summary
| Scope Type        | Accessible From |
|------------------|----------------|
| Global Scope    | Anywhere in the program |
| Function Scope  | Only inside the function |
| Block Scope     | Only inside `{}` (let, const) |
| Lexical Scope   | Inner function can access outer function’s variables |
| Scope Chain     | Looks for variables in parent scopes if not found locally |

### JavaScript Interview Questions on `var` Keyword & Function Scope

#### 1. What is the difference between `var`, `let`, and `const`?
**Answer:**  
- `var` is **function-scoped**, while `let` and `const` are **block-scoped**.
- `var` allows **re-declaration**, while `let` and `const` do **not**.
- `const` must be **initialized at declaration** and cannot be **reassigned**.

**Example:**
```javascript
function example() {
    var a = 10;
    let b = 20;
    const c = 30;
    if (true) {
        var a = 40; // ✅ Allowed (Re-declaration inside function scope)
        let b = 50; // ✅ Allowed (Block scope)
        const c = 60; // ✅ Allowed (Block scope)
        console.log(a, b, c); // 40 50 60
    }
    console.log(a); // 40
    console.log(b); // 20
    console.log(c); // 30
}
example();
```

---

#### 2. Does `var` have block scope?
**Answer:**  
No, `var` does **not** have block scope. It is **function-scoped**, meaning that a `var` declared inside a block (`{}`) is still accessible outside that block if within the same function.

**Example:**
```javascript
function test() {
    if (true) {
        var x = 10;
    }
    console.log(x); // ✅ Accessible, prints 10
}
test();
```

---

#### 3. What happens if you declare `var` multiple times in the same function?
**Answer:**  
If you declare `var` multiple times, the last assigned value **overwrites** the previous one.

**Example:**
```javascript
function duplicateVar() {
    var x = 10;
    var x = 20; // No error, allowed in function scope
    console.log(x); // 20
}
duplicateVar();
```

---

#### 4. Can `var` be accessed before declaration?
**Answer:**  
Yes, due to **hoisting**, `var` declarations are **moved** to the top of their scope but remain `undefined` until assigned a value.

**Example:**
```javascript
console.log(a); // ✅ No error, but prints undefined
var a = 10;
```

---

#### 5. What is function scope in JavaScript?
**Answer:**  
Function scope means that **variables declared inside a function using `var` are only accessible within that function**.

**Example:**
```javascript
function myFunction() {
    var localVar = "I am local";
    console.log(localVar); // ✅ Accessible here
}

myFunction();
console.log(localVar); // ❌ Error: localVar is not defined
```

---

#### 6. What happens when `var` is declared inside a function and accessed outside?
**Answer:**  
It results in a **ReferenceError** because `var` is function-scoped and not accessible outside the function.

**Example:**
```javascript
function testScope() {
    var insideVar = "Inside Function";
}
console.log(insideVar); // ❌ ReferenceError: insideVar is not defined
```

---

#### 7. What is the effect of using `var` inside nested functions?
**Answer:**  
A variable declared with `var` inside a function is accessible **within that function and its inner functions** but **not outside**.

**Example:**
```javascript
function outerFunction() {
    var outerVar = "I am outer";

    function innerFunction() {
        console.log(outerVar); // ✅ Accessible due to function scope
    }

    innerFunction();
}
outerFunction();
console.log(outerVar); // ❌ Error: outerVar is not defined
```

---

#### 8. Does `var` support block scope inside loops?
**Answer:**  
No, `var` does **not** have block scope. It leaks out of the loop block.

**Example:**
```javascript
for (var i = 0; i < 3; i++) {
    console.log(i); // ✅ 0, 1, 2
}
console.log(i); // ✅ Still accessible, prints 3
```

---

#### 9. Can `var` variables be updated and redeclared?
**Answer:**  
Yes, `var` variables can be **redeclared** and **updated** within the same scope.

**Example:**
```javascript
var x = 5;
var x = 10; // ✅ No error, allowed
console.log(x); // 10

x = 20; // ✅ Updated successfully
console.log(x); // 20
```

---

#### 10. What is the impact of using `var` in global scope?
**Answer:**  
A `var` declared in the **global scope** becomes a **property of the `window` object** in browsers.

**Example:**
```javascript
var globalVar = "I am global";
console.log(window.globalVar); // ✅ "I am global"
```

---

### **Summary Table**
| Question | Answer |
|----------|--------|
| `var` vs `let` vs `const` | `var` is function-scoped, `let` and `const` are block-scoped |
| Does `var` have block scope? | No, only function scope |
| Multiple `var` declarations? | Allowed, last value overwrites previous |
| Accessing `var` before declaration? | Yes, due to hoisting, but value is `undefined` |
| What is function scope? | Variables declared in a function are only accessible inside it |
| Accessing `var` outside function? | Not possible, results in a `ReferenceError` |
| `var` inside nested functions? | Accessible inside inner functions but not outside parent function |
| `var` in loops? | Leaks outside loop block |
| Can `var` be updated/redeclared? | Yes, both are allowed |
| Global `var` impact? | Becomes `window` property in browsers |

---

### **Conclusion**
- Use **`let`** and **`const`** instead of `var` to avoid **unexpected behavior**.
- Prefer `let` for variables that change and `const` for constants.
- Avoid polluting the **global scope** with `var`.

# Mutable vs Immutable in JavaScript

In JavaScript, **mutability** and **immutability** refer to whether a value can be changed after it is created.

## 1. Mutable (Changeable)
Mutable data types can be modified after their creation. Any changes made to them affect the original value.

### Examples of Mutable Data Types:
- **Objects**
- **Arrays**
- **Functions**

### Example of Mutable Data (Object)
```javascript
let person = { name: "Karishma", age: 25 };

person.age = 26; // ✅ Modifying the object
console.log(person); // { name: "Karishma", age: 26 }
```
Here, the `person` object is **mutable** because we changed its `age` property.

### Example of Mutable Data (Array)
```javascript
let numbers = [1, 2, 3];
numbers.push(4); // ✅ Adding element to the array
console.log(numbers); // [1, 2, 3, 4]
```
Here, the array is **mutable** because we modified it by adding a new element.

---

## 2. Immutable (Unchangeable)
Immutable data types **cannot be changed** once they are created. If you need to modify them, you have to create a new value.

### Examples of Immutable Data Types:
- **Primitive Data Types:**
  - `String`
  - `Number`
  - `Boolean`
  - `BigInt`
  - `Symbol`
  - `Undefined`
  - `Null`

### Example of Immutable Data (String)
```javascript
let str = "Hello";
str[0] = "M"; // ❌ No effect
console.log(str); // "Hello" (unchanged)
```
Here, strings are **immutable**, so modifying a character does not change the original string.

### Example of Creating a New Immutable Value
```javascript
let name = "Karishma";
let newName = name + " Saini"; // ✅ Creates a new string
console.log(newName); // "Karishma Saini"
```
Instead of modifying `name`, JavaScript created a **new** string.

---

## 3. How to Make Objects Immutable?
By default, objects and arrays are **mutable**, but we can prevent changes using:  

### **1. `Object.freeze()` (Completely Freezes an Object)**
```javascript
let user = { name: "Piyush", age: 20 };
Object.freeze(user); // ❌ Now, changes are not allowed

user.age = 21; // ❌ No effect
console.log(user.age); // 20 (unchanged)
```

### **2. `Object.seal()` (Allows Modification but No New Properties)**
```javascript
let user = { name: "Piyush", age: 20 };
Object.seal(user);

user.age = 21; // ✅ Allowed
user.city = "Delhi"; // ❌ Not allowed (new properties cannot be added)
console.log(user); // { name: "Piyush", age: 21 }
```

---

## Summary Table

| Data Type  | Mutable or Immutable? | Example |
|------------|----------------------|---------|
| Object     | Mutable | `{ name: "Karishma" }` → Can modify properties |
| Array      | Mutable | `[1, 2, 3]` → Can add/remove elements |
| String     | Immutable | `"Hello"` → Cannot change characters |
| Number     | Immutable | `10` → Cannot change |
| Boolean    | Immutable | `true` → Cannot change |

---

Would you like more examples or explanations? 😊

# Pure vs Impure Functions in JavaScript

## 1. Pure Functions  
A **pure function** is a function that:  
✅ **Always returns the same output** for the same input.  
✅ **Has no side effects** (does not modify external state, global variables, DOM, etc.).  

### Example of a Pure Function
```javascript
function add(a, b) {
    return a + b; // ✅ No external modifications, always returns the same output
}

console.log(add(2, 3)); // 5
console.log(add(2, 3)); // 5 (Same input, same output)
```
✅ The function does not modify anything outside itself.  

---

## 2. Impure Functions  
An **impure function** does one or both of the following:  
❌ **Modifies global state or external variables**  
❌ **Has side effects** (changes DOM, logs to console, fetches data, etc.)  

### Example of an Impure Function (Modifies External State)
```javascript
let count = 0;

function increment() {
    count++; // ❌ Modifies external state (global variable)
    return count;
}

console.log(increment()); // 1
console.log(increment()); // 2 (Different output for same function call)
```
❌ The function changes the global `count`, making it **impure**.  

### Example of an Impure Function (Side Effects: Console Log & DOM Change)
```javascript
function updateTitle() {
    document.title = "New Title"; // ❌ Side effect: Modifies webpage
}

updateTitle();
```
❌ This function is impure because it **modifies the DOM**.  

### Example of an Impure Function (Fetching Data)
```javascript
function fetchData() {
    fetch("https://api.example.com/data") // ❌ Side effect: Network request
        .then(response => response.json())
        .then(data => console.log(data));
}

fetchData(); // Calls an external API
```
❌ This function is impure because it depends on an external API call.

---

## How to Make an Impure Function Pure?  
Instead of modifying external state, return a **new value**.  

### ✅ Refactored to a Pure Function
```javascript
function incrementPure(count) {
    return count + 1; // ✅ Returns a new value instead of modifying global variable
}

console.log(incrementPure(0)); // 1
console.log(incrementPure(0)); // 1 (Same input, same output)
```
✅ Now the function is **pure** because it does not modify external state.  

### ✅ Refactored Fetch Function (Pure Alternative)
```javascript
async function getData(url) {
    const response = await fetch(url); // ✅ No side effects, takes input and returns output
    return response.json();
}

getData("https://api.example.com/data").then(data => console.log(data));
```
✅ The function now takes an input (`url`) and returns output (`data`) without modifying external state directly.

---

## Summary Table  

| Feature | Pure Function ✅ | Impure Function ❌ |
|---------|-----------------|-----------------|
| **Same Input, Same Output?** | ✅ Yes | ❌ No |
| **Side Effects?** | ❌ No | ✅ Yes |
| **Modifies External State?** | ❌ No | ✅ Yes |
| **Example** | `Math.abs(-5) → 5` | `console.log("Hello")` |



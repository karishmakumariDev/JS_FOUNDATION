# Recursion and Stack: Easy Explanation

## What is Recursion?
Recursion is a technique where a function calls itself to solve a smaller version of the same problem.

It is useful when:
- A problem can be broken into smaller subproblems of the same kind.
- The solution can be built step by step using previous results.
- Certain data structures, like trees, require recursive solutions.

### Example: Calculating Power (x^n)
Let's say we want to calculate x raised to the power n, i.e., `x^n`.

### Method 1: Using a Loop (Iterative Approach)
```js
function pow(x, n) {
  let result = 1;
  for (let i = 0; i < n; i++) {
    result *= x;
  }
  return result;
}

console.log(pow(2, 3)); // Output: 8
```
Here, we run a loop `n` times and multiply `x` repeatedly.

### Method 2: Using Recursion
```js
function pow(x, n) {
  if (n == 1) {
    return x;
  } else {
    return x * pow(x, n - 1);
  }
}

console.log(pow(2, 3)); // Output: 8
```
#### How Recursion Works:
1. **Base Case**: If `n == 1`, return `x`.
2. **Recursive Step**: `pow(x, n)` is calculated as `x * pow(x, n - 1)`, reducing the problem size each time.
3. The function keeps calling itself until it reaches `n == 1`, then starts returning values back up the chain.

### Step-by-Step Execution of `pow(2, 3)`:
```
pow(2, 3) = 2 * pow(2, 2)
pow(2, 2) = 2 * pow(2, 1)
pow(2, 1) = 2
```
When `pow(2, 1)` returns `2`, the results start getting multiplied as they return:
```
pow(2, 2) = 2 * 2 = 4
pow(2, 3) = 2 * 4 = 8
```

## Execution Context and Call Stack
When a function runs, JavaScript stores its execution details (like variables and position in code) in the **execution context**.

### What Happens During Recursive Calls?
Each recursive call stores its execution context in the **call stack**.
1. `pow(2, 3)` is called → Stored in stack
2. `pow(2, 2)` is called → Stored in stack
3. `pow(2, 1)` is called → Stored in stack
4. `pow(2, 1)` returns `2` → Removed from stack
5. `pow(2, 2)` resumes, returns `4` → Removed from stack
6. `pow(2, 3)` resumes, returns `8` → Removed from stack

Each time a function finishes, its execution context is removed from the stack, freeing memory.

## Memory Usage: Recursion vs Loop
- **Recursion**: Uses memory for every function call in the stack.
- **Loop**: Uses a single memory space, making it more memory-efficient.

### Which One to Use?
- **Use recursion** when the problem is naturally recursive (e.g., tree traversal, factorial, Fibonacci numbers).
- **Use loops** when memory optimization is needed, or recursion depth might be too high.

### Summary
- Recursion is when a function calls itself.
- It breaks a problem into smaller subproblems until it reaches a base case.
- Each call is stored in the call stack and removed when it completes.
- Recursion can be memory-heavy, but it simplifies code in some cases.
- Loops are often more efficient but may require extra logic.

### Example of Tail Recursion (Optimized Recursion)
Some languages optimize recursion using **tail recursion**, where the recursive call is the last operation in a function.
```js
function powTail(x, n, result = 1) {
  if (n == 0) return result;
  return powTail(x, n - 1, result * x);
}

console.log(powTail(2, 3)); // Output: 8
```
This avoids adding extra stack frames, reducing memory usage.

Recursion is powerful but should be used wisely! 🚀
# Recursive Traversals and Data Structures

## Recursive Traversals

Recursion is a powerful technique in programming, and one of its key applications is recursive traversal.

### Example: Company Staff Structure

Consider a company with a hierarchical structure:

```javascript
let company = {
  sales: [{ name: 'John', salary: 1000 }, { name: 'Alice', salary: 1600 }],
  development: {
    sites: [{ name: 'Peter', salary: 2000 }, { name: 'Alex', salary: 1800 }],
    internals: [{ name: 'Jack', salary: 1300 }]
  }
};
```

In this structure:
- Some departments contain employees directly (as an array of objects).
- Other departments are divided into subdepartments, each with its own employees.
- This can continue indefinitely, forming a recursive structure.

### Summing All Salaries Using Recursion

An iterative approach to summing all salaries would be complex due to the nested structure. Instead, recursion provides a cleaner solution:

```javascript
function sumSalaries(department) {
  if (Array.isArray(department)) {
    return department.reduce((total, employee) => total + employee.salary, 0);
  } else {
    let sum = 0;
    for (let subdep of Object.values(department)) {
      sum += sumSalaries(subdep);
    }
    return sum;
  }
}

alert(sumSalaries(company)); // Output: 7700
```

### Explanation
1. **Base Case**: If `department` is an array, sum the salaries using `reduce()`.
2. **Recursive Case**: If `department` is an object, iterate over its subdepartments and recursively sum their salaries.
3. The recursion continues until it reaches the lowest level (individual employees), and their salaries are summed up.

## Recursive Data Structures

### Definition
A **recursive data structure** is a structure that is defined in terms of itself.

Examples:
- A company department can contain subdepartments, forming a recursive tree.
- HTML documents follow a recursive structure where elements contain other elements.

### Example: Linked List

Arrays are commonly used for ordered collections, but they have performance drawbacks when inserting or deleting elements at the beginning. A **linked list** provides a more efficient alternative.

#### Linked List Structure

A linked list consists of nodes, each containing:
- A `value` (the data stored in the node).
- A `next` reference pointing to the next node (or `null` if it’s the last node).

```javascript
let list = {
  value: 1,
  next: {
    value: 2,
    next: {
      value: 3,
      next: {
        value: 4,
        next: null
      }
    }
  }
};
```

#### Alternative Way to Create a Linked List

```javascript
let list = { value: 1 };
list.next = { value: 2 };
list.next.next = { value: 3 };
list.next.next.next = { value: 4 };
list.next.next.next.next = null;
```

### Linked List Operations

#### Inserting an Element at the Beginning
```javascript
list = { value: "new item", next: list };
```

#### Removing an Element from the Middle
```javascript
list.next = list.next.next;
```

### Linked List vs. Array
| Feature       | Array | Linked List |
|--------------|-------|-------------|
| Fast random access | ✅ | ❌ |
| Efficient insert/delete at start | ❌ | ✅ |
| Uses contiguous memory | ✅ | ❌ |

## Summary

### Key Terms
- **Recursion**: A function calling itself to solve a problem.
- **Recursive Step**: The point where the function calls itself.
- **Base Case**: The condition where recursion stops.
- **Recursive Data Structure**: A structure defined in terms of itself (e.g., trees, linked lists).

### Takeaways
- Recursion makes traversing complex structures like company hierarchies and trees easier.
- Linked lists provide efficient insertion and deletion but are slower for random access.
- Recursion should be used wisely, as excessive recursion can lead to performance issues.

This structured approach simplifies recursive concepts while keeping the depth intact.


# Rest Parameters and Spread Syntax

## Rest Parameters (...)
In JavaScript, functions can accept any number of arguments, even if they are not explicitly defined in the function.

### Example:
```js
function sum(a, b) {
  return a + b;
}

console.log(sum(1, 2, 3, 4, 5)); // Output: 3 (only first two are used)
```
Here, the function only uses the first two parameters, and the rest are ignored.

### Using Rest Parameters
Rest parameters allow us to collect all remaining arguments into an array.

```js
function sumAll(...args) { // args is an array
  let sum = 0;
  for (let arg of args) sum += arg;
  return sum;
}

console.log(sumAll(1)); // 1
console.log(sumAll(1, 2)); // 3
console.log(sumAll(1, 2, 3)); // 6
```

### Using Rest Parameters with Named Parameters
We can also use named parameters before rest parameters.

```js
function showName(firstName, lastName, ...titles) {
  console.log(firstName + ' ' + lastName); // Julius Caesar
  console.log(titles[0]); // Consul
  console.log(titles[1]); // Imperator
  console.log(titles.length); // 2
}

showName("Julius", "Caesar", "Consul", "Imperator");
```

### Important Rule:
Rest parameters must always be at the **end** of the function parameter list.

```js
function f(arg1, ...rest, arg2) { // ❌ Error
  // rest must be the last parameter
}
```

## Spread Syntax (...)
Spread syntax allows an array (or object) to be expanded into individual elements.

### Example:
```js
let numbers = [3, 5, 1];
console.log(Math.max(...numbers)); // Output: 5
```

### Combining Arrays with Spread
```js
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let combined = [...arr1, ...arr2];
console.log(combined); // [1, 2, 3, 4, 5, 6]
```

### Copying Arrays
```js
let original = [1, 2, 3];
let copy = [...original];
console.log(copy); // [1, 2, 3]
```

### Conclusion
- **Rest parameters (`...args`)** collect multiple arguments into an array.
- **Spread syntax (`...array`)** expands elements of an array (or object) into individual values.
- Rest parameters must be **at the end** of the function parameters.
- Spread syntax is useful for **copying, merging, and passing array elements as function arguments**.

**Understanding Rest Parameters and Spread Syntax in JavaScript**

### Rest Parameters (...)
Sometimes, we may need to pass multiple arguments to a function, but we don’t know how many. This is where **rest parameters** come in handy.

#### Example:
```javascript
function sumAll(...numbers) {
  let sum = 0;
  for (let num of numbers) {
    sum += num;
  }
  return sum;
}

console.log(sumAll(1, 2, 3, 4, 5)); // Output: 15
```
- The `...numbers` gathers all extra arguments into an array.
- We can then use this array inside the function.

#### Important Rules:
1. A function can have only **one** rest parameter.
2. The rest parameter **must be the last** in the function parameter list.

```javascript
function incorrectUsage(...nums, lastNum) {
  // This will cause an error
}
```

### The "arguments" Object
Before rest parameters were introduced, JavaScript provided the `arguments` object.

```javascript
function showArgs() {
  console.log(arguments[0]); // First argument
  console.log(arguments.length); // Number of arguments
}

showArgs("Hello", "World");
```
- **Limitations of `arguments`:**
  - It is **not an array**, so array methods like `.map()` or `.forEach()` won’t work.
  - It contains **all arguments**, we cannot select only a part of them.

### Spread Syntax (...)
The **spread syntax** is used to **expand** an array into individual elements.

#### Example:
```javascript
let numbers = [3, 5, 1];
console.log(Math.max(...numbers)); // Output: 5
```

Here, `...numbers` expands `[3, 5, 1]` into `3, 5, 1`, which `Math.max()` understands.

#### Merging Arrays:
```javascript
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let merged = [...arr1, ...arr2];
console.log(merged); // Output: [1, 2, 3, 4, 5, 6]
```

#### Copying an Array:
```javascript
let original = [1, 2, 3];
let copy = [...original];
console.log(copy); // Output: [1, 2, 3]
```

### Spread Syntax with Objects
We can use spread syntax to copy or merge objects.

```javascript
let obj1 = { a: 1, b: 2 };
let obj2 = { c: 3, d: 4 };
let mergedObj = { ...obj1, ...obj2 };
console.log(mergedObj); // Output: { a: 1, b: 2, c: 3, d: 4 }
```

### Summary
- **Rest parameters (`...`)** collect extra arguments into an array.
- **Spread syntax (`...`)** expands an array or object into individual elements.
- `arguments` is an older way to access function arguments but is limited.
- Use **spread syntax** for copying and merging arrays/objects.

Rest and spread syntax make working with JavaScript functions and arrays much easier!

#########################################################

**Variable Scope and Closures in JavaScript**

JavaScript is a very flexible language that allows functions to be created, passed as arguments, and called from different places in the code. In this document, we will learn about variable scope and closures in an easy way.

### **Variable Scope**

Scope defines where a variable can be accessed in the code. There are three types of scopes in JavaScript:

1. **Global Scope:** A variable declared outside any function or block is available everywhere in the code.
2. **Function Scope:** A variable declared inside a function is accessible only within that function.
3. **Block Scope:** Variables declared using `let` and `const` inside a block `{}` are only available inside that block.

#### **Example of Block Scope**
```js
{
  let message = "Hello"; // Only visible inside this block
  console.log(message); // Output: Hello
}

console.log(message); // Error: message is not defined
```

If a variable is declared inside a block, it cannot be accessed outside that block.

#### **Block Scope in Loops and Conditions**
```js
if (true) {
  let phrase = "Hello!";
  console.log(phrase); // Output: Hello!
}

console.log(phrase); // Error: phrase is not defined
```
In the example above, `phrase` is only accessible inside the `if` block.

Similarly, variables inside a `for` loop are only available inside the loop:
```js
for (let i = 0; i < 3; i++) {
  console.log(i); // Outputs: 0, 1, 2
}

console.log(i); // Error: i is not defined
```

### **Closures in JavaScript**

A **closure** is a function that remembers variables from its outer scope even after the outer function has finished execution.

#### **Example of a Closure**
```js
function outerFunction() {
  let outerVariable = "I am from outer function";
  
  function innerFunction() {
    console.log(outerVariable); // Inner function can access outerVariable
  }
  
  return innerFunction;
}

const myClosure = outerFunction();
myClosure(); // Output: I am from outer function
```

In this example, `innerFunction` is returned from `outerFunction`, but it still remembers the `outerVariable`. This is the power of closures.

### **Why Are Closures Useful?**
1. **Data Privacy:** Closures help to create private variables that cannot be accessed directly from outside.
2. **Callbacks and Event Handlers:** Closures are used in asynchronous programming, like in event listeners and setTimeout functions.
3. **Function Factories:** Closures help create functions dynamically based on different values.

#### **Example of Data Privacy using Closures**
```js
function counter() {
  let count = 0;
  
  return function () {
    count++;
    console.log(count);
  };
}

const myCounter = counter();
myCounter(); // Output: 1
myCounter(); // Output: 2
myCounter(); // Output: 3
```
Here, the `count` variable is private and cannot be accessed directly, ensuring data privacy.

### **Summary**
- **Scope** determines where a variable can be accessed.
- **Block Scope** means variables inside `{}` are only available inside the block.
- **Closures** allow functions to remember variables from their outer scope even after the function has finished executing.
- **Closures** are useful for data privacy, callbacks, and function factories.

This makes JavaScript powerful and flexible when handling functions and variables efficiently.

**Nested Functions and Lexical Environment in JavaScript (Easy Explanation)**

### **What are Nested Functions?**
A function is called "nested" when it is written inside another function. In JavaScript, this is very common and useful for organizing code.

#### **Example:**
```js
function sayHiBye(firstName, lastName) {
  // A helper function inside sayHiBye
  function getFullName() {
    return firstName + " " + lastName;
  }
  alert("Hello, " + getFullName());
  alert("Bye, " + getFullName());
}
```
Here, **getFullName()** is a function inside **sayHiBye()**. It can access **firstName** and **lastName** because it is inside the same function.

---
### **Returning a Nested Function**
A nested function can be returned and used somewhere else. Even when it is used outside, it still remembers the outer function’s variables.

#### **Example:**
```js
function makeCounter() {
  let count = 0;
  return function () {
    return count++;
  };
}
let counter = makeCounter();
alert(counter()); // 0
alert(counter()); // 1
alert(counter()); // 2
```
Here, **counter** is a function that remembers the **count** variable even after **makeCounter()** has finished running.

---
### **Understanding Lexical Environment**
When JavaScript runs code, it creates a special hidden object called the **Lexical Environment**.

#### **Lexical Environment Contains:**
1. **Environment Record** – Stores all variables inside a function.
2. **Outer Reference** – A link to the outer function's variables.

Every time a function is called, a new **Lexical Environment** is created for it. If the function has nested functions, they get their own **Lexical Environment** but still have access to the outer function’s variables.

#### **Example:**
```js
function outer() {
  let outerVar = "I am outer";
  function inner() {
    alert(outerVar); // Can access outerVar
  }
  return inner;
}
let innerFunction = outer();
innerFunction(); // Still has access to outerVar
```
Even after **outer()** has finished running, **innerFunction()** can still access **outerVar** because of the **Lexical Environment**.

---
### **Key Takeaways**
- **Nested functions** can access variables from the outer function.
- **Returning functions** keeps the outer variables alive.
- **Lexical Environment** keeps track of variables and where they belong.
- Even if a function runs later, it remembers the outer function’s variables.

This concept is useful in JavaScript when working with closures, event listeners, and callbacks! 🚀
**Step 2: Function Declarations**
A function in JavaScript is like a value, similar to a variable.

However, there is a key difference: A Function Declaration is fully initialized immediately when it is defined.

When JavaScript creates a Lexical Environment (a place where variables and functions are stored during execution), a Function Declaration is instantly available for use. This means we can call the function even before its actual declaration in the code.

For example:

```js
sayHello(); // Works even before the function is declared

function sayHello() {
  console.log("Hello!");
}
```

This behavior applies only to Function Declarations, not to Function Expressions (functions assigned to variables), like:

```js
let sayHello = function() {
  console.log("Hello!");
};
```

Here, we cannot call `sayHello()` before its definition because it behaves like a normal variable.

---

**Step 3: Inner and Outer Lexical Environment**
When a function runs, JavaScript automatically creates a new Lexical Environment to store local variables and function parameters.

For example:

```js
let phrase = "Hello";

function say(name) {
  console.log(phrase + ", " + name);
}

say("John");
```

Here’s how JavaScript handles it:
1. A global Lexical Environment is created, containing `phrase` and the `say` function.
2. When `say("John")` is called, a new inner Lexical Environment is created.
3. This new environment contains only the parameter `name = "John"`.
4. When `phrase` is needed, JavaScript first looks inside the inner environment but doesn’t find it. Then, it checks the outer global environment and finds `phrase = "Hello"`.

So, the function can access variables from its outer Lexical Environment but not the other way around.

---

**Step 4: Returning a Function (Closures)**
Let’s look at an example where a function returns another function:

```js
function makeCounter() {
  let count = 0;

  return function() {
    return count++;
  };
}

let counter = makeCounter();
console.log(counter()); // 0
console.log(counter()); // 1
console.log(counter()); // 2
```

### How it works:
1. `makeCounter()` is called, creating a new Lexical Environment with `count = 0`.
2. The function inside `makeCounter()` is returned and stored in `counter`.
3. Even after `makeCounter()` has finished executing, the returned function still remembers `count` because of closures.

Closures allow functions to remember variables from their outer scope even after the outer function has finished executing.

---

**Garbage Collection and Memory Management**
Normally, when a function finishes, its variables are removed from memory.

However, if an inner function is still being used, JavaScript keeps the Lexical Environment in memory.

For example:

```js
function f() {
  let value = 123;

  return function() {
    console.log(value);
  };
}

let g = f(); // The function still holds a reference to `value`
g(); // 123
```

If we later remove the reference:

```js
g = null; // Now the memory for `value` is freed
```

This is important for performance, as holding onto unnecessary variables can lead to memory leaks.

---

**Optimizations in JavaScript Engines (V8)**
JavaScript engines like V8 optimize memory usage by removing variables that are no longer needed.

For example, in Chrome’s Developer Tools, if we try to access a variable that JavaScript has optimized out, it won’t exist:

```js
function f() {
  let value = Math.random();

  function g() {
    debugger; // Try accessing `value` in the console
  }

  return g;
}

let g = f();
g();
```

In some cases, an outer variable might be removed from memory if it is not used inside the function.

This is why developers sometimes face unexpected behavior while debugging.

---

### Summary
- Function Declarations are fully initialized at the time of creation and can be used before declaration.
- Every function creates its own Lexical Environment.
- Functions can access variables from their outer Lexical Environment.
- Closures allow functions to remember outer variables even after the function execution is complete.
- JavaScript engines optimize memory by removing unused variables.

This understanding is essential for writing efficient JavaScript code! 🚀

####################################################

# The old "var"

## Why learn about "var"?
This article helps understand old JavaScript code. Today, we mostly use `let` and `const`, but knowing `var` is useful when working with older scripts.

## Three ways to declare variables
We can declare variables using:
- `let`
- `const`
- `var`

`var` works similarly to `let`, but it behaves differently in some cases.

```js
var message = "Hi";
alert(message); // Hi
```

Although `var` is not commonly used today, it still appears in older code. If you're updating old scripts, it's important to know how `var` works.

## 1. "var" has no block scope
Variables declared with `var` do not stay inside `{}` blocks. They are either **global** or **function-scoped**.

Example:
```js
if (true) {
  var test = true;
}
alert(test); // Works, because "test" is global
```

If we use `let`, the variable stays inside the `if` block:
```js
if (true) {
  let test = true;
}
alert(test); // Error: test is not defined
```

The same happens in loops:
```js
for (var i = 0; i < 10; i++) {
  var one = 1;
}
alert(i);   // 10, "i" is still available
alert(one); // 1, "one" is still available
```

But inside a function, `var` remains function-scoped:
```js
function sayHi() {
  if (true) {
    var phrase = "Hello";
  }
  alert(phrase); // Works
}
sayHi();
alert(phrase); // Error: phrase is not defined
```

## 2. "var" allows redeclaration
Declaring the same variable twice with `let` gives an error:
```js
let user;
let user; // Error: "user" is already declared
```

With `var`, you can declare the same variable multiple times:
```js
var user = "Pete";
var user = "John"; // No error
alert(user); // John
```

## 3. "var" is hoisted (moved to the top)
`var` declarations are processed before the code runs. This means we can use a `var` variable before declaring it.

Example:
```js
function sayHi() {
  phrase = "Hello";
  alert(phrase);
  var phrase;
}
sayHi();
```

This works because JavaScript moves the `var` declaration to the top:
```js
function sayHi() {
  var phrase; // Declaration moved to the top
  phrase = "Hello";
  alert(phrase);
}
sayHi();
```

However, only the declaration is moved, not the assignment:
```js
function sayHi() {
  alert(phrase); // undefined
  var phrase = "Hello";
}
sayHi();
```

## 4. IIFE (Immediately Invoked Function Expression)
Before `let` and `const`, developers used IIFE to create block-scoped variables.

Example:
```js
(function() {
  var message = "Hello";
  alert(message); // Works
})();
```

Wrapping the function in `()` makes JavaScript treat it as an expression and run it immediately.

Other ways to write IIFE:
```js
(function() { alert("Parentheses around function"); })();

!function() { alert("Using ! before function"); }();

+function() { alert("Using + before function"); }();
```

IIFE is rarely used now because `let` and `const` provide block scope.

## Summary
`var` is different from `let` and `const` in these ways:
1. `var` **does not have block scope** – it is either global or function-scoped.
2. `var` **allows redeclaration**.
3. `var` **is hoisted** – declarations are moved to the top before execution.

Because of these differences, `var` is rarely used today. `let` and `const` are safer and easier to use. However, understanding `var` helps when working with old JavaScript code.

#######################################################

# Global Object

The global object contains variables and functions that are available everywhere. It provides built-in features of JavaScript and the environment.

## Names of Global Object
- **Browser**: `window`
- **Node.js**: `global`
- **Universal (all environments)**: `globalThis` (recommended for compatibility)

## Accessing the Global Object
You can use properties of the global object directly:
```js
alert("Hello");
// Same as
window.alert("Hello");
```

## Variables and the Global Object
Variables declared with `var` (not `let` or `const`) become properties of the global object:
```js
var gVar = 5;
alert(window.gVar); // 5
```
However, `let` and `const` do not behave this way:
```js
let gLet = 5;
alert(window.gLet); // undefined
```

## Storing Global Values
To store truly global values, assign them to the global object directly:
```js
window.currentUser = { name: "John" };
alert(currentUser.name); // John
```
**Note:** Using global variables is discouraged because they can cause errors and make testing harder.

## Checking Feature Support (Polyfills)
Use the global object to check if a modern feature is supported:
```js
if (!window.Promise) {
  alert("Your browser is really old!");
}
```
If a feature is missing, you can create a **polyfill**:
```js
if (!window.Promise) {
  window.Promise = function() {
    // Custom implementation
  };
}
```

## Summary
- The global object stores built-in features and environment-specific values.
- Use `globalThis` for cross-platform compatibility.
- Avoid unnecessary global variables.
- Use the global object to check and add missing features for older environments.

##################################################################

# Function Object, NFE

## Functions in JavaScript are Objects
In JavaScript, functions are treated as objects. This means:
- They can have properties.
- They can be passed as arguments.
- They can be assigned to variables.

## The "name" Property
Every function has a `name` property that stores its name:

```js
function sayHi() {
  alert("Hi");
}

alert(sayHi.name); // Output: sayHi
```

Even if you assign an anonymous function to a variable, JavaScript assigns the variable name to the function:

```js
let sayHello = function() {
  alert("Hello");
};

alert(sayHello.name); // Output: sayHello
```

For object methods, the property name is also set:

```js
let user = {
  sayHi() {},
  sayBye: function() {}
};

alert(user.sayHi.name); // Output: sayHi
alert(user.sayBye.name); // Output: sayBye
```

However, if a function is created inside an array, it may not have a name:

```js
let arr = [function() {}];
alert(arr[0].name); // Output: "" (empty string)
```

## The "length" Property
The `length` property tells us how many parameters a function has:

```js
function oneParam(a) {}
function twoParams(a, b) {}
function manyParams(a, b, ...more) {}

alert(oneParam.length); // 1
alert(twoParams.length); // 2
alert(manyParams.length); // 2 (rest parameters are not counted)
```

## Using "length" in Functions
We can use `length` to handle functions differently based on their number of parameters:

```js
function ask(question, ...handlers) {
  let isYes = confirm(question);

  for (let handler of handlers) {
    if (handler.length === 0) {
      if (isYes) handler();
    } else {
      handler(isYes);
    }
  }
}

ask("Do you agree?", 
    () => alert("You said yes"), 
    result => alert(result));
```

If a function has no parameters, it runs only when the user answers "yes". If it has parameters, it runs in both cases.

## Custom Properties
Functions can have custom properties, just like objects:

```js
function sayHi() {
  alert("Hi");
  sayHi.counter++;
}

sayHi.counter = 0; // Initialize property

sayHi(); // Hi
sayHi(); // Hi

alert(`Called ${sayHi.counter} times`); // Called 2 times
```

### Function Properties vs. Variables
A property added to a function (`sayHi.counter`) is different from a local variable inside it (`let counter`).

## Function Properties vs. Closures
We can use function properties instead of closures to store values:

```js
function makeCounter() {
  function counter() {
    return counter.count++;
  }
  counter.count = 0;
  return counter;
}

let counter = makeCounter();
alert(counter()); // 0
alert(counter()); // 1
```

Since `count` is stored as a function property, we can modify it externally:

```js
counter.count = 10;
alert(counter()); // 10
```

### Closure vs. Function Properties
- **Closure:** Keeps variables private and only accessible inside the function.
- **Function Property:** Allows external modifications.

Use closures for security and function properties when external changes are needed.

# Named Function Expression (NFE)

A **Named Function Expression (NFE)** is a function expression with a name.

### Example:
```js
let sayHi = function func(who) {
  alert(`Hello, ${who}`);
};
```
Here, `func` is the name inside the function but is **not visible outside**.

## Why Use Named Function Expressions?
### 1. Self-Reference for Recursion
If `who` is missing, the function calls itself:
```js
let sayHi = function func(who) {
  if (who) {
    alert(`Hello, ${who}`);
  } else {
    func("Guest"); // Calls itself
  }
};

sayHi(); // Hello, Guest
func(); // ❌ Error: func is not defined outside
```

### 2. Protect Against Reassignments
If the function is assigned to another variable, direct calls still work:
```js
let sayHi = function func(who) {
  if (who) {
    alert(`Hello, ${who}`);
  } else {
    func("Guest");
  }
};

let welcome = sayHi;
sayHi = null;

welcome(); // ✅ Works: Hello, Guest
```
Using `func` instead of `sayHi` ensures internal calls remain unaffected.

## Function Properties
### 1. `name` Property
Returns the function’s name:
```js
function greet() {}
alert(greet.name); // greet
```

### 2. `length` Property
Returns the number of declared parameters:
```js
function add(a, b) {}
alert(add.length); // 2
```

## Functions as Objects
Functions can have properties:
```js
function sayHello() {
  alert("Hello");
  sayHello.count++;
}
sayHello.count = 0;

sayHello();
sayHello();
alert(sayHello.count); // 2
```
The property `count` is stored in the function but **is not a local variable**.

## Summary
- **Functions are objects** and can have properties.
- **`name`** stores the function name.
- **`length`** stores the number of parameters.
- **Named Function Expressions (NFE)** allow **self-reference** and protect against reassignment issues.
- Many libraries use function properties to reduce global pollution (e.g., `_.clone` in Lodash).

################################################################

# The "new Function" Syntax

### Overview
The `new Function` syntax allows us to create functions dynamically using a string. This method is rarely used but is useful in specific cases where function code is generated at runtime.

### Syntax
```js
let func = new Function ([arg1, arg2, ...argN], functionBody);
```
- The function is created with arguments `arg1, arg2, ..., argN` and executes `functionBody`.

### Example
A function with two parameters:
```js
let sum = new Function('a', 'b', 'return a + b');
alert(sum(1, 2)); // 3
```
A function without parameters:
```js
let sayHi = new Function('alert("Hello")');
sayHi(); // Hello
```

### Key Differences
Unlike regular functions, `new Function` creates a function **at runtime from a string**, rather than being pre-defined in the script.

For example, receiving a function from a server:
```js
let str = ... // Code received dynamically from the server
let func = new Function(str);
func();
```

### Closure & Scope
Normally, functions remember their lexical scope, but `new Function` does not.

Example where `new Function` **does not** capture outer variables:
```js
function getFunc() {
  let value = "test";
  let func = new Function('alert(value)');
  return func;
}
getFunc()(); // Error: value is not defined
```

However, a regular function **does** capture outer variables:
```js
function getFunc() {
  let value = "test";
  let func = function() { alert(value); };
  return func;
}
getFunc()(); // "test"
```

### Why Doesn't `new Function` Capture Scope?
- JavaScript minifiers rename variables (`let userName` → `let a`), making outer references unreliable.
- Restricting access to outer scope prevents unintended side effects and errors.
- Instead of using outer variables, **pass arguments explicitly**.

### Summary
- `new Function` creates functions from a string at runtime.
- Syntax:
  ```js
  new Function('a', 'b', 'return a + b'); // Basic
  new Function('a,b', 'return a + b'); // Comma-separated
  new Function('a , b', 'return a + b'); // With spaces
  ```
- Functions created this way have their scope set to the **global** environment, not the enclosing lexical scope.
- **Best practice**: Pass required variables as function arguments instead of relying on outer variables.

#################################################################################

# Scheduling: setTimeout and setInterval

## Introduction
In JavaScript, we can schedule function execution for a later time using:

1. **setTimeout** - Runs a function once after a given time.
2. **setInterval** - Runs a function repeatedly after a given time.

These are **not part of JavaScript** but are provided by browsers and Node.js.

---

## `setTimeout` - Run Once After a Delay
### Syntax:
```js
let timerId = setTimeout(func, delay, arg1, arg2, ...);
```
### Example:
```js
function sayHi() {
  console.log('Hello');
}

setTimeout(sayHi, 1000); // Runs once after 1 second
```

### `setTimeout` with Arguments
```js
function greet(name) {
  console.log(`Hello, ${name}`);
}

setTimeout(greet, 2000, "John"); // Hello, John (after 2 sec)
```

### Cancel `setTimeout`
```js
let timerId = setTimeout(() => console.log("Will not run"), 1000);
clearTimeout(timerId); // Cancels the scheduled execution
```

---

## `setInterval` - Run Repeatedly
### Syntax:
```js
let timerId = setInterval(func, delay, arg1, arg2, ...);
```
### Example:
```js
let counter = 1;
let intervalId = setInterval(() => {
  console.log(`Count: ${counter++}`);
  if (counter > 5) clearInterval(intervalId); // Stops after 5 times
}, 1000);
```

---

## `setTimeout` vs `setInterval`
### `setTimeout` Example (Flexible Scheduling)
```js
let delay = 1000;
function repeat() {
  console.log("Tick");
  setTimeout(repeat, delay); // Next execution is scheduled after completion
}
repeat();
```

### `setInterval` Example (Fixed Interval)
```js
setInterval(() => console.log("Tick"), 1000);
```
**Note:** `setInterval` does not wait for previous execution to finish.

---

## Zero Delay (`setTimeout(func, 0)`) 
Even with `0ms` delay, it runs **after** the current script finishes.
```js
setTimeout(() => console.log("World"));
console.log("Hello");
// Output: Hello (first), then World
```

---

## Nested `setTimeout` (Better than `setInterval`)
```js
let i = 1;
setTimeout(function run() {
  console.log(i++);
  if (i <= 5) setTimeout(run, 1000); // Stops after 5 times
}, 1000);
```

---

## Summary
- **`setTimeout(func, delay, args...)`** - Runs once after `delay`.
- **`clearTimeout(timerId)`** - Cancels `setTimeout`.
- **`setInterval(func, delay, args...)`** - Runs repeatedly.
- **`clearInterval(timerId)`** - Stops `setInterval`.
- **`setTimeout(func, 0)`** - Runs after current script finishes.
- **Use nested `setTimeout`** for better control over execution time.

---

### ⚠️ Things to Remember
- **`setInterval` might run before the previous execution finishes.**
- **Timers may be delayed due to CPU load or browser background mode.**
- **Browser limits nested timers to minimum 4ms after the 5th execution.**

Now you have a clear understanding of scheduling functions in JavaScript! 🚀

############################################################################################################

# Decorators and Forwarding, call/apply

JavaScript provides exceptional flexibility when dealing with functions. Functions can be passed around, used as objects, and even modified dynamically. This document explores how to forward calls between functions and decorate them efficiently.

## Transparent Caching

### Problem Statement
Suppose we have a function `slow(x)`, which is CPU-intensive but returns stable results. Instead of modifying `slow()`, we can create a **wrapper function** that caches results to optimize performance.

### Implementation
```js
function slow(x) {
  alert(`Called with ${x}`);
  return x;
}

function cachingDecorator(func) {
  let cache = new Map();
  return function(x) {
    if (cache.has(x)) {
      return cache.get(x);
    }
    let result = func(x);
    cache.set(x, result);
    return result;
  };
}

slow = cachingDecorator(slow);

alert(slow(1)); // slow(1) is computed and cached
alert("Again: " + slow(1)); // slow(1) result returned from cache
alert(slow(2)); // slow(2) is computed and cached
alert("Again: " + slow(2)); // slow(2) result returned from cache
```

### Explanation
- `cachingDecorator` takes a function and returns a modified version that caches results.
- If the function is called with a previously seen argument, the cached result is returned.
- The original function remains untouched, keeping the main code cleaner and reusable.

## Using `func.call` for Context Preservation

The previous decorator works fine for standalone functions but fails for object methods:

```js
let worker = {
  someMethod() {
    return 1;
  },
  slow(x) {
    alert("Called with " + x);
    return x * this.someMethod();
  }
};

worker.slow = cachingDecorator(worker.slow);
alert(worker.slow(2)); // Error: Cannot read property 'someMethod' of undefined
```

### Why Does This Happen?
- `cachingDecorator` calls the original function as `func(x)`, losing the `this` context.
- When a function is called without an object reference, `this` is `undefined` in strict mode.

### Solution: Use `call` to Preserve `this`
We can fix this by explicitly passing `this` using `func.call(this, x)`, ensuring the original method runs with the correct context.

```js
function cachingDecorator(func) {
  let cache = new Map();
  return function(x) {
    if (cache.has(x)) {
      return cache.get(x);
    }
    let result = func.call(this, x); // Preserve `this`
    cache.set(x, result);
    return result;
  };
}

worker.slow = cachingDecorator(worker.slow);
alert(worker.slow(2)); // Works fine, calls and caches the result
alert(worker.slow(2)); // Returns cached result
```

## Understanding `func.call`
`func.call(context, arg1, arg2, ...)` explicitly sets `this` when calling a function.

### Example Usage
```js
function sayHi() {
  alert(this.name);
}

let user = { name: "John" };
let admin = { name: "Admin" };

sayHi.call(user);  // John
sayHi.call(admin); // Admin
```

Using `call`, we can pass any object as `this` dynamically.

```js
function say(phrase) {
  alert(this.name + ": " + phrase);
}

let user = { name: "John" };
say.call(user, "Hello"); // John: Hello
```

## Summary
- **Decorators** allow modifying functions without changing their core logic.
- **Caching Decorators** store results to improve performance.
- **`call` ensures correct `this` binding** when decorating object methods.
- This approach keeps the main function code clean, modular, and reusable.

By applying these concepts, we can write more efficient and maintainable JavaScript code!

Going multi-argument
Now let’s make cachingDecorator even more universal. Till now it was working only with single-argument functions.

Now how to cache the multi-argument worker.slow method?

```js
let worker = {
  slow(min, max) {
    return min + max; // scary CPU-hogger is assumed
  }
};

// should remember same-argument calls
worker.slow = cachingDecorator(worker.slow);
```
Previously, for a single argument x we could just `cache.set(x, result)` to save the result and `cache.get(x)` to retrieve it. But now we need to remember the result for a combination of arguments `(min,max)`. The native `Map` takes a single value only as the key.

There are many solutions possible:

1. Implement a new (or use a third-party) map-like data structure that is more versatile and allows multi-keys.
2. Use nested maps: `cache.set(min)` will be a `Map` that stores the pair `(max, result)`. So we can get result as `cache.get(min).get(max)`.
3. Join two values into one. In our particular case we can just use a string `"min,max"` as the `Map` key. For flexibility, we can allow providing a hashing function for the decorator that knows how to make one value from many.

For many practical applications, the 3rd variant is good enough, so we’ll stick to it.

Also, we need to pass not just `x`, but all arguments in `func.call`. Let’s recall that in a `function()` we can get a pseudo-array of its arguments as `arguments`, so `func.call(this, x)` should be replaced with `func.call(this, ...arguments)`.

Here’s a more powerful `cachingDecorator`:

```js
let worker = {
  slow(min, max) {
    alert(`Called with ${min},${max}`);
    return min + max;
  }
};

function cachingDecorator(func, hash) {
  let cache = new Map();
  return function() {
    let key = hash(arguments); // (*)
    if (cache.has(key)) {
      return cache.get(key);
    }

    let result = func.call(this, ...arguments); // (**)

    cache.set(key, result);
    return result;
  };
}

function hash(args) {
  return [].join.call(args);
}

worker.slow = cachingDecorator(worker.slow, hash);

alert(worker.slow(3, 5)); // works
alert("Again " + worker.slow(3, 5)); // same (cached)
```

### func.apply
Instead of `func.call(this, ...arguments)` we could use `func.apply(this, arguments)`.

The syntax of built-in method `func.apply` is:

```js
func.apply(context, args)
```

It runs `func` setting `this=context` and using an array-like object `args` as the list of arguments.

The only syntax difference between `call` and `apply` is that `call` expects a list of arguments, while `apply` takes an array-like object with them.

### Borrowing a method
We take (borrow) a `join` method from a regular array `[].join` and use `[].join.call` to run it in the context of `arguments`.

```js
function hash() {
  alert([].join.call(arguments)); // 1,2
}

hash(1, 2);
```

### Summary
Decorator is a wrapper around a function that alters its behavior. The main job is still carried out by the function.

Decorators can be seen as “features” or “aspects” that can be added to a function. We can add one or add many. And all this without changing its code!

To implement `cachingDecorator`, we studied methods:

- `func.call(context, arg1, arg2…)` – calls `func` with given context and arguments.
- `func.apply(context, args)` – calls `func` passing `context` as `this` and array-like `args` into a list of arguments.
- The generic call forwarding is usually done with `apply`:

```js
let wrapper = function() {
  return original.apply(this, arguments);
};
```

### Tasks
#### Spy decorator
**importance: 5**

Create a decorator `spy(func)` that should return a wrapper that saves all calls to function in its `calls` property.

Every call is saved as an array of arguments.

For instance:

```js
function work(a, b) {
  alert(a + b); // work is an arbitrary function or method
}

work = spy(work);

work(1, 2); // 3
work(4, 5); // 9

for (let args of work.calls) {
  alert('call:' + args.join()); // "call:1,2", "call:4,5"
}
```

P.S. That decorator is sometimes useful for unit-testing. Its advanced form is `sinon.spy` in Sinon.JS library.

#########################################################################################################

Function binding
When passing object methods as callbacks, for instance to setTimeout, there’s a known problem: “losing this”.

In this chapter we’ll see the ways to fix it.

Losing “this”
We’ve already seen examples of losing this. Once a method is passed somewhere separately from the object – this is lost.

Here’s how it may happen with setTimeout:

let user = {
  firstName: "John",
  sayHi() {
    alert(`Hello, ${this.firstName}!`);
  }
};

setTimeout(user.sayHi, 1000); // Hello, undefined!
As we can see, the output shows not “John” as this.firstName, but undefined!

That’s because setTimeout got the function user.sayHi, separately from the object. The last line can be rewritten as:

let f = user.sayHi;
setTimeout(f, 1000); // lost user context
The method setTimeout in-browser is a little special: it sets this=window for the function call (for Node.js, this becomes the timer object, but doesn’t really matter here). So for this.firstName it tries to get window.firstName, which does not exist. In other similar cases, usually this just becomes undefined.

The task is quite typical – we want to pass an object method somewhere else (here – to the scheduler) where it will be called. How to make sure that it will be called in the right context?

Solution 1: a wrapper
The simplest solution is to use a wrapping function:

let user = {
  firstName: "John",
  sayHi() {
    alert(`Hello, ${this.firstName}!`);
  }
};

setTimeout(function() {
  user.sayHi(); // Hello, John!
}, 1000);
Now it works, because it receives user from the outer lexical environment, and then calls the method normally.

The same, but shorter:

setTimeout(() => user.sayHi(), 1000); // Hello, John!
Looks fine, but a slight vulnerability appears in our code structure.

What if before setTimeout triggers (there’s one second delay!) user changes value? Then, suddenly, it will call the wrong object!

let user = {
  firstName: "John",
  sayHi() {
    alert(`Hello, ${this.firstName}!`);
  }
};

setTimeout(() => user.sayHi(), 1000);

// ...the value of user changes within 1 second
user = {
  sayHi() { alert("Another user in setTimeout!"); }
};

// Another user in setTimeout!
The next solution guarantees that such thing won’t happen.

Solution 2: bind
Functions provide a built-in method bind that allows to fix this.

The basic syntax is:

// more complex syntax will come a little later
let boundFunc = func.bind(context);
The result of func.bind(context) is a special function-like “exotic object”, that is callable as function and transparently passes the call to func setting this=context.

In other words, calling boundFunc is like func with fixed this.

For instance, here funcUser passes a call to func with this=user:

let user = {
  firstName: "John"
};

function func() {
  alert(this.firstName);
}

let funcUser = func.bind(user);
funcUser(); // John
Here func.bind(user) as a “bound variant” of func, with fixed this=user.

All arguments are passed to the original func “as is”, for instance:

let user = {
  firstName: "John"
};

function func(phrase) {
  alert(phrase + ', ' + this.firstName);
}

// bind this to user
let funcUser = func.bind(user);

funcUser("Hello"); // Hello, John (argument "Hello" is passed, and this=user)
Now let’s try with an object method:

let user = {
  firstName: "John",
  sayHi() {
    alert(`Hello, ${this.firstName}!`);
  }
};

let sayHi = user.sayHi.bind(user); // (*)

// can run it without an object
sayHi(); // Hello, John!

setTimeout(sayHi, 1000); // Hello, John!

// even if the value of user changes within 1 second
// sayHi uses the pre-bound value which is reference to the old user object
user = {
  sayHi() { alert("Another user in setTimeout!"); }
};
In the line (*) we take the method user.sayHi and bind it to user. The sayHi is a “bound” function, that can be called alone or passed to setTimeout – doesn’t matter, the context will be right.

Here we can see that arguments are passed “as is”, only this is fixed by bind:

let user = {
  firstName: "John",
  say(phrase) {
    alert(`${phrase}, ${this.firstName}!`);
  }
};

let say = user.say.bind(user);

say("Hello"); // Hello, John! ("Hello" argument is passed to say)
say("Bye"); // Bye, John! ("Bye" is passed to say)
Convenience method: bindAll
If an object has many methods and we plan to actively pass it around, then we could bind them all in a loop:

for (let key in user) {
  if (typeof user[key] == 'function') {
    user[key] = user[key].bind(user);
  }
}
JavaScript libraries also provide functions for convenient mass binding , e.g. _.bindAll(object, methodNames) in lodash.

Partial functions
Until now we have only been talking about binding this. Let’s take it a step further.

We can bind not only this, but also arguments. That’s rarely done, but sometimes can be handy.

The full syntax of bind:

let bound = func.bind(context, [arg1], [arg2], ...);
It allows to bind context as this and starting arguments of the function.

For instance, we have a multiplication function mul(a, b):

function mul(a, b) {
  return a * b;
}
Let’s use bind to create a function double on its base:

function mul(a, b) {
  return a * b;
}

let double = mul.bind(null, 2);

alert( double(3) ); // = mul(2, 3) = 6
alert( double(4) ); // = mul(2, 4) = 8
alert( double(5) ); // = mul(2, 5) = 10
The call to mul.bind(null, 2) creates a new function double that passes calls to mul, fixing null as the context and 2 as the first argument. Further arguments are passed “as is”.

That’s called partial function application – we create a new function by fixing some parameters of the existing one.

Please note that we actually don’t use this here. But bind requires it, so we must put in something like null.

The function triple in the code below triples the value:

function mul(a, b) {
  return a * b;
}

let triple = mul.bind(null, 3);

alert( triple(3) ); // = mul(3, 3) = 9
alert( triple(4) ); // = mul(3, 4) = 12
alert( triple(5) ); // = mul(3, 5) = 15
Why do we usually make a partial function?

The benefit is that we can create an independent function with a readable name (double, triple). We can use it and not provide the first argument every time as it’s fixed with bind.

In other cases, partial application is useful when we have a very generic function and want a less universal variant of it for convenience.

For instance, we have a function send(from, to, text). Then, inside a user object we may want to use a partial variant of it: sendTo(to, text) that sends from the current user.

Going partial without context
What if we’d like to fix some arguments, but not the context this? For example, for an object method.

The native bind does not allow that. We can’t just omit the context and jump to arguments.

Fortunately, a function partial for binding only arguments can be easily implemented.

Like this:

function partial(func, ...argsBound) {
  return function(...args) { // (*)
    return func.call(this, ...argsBound, ...args);
  }
}

// Usage:
let user = {
  firstName: "John",
  say(time, phrase) {
    alert(`[${time}] ${this.firstName}: ${phrase}!`);
  }
};

// add a partial method with fixed time
user.sayNow = partial(user.say, new Date().getHours() + ':' + new Date().getMinutes());

user.sayNow("Hello");
// Something like:
// [10:00] John: Hello!
The result of partial(func[, arg1, arg2...]) call is a wrapper (*) that calls func with:

Same this as it gets (for user.sayNow call it’s user)
Then gives it ...argsBound – arguments from the partial call ("10:00")
Then gives it ...args – arguments given to the wrapper ("Hello")
So easy to do it with the spread syntax, right?

Also there’s a ready _.partial implementation from lodash library.

Summary
Method func.bind(context, ...args) returns a “bound variant” of function func that fixes the context this and first arguments if given.

Usually we apply bind to fix this for an object method, so that we can pass it somewhere. For example, to setTimeout.

When we fix some arguments of an existing function, the resulting (less universal) function is called partially applied or partial.

Partials are convenient when we don’t want to repeat the same argument over and over again. Like if we have a send(from, to) function, and from should always be the same for our task, we can get a partial and go on with it.

# Arrow Functions in JavaScript

## Introduction
Arrow functions are not just a shorter way to write functions; they also have unique features that make them useful in certain situations.

## Key Features
1. **No `this` binding**
2. **No `arguments` object**
3. **Cannot be used as constructors (`new` keyword)**

---

## 1. Arrow Functions and `this`
Unlike regular functions, arrow functions do not have their own `this`. Instead, they take the `this` value from their surrounding scope.

### Example:
```js
let group = {
  title: "Our Group",
  students: ["John", "Pete", "Alice"],

  showList() {
    this.students.forEach(
      student => console.log(this.title + ': ' + student)
    );
  }
};

group.showList();
```
✅ Works fine because `this.title` comes from `showList()`.

### What if we use a regular function?
```js
let group = {
  title: "Our Group",
  students: ["John", "Pete", "Alice"],

  showList() {
    this.students.forEach(function(student) {
      console.log(this.title + ': ' + student);
    });
  }
};

group.showList();
```
❌ Error! `this` inside the regular function is `undefined` because `forEach` runs the function with `this=undefined` by default.

---

## 2. Arrow Functions and `arguments`
Arrow functions do not have their own `arguments` object.

### Example:
```js
function defer(f, ms) {
  return function() {
    setTimeout(() => f.apply(this, arguments), ms);
  };
}

function sayHi(who) {
  console.log('Hello, ' + who);
}

let sayHiDeferred = defer(sayHi, 2000);
sayHiDeferred("John"); // "Hello, John" after 2 seconds
```
✅ Works fine because the arrow function takes `arguments` from its surrounding function.

If we used a regular function inside `setTimeout`, we would need extra variables:
```js
function defer(f, ms) {
  return function(...args) {
    let ctx = this;
    setTimeout(function() {
      f.apply(ctx, args);
    }, ms);
  };
}
```
This version needs `ctx` and `args` because a regular function has its own `this` and `arguments`.

---

## 3. Arrow Functions Cannot Be Used with `new`
Since arrow functions do not have `this`, they cannot be used as constructors.

### Example:
```js
let User = (name) => {
  this.name = name;
};

let user = new User("John"); // ❌ Error! Arrow functions cannot be used with `new`
```
A regular function should be used instead:
```js
function User(name) {
  this.name = name;
}

let user = new User("John"); // ✅ Works fine
```

---

## 4. Arrow Functions vs `bind()`
A regular function can be bound to an object using `.bind()`:
```js
let user = {
  name: "John",
  sayHi() {
    console.log("Hello, " + this.name);
  }
};

let sayHi = user.sayHi.bind(user);
sayHi(); // ✅ "Hello, John"
```
With an arrow function, `this` is automatically taken from the surrounding context, so no need to bind manually.

---

## Summary
✅ **Arrow Functions:**
- Do **not** have their own `this`
- Do **not** have `arguments`
- Cannot be used with `new`
- Useful for short functions, especially inside methods and callbacks

Use arrow functions when you need to keep `this` from the surrounding scope!


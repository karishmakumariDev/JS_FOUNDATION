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


# Understanding the Global Object in JavaScript

## What is the Global Object?
The **global object** is a special object that holds variables and functions accessible from anywhere in the program. These are either built into JavaScript or provided by the environment (like a browser or Node.js).

### Different Names in Different Environments
- In a **browser**, the global object is called **`window`**.
- In **Node.js**, it is called **`global`**.
- In other environments, it might have different names.
- The standard name for the global object across all environments is **`globalThis`** (introduced in recent JavaScript versions).

### Accessing the Global Object
You can directly access properties and methods of the global object. For example:

```js
alert("Hello"); // Works without window
// Same as:
window.alert("Hello");
```

## Global Variables and Functions
### Declaring Variables with `var`
If you declare a variable using **`var`**, it automatically becomes a property of the global object:

```js
var gVar = 5;
alert(window.gVar); // Output: 5
```

### Function Declarations
Functions declared with the `function` keyword (not function expressions) also become properties of the global object.

**Note:** This behavior is mostly for older code compatibility and is not recommended in modern JavaScript.

### Declaring Variables with `let` or `const`
If you use **`let`** or **`const`**, the variable does **not** become part of the global object:

```js
let gLet = 5;
alert(window.gLet); // Output: undefined
```

## Making Global Variables Explicitly
If you want a value to be **globally accessible**, you can add it directly to the `window` object:

```js
// Storing user information globally
window.currentUser = { name: "John" };

// Accessing the global variable from anywhere in the script
alert(currentUser.name); // Output: John

// If there is another local variable with the same name, use window to avoid conflicts
alert(window.currentUser.name); // Output: John
```

## Why Avoid Global Variables?
Using global variables is generally **not a good practice** because:
1. **It can cause conflicts** – If multiple scripts use the same variable name, unexpected issues may arise.
2. **It makes debugging harder** – Changes in one part of the code can affect another part unexpectedly.
3. **It reduces modularity** – Functions should take inputs and return outputs instead of depending on external variables.

### Best Practices:
- Use **local variables** whenever possible.
- Pass variables as **function arguments** instead of using global variables.
- If necessary, use **modules** in JavaScript (`import` and `export`).

By following these best practices, you can write **clean, maintainable, and bug-free** JavaScript code!

**Using Global Object for Polyfills**

### Checking for Modern Features
The global object can be used to check if modern JavaScript features are supported in a browser.

For example, checking if `Promise` is available:

```js
if (!window.Promise) {
  alert("Your browser is really old!");
}
```

If the feature is missing, we can create a **polyfill**, which is a custom implementation of the missing feature:

```js
if (!window.Promise) {
  window.Promise = ... // Custom implementation of Promise
}
```

### Summary
- The **global object** stores variables and functions that are accessible everywhere.
- It includes built-in JavaScript features like `Array` and environment-specific properties like `window.innerHeight` (browser window height).
- The universal name for the global object is **globalThis**, but environment-specific names include:
  - `window` (for browsers)
  - `global` (for Node.js)
- Only store values in the global object if they are truly necessary.
- In browsers (when not using modules), variables declared with `var` become properties of the global object.
- To ensure code clarity and compatibility, always access global properties explicitly, like `window.x`.

#######################################################################

**Rest Parameters and Spread Syntax**

Many JavaScript functions can accept any number of arguments. For example:

- `Math.max(arg1, arg2, ..., argN)` – Returns the largest argument.
- `Object.assign(dest, src1, ..., srcN)` – Copies properties from multiple sources to the destination object.

In this chapter, we will learn how to use these features and how to pass arrays as function parameters.

---

### Rest Parameters (...)
A function can be called with any number of arguments, regardless of how it is defined.

Example:
```js
function sum(a, b) {
  return a + b;
}

alert(sum(1, 2, 3, 4, 5)); // Only first two arguments are used: 1 + 2 = 3
```

To collect extra arguments into an array, we use three dots `...` followed by a variable name:

```js
function sumAll(...args) {  // args is an array
  let sum = 0;
  for (let arg of args) sum += arg;
  return sum;
}

alert(sumAll(1));        // 1
alert(sumAll(1, 2));     // 3
alert(sumAll(1, 2, 3));  // 6
```

We can also collect only part of the arguments:

```js
function showName(firstName, lastName, ...titles) {
  alert(firstName + ' ' + lastName); // Julius Caesar
  alert(titles[0]); // Consul
  alert(titles[1]); // Imperator
  alert(titles.length); // 2
}

showName("Julius", "Caesar", "Consul", "Imperator");
```

**Important:** Rest parameters must always be at the end of the function parameters:

```js
function f(arg1, ...rest, arg2) {  // ❌ Error: arg2 cannot come after ...rest
}
```

---

### The "arguments" Variable

JavaScript provides an `arguments` object that holds all function arguments as an array-like object:

```js
function showName() {
  alert(arguments.length);
  alert(arguments[0]);
  alert(arguments[1]);
}

showName("Julius", "Caesar"); // Outputs: 2, Julius, Caesar
showName("Ilya"); // Outputs: 1, Ilya, undefined
```

Older JavaScript code used `arguments` instead of rest parameters. However, `arguments` has limitations:
- It is not a real array (no `map`, `filter`, etc.).
- It always contains all arguments (you can't select only part of them).

**Rest parameters are preferred** over `arguments` in modern JavaScript.

---

### Arrow Functions and "arguments"
Arrow functions do **not** have their own `arguments` object. They inherit `arguments` from the surrounding function:

```js
function f() {
  let showArg = () => alert(arguments[0]);
  showArg();
}

f(1); // Outputs: 1
```

This is similar to how arrow functions do not have their own `this`.

---

### Summary
- Rest parameters (`...args`) collect extra function arguments into an array.
- The `arguments` object exists in normal functions but is not a real array.
- Arrow functions do not have their own `arguments` object.
- Use rest parameters instead of `arguments` for better flexibility and modern JavaScript practices.

**Spread Syntax in Simple Terms**

### What is Spread Syntax?
Spread syntax (`...`) allows us to expand an array or an object into individual elements or properties. It is useful when working with functions, arrays, and objects.

---

### Using Spread with Functions
The `Math.max()` function finds the largest number from a list. 

```js
alert(Math.max(3, 5, 1)); // 5
```

If we have an array `[3, 5, 1]`, we cannot pass it directly to `Math.max()`.

```js
let arr = [3, 5, 1];
alert(Math.max(arr)); // NaN (not a valid input)
```

Using spread syntax, we can expand the array into individual values:

```js
alert(Math.max(...arr)); // 5
```

---

### Combining Arrays with Spread
We can merge multiple arrays:

```js
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let merged = [...arr1, ...arr2];
alert(merged); // 1,2,3,4,5,6
```

We can also mix normal values with arrays:

```js
let numbers = [2, 3, 4];
let mixed = [1, ...numbers, 5];
alert(mixed); // 1,2,3,4,5
```

---

### Using Spread with Strings
Spread syntax can break a string into an array of characters:

```js
let str = "Hello";
alert([...str]); // H,e,l,l,o
```

This works like `Array.from(str)`:

```js
alert(Array.from(str)); // H,e,l,l,o
```

However, `Array.from()` can also handle array-like objects, while spread syntax only works with iterables.

---

### Copying Arrays and Objects with Spread
#### Copying an Array
We can create an exact copy of an array:

```js
let arr = [1, 2, 3];
let arrCopy = [...arr];

alert(JSON.stringify(arr) === JSON.stringify(arrCopy)); // true
alert(arr === arrCopy); // false (different memory reference)
```

#### Copying an Object
Similarly, we can copy an object:

```js
let obj = { a: 1, b: 2, c: 3 };
let objCopy = { ...obj };

alert(JSON.stringify(obj) === JSON.stringify(objCopy)); // true
alert(obj === objCopy); // false (different memory reference)
```

This is a shorter way than using `Object.assign()`.

---

### Summary
- **Rest parameters (`...args`)** gather arguments into an array.
- **Spread syntax (`...arr`)** expands an array into individual elements.
- Spread syntax works with **arrays, objects, and strings**.
- It helps in **copying, merging, and passing arguments** easily.

Spread syntax makes JavaS

##################################################################

# Function Object and Named Function Expressions (NFE)

## Functions are Objects
In JavaScript, functions are a type of value, and every value has a type. The type of a function is an **object**.

We can think of functions as **callable action objects**. We can:
- Call them like normal functions.
- Add or remove properties.
- Pass them as references.

---

## The "name" Property
JavaScript functions have a built-in **name** property that stores the function's name.

Example:
```js
function sayHello() {
  alert("Hello");
}

alert(sayHello.name); // Output: sayHello
```
Even if a function is assigned without a name, JavaScript tries to figure out its name:
```js
let greet = function() {
  alert("Hi");
};

alert(greet.name); // Output: greet
```
JavaScript assigns a name from the variable to which the function is assigned.

The same happens if we use a function as a default parameter:
```js
function test(func = function() {}) {
  alert(func.name); // Output: func
}

test();
```

**Object Methods Also Have Names:**
```js
let user = {
  sayHi() { },
  sayBye: function() { }
};

alert(user.sayHi.name); // Output: sayHi
alert(user.sayBye.name); // Output: sayBye
```

But sometimes, JavaScript cannot determine the function name:
```js
let arr = [function() {}];
alert(arr[0].name); // Output: "" (empty string)
```

---

## The "length" Property
Another useful function property is **length**. It tells how many parameters the function expects.

Example:
```js
function f1(a) {}
function f2(a, b) {}
function many(a, b, ...more) {}

alert(f1.length); // Output: 1
alert(f2.length); // Output: 2
alert(many.length); // Output: 2 (rest parameters are not counted)
```

### Using "length" for Function Behavior
We can use `length` to handle functions differently based on the number of parameters they take.

Example:
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
  () => alert("You said Yes"),
  result => alert(result)
);
```
- If a handler has **0 parameters**, it only runs when the user says "Yes".
- If a handler has **parameters**, it runs in both cases (Yes or No).

This technique is useful in JavaScript libraries for handling different types of functions dynamically.

---

## Summary
1. **Functions are objects** in JavaScript, and we can treat them like objects.
2. The **name** property stores the function name (or assigns it based on context).
3. The **length** property tells how many parameters a function expects.
4. We can use these properties to create **flexible and dynamic functions**.

This makes JavaScript functions powerful and adaptable. 🎯




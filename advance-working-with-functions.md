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



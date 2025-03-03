## JavaScript Object Example
In JavaScript, an object is a collection of key-value pairs. Here is an example of an object named `user`:

```javascript
let user = {     // an object
  name: "John",  // by key "name" store value "John"
  age: 30        // by key "age" store value 30
};
```

### Explanation:
- The `user` object has two properties: `name` and `age`.
- `name` holds the string value "John".
- `age` holds the numeric value `30`.
- Objects in JavaScript store data in key-value pairs, where keys are strings and values can be of any data type.

### Accessing Object Properties:
You can access the properties of an object using dot notation or bracket notation:

```javascript
console.log(user.name); // Output: John
console.log(user["age"]); // Output: 30
let currentKey = 'age';
console.log(user[currentKey]) // Output: 30
```

### Modifying Object Properties:
You can modify the properties of an object like this:

```javascript
user.age = 31;
console.log(user.age); // Output: 31
```

### Adding New Properties:
You can also add new properties to the object dynamically:

```javascript
user.city = "New York";
console.log(user.city); // Output: New York
```



### Deleting Properties:
To remove a property from an object, use the `delete` keyword:

```javascript
delete user.age;
console.log(user.age); // Output: undefined
```

### Conclusion:
Objects are a fundamental part of JavaScript and are used to store and manage data efficiently.

# **What is an Object in JavaScript?**
In JavaScript, an **object** is a collection of **key-value pairs**, where keys are called **properties**, and values can be of any data type (strings, numbers, arrays, functions, other objects, etc.). Objects allow us to store related data and functionality together.

Objects are one of the fundamental data types in JavaScript, and they help in organizing data logically.

## **Creating an Object in JavaScript**
You can create objects in multiple ways:

### **1. Using Object Literal (Most Common Way)**
```javascript
let person = {
    name: "Karishma",
    age: 25,
    city: "Delhi"
};
console.log(person.name); // Output: Karishma
```

### **2. Using `new Object()`**
```javascript
let car = new Object();
car.brand = "Toyota";
car.model = "Camry";
car.year = 2023;
console.log(car.brand); // Output: Toyota
```

### **3. Using Constructor Function**
### What is a Constructor Function in JavaScript?

A constructor function is a special type of function used to create multiple objects with similar properties. It acts as a blueprint for creating objects dynamically. Constructor functions use the this keyword to assign values and must be called using the new keyword.
```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}
let p1 = new Person("Karishma", 25);
console.log(p1.name); // Output: Karishma
```

### **4. Using Class (ES6+)**
```javascript
class Student {
    constructor(name, grade) {
        this.name = name;
        this.grade = grade;
    }
}
let student1 = new Student("Karishma", "A");
console.log(student1.grade); // Output: A
```

---

## **What is a Property in JavaScript Objects?**
A **property** in JavaScript is a key-value pair within an object.  
- The **key** is a **string** (or symbol).  
- The **value** can be any **data type** (string, number, boolean, object, array, function, etc.).

### **Example of Object Properties**
```javascript
let laptop = {
    brand: "HP",
    price: 50000,
    isAvailable: true
};
console.log(laptop.brand);  // Output: HP
console.log(laptop["price"]); // Output: 50000
```

## **When are Properties Used?**
Properties are used:
1. **To store object-specific information** (like `name`, `age`, etc.).
2. **To modify object values dynamically** (e.g., updating `laptop.price`).
3. **To access and use object data in programs**.
4. **To define functions (methods) inside objects**.

### **Example of Method (Function as a Property)**
```javascript
let user = {
    name: "Karishma",
    greet: function() {
        return "Hello, " + this.name;
    }
};
console.log(user.greet()); // Output: Hello, Karishma
```

## **Summary:**
- **Objects** are used to store related data.
- **Properties** define the characteristics of an object.
- You can access properties using **dot notation (`obj.key`)** or **bracket notation (`obj["key"]`)**.





## Object Methods and "this"

Objects are usually created to represent entities of the real world, like users, orders, etc.

```javascript
let user = {
  name: "John",
  age: 30
};
```

### Method Examples

To teach the user to say hello:

```javascript
user.sayHi = function() {
  alert("Hello!");
};

user.sayHi(); // Hello!
```

A function that is a property of an object is called a **method**.

Using a pre-declared function as a method:

```javascript
let user = {};

function sayHi() {
  alert("Hello!");
}

user.sayHi = sayHi;

user.sayHi(); // Hello!
```

### Object-Oriented Programming (OOP)

When we use objects to represent entities, it is called Object-Oriented Programming (OOP).

### Method Shorthand

Instead of:

```javascript
user = {
  sayHi: function() {
    alert("Hello");
  }
};
```

We use shorthand:

```javascript
user = {
  sayHi() {
    alert("Hello");
  }
};
```

### "this" in Methods

To access object properties inside a method, we use `this`:

```javascript
let user = {
  name: "John",
  age: 30,

  sayHi() {
    alert(this.name);
  }
};

user.sayHi(); // John
```

Avoid using the object name inside methods, as it may cause issues when copying objects.

### "this" is Not Bound

JavaScript evaluates `this` at runtime based on the calling object:

```javascript
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert(this.name);
}

user.f = sayHi;
admin.f = sayHi;

user.f(); // John
admin.f(); // Admin
```

### Calling Without an Object

```javascript
function sayHi() {
  alert(this);
}

sayHi(); // undefined (in strict mode)
```

### Arrow Functions Have No "this"

Arrow functions do not have their own `this`:

```javascript
let user = {
  firstName: "Ilya",
  sayHi() {
    let arrow = () => alert(this.firstName);
    arrow();
  }
};

user.sayHi(); // Ilya
```

### Summary

- Methods allow objects to "act".
- `this` refers to the calling object.
- Arrow functions inherit `this` from their surrounding scope.

### Tasks

#### Using "this" in Object Literal

```javascript
function makeUser() {
  return {
    name: "John",
    ref: this
  };
}

let user = makeUser();

alert(user.ref.name); // Error
```

#### Create a Calculator

```javascript
let calculator = {
  read() {
    this.a = +prompt("Enter first number:", 0);
    this.b = +prompt("Enter second number:", 0);
  },
  sum() {
    return this.a + this.b;
  },
  mul() {
    return this.a * this.b;
  }
};

calculator.read();
alert(calculator.sum());
alert(calculator.mul());
```

#### Chaining

```javascript
let ladder = {
  step: 0,
  up() {
    this.step++;
    return this;
  },
  down() {
    this.step--;
    return this;
  },
  showStep() {
    alert(this.step);
    return this;
  }
};

ladder.up().up().down().showStep().down().showStep();
```


# Symbol Type

## By Specification
Only two primitive types may serve as object property keys:

- `string` type
- `symbol` type

Otherwise, if one uses another type, such as `number`, it’s auto-converted to a string. So that:

```js
obj[1] // same as obj["1"]
obj[true] // same as obj["true"]
```

Until now, we’ve been using only strings. Now let’s explore symbols and see what they can do for us.

---

## Symbols
A **symbol** represents a unique identifier. A value of this type can be created using `Symbol()`:

```js
let id = Symbol();
```

Upon creation, we can give symbols a description (also called a symbol name), mostly useful for debugging purposes:

```js
let id = Symbol("id"); // id is a symbol with the description "id"
```

Symbols are guaranteed to be unique, even if they have the same description:

```js
let id1 = Symbol("id");
let id2 = Symbol("id");

console.log(id1 === id2); // false
```

### Symbols Don’t Auto-Convert to a String

Unlike other values, symbols do **not** implicitly convert to strings:

```js
let id = Symbol("id");
alert(id); // TypeError: Cannot convert a Symbol value to a string
```

To display a symbol, use `.toString()`:

```js
alert(id.toString()); // Symbol(id)
```

Or access its `description` property:

```js
alert(id.description); // "id"
```

---

## "Hidden" Properties

Symbols allow us to create hidden properties in an object that no other code can accidentally access or overwrite:

```js
let user = { name: "John" };
let id = Symbol("id");
user[id] = 1;

console.log(user[id]); // 1
```

This is useful when working with third-party objects to prevent property conflicts.

---

## Symbols in Object Literals

To use a symbol as an object key, wrap it in square brackets:

```js
let id = Symbol("id");
let user = {
  name: "John",
  [id]: 123
};
```

Without brackets, it would be treated as a string key.

---

## Symbols Are Skipped by `for...in`

Symbolic properties do not appear in `for...in` loops:

```js
let id = Symbol("id");
let user = { name: "John", age: 30, [id]: 123 };

for (let key in user) console.log(key); // name, age (no symbols)

console.log("Direct:", user[id]); // Direct: 123
```

However, `Object.assign` copies symbols:

```js
let clone = Object.assign({}, user);
console.log(clone[id]); // 123
```

---

## Global Symbols

To create a globally shared symbol, use `Symbol.for(key)`. If the symbol already exists, it returns the existing one:

```js
let id1 = Symbol.for("id");
let id2 = Symbol.for("id");

console.log(id1 === id2); // true
```

### `Symbol.keyFor()`
To retrieve the key of a global symbol:

```js
let sym = Symbol.for("name");
console.log(Symbol.keyFor(sym)); // "name"
```

This only works for global symbols. For regular symbols, use `.description`:

```js
let localSymbol = Symbol("name");
console.log(localSymbol.description); // "name"
```

---

## System Symbols
JavaScript provides built-in symbols for various behaviors:

- `Symbol.hasInstance`
- `Symbol.isConcatSpreadable`
- `Symbol.iterator`
- `Symbol.toPrimitive`

For example, `Symbol.toPrimitive` allows custom object-to-primitive conversions.

---

## Summary

- Symbols are unique primitive values created using `Symbol()`.
- They can be used as object keys but are **not** auto-converted to strings.
- They allow **hidden** object properties that don’t show up in loops.
- Global symbols (`Symbol.for`) allow symbol sharing across code.
- System symbols (`Symbol.*`) help modify JavaScript behavior.

Even though symbols are hidden, methods like `Object.getOwnPropertySymbols(obj)` and `Reflect.ownKeys(obj)` can access them.





# Object References and Copying in JavaScript

## Primitive Values vs Objects

Objects and primitive values behave differently when assigned or copied.

### Primitive Values
Primitive values such as strings, numbers, and booleans are copied "as a whole value".

```javascript
let message = "Hello!";
let phrase = message;
```
Each variable holds an independent copy of the string "Hello!".

### Objects
Objects are stored and copied "by reference". A variable assigned to an object holds a reference to its memory address, not the object itself.

```javascript
let user = {
  name: "John"
};
```

When assigning an object to another variable, only the reference is copied, not the object itself:

```javascript
let admin = user;
```
Both `user` and `admin` reference the same object in memory.

```javascript
admin.name = "Pete";
alert(user.name); // 'Pete'
```
Changes made through one reference affect the original object.

## Comparison by Reference
Two objects are equal only if they reference the same memory location:

```javascript
let a = {};
let b = a;
alert(a == b); // true
alert(a === b); // true
```
Two independently created objects are not equal, even if their properties are identical:

```javascript
let a = {};
let b = {};
alert(a == b); // false
```

## Const Objects Can Be Modified
A `const` object can still have its properties modified because only the reference is constant:

```javascript
const user = {
  name: "John"
};
user.name = "Pete"; // Allowed
alert(user.name); // Pete
```
However, reassigning `user` to a new object is not allowed:

```javascript
user = { name: "Alice" }; // Error
```

## Cloning and Merging Objects

### Shallow Cloning with a Loop

We can clone an object manually by copying its properties:

```javascript
let user = {
  name: "John",
  age: 30
};

let clone = {};
for (let key in user) {
  clone[key] = user[key];
}
clone.name = "Pete";
alert(user.name); // John (unchanged)
```

### Using `Object.assign`

`Object.assign` can be used to copy properties from one object to another:

```javascript
let user = { name: "John" };
let permissions1 = { canView: true };
let permissions2 = { canEdit: true };

Object.assign(user, permissions1, permissions2);
alert(user.canView); // true
alert(user.canEdit); // true
```

It can also be used to clone objects:

```javascript
let clone = Object.assign({}, user);
```

### Nested Cloning Issue

If an object has nested objects, `Object.assign` only copies references to the nested objects:

```javascript
let user = {
  name: "John",
  sizes: {
    height: 182,
    width: 50
  }
};

let clone = Object.assign({}, user);
alert(user.sizes === clone.sizes); // true
```
Modifying `clone.sizes.width` will also affect `user.sizes.width`.

## Deep Cloning with `structuredClone`

`structuredClone` creates a deep copy, ensuring nested objects are also cloned:

```javascript
let user = {
  name: "John",
  sizes: {
    height: 182,
    width: 50
  }
};

let clone = structuredClone(user);
alert(user.sizes === clone.sizes); // false
```

### Handling Circular References

`structuredClone` can handle circular references, where an object references itself:

```javascript
let user = {};
user.me = user;
let clone = structuredClone(user);
alert(clone.me === clone); // true
```

### Limitations of `structuredClone`

It does not support functions:

```javascript
structuredClone({ f: function() {} }); // Error
```
For complex cases, libraries like Lodash’s `_.cloneDeep(obj)` can be used.

## Summary
- Objects are copied by reference, meaning changes via one reference affect all references.
- `Object.assign` creates a shallow copy, meaning nested objects are still shared.
- `structuredClone` performs a deep copy, duplicating nested objects as well.
- `_.cloneDeep(obj)` from Lodash can be used for complex cloning scenarios.

# The JavaScript language: Objects - The Basics

## Object References and Copying

Objects in JavaScript are stored and copied by reference, while primitives are copied as a whole value.

### Copying Primitives

```js
let message = "Hello!";
let phrase = message;
```

Each variable holds a separate copy of the value.

### Copying Objects

Objects are stored in memory, and variables store references to them:

```js
let user = { name: "John" };
```

Assigning an object to another variable copies the reference:

```js
let admin = user;
admin.name = "Pete";
alert(user.name); // 'Pete'
```

Both `user` and `admin` reference the same object.

### Comparison by Reference

Two objects are equal only if they reference the same object:

```js
let a = {};
let b = a;
alert(a == b); // true
alert(a === b); // true
```

Different objects, even with identical properties, are not equal:

```js
let a = {};
let b = {};
alert(a == b); // false
```

### `const` Objects Can Be Modified

The reference cannot change, but the object properties can:

```js
const user = { name: "John" };
user.name = "Pete"; // Allowed
alert(user.name); // Pete
```

### Cloning and Merging Objects

Using `Object.assign()` to copy properties:

```js
let user = { name: "John", age: 30 };
let clone = Object.assign({}, user);
alert(clone.name); // "John"
```

### Nested Cloning

Shallow copy keeps references to nested objects:

```js
let user = { name: "John", sizes: { height: 182, width: 50 } };
let clone = Object.assign({}, user);
alert(user.sizes === clone.sizes); // true
```

Deep cloning can be done using `structuredClone()`:

```js
let clone = structuredClone(user);
alert(user.sizes === clone.sizes); // false
```

## Constructor, Operator `new`

### Constructor Function

```js
function User(name) {
  this.name = name;
  this.isAdmin = false;
}
let user = new User("Jack");
alert(user.name); // Jack
alert(user.isAdmin); // false
```

### `new` Execution Steps

1. Creates an empty object.
2. Assigns `this` to the new object.
3. Executes the function.
4. Returns `this`.

### `new.target`

Determines if a function was called with `new`:

```js
function User() {
  alert(new.target);
}
User(); // undefined
new User(); // function User {...}
```

### Returning Objects from Constructors

Returning an object replaces `this`:

```js
function BigUser() {
  this.name = "John";
  return { name: "Godzilla" };
}
alert(new BigUser().name); // Godzilla
```

Returning a primitive is ignored:

```js
function SmallUser() {
  this.name = "John";
  return;
}
alert(new SmallUser().name); // John
```

### Methods in Constructor

```js
function User(name) {
  this.name = name;
  this.sayHi = function() {
    alert("My name is: " + this.name);
  };
}
let john = new User("John");
john.sayHi(); // My name is: John
```

## Tasks

### Two Functions – One Object

Create functions `A` and `B` so that `new A() == new B()`:

```js
let obj = {};
function A() { return obj; }
function B() { return obj; }
alert(new A() == new B()); // true
```

### Create New Calculator

```js
function Calculator() {
  this.read = function() {
    this.a = +prompt("Enter a:", 0);
    this.b = +prompt("Enter b:", 0);
  };
  this.sum = function() {
    return this.a + this.b;
  };
  this.mul = function() {
    return this.a * this.b;
  };
}
let calculator = new Calculator();
calculator.read();
alert("Sum=" + calculator.sum());
alert("Mul=" + calculator.mul());
```

### Create New Accumulator

```js
function Accumulator(startingValue) {
  this.value = startingValue;
  this.read = function() {
    this.value += +prompt("Enter a number:", 0);
  };
}
let accumulator = new Accumulator(1);
accumulator.read();
accumulator.read();
alert(accumulator.value);
```

---




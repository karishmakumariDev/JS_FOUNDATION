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


# The JavaScript Language

## Objects: The Basics

### March 31, 2024

## Object to Primitive Conversion

### What happens when objects are added `obj1 + obj2`, subtracted `obj1 - obj2` or printed using `alert(obj)`?

JavaScript doesn’t allow you to customize how operators work on objects. Unlike some other programming languages, such as Ruby or C++, we can’t implement a special object method to handle addition (or other operators).

In case of such operations, objects are auto-converted to primitives, and then the operation is carried out over these primitives and results in a primitive value.

That’s an important limitation: the result of `obj1 + obj2` (or another math operation) can’t be another object!

E.g. we can’t make objects representing vectors or matrices (or achievements or whatever), add them and expect a “summed” object as the result. Such architectural feats are automatically “off the board”.

So, because we can’t technically do much here, there’s no maths with objects in real projects. When it happens, with rare exceptions, it’s because of a coding mistake.

In this chapter we’ll cover how an object converts to primitive and how to customize it.

## We have two purposes:

- It will allow us to understand what’s going on in case of coding mistakes when such an operation happened accidentally.
- There are exceptions, where such operations are possible and look good. E.g. subtracting or comparing dates (`Date` objects). We’ll come across them later.

## Conversion Rules

In the chapter **Type Conversions**, we’ve seen the rules for numeric, string, and boolean conversions of primitives. But we left a gap for objects. Now, as we know about methods and symbols it becomes possible to fill it.

- There’s no conversion to boolean. All objects are `true` in a boolean context, as simple as that. There exist only numeric and string conversions.
- The numeric conversion happens when we subtract objects or apply mathematical functions. For instance, `Date` objects (to be covered in the chapter **Date and Time**) can be subtracted, and the result of `date1 - date2` is the time difference between two dates.
- As for the string conversion – it usually happens when we output an object with `alert(obj)` and in similar contexts.

We can implement string and numeric conversion by ourselves, using special object methods.

Now let’s get into technical details, because it’s the only way to cover the topic in-depth.

## Hints

### How does JavaScript decide which conversion to apply?

There are three variants of type conversion, that happen in various situations. They’re called **“hints”**, as described in the specification:

- **"string"**
  - For an object-to-string conversion, when we’re doing an operation on an object that expects a string, like `alert`:

```js
// output
alert(obj);

// using object as a property key
anotherObj[obj] = 123;
```

- **"number"**
  - For an object-to-number conversion, like when we’re doing maths:

```js
// explicit conversion
let num = Number(obj);

// maths (except binary plus)
let n = +obj; // unary plus
let delta = date1 - date2;

// less/greater comparison
let greater = user1 > user2;
```

Most built-in mathematical functions also include such conversion.

- **"default"**
  - Occurs in rare cases when the operator is “not sure” what type to expect.

```js
// binary plus uses the "default" hint
let total = obj1 + obj2;

// obj == number uses the "default" hint
if (user == 1) { ... };
```

## Symbol.toPrimitive

Let’s start from the first method. There’s a built-in symbol named `Symbol.toPrimitive` that should be used to name the conversion method, like this:

```js
obj[Symbol.toPrimitive] = function(hint) {
  // here goes the code to convert this object to a primitive
  // it must return a primitive value
  // hint = one of "string", "number", "default"
};
```

If the method `Symbol.toPrimitive` exists, it’s used for all hints, and no more methods are needed.

For instance, here `user` object implements it:

```js
let user = {
  name: "John",
  money: 1000,

  [Symbol.toPrimitive](hint) {
    alert(`hint: ${hint}`);
    return hint == "string" ? `{name: "${this.name}"}` : this.money;
  }
};

// conversions demo:
alert(user); // hint: string -> {name: "John"}
alert(+user); // hint: number -> 1000
alert(user + 500); // hint: default -> 1500
```

## toString/valueOf

If there’s no `Symbol.toPrimitive`, then JavaScript tries to find methods `toString` and `valueOf`:

```js
let user = {
  name: "John",
  money: 1000,

  // for hint="string"
  toString() {
    return `{name: "${this.name}"}`;
  },

  // for hint="number" or "default"
  valueOf() {
    return this.money;
  }
};

alert(user); // toString -> {name: "John"}
alert(+user); // valueOf -> 1000
alert(user + 500); // valueOf -> 1500
```

## A conversion can return any primitive type

The important thing to know about all primitive-conversion methods is that they do not necessarily return the **“hinted” primitive**.

There is no control whether `toString` returns exactly a string, or whether `Symbol.toPrimitive` method returns a number for the hint `"number"`.

The only mandatory thing: these methods **must return a primitive, not an object**.

## Further Conversions

As we know already, many operators and functions perform type conversions, e.g. multiplication `*` converts operands to numbers.

For instance:

```js
let obj = {
  toString() {
    return "2";
  }
};

alert(obj * 2); // 4, object converted to primitive "2", then multiplication made it a number
```

## Summary

- The object-to-primitive conversion is called automatically by many built-in functions and operators that expect a primitive as a value.
- There are 3 types (**hints**) of it:
  - **"string"** (for alert and other operations that need a string)
  - **"number"** (for maths)
  - **"default"** (few operators, usually objects implement it the same way as "number")
- The conversion algorithm is:
  - Call `obj[Symbol.toPrimitive](hint)` if the method exists.
  - Otherwise, try calling `obj.toString()` or `obj.valueOf()`.
- In practice, implementing only `obj.toString()` is often enough as a **“catch-all” method** for string conversions.



# The JavaScript language

## Objects: the basics

**October 14, 2022**

### Garbage collection
Memory management in JavaScript is performed automatically and invisibly to us. We create primitives, objects, functions… All that takes memory.

What happens when something is not needed any more? How does the JavaScript engine discover it and clean it up?

### Reachability
The main concept of memory management in JavaScript is **reachability**.

Simply put, "reachable" values are those that are accessible or usable somehow. They are guaranteed to be stored in memory.

There’s a base set of inherently reachable values, that cannot be deleted for obvious reasons.

For instance:
- The currently executing function, its local variables and parameters.
- Other functions on the current chain of nested calls, their local variables and parameters.
- Global variables.
- (there are some other, internal ones as well)

These values are called **roots**.

Any other value is considered reachable if it’s reachable from a root by a reference or by a chain of references.

For instance, if there’s an object in a global variable, and that object has a property referencing another object, that object is considered reachable. And those that it references are also reachable. Detailed examples to follow.

There’s a background process in the JavaScript engine that is called **garbage collector**. It monitors all objects and removes those that have become unreachable.

### A simple example
Here’s the simplest example:

```javascript
// user has a reference to the object
let user = {
  name: "John"
};
```

Here the arrow depicts an object reference. The global variable `user` references the object `{ name: "John" }` (we’ll call it John for brevity). The `name` property of John stores a primitive, so it’s painted inside the object.

If the value of `user` is overwritten, the reference is lost:

```javascript
user = null;
```

Now John becomes unreachable. There’s no way to access it, no references to it. Garbage collector will junk the data and free the memory.

### Two references
Now let’s imagine we copied the reference from `user` to `admin`:

```javascript
// user has a reference to the object
let user = {
  name: "John"
};

let admin = user;
```

Now if we do the same:

```javascript
user = null;
```

…Then the object is still reachable via `admin` global variable, so it must stay in memory. If we overwrite `admin` too, then it can be removed.

### Interlinked objects
Now a more complex example. The family:

```javascript
function marry(man, woman) {
  woman.husband = man;
  man.wife = woman;

  return {
    father: man,
    mother: woman
  };
}

let family = marry({
  name: "John"
}, {
  name: "Ann"
});
```

Function `marry` “marries” two objects by giving them references to each other and returns a new object that contains them both.

#### Removing references

```javascript
delete family.father;
delete family.mother.husband;
```

It’s not enough to delete only one of these two references, because all objects would still be reachable.

But if we delete both, then we can see that John has no incoming reference any more.

### Unreachable island
It is possible that the whole island of interlinked objects becomes unreachable and is removed from the memory.

```javascript
family = null;
```

This example demonstrates how important the concept of reachability is.

### Internal algorithms
The basic garbage collection algorithm is called **“mark-and-sweep”**.

#### Steps of garbage collection:
1. The garbage collector takes roots and “marks” (remembers) them.
2. Then it visits and “marks” all references from them.
3. Then it visits marked objects and marks their references. All visited objects are remembered, so as not to visit the same object twice in the future.
4. …And so on until every reachable (from the roots) reference is visited.
5. All objects except marked ones are removed.

### Optimizations
Some of the optimizations:
- **Generational collection** – objects are split into two sets: “new ones” and “old ones”. Many objects have a short life span, so they are cleared quickly.
- **Incremental collection** – large memory sets are cleared in smaller parts instead of all at once, preventing execution delays.
- **Idle-time collection** – the garbage collector runs while the CPU is idle to reduce performance impact.

### Summary
- Garbage collection is performed automatically. We cannot force or prevent it.
- Objects are retained in memory while they are **reachable**.
- Being referenced is **not the same** as being reachable from a root.
- Modern engines implement advanced garbage collection algorithms.

For further reading:
- **The Garbage Collection Handbook: The Art of Automatic Memory Management** by R. Jones et al.
- **A tour of V8: Garbage Collection** – article about V8’s garbage collector.
- **V8 blog** – for updates on memory management.



# The JavaScript language

## Objects: the basics

**October 14, 2022**

### Garbage collection
Memory management in JavaScript is performed automatically and invisibly to us. We create primitives, objects, functions… All that takes memory.

What happens when something is not needed any more? How does the JavaScript engine discover it and clean it up?

### Reachability
The main concept of memory management in JavaScript is **reachability**.

Simply put, "reachable" values are those that are accessible or usable somehow. They are guaranteed to be stored in memory.

There’s a base set of inherently reachable values, that cannot be deleted for obvious reasons.

For instance:
- The currently executing function, its local variables and parameters.
- Other functions on the current chain of nested calls, their local variables and parameters.
- Global variables.
- (there are some other, internal ones as well)

These values are called **roots**.

Any other value is considered reachable if it’s reachable from a root by a reference or by a chain of references.

For instance, if there’s an object in a global variable, and that object has a property referencing another object, that object is considered reachable. And those that it references are also reachable. Detailed examples to follow.

There’s a background process in the JavaScript engine that is called **garbage collector**. It monitors all objects and removes those that have become unreachable.

### A simple example
Here’s the simplest example:

```javascript
// user has a reference to the object
let user = {
  name: "John"
};
```

Here the arrow depicts an object reference. The global variable `user` references the object `{ name: "John" }` (we’ll call it John for brevity). The `name` property of John stores a primitive, so it’s painted inside the object.

If the value of `user` is overwritten, the reference is lost:

```javascript
user = null;
```

Now John becomes unreachable. There’s no way to access it, no references to it. Garbage collector will junk the data and free the memory.

### Two references
Now let’s imagine we copied the reference from `user` to `admin`:

```javascript
// user has a reference to the object
let user = {
  name: "John"
};

let admin = user;
```

Now if we do the same:

```javascript
user = null;
```

…Then the object is still reachable via `admin` global variable, so it must stay in memory. If we overwrite `admin` too, then it can be removed.

### Interlinked objects
Now a more complex example. The family:

```javascript
function marry(man, woman) {
  woman.husband = man;
  man.wife = woman;

  return {
    father: man,
    mother: woman
  };
}

let family = marry({
  name: "John"
}, {
  name: "Ann"
});
```

Function `marry` “marries” two objects by giving them references to each other and returns a new object that contains them both.

#### Removing references

```javascript
delete family.father;
delete family.mother.husband;
```

It’s not enough to delete only one of these two references, because all objects would still be reachable.

But if we delete both, then we can see that John has no incoming reference any more.

### Unreachable island
It is possible that the whole island of interlinked objects becomes unreachable and is removed from the memory.

```javascript
family = null;
```

This example demonstrates how important the concept of reachability is.

### Internal algorithms
The basic garbage collection algorithm is called **“mark-and-sweep”**.

#### Steps of garbage collection:
1. The garbage collector takes roots and “marks” (remembers) them.
2. Then it visits and “marks” all references from them.
3. Then it visits marked objects and marks their references. All visited objects are remembered, so as not to visit the same object twice in the future.
4. …And so on until every reachable (from the roots) reference is visited.
5. All objects except marked ones are removed.

### Optimizations
Some of the optimizations:
- **Generational collection** – objects are split into two sets: “new ones” and “old ones”. Many objects have a short life span, so they are cleared quickly.
- **Incremental collection** – large memory sets are cleared in smaller parts instead of all at once, preventing execution delays.
- **Idle-time collection** – the garbage collector runs while the CPU is idle to reduce performance impact.

### Summary
- Garbage collection is performed automatically. We cannot force or prevent it.
- Objects are retained in memory while they are **reachable**.
- Being referenced is **not the same** as being reachable from a root.
- Modern engines implement advanced garbage collection algorithms.

For further reading:
- **The Garbage Collection Handbook: The Art of Automatic Memory Management** by R. Jones et al.
- **A tour of V8: Garbage Collection** – article about V8’s garbage collector.
- **V8 blog** – for updates on memory management.



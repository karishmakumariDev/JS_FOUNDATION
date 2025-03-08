# Methods of Primitives in JavaScript

JavaScript allows us to work with primitives (strings, numbers, etc.) as if they were objects. They also provide methods that can be called on them. However, primitives are not objects, and understanding this behavior is essential.

## **Key Differences Between Primitives and Objects**

### **A Primitive:**
- Is a value of a primitive type.
- There are 7 primitive types in JavaScript:
  - `string`
  - `number`
  - `bigint`
  - `boolean`
  - `symbol`
  - `null`
  - `undefined`

### **An Object:**
- Can store multiple values as properties.
- Can be created using `{}`. Example:
  ```javascript
  let user = { name: "John", age: 30 };
  ```
- Functions are also objects in JavaScript.
- Objects can store functions as properties (methods):
  ```javascript
  let john = {
    name: "John",
    sayHi: function() {
      alert("Hi buddy!");
    }
  };
  john.sayHi(); // Hi buddy!
  ```
- JavaScript has built-in objects like `Date`, `Error`, `HTMLElement`, etc.

## **Primitives as Objects**

The challenge for JavaScript creators:
1. Developers want methods for primitives like strings and numbers.
2. But primitives should remain lightweight and fast.

### **Solution:**
- Primitives remain simple values.
- JavaScript allows access to methods and properties on primitives.
- A special "object wrapper" is created temporarily to provide methods and properties.
- The wrapper object is destroyed immediately after use.
- Wrapper objects for different primitive types:
  - `String`
  - `Number`
  - `Boolean`
  - `Symbol`
  - `BigInt`

### **Example:**
```javascript
let str = "Hello";
alert(str.toUpperCase()); // HELLO
```
#### **What Happens?**
1. `str` is a primitive.
2. JavaScript creates a temporary `String` object.
3. The method `.toUpperCase()` is called on the temporary object.
4. A new string is returned.
5. The temporary object is destroyed.

### **Number Methods:**
```javascript
let n = 1.23456;
alert(n.toFixed(2)); // 1.23
```

## **Constructors: String, Number, Boolean**
Using `new` with primitives creates wrapper objects, which is not recommended.

```javascript
alert(typeof 0); // "number"
alert(typeof new Number(0)); // "object"
```
Objects are always truthy:
```javascript
let zero = new Number(0);
if (zero) {
  alert("zero is truthy!?!");
}
```
**Instead, use type conversion functions:**
```javascript
let num = Number("123"); // Converts string to number
```

## **Null and Undefined Have No Methods**
```javascript
alert(null.test); // ❌ Error
```

## **Adding Properties to Primitives**
### **Consider this code:**
```javascript
let str = "Hello";
str.test = 5;
alert(str.test);
```
### **What Happens?**
1. `str` is a primitive.
2. JavaScript creates a temporary `String` object.
3. Property `test` is added to the temporary object.
4. The object is destroyed immediately.
5. When `alert(str.test)` runs, the property no longer exists.
6. **Output: `undefined`**

### **Correct Way to Store Properties:**
```javascript
let strObj = new String("Hello");
strObj.test = 5;
alert(strObj.test); // ✅ Output: 5
```

## **Summary**
- Primitives except `null` and `undefined` provide methods via temporary objects.
- Temporary objects optimize performance and prevent unnecessary memory usage.
- `new String()`, `new Number()`, and `new Boolean()` create objects, but should be avoided.
- Methods like `toUpperCase()` and `toFixed()` work on primitives through wrapper objects.
- You **cannot** add properties to primitive values directly.



######### 
# Array Methods

Arrays provide a lot of methods. To make things easier, in this chapter, they are split into groups.

## Add/Remove Items
We already know methods that add and remove items from the beginning or the end:

- `arr.push(...items)` – adds items to the end,
- `arr.pop()` – extracts an item from the end,
- `arr.shift()` – extracts an item from the beginning,
- `arr.unshift(...items)` – adds items to the beginning.

Here are a few others.

## splice
How to delete an element from the array?

The arrays are objects, so we can try to use `delete`:

```js
let arr = ["I", "go", "home"];

delete arr[1]; // remove "go"

alert( arr[1] ); // undefined

// now arr = ["I",  , "home"];
alert( arr.length ); // 3
```

The element was removed, but the array still has 3 elements (`arr.length == 3`). That’s because `delete obj.key` removes a value by the key but does not shift the remaining elements.

So, special methods should be used.

### Using `splice`
The `arr.splice` method is a Swiss army knife for arrays. It can insert, remove, and replace elements.

#### Syntax:
```js
arr.splice(start[, deleteCount, elem1, ..., elemN])
```

It modifies `arr` starting from the index `start`, removes `deleteCount` elements, and then inserts `elem1, ..., elemN` at their place. It returns the array of removed elements.

#### Example:

```js
let arr = ["I", "study", "JavaScript"];

arr.splice(1, 1); // from index 1 remove 1 element

alert( arr ); // ["I", "JavaScript"]
```

### Replacing Elements

```js
let arr = ["I", "study", "JavaScript", "right", "now"];

// remove 3 first elements and replace them with another
arr.splice(0, 3, "Let's", "dance");

alert( arr ); // ["Let's", "dance", "right", "now"]
```

### Inserting Without Deleting

```js
let arr = ["I", "study", "JavaScript"];

// Insert "complex" and "language" at index 2
arr.splice(2, 0, "complex", "language");

alert( arr ); // ["I", "study", "complex", "language", "JavaScript"]
```

### Negative Indexes Allowed

```js
let arr = [1, 2, 5];

// from index -1 (one step from the end)
// delete 0 elements,
// then insert 3 and 4
arr.splice(-1, 0, 3, 4);

alert( arr ); // [1, 2, 3, 4, 5]
```

## slice
The method `arr.slice` is much simpler than `arr.splice`.

#### Syntax:
```js
arr.slice([start], [end])
```

It returns a new array copying all items from index `start` to `end` (not including `end`). Negative indexes work as well.

#### Example:

```js
let arr = ["t", "e", "s", "t"];

alert( arr.slice(1, 3) ); // ["e", "s"]
alert( arr.slice(-2) ); // ["s", "t"]
```

Calling `arr.slice()` without arguments creates a copy of `arr`.

## concat
The method `arr.concat` creates a new array that includes values from other arrays and additional items.

#### Syntax:
```js
arr.concat(arg1, arg2...)
```

It accepts any number of arguments – either arrays or values. If an argument is an array, all its elements are copied. Otherwise, the argument itself is copied.

#### Examples:

```js
let arr = [1, 2];

alert( arr.concat([3, 4]) ); // [1, 2, 3, 4]
alert( arr.concat([3, 4], [5, 6]) ); // [1, 2, 3, 4, 5, 6]
alert( arr.concat([3, 4], 5, 6) ); // [1, 2, 3, 4, 5, 6]
```

### Handling Array-like Objects
Normally, `concat` only copies elements from arrays. Other objects, even if they look like arrays, are added as a whole:

```js
let arr = [1, 2];

let arrayLike = {
  0: "something",
  length: 1
};

alert( arr.concat(arrayLike) ); // [1, 2, [object Object]]
```

However, if an object has the special property `Symbol.isConcatSpreadable`, it is treated as an array:

```js
let arr = [1, 2];

let arrayLike = {
  0: "something",
  1: "else",
  [Symbol.isConcatSpreadable]: true,
  length: 2
};

alert( arr.concat(arrayLike) ); // [1, 2, "something", "else"]
```
## Iterate: forEach

The `arr.forEach` method allows running a function for every element of the array.

### Syntax:
```javascript
arr.forEach(function(item, index, array) {
  // ... do something with an item
});
```
Example:
```javascript
// For each element, call alert
["Bilbo", "Gandalf", "Nazgul"].forEach(alert);
```
A more elaborate example:
```javascript
["Bilbo", "Gandalf", "Nazgul"].forEach((item, index, array) => {
  alert(`${item} is at index ${index} in ${array}`);
});
```
The result of the function (if any) is discarded.

## Searching in Array
### indexOf/lastIndexOf and includes
These methods operate similarly to their string counterparts but work with array items:
- `arr.indexOf(item, from)`: Searches from index `from`, returns the index or `-1` if not found.
- `arr.includes(item, from)`: Searches from index `from`, returns `true` if found.

Example:
```javascript
let arr = [1, 0, false];
alert(arr.indexOf(0)); // 1
alert(arr.includes(1)); // true
```
`arr.lastIndexOf(item, from)` works like `indexOf`, but searches from right to left.

### Includes Handles NaN Correctly
```javascript
const arr = [NaN];
alert(arr.indexOf(NaN)); // -1 (wrong)
alert(arr.includes(NaN)); // true (correct)
```

## find and findIndex/findLastIndex
`arr.find(fn)` searches for an object matching a condition.

Example:
```javascript
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];

let user = users.find(item => item.id == 1);
alert(user.name); // John
```

- `arr.findIndex(fn)`: Returns the index of the matching item or `-1` if not found.
- `arr.findLastIndex(fn)`: Searches from right to left.

Example:
```javascript
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"},
  {id: 4, name: "John"}
];

alert(users.findIndex(user => user.name == 'John')); // 0
alert(users.findLastIndex(user => user.name == 'John')); // 3
```

## filter
`arr.filter(fn)` returns an array of matching elements.

Example:
```javascript
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];

let someUsers = users.filter(item => item.id < 3);
alert(someUsers.length); // 2
```

## Transform an Array
### map
`arr.map(fn)` transforms an array.

Example:
```javascript
let lengths = ["Bilbo", "Gandalf", "Nazgul"].map(item => item.length);
alert(lengths); // 5,7,6
```

### sort(fn)
`arr.sort()` sorts an array lexicographically.

Example:
```javascript
let arr = [1, 2, 15];
arr.sort();
alert(arr); // 1, 15, 2
```
To sort numerically:
```javascript
arr.sort((a, b) => a - b);
alert(arr); // 1, 2, 15
```

### reverse
`arr.reverse()` reverses the order of elements.
```javascript
let arr = [1, 2, 3, 4, 5];
arr.reverse();
alert(arr); // 5,4,3,2,1
```

### split and join
- `str.split(delim)`: Splits a string into an array.
- `arr.join(glue)`: Joins array elements into a string.

Example:
```javascript
let names = 'Bilbo, Gandalf, Nazgul';
let arr = names.split(', ');
alert(arr.join(';')); // Bilbo;Gandalf;Nazgul
```

## reduce/reduceRight

When we need to iterate over an array – we can use `forEach`, `for`, or `for..of`.

When we need to iterate and return the data for each element – we can use `map`.

The methods `arr.reduce` and `arr.reduceRight` also belong to that breed but are a little bit more intricate. They are used to calculate a single value based on the array.

### Syntax:
```js
let value = arr.reduce(function(accumulator, item, index, array) {
  // ...
}, [initial]);
```

### Arguments:
- `accumulator` – is the result of the previous function call, equals `initial` the first time (if `initial` is provided).
- `item` – is the current array item.
- `index` – is its position.
- `array` – is the array.

### Example: Sum of an array
```js
let arr = [1, 2, 3, 4, 5];
let result = arr.reduce((sum, current) => sum + current, 0);
alert(result); // 15
```

If no initial value is provided, `reduce` will use the first element as the initial value and start from the second element. However, calling `reduce` on an empty array without an initial value will cause an error.

### reduceRight
The method `arr.reduceRight` does the same but processes the array from right to left.

---

## Array.isArray
Arrays do not form a separate language type; they are based on objects.

### Example:
```js
alert(typeof {}); // object
alert(typeof []); // object
alert(Array.isArray({})); // false
alert(Array.isArray([])); // true
```

---

## Most methods support `thisArg`
Many array methods like `find`, `filter`, and `map` accept an optional additional parameter `thisArg`, which allows setting `this` in the callback function.

### Example:
```js
let army = {
  minAge: 18,
  maxAge: 27,
  canJoin(user) {
    return user.age >= this.minAge && user.age < this.maxAge;
  }
};

let users = [
  {age: 16},
  {age: 20},
  {age: 23},
  {age: 30}
];

let soldiers = users.filter(army.canJoin, army);
alert(soldiers.length); // 2
alert(soldiers[0].age); // 20
alert(soldiers[1].age); // 23
```

---

## Cheat Sheet of Array Methods

### To add/remove elements:
- `push(...items)` – adds items to the end.
- `pop()` – extracts an item from the end.
- `shift()` – extracts an item from the beginning.
- `unshift(...items)` – adds items to the beginning.
- `splice(pos, deleteCount, ...items)` – removes and inserts items at a specific position.
- `slice(start, end)` – creates a new array from a portion of another array.
- `concat(...items)` – merges arrays.

### To search among elements:
- `indexOf/lastIndexOf(item, pos)` – finds item index.
- `includes(value)` – checks if the array contains a value.
- `find/filter(func)` – finds elements based on a condition.
- `findIndex` – returns index instead of value.

### To iterate over elements:
- `forEach(func)` – calls `func` for each element.

### To transform an array:
- `map(func)` – transforms elements.
- `sort(func)` – sorts an array in place.
- `reverse()` – reverses the array in place.
- `split/join` – converts a string to an array and vice versa.
- `reduce/reduceRight(func, initial)` – calculates a single value from an array.

### Additional methods:
- `Array.isArray(value)` – checks if a value is an array.
- `some(fn)/every(fn)` – checks if any/all elements match a condition.
- `fill(value, start, end)` – fills an array with a value.
- `copyWithin(target, start, end)` – copies elements inside the same array.
- `flat(depth)/flatMap(fn)` – flattens a nested array.

---

## Tasks

### 1. Convert `border-left-width` to `borderLeftWidth`
Write a function `camelize(str)` that converts a dash-separated string into camelCase.

#### Example:
```js
camelize("background-color") == 'backgroundColor';
camelize("list-style-image") == 'listStyleImage';
camelize("-webkit-transition") == 'WebkitTransition';
```

#### Solution:
```js
function camelize(str) {
  return str
    .split('-')
    .map((word, index) => index == 0 ? word : word[0].toUpperCase() + word.slice(1))
    .join('');
}
```

---

### 2. Filter range
Write a function `filterRange(arr, a, b)` that filters an array to return elements within a given range without modifying the original array.

#### Example:
```js
let arr = [5, 3, 8, 1];
let filtered = filterRange(arr, 1, 4);
alert(filtered); // [3, 1]
alert(arr); // [5, 3, 8, 1] (not modified)
```

#### Solution:
```js
function filterRange(arr, a, b) {
  return arr.filter(item => (a <= item && item <= b));
}
```

---

Look through this cheat sheet whenever you need to work with arrays. With practice, you'll remember these methods naturally!

### 1. Filter range "in place"

**Question:** Write a function `filterRangeInPlace(arr, a, b)` that modifies `arr` by removing values outside the range `[a, b]`.

**Answer:**
```javascript
function filterRangeInPlace(arr, a, b) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] < a || arr[i] > b) {
      arr.splice(i, 1);
      i--; // Because array length decreases after splice
    }
  }
}

let arr = [5, 3, 8, 1];
filterRangeInPlace(arr, 1, 4);
console.log(arr); // [3, 1]
```

### 2. Sort in decreasing order

**Question:** Sort an array in decreasing order.

**Answer:**
```javascript
let arr = [5, 2, 1, -10, 8];
arr.sort((a, b) => b - a);
console.log(arr); // [8, 5, 2, 1, -10]
```

### 3. Copy and sort array

**Question:** Create a function `copySorted(arr)` that returns a sorted copy of `arr` without modifying the original.

**Answer:**
```javascript
function copySorted(arr) {
  return [...arr].sort();
}

let arr = ["HTML", "JavaScript", "CSS"];
let sorted = copySorted(arr);

console.log(sorted); // ["CSS", "HTML", "JavaScript"]
console.log(arr); // ["HTML", "JavaScript", "CSS"]
```

### 4. Create an extendable calculator

**Question:** Implement a calculator with extendable operations.

**Answer:**
```javascript
function Calculator() {
  this.methods = {
    "+": (a, b) => a + b,
    "-": (a, b) => a - b,
  };

  this.calculate = function (str) {
    let [a, op, b] = str.split(" ");
    a = +a;
    b = +b;
    return this.methods[op] ? this.methods[op](a, b) : NaN;
  };

  this.addMethod = function (name, func) {
    this.methods[name] = func;
  };
}

let calc = new Calculator();
console.log(calc.calculate("3 + 7")); // 10

let powerCalc = new Calculator();
powerCalc.addMethod("*", (a, b) => a * b);
powerCalc.addMethod("/", (a, b) => a / b);
powerCalc.addMethod("**", (a, b) => a ** b);

console.log(powerCalc.calculate("2 ** 3")); // 8
```

### 5. Map to names

**Question:** Convert an array of user objects to an array of names.

**Answer:**
```javascript
let users = [
  { name: "John", age: 25 },
  { name: "Pete", age: 30 },
  { name: "Mary", age: 28 },
];

let names = users.map(user => user.name);
console.log(names); // ["John", "Pete", "Mary"]
```

### 6. Map to objects

**Question:** Convert an array of user objects to a new array containing `id` and `fullName`.

**Answer:**
```javascript
let users = [
  { name: "John", surname: "Smith", id: 1 },
  { name: "Pete", surname: "Hunt", id: 2 },
  { name: "Mary", surname: "Key", id: 3 },
];

let usersMapped = users.map(user => ({
  fullName: `${user.name} ${user.surname}`,
  id: user.id
}));

console.log(usersMapped[0].id); // 1
console.log(usersMapped[0].fullName); // John Smith
```

### 7. Sort users by age

**Question:** Sort an array of user objects by age.

**Answer:**
```javascript
function sortByAge(arr) {
  arr.sort((a, b) => a.age - b.age);
}

let users = [
  { name: "Pete", age: 30 },
  { name: "John", age: 25 },
  { name: "Mary", age: 28 },
];

sortByAge(users);
console.log(users.map(user => user.name)); // ["John", "Mary", "Pete"]
```

### 8. Shuffle an array

**Question:** Write a function `shuffle(array)` that randomly reorders elements.

**Answer:**
```javascript
function shuffle(array) {
  array.sort(() => Math.random() - 0.5);
}

let arr = [1, 2, 3];
shuffle(arr);
console.log(arr); // Randomized order
```

### 9. Get average age

**Question:** Write a function `getAverageAge(users)` to calculate the average age.

**Answer:**
```javascript
function getAverageAge(users) {
  return users.reduce((sum, user) => sum + user.age, 0) / users.length;
}

let users = [
  { name: "John", age: 25 },
  { name: "Pete", age: 30 },
  { name: "Mary", age: 29 },
];

console.log(getAverageAge(users)); // 28
```

### 10. Filter unique array members

**Question:** Implement `unique(arr)` to return unique elements from an array.

**Answer:**
```javascript
function unique(arr) {
  return [...new Set(arr)];
}

let strings = ["Hare", "Krishna", "Hare", "Krishna", "Krishna", "Hare", ":-O"];
console.log(unique(strings)); // ["Hare", "Krishna", ":-O"]
```

### 11. Create keyed object from array

**Question:** Write `groupById(arr)` to convert an array into an object keyed by `id`.

**Answer:**
```javascript
function groupById(arr) {
  return arr.reduce((acc, user) => {
    acc[user.id] = user;
    return acc;
  }, {});
}

let users = [
  { id: "john", name: "John Smith", age: 20 },
  { id: "ann", name: "Ann Smith", age: 24 },
  { id: "pete", name: "Pete Peterson", age: 31 },
];

let usersById = groupById(users);
console.log(usersById);
```


# Object.keys, Object.values, Object.entries

## Iterating Over Data Structures

JavaScript provides various methods to iterate over different data structures. Previously, we explored:

- `map.keys()`
- `map.values()`
- `map.entries()`

These methods are generic and widely used in data structures like:

- **Map**
- **Set**
- **Array**
- **Plain Objects** (with a different syntax)

## Object Methods
For plain objects, JavaScript provides:

- `Object.keys(obj)`: Returns an array of keys.
- `Object.values(obj)`: Returns an array of values.
- `Object.entries(obj)`: Returns an array of `[key, value]` pairs.

### Differences Between `Map` and `Object`

| Feature      | Map            | Object                    |
|-------------|---------------|---------------------------|
| Call Syntax | `map.keys()`   | `Object.keys(obj)`        |
| Returns     | Iterable       | "Real" Array             |

The main reasons for using `Object.keys(obj)`, `Object.values(obj)`, and `Object.entries(obj)` instead of calling them directly on objects are:

1. **Flexibility**: Objects may define their own methods like `data.values()`, so `Object.values(data)` avoids conflicts.
2. **Historical Reasons**: `Object.*` methods return real arrays rather than iterables.

## Example Usage

```js
let user = {
  name: "John",
  age: 30
};

console.log(Object.keys(user));    // ["name", "age"]
console.log(Object.values(user));  // ["John", 30]
console.log(Object.entries(user)); // [["name", "John"], ["age", 30]]
```

## Looping Over Object Values

```js
let user = {
  name: "John",
  age: 30
};

for (let value of Object.values(user)) {
  console.log(value); // "John", then 30
}
```

## Ignoring Symbolic Properties

Like `for...in`, `Object.keys/values/entries` ignore properties with `Symbol` keys. If needed, use:

- `Object.getOwnPropertySymbols(obj)`: Returns only symbolic keys.
- `Reflect.ownKeys(obj)`: Returns all keys, including symbolic ones.

```js
let user = {
  name: "John",
  age: 30,
  [Symbol("id")]: 123
};

console.log(Object.keys(user)); // ["name", "age"]
console.log(Reflect.ownKeys(user)); // ["name", "age", Symbol(id)]
```

## Transforming Objects

Unlike arrays, objects lack methods like `map` and `filter`. However, we can achieve similar functionality using:

1. `Object.entries(obj)`: Converts an object into an array of key-value pairs.
2. Apply array transformations (e.g., `map`).
3. `Object.fromEntries(array)`: Converts the modified array back into an object.

### Example: Doubling Object Values

```js
let prices = {
  banana: 1,
  orange: 2,
  meat: 4,
};

let doublePrices = Object.fromEntries(
  Object.entries(prices).map(([key, value]) => [key, value * 2])
);

console.log(doublePrices.meat); // 8
```

This method allows powerful transformations in a clean, readable way.

Numbers

In modern JavaScript, there are two types of numbers:

Regular numbers in JavaScript are stored in 64-bit format IEEE-754, also known as “double precision floating point numbers”. These are numbers that we’re using most of the time, and we’ll talk about them in this chapter.

BigInt numbers represent integers of arbitrary length. They are sometimes needed because a regular integer number can’t safely exceed (2^53-1) or be less than -(2^53-1). As BigInts are used in a few special areas, we devote them to a special chapter BigInt.

More ways to write a number

Imagine we need to write 1 billion. The obvious way is:
```js
let billion = 1000000000;
```
We also can use underscore `_` as the separator:
```js
let billion = 1_000_000_000;
```

In JavaScript, we can shorten a number by appending the letter `e` to it and specifying the zeroes count:
```js
let billion = 1e9;  // 1 billion, literally: 1 and 9 zeroes
alert(7.3e9);  // 7.3 billions (same as 7300000000 or 7_300_000_000)
```
A negative number after `e` means division by 1 with the given number of zeroes:
```js
1e-3 === 1 / 1000; // 0.001
1.23e-6 === 1.23 / 1000000; // 0.00000123
1234e-2 === 1234 / 100; // 12.34
```

Hex, binary, and octal numbers

Hexadecimal numbers are widely used in JavaScript:
```js
alert(0xff); // 255
alert(0xFF); // 255
```
Binary and octal numeral systems are supported using the `0b` and `0o` prefixes:
```js
let a = 0b11111111; // binary form of 255
let b = 0o377; // octal form of 255
alert(a == b); // true
```

`toString(base)`

The method `num.toString(base)` returns a string representation of `num` in the numeral system with the given base:
```js
let num = 255;
alert(num.toString(16));  // ff
alert(num.toString(2));   // 11111111
```

Rounding numbers

JavaScript provides several methods for rounding numbers:
- `Math.floor`: Rounds down
- `Math.ceil`: Rounds up
- `Math.round`: Rounds to the nearest integer
- `Math.trunc`: Removes anything after the decimal point

Example:
```js
let num = 1.23456;
alert(Math.round(num * 100) / 100); // 1.23
```
The `toFixed(n)` method rounds the number to `n` digits after the decimal point and returns a string:
```js
let num = 12.34;
alert(num.toFixed(1)); // "12.3"
```

Imprecise calculations

JavaScript numbers have precision issues due to their binary representation:
```js
alert(0.1 + 0.2 == 0.3); // false
alert(0.1 + 0.2); // 0.30000000000000004
```
To fix this, use rounding methods:
```js
let sum = 0.1 + 0.2;
alert(+sum.toFixed(2)); // 0.3
```

Funny behavior
```js
alert(9999999999999999); // 10000000000000000
```
JavaScript attempts to fit numbers within its limitations, sometimes causing unexpected results.

Also, JavaScript has both `0` and `-0`, though they mostly behave the same way.

## Tests: isFinite and isNaN

### Special Numeric Values
- **Infinity** (and `-Infinity`) is greater (or lesser) than anything.
- **NaN** represents an error.
- Both belong to the `number` type but require special functions for validation.

### isNaN(value)
- Converts the argument to a number and checks if it's `NaN`.
```js
alert(isNaN(NaN)); // true
alert(isNaN("str")); // true
```
- `NaN` is unique in that it does not equal itself:
```js
alert(NaN === NaN); // false
```

### isFinite(value)
- Converts the argument to a number and returns `true` if it's a regular number (not `NaN`, `Infinity`, or `-Infinity`).
```js
alert(isFinite("15")); // true
alert(isFinite("str")); // false
alert(isFinite(Infinity)); // false
```

### Number.isNaN and Number.isFinite
- **Number.isNaN(value)** checks if the value is exactly `NaN` without type conversion.
```js
alert(Number.isNaN(NaN)); // true
alert(Number.isNaN("str" / 2)); // true
alert(Number.isNaN("str")); // false
```
- **Number.isFinite(value)** checks if the value is a finite number without conversion.
```js
alert(Number.isFinite(123)); // true
alert(Number.isFinite("123")); // false
```

### Object.is(a, b)
- Works like `===` but is more reliable:
  - `Object.is(NaN, NaN) === true`
  - `Object.is(0, -0) === false`

## parseInt and parseFloat
- Convert a string to a number until an error occurs.
```js
alert(parseInt("100px")); // 100
alert(parseFloat("12.5em")); // 12.5
alert(parseInt("12.3")); // 12
alert(parseFloat("12.3.4")); // 12.3
```
- Returns `NaN` when no digits can be read.
```js
alert(parseInt("a123")); // NaN
```

### parseInt(str, radix)
- Parses numbers in different numeral systems.
```js
alert(parseInt("0xff", 16)); // 255
alert(parseInt("ff", 16)); // 255
alert(parseInt("2n9c", 36)); // 123456
```

## Other Math Functions
### Math.random()
- Returns a random number between `0` and `1`.
```js
alert(Math.random());
```

### Math.max() and Math.min()
- Return the largest and smallest values.
```js
alert(Math.max(3, 5, -10, 0, 1)); // 5
alert(Math.min(1, 2)); // 1
```

### Math.pow(n, power)
- Returns `n` raised to `power`.
```js
alert(Math.pow(2, 10)); // 1024
```

## Summary
- Use **`isNaN`** and **`Number.isNaN`** to check for `NaN`.
- Use **`isFinite`** and **`Number.isFinite`** to check for finite numbers.
- Use **`parseInt`/`parseFloat`** for soft conversions.
- Use **Math functions** like `Math.random()`, `Math.max()`, `Math.min()`, and `Math.pow()` for calculations.

# Iterables

Iterable objects are a generalization of arrays. That’s a concept that allows us to make any object usable in a `for..of` loop.

Of course, Arrays are iterable. But there are many other built-in objects that are iterable as well. For instance, strings are also iterable.

If an object isn’t technically an array but represents a collection (list, set) of something, then `for..of` is a great syntax to loop over it. Let's see how to make it work.

## Symbol.iterator

We can easily grasp the concept of iterables by making one of our own.

For instance, we have an object that is not an array but looks suitable for `for..of`.

Like a range object that represents an interval of numbers:

```javascript
let range = {
  from: 1,
  to: 5
};
```

We want `for..of` to work:

```javascript
for(let num of range) {
  console.log(num); // 1,2,3,4,5
}
```

To make the `range` object iterable (and thus let `for..of` work) we need to add a method to the object named `Symbol.iterator` (a special built-in symbol just for that).

When `for..of` starts, it calls that method once (or errors if not found). The method must return an iterator – an object with the method `next()`.

Onward, `for..of` works only with that returned object. When `for..of` wants the next value, it calls `next()` on that object.

The result of `next()` must have the form `{done: Boolean, value: any}`, where `done=true` means that the loop is finished, otherwise `value` is the next value.

### Full implementation of range:

```javascript
let range = {
  from: 1,
  to: 5
};

// 1. call to for..of initially calls this
range[Symbol.iterator] = function() {

  return {
    current: this.from,
    last: this.to,

    next() {
      if (this.current <= this.last) {
        return { done: false, value: this.current++ };
      } else {
        return { done: true };
      }
    }
  };
};

for (let num of range) {
  console.log(num); // 1, then 2, 3, 4, 5
}
```

### Alternative implementation

We can simplify the code by using `range` itself as the iterator:

```javascript
let range = {
  from: 1,
  to: 5,

  [Symbol.iterator]() {
    this.current = this.from;
    return this;
  },

  next() {
    if (this.current <= this.to) {
      return { done: false, value: this.current++ };
    } else {
      return { done: true };
    }
  }
};

for (let num of range) {
  console.log(num); // 1, then 2, 3, 4, 5
}
```

## Infinite Iterators

Infinite iterators are also possible. For instance, the range becomes infinite for `range.to = Infinity`. We can also make an iterable object that generates an infinite sequence of pseudorandom numbers.

## String is Iterable

Arrays and strings are the most widely used built-in iterables.

For a string, `for..of` loops over its characters:

```javascript
for (let char of "test") {
  console.log(char); // t, then e, then s, then t
}
```

It works correctly with surrogate pairs:

```javascript
let str = '𝒳😂';
for (let char of str) {
    console.log(char); // 𝒳, and then 😂
}
```

## Calling an Iterator Explicitly

We can also call an iterator explicitly:

```javascript
let str = "Hello";

let iterator = str[Symbol.iterator]();

while (true) {
  let result = iterator.next();
  if (result.done) break;
  console.log(result.value); // outputs characters one by one
}
```

## Iterables and Array-Likes

Two official terms:

1. **Iterables** implement the `Symbol.iterator` method.
2. **Array-likes** have indexes and `length`, so they look like arrays but may not be iterable.

Example of an array-like but not iterable object:

```javascript
let arrayLike = {
  0: "Hello",
  1: "World",
  length: 2
};

// Error (no Symbol.iterator)
for (let item of arrayLike) {}
```

## Array.from

`Array.from` converts iterables or array-likes into real arrays.

Example with an array-like object:

```javascript
let arrayLike = {
  0: "Hello",
  1: "World",
  length: 2
};

let arr = Array.from(arrayLike);
console.log(arr.pop()); // World (method works)
```

Example with an iterable object:

```javascript
let arr = Array.from(range);
console.log(arr); // [1,2,3,4,5]
```

Using a mapping function:

```javascript
let arr = Array.from(range, num => num * num);
console.log(arr); // [1,4,9,16,25]
```

Converting a string into an array of characters:

```javascript
let str = '𝒳😂';

let chars = Array.from(str);

console.log(chars[0]); // 𝒳
console.log(chars[1]); // 😂
console.log(chars.length); // 2
```

## Summary

- Objects that can be used in `for..of` are called **iterable**.
- Iterables must implement `Symbol.iterator`, returning an iterator.
- An iterator has a `next()` method that returns `{done: Boolean, value: any}`.
- `for..of` automatically calls `Symbol.iterator()`.
- Strings and arrays are built-in iterables.
- Objects with indexed properties and `length` are **array-like** but may not be iterable.
- `Array.from(obj[, mapFn, thisArg])` creates an array from an iterable or array-like object.

# Destructuring Assignment in JavaScript

## Introduction
The two most commonly used data structures in JavaScript are **Objects** and **Arrays**.
- **Objects** store data in key-value pairs.
- **Arrays** store data in an ordered list.

When passing objects or arrays to functions, sometimes we only need specific elements or properties. **Destructuring assignment** allows us to "unpack" arrays or objects into multiple variables in a convenient way.

Destructuring is also useful when dealing with functions with multiple parameters and default values.

---

## Array Destructuring
### Example:
```javascript
let arr = ["John", "Smith"];
let [firstName, surname] = arr;

console.log(firstName); // John
console.log(surname);  // Smith
```
### How it Works:
- The array `arr` contains two elements.
- The destructuring assignment `[firstName, surname] = arr` extracts values into respective variables.

#### Destructuring with `split()`
```javascript
let [firstName, surname] = "John Smith".split(' ');
console.log(firstName); // John
console.log(surname);  // Smith
```
---

## Skipping Elements
```javascript
let [firstName, , title] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];
console.log(title); // Consul
```
### Explanation:
- The second element is ignored using an extra comma `,`.

---

## Works with Any Iterable
```javascript
let [a, b, c] = "abc"; // ['a', 'b', 'c']
let [one, two, three] = new Set([1, 2, 3]);
```
### Explanation:
- **Destructuring works with any iterable**, such as strings, arrays, and sets.
- JavaScript internally uses `for..of` to iterate and assign values.

---

## Assigning to Object Properties
```javascript
let user = {};
[user.name, user.surname] = "John Smith".split(' ');
console.log(user.name); // John
console.log(user.surname); // Smith
```
### Explanation:
- Instead of assigning values to variables, we assign them to an object's properties.

---

## Looping with `Object.entries()`
```javascript
let user = { name: "John", age: 30 };
for (let [key, value] of Object.entries(user)) {
  console.log(`${key}: ${value}`);
}
```
### Explanation:
- `Object.entries(user)` returns an array of `[key, value]` pairs.
- We use **destructuring** inside the `for..of` loop.

---

## Swapping Variables
```javascript
let guest = "Jane";
let admin = "Pete";
[guest, admin] = [admin, guest];
console.log(guest); // Pete
console.log(admin); // Jane
```
### Explanation:
- This **swaps values** without needing a temporary variable.

---

## Rest `...` Operator
```javascript
let [name1, name2, ...rest] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];
console.log(rest); // ['Consul', 'of the Roman Republic']
```
### Explanation:
- The `...rest` collects the remaining elements into an array.

---

## Default Values
```javascript
let [name = "Guest", surname = "Anonymous"] = ["Julius"];
console.log(name);    // Julius
console.log(surname); // Anonymous
```
### Explanation:
- If no value exists, the default value is used.

---

## Object Destructuring
```javascript
let options = {
  title: "Menu",
  width: 100,
  height: 200
};
let {title, width, height} = options;
console.log(title);  // Menu
console.log(width);  // 100
console.log(height); // 200
```
### Explanation:
- Object properties are assigned to variables of the same name.

---

## Changing Variable Names
```javascript
let {width: w, height: h, title} = options;
console.log(w);      // 100
console.log(h);      // 200
```
### Explanation:
- The property `width` is assigned to `w`, and `height` to `h`.

---

## Using Default Values in Objects
```javascript
let {width = 100, height = 200, title} = { title: "Menu" };
console.log(width);  // 100 (default value used)
console.log(height); // 200 (default value used)
```
### Explanation:
- Missing properties use default values.

---

## Nested Destructuring
```javascript
let options = {
  size: { width: 100, height: 200 },
  items: ["Cake", "Donut"],
  extra: true
};
let {
  size: { width, height },
  items: [item1, item2],
  title = "Menu"
} = options;
console.log(width);  // 100
console.log(height); // 200
console.log(item1);  // Cake
console.log(item2);  // Donut
```
### Explanation:
- We extract **nested properties** from an object.

---

## Function Parameters with Destructuring
```javascript
function showMenu({ title = "Untitled", width = 200, height = 100, items = [] }) {
  console.log(`${title} ${width} ${height}`);
  console.log(items);
}
let options = { title: "My Menu", items: ["Item1", "Item2"] };
showMenu(options);
```
### Explanation:
- The function **directly extracts properties** from the passed object.

---

## Default Function Parameters
```javascript
function showMenu({ title = "Menu", width = 100, height = 200 } = {}) {
  console.log(`${title} ${width} ${height}`);
}
showMenu(); // Menu 100 200
```
### Explanation:
- If no argument is passed, the function **uses an empty object `{}`** as the default.

---

## Summary
- **Array destructuring** allows extracting elements from an array.
- **Object destructuring** allows extracting properties from an object.
- **The rest operator (`...`)** gathers remaining elements.
- **Default values** ensure missing properties don’t cause errors.
- **Destructuring is useful in function parameters**, making code more readable.

By mastering destructuring, we can write cleaner and more efficient JavaScript code!


########################################################
# Strings in JavaScript

In JavaScript, textual data is stored as **strings**. There is no separate type for a single character.

The internal format for strings is always **UTF-16**, and it is not tied to the page encoding.

## Quotes

Strings can be enclosed within either **single quotes**, **double quotes**, or **backticks**:

```js
let single = 'single-quoted';
let double = "double-quoted";
let backticks = `backticks`;
```

Single and double quotes are essentially the same. **Backticks**, however, allow us to embed any expression into the string using **`${…}`**:

```js
function sum(a, b) {
  return a + b;
}

alert(`1 + 2 = ${sum(1, 2)}.`); // 1 + 2 = 3.
```

### Multiline Strings with Backticks

Another advantage of using backticks is that they allow a string to span multiple lines:

```js
let guestList = `Guests:
 * John
 * Pete
 * Mary`;

alert(guestList); // A list of guests, multiple lines
```

Using single or double quotes for multiline strings will cause an error:

```js
let guestList = "Guests: // Error: Unexpected token ILLEGAL
  * John";
```

Backticks also support **tagged templates**, allowing a function to process the template string:

```js
func`string`
```

## Special Characters

It is possible to create multiline strings with single and double quotes using a **newline character (`\n`)**:

```js
let guestList = "Guests:\n * John\n * Pete\n * Mary";

alert(guestList); // A multiline list of guests, same as above
```

### Other Special Characters

| Character | Description |
|-----------|------------|
| `\n` | New line |
| `\r` | Carriage return (mainly for Windows) |
| `\'`, `\"`, ``\``` | Quotes |
| `\\` | Backslash |
| `\t` | Tab |
| `\b`, `\f`, `\v` | Backspace, Form Feed, Vertical Tab (legacy, not commonly used) |

Since the backslash `\` is an **escape character**, to show an actual backslash, we need to double it:

```js
alert( `The backslash: \\` ); // The backslash: \
```

Escaped quotes allow using the same type of quotes within a string:

```js
alert( 'I\'m the Walrus!' ); // I'm the Walrus!
```

Alternatively, we can switch to double quotes or backticks:

```js
alert( "I'm the Walrus!" ); // I'm the Walrus!
```

## String Length

The **length** property gives the string length:

```js
alert( `My\n`.length ); // 3
```

> **Note:** `\n` is a single special character, so the length is **3**.

### `length` is a Property, Not a Function

Incorrect usage:
```js
str.length(); // ❌ This will not work
```

Correct usage:
```js
str.length; // ✅
```
# Accessing Characters

To get a character at position `pos`, use square brackets `[pos]` or call the method `str.at(pos)`. The first character starts from the zero position:

```js
let str = `Hello`;

// the first character
alert( str[0] ); // H
alert( str.at(0) ); // H

// the last character
alert( str[str.length - 1] ); // o
alert( str.at(-1) );
```

The `.at(pos)` method allows negative positions. If `pos` is negative, then it’s counted from the end of the string.

The square brackets always return `undefined` for negative indexes:

```js
let str = `Hello`;
alert( str[-2] ); // undefined
alert( str.at(-2) ); // l
```

### Iterating Over Characters

We can iterate over characters using `for..of`:

```js
for (let char of "Hello") {
  alert(char); // H, e, l, l, o
}
```

## Strings are Immutable

Strings can’t be changed in JavaScript. It is impossible to change a character:

```js
let str = 'Hi';
str[0] = 'h'; // error
alert( str[0] ); // doesn't work
```

To modify a string, create a new one:

```js
let str = 'Hi';
str = 'h' + str[1];
alert( str ); // hi
```

## Changing the Case

```js
alert( 'Interface'.toUpperCase() ); // INTERFACE
alert( 'Interface'.toLowerCase() ); // interface
alert( 'Interface'[0].toLowerCase() ); // 'i'
```

## Searching for a Substring

### `str.indexOf`

Finds a substring within a string:

```js
let str = 'Widget with id';
alert( str.indexOf('Widget') ); // 0
alert( str.indexOf('widget') ); // -1
alert( str.indexOf("id") ); // 1
```

To find subsequent occurrences:

```js
let str = 'Widget with id';
alert( str.indexOf('id', 2) ); // 12
```

Finding all occurrences:

```js
let str = 'As sly as a fox, as strong as an ox';
let target = 'as';

let pos = -1;
while ((pos = str.indexOf(target, pos + 1)) != -1) {
  alert( pos );
}
```

### `str.lastIndexOf`

Searches from the end:

```js
let str = "Widget with id";
alert( str.lastIndexOf("id") ); // 12
```

### `includes`, `startsWith`, `endsWith`

```js
alert( "Widget with id".includes("Widget") ); // true
alert( "Hello".includes("Bye") ); // false
alert( "Widget".startsWith("Wid") ); // true
alert( "Widget".endsWith("get") ); // true
```

## Getting a Substring

### `slice`

```js
let str = "stringify";
alert( str.slice(0, 5) ); // 'strin'
alert( str.slice(-4, -1) ); // 'gif'
```

### `substring`

```js
let str = "stringify";
alert( str.substring(2, 6) ); // "ring"
alert( str.substring(6, 2) ); // "ring"
```

### `substr`

```js
let str = "stringify";
alert( str.substr(2, 4) ); // 'ring'
alert( str.substr(-4, 2) ); // 'gi'
```

## Comparing Strings

Strings are compared character-by-character in alphabetical order:

```js
alert( 'a' > 'Z' ); // true
alert( 'Österreich' > 'Zealand' ); // true
```

### Unicode and Character Codes

```js
alert( "Z".codePointAt(0) ); // 90
alert( "z".codePointAt(0) ); // 122
alert( String.fromCodePoint(90) ); // Z
```

### Correct Comparisons

```js
alert( 'Österreich'.localeCompare('Zealand') ); // -1
```

## Summary

- Use backticks for multi-line strings and embedding expressions.
- Use `[]` or `at()` to access characters.
- Use `slice` or `substring` to extract substrings.
- Use `toLowerCase` and `toUpperCase` to change case.
- Use `indexOf` for searching, and `includes/startsWith/endsWith` for simple checks.
- Use `localeCompare` for language-sensitive string comparisons.
- Other useful methods: `trim()`, `repeat()`, and regex-based search/replace.

JavaScript strings are immutable and follow Unicode encoding for comparisons.

###############################################
# Map and Set

Till now, we’ve learned about the following complex data structures:

- **Objects** are used for storing keyed collections.
- **Arrays** are used for storing ordered collections.

But that’s not enough for real life. That’s why **Map** and **Set** also exist.

## Map

**Map** is a collection of keyed data items, just like an Object. But the main difference is that **Map allows keys of any type**.

### Methods and Properties

- `new Map()` – creates the map.
- `map.set(key, value)` – stores the value by the key.
- `map.get(key)` – returns the value by the key, `undefined` if the key doesn’t exist in the map.
- `map.has(key)` – returns `true` if the key exists, `false` otherwise.
- `map.delete(key)` – removes the element (the key/value pair) by the key.
- `map.clear()` – removes everything from the map.
- `map.size` – returns the current element count.

### Example

```javascript
let map = new Map();

map.set('1', 'str1');   // a string key
map.set(1, 'num1');     // a numeric key
map.set(true, 'bool1'); // a boolean key

alert( map.get(1) );   // 'num1'
alert( map.get('1') ); // 'str1'

alert( map.size ); // 3
```

Unlike objects, **keys are not converted to strings**. Any type of key is possible.

### Using Objects as Keys

```javascript
let john = { name: "John" };

let visitsCountMap = new Map();

visitsCountMap.set(john, 123);

alert( visitsCountMap.get(john) ); // 123
```

Using objects as keys is one of the most notable features of **Map**.

### How Map Compares Keys

Map uses the **SameValueZero** algorithm to compare keys. It is similar to strict equality (`===`), but **NaN is considered equal to NaN**.

### Chaining

`map.set` returns the map itself, allowing method chaining:

```javascript
map.set('1', 'str1')
  .set(1, 'num1')
  .set(true, 'bool1');
```

### Iteration over Map

For looping over a Map, there are three methods:

- `map.keys()` – returns an iterable for keys.
- `map.values()` – returns an iterable for values.
- `map.entries()` – returns an iterable for entries `[key, value]`.

#### Example

```javascript
let recipeMap = new Map([
  ['cucumber', 500],
  ['tomatoes', 350],
  ['onion', 50]
]);

for (let vegetable of recipeMap.keys()) {
  alert(vegetable); // cucumber, tomatoes, onion
}

for (let amount of recipeMap.values()) {
  alert(amount); // 500, 350, 50
}

for (let entry of recipeMap) {
  alert(entry); // cucumber,500 (and so on)
}
```

**Map preserves the insertion order**, unlike a regular object.

### forEach Method

```javascript
recipeMap.forEach((value, key) => {
  alert(`${key}: ${value}`);
});
```

### Object.entries: Convert Object to Map

```javascript
let obj = {
  name: "John",
  age: 30
};

let map = new Map(Object.entries(obj));

alert(map.get('name')); // John
```

### Object.fromEntries: Convert Map to Object

```javascript
let map = new Map();
map.set('banana', 1);
map.set('orange', 2);
map.set('meat', 4);

let obj = Object.fromEntries(map);

alert(obj.orange); // 2
```
# Set
A **Set** is a special type of collection – a “set of values” (without keys), where each value may occur only once.

### Main Methods:
- `new Set([iterable])` – creates the set, and if an iterable object is provided (usually an array), copies values from it into the set.
- `set.add(value)` – adds a value, returns the set itself.
- `set.delete(value)` – removes the value, returns `true` if value existed at the moment of the call, otherwise `false`.
- `set.has(value)` – returns `true` if the value exists in the set, otherwise `false`.
- `set.clear()` – removes everything from the set.
- `set.size` – returns the count of elements in the set.

The main feature is that repeated calls of `set.add(value)` with the same value don’t do anything. That’s why each value appears in a **Set** only once.

### Example:
```javascript
let set = new Set();

let john = { name: "John" };
let pete = { name: "Pete" };
let mary = { name: "Mary" };

// Visits, some users come multiple times
set.add(john);
set.add(pete);
set.add(mary);
set.add(john);
set.add(mary);

// Set keeps only unique values
alert(set.size); // 3

for (let user of set) {
  alert(user.name); // John, then Pete, then Mary
}
```

Using an **array** and checking for duplicates on every insertion with `arr.find` would be inefficient. **Set** is optimized internally for uniqueness checks.

## Iteration over Set
We can loop over a set using `for..of` or `forEach`:

```javascript
let set = new Set(["oranges", "apples", "bananas"]);

for (let value of set) alert(value);

// The same with forEach:
set.forEach((value, valueAgain, set) => {
  alert(value);
});
```

> **Note:** The callback function in `forEach` has three arguments: a value, then the same value `valueAgain`, and then the target object. This is for compatibility with **Map**.

### Set Methods for Iterators:
- `set.keys()` – returns an iterable object for values.
- `set.values()` – same as `set.keys()`, for compatibility with **Map**.
- `set.entries()` – returns an iterable object for entries `[value, value]`, exists for compatibility with **Map**.

---

# Summary

### **Map** – A collection of keyed values.
#### **Methods and properties:**
- `new Map([iterable])` – creates the map, with optional iterable (e.g., an array of `[key,value]` pairs for initialization).
- `map.set(key, value)` – stores the value by the key, returns the map itself.
- `map.get(key)` – returns the value by the key, `undefined` if key doesn’t exist.
- `map.has(key)` – returns `true` if the key exists, `false` otherwise.
- `map.delete(key)` – removes the element by the key, returns `true` if key existed, otherwise `false`.
- `map.clear()` – removes everything from the map.
- `map.size` – returns the current element count.

#### **Differences from a regular Object:**
- Any keys can be used, including objects as keys.
- Additional convenient methods and a `size` property.

---

### **Set** – A collection of unique values.
#### **Methods and properties:**
- `new Set([iterable])` – creates the set, with optional iterable (e.g., an array of values for initialization).
- `set.add(value)` – adds a value (does nothing if value exists), returns the set itself.
- `set.delete(value)` – removes the value, returns `true` if value existed, otherwise `false`.
- `set.has(value)` – returns `true` if the value exists in the set, otherwise `false`.
- `set.clear()` – removes everything from the set.
- `set.size` – returns the count of elements.

### **Important Notes:**
- Iteration over **Map** and **Set** is always in insertion order.
- Elements **cannot** be directly accessed by their number.
- **Set** ensures uniqueness, while **Map** stores key-value pairs efficiently.

##############################################
# Arrays and Objects in JavaScript

Objects allow you to store keyed collections of values. That’s fine.

But quite often we find that we need an ordered collection, where we have a 1st, a 2nd, a 3rd element, and so on. For example, we need that to store a list of something: users, goods, HTML elements, etc.

It is not convenient to use an object here because it provides no methods to manage the order of elements. We can’t insert a new property “between” the existing ones. Objects are just not meant for such use.

There exists a special data structure named **Array**, to store ordered collections.

## Declaration
There are two syntaxes for creating an empty array:

```javascript
let arr = new Array();
let arr = [];
```

Almost all the time, the second syntax is used. We can supply initial elements in the brackets:

```javascript
let fruits = ["Apple", "Orange", "Plum"];
```

Array elements are numbered, starting with zero.

We can get an element by its number in square brackets:

```javascript
let fruits = ["Apple", "Orange", "Plum"];

alert(fruits[0]); // Apple
alert(fruits[1]); // Orange
alert(fruits[2]); // Plum
```

We can replace an element:

```javascript
fruits[2] = 'Pear'; // now ["Apple", "Orange", "Pear"]
```

Or add a new one to the array:

```javascript
fruits[3] = 'Lemon'; // now ["Apple", "Orange", "Pear", "Lemon"]
```

The total count of the elements in the array is its length:

```javascript
let fruits = ["Apple", "Orange", "Plum"];

alert(fruits.length); // 3
```

We can also use alert to show the whole array:

```javascript
let fruits = ["Apple", "Orange", "Plum"];

alert(fruits); // Apple,Orange,Plum
```

An array can store elements of any type.

For instance:

```javascript
// mix of values
let arr = ['Apple', { name: 'John' }, true, function() { alert('hello'); }];

// get the object at index 1 and then show its name
alert(arr[1].name); // John

// get the function at index 3 and run it
arr[3](); // hello
```

## Trailing Comma
An array, just like an object, may end with a comma:

```javascript
let fruits = [
  "Apple",
  "Orange",
  "Plum",
];
```

The “trailing comma” style makes it easier to insert/remove items because all lines become alike.

## Get Last Elements with `at`

A recent addition to JavaScript is the `.at()` method.

Let’s say we want the last element of the array.

```javascript
let fruits = ["Apple", "Orange", "Plum"];

alert(fruits[fruits.length - 1]); // Plum
```

Instead of writing the variable name twice, we can use:

```javascript
alert(fruits.at(-1)); // Plum
```

In other words, `arr.at(i)`:
- is exactly the same as `arr[i]`, if `i >= 0`.
- for negative values of `i`, it steps back from the end of the array.

## Methods pop/push, shift/unshift

A queue is one of the most common uses of an array. In computer science, this means an ordered collection of elements which supports two operations:
- `push` appends an element to the end.
- `shift` gets an element from the beginning, advancing the queue, so that the 2nd element becomes the 1st.

There’s another use case for arrays – the data structure named **stack**.

It supports two operations:
- `push` adds an element to the end.
- `pop` takes an element from the end.

For stacks, the latest pushed item is received first, which is called **LIFO** (Last-In-First-Out). For queues, we have **FIFO** (First-In-First-Out).

JavaScript arrays can work as both queues and stacks.

### Methods that work with the end of the array:

#### `pop`
Extracts the last element of the array and returns it:

```javascript
let fruits = ["Apple", "Orange", "Pear"];

alert(fruits.pop()); // remove "Pear" and alert it
alert(fruits); // Apple, Orange
```

#### `push`
Appends the element to the end of the array:

```javascript
let fruits = ["Apple", "Orange"];

fruits.push("Pear");

alert(fruits); // Apple, Orange, Pear
```

### Methods that work with the beginning of the array:

#### `shift`
Extracts the first element of the array and returns it:

```javascript
let fruits = ["Apple", "Orange", "Pear"];

alert(fruits.shift()); // remove Apple and alert it
alert(fruits); // Orange, Pear
```

#### `unshift`
Adds an element to the beginning of the array:

```javascript
let fruits = ["Orange", "Pear"];

fruits.unshift('Apple');

alert(fruits); // Apple, Orange, Pear
```

### Adding Multiple Elements

Methods `push` and `unshift` can add multiple elements at once:

```javascript
let fruits = ["Apple"];

fruits.push("Orange", "Peach");
fruits.unshift("Pineapple", "Lemon");

// ["Pineapple", "Lemon", "Apple", "Orange", "Peach"]
alert(fruits);
```

## Internals
An array is a special kind of object. The square brackets used to access a property `arr[0]` actually come from the object syntax. That’s essentially the same as `obj[key]`, where `arr` is the object, while numbers are used as keys.

They extend objects, providing special methods to work with ordered collections of data and also the `length` property. But at the core, it’s still an object.

### Copy by Reference
```javascript
let fruits = ["Banana"];
let arr = fruits; // copy by reference

console.log(arr === fruits); // true

arr.push("Pear"); // modify the array by reference
console.log(fruits); // ["Banana", "Pear"]
```

### Misusing Arrays
Arrays should be used as ordered collections, but they can be misused:
```javascript
let fruits = [];
fruits[99999] = 5; // assigning a far index
fruits.age = 25; // adding a property
```
Using non-numeric properties or sparse indices turns off JavaScript’s array optimizations.

### Performance: push/pop vs shift/unshift
- **push/pop** are fast since they operate at the end.
- **shift/unshift** are slow since they involve renumbering elements.

```javascript
let fruits = ["Apple", "Orange", "Pear"];
fruits.shift(); // removes first element
```

### Loops
**For loop:**
```javascript
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}
```

**for..of loop:** (preferred for arrays)
```javascript
for (let fruit of fruits) {
  console.log(fruit);
}
```

**for..in loop:** (avoid for arrays)
```javascript
for (let key in arr) {
  console.log(arr[key]);
}
```

### `length` Property
The `length` property reflects the highest numeric index plus one.
```javascript
let fruits = [];
fruits[123] = "Apple";
console.log(fruits.length); // 124
```

Truncating an array:
```javascript
let arr = [1, 2, 3, 4, 5];
arr.length = 2;
console.log(arr); // [1, 2]
```

### `new Array()`
Using `new Array()` is rare. Beware:
```javascript
let arr = new Array(2);
console.log(arr.length); // 2 (empty slots, not [2])
```
Prefer `[]` over `new Array()`.

### Multidimensional Arrays
```javascript
let matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

console.log(matrix[0][1]); // 2
```

### `toString` Conversion
```javascript
let arr = [1, 2, 3];
console.log(arr.toString()); // "1,2,3"
```

### Avoid `==` for Arrays
Arrays are objects, and `==` does not compare contents.
```javascript
console.log([] == []); // false
console.log([0] == [0]); // false
```
Use loops or methods like `JSON.stringify()` for comparison.

## Summary
- **Use arrays for ordered data**.
- **Methods:** `push()`, `pop()`, `shift()`, `unshift()`.
- **Loops:** `for`, `for..of` (avoid `for..in`).
- **Comparison:** Never use `==`; compare item-by-item.

We will continue with array methods in the next chapter.


#####################################################
## Understanding JSON Methods and toJSON in JavaScript

### Why Convert Objects to Strings?
In JavaScript, we often need to convert objects into strings for various reasons:
- Sending data over a network.
- Storing data in local storage.
- Logging objects in a readable format.

### Basic Object to String Conversion
Consider the following JavaScript object:
```javascript
let user = {
  name: "John",
  age: 30,

  toString() {
    return `{name: "${this.name}", age: ${this.age}}`;
  }
};

alert(user); // {name: "John", age: 30}
```
Here, we define a `toString` method to manually convert the object into a string. However, this approach has some problems:
- If we add or remove properties, we must update the `toString` method.
- Handling nested objects manually can be complex.

### JSON.stringify for Automatic Conversion
Instead of writing a custom `toString` method, we can use `JSON.stringify`:
```javascript
let user = {
  name: "John",
  age: 30
};

let json = JSON.stringify(user);
alert(json); // "{"name":"John","age":30}"
```
This method automatically converts an object into a JSON string, making it much easier to work with.

### Handling Nested Objects
If an object has nested properties, `JSON.stringify` handles them as well:
```javascript
let user = {
  name: "John",
  age: 30,
  address: {
    city: "New York",
    zip: "10001"
  }
};

let json = JSON.stringify(user, null, 2);
alert(json);
```
Output:
```
{
  "name": "John",
  "age": 30,
  "address": {
    "city": "New York",
    "zip": "10001"
  }
}
```

### Using toJSON for Custom Conversion
Sometimes, we need more control over how an object is converted. We can define a `toJSON` method inside the object:
```javascript
let user = {
  name: "John",
  age: 30,
  password: "secret", // We don’t want to include this in JSON

  toJSON() {
    return {
      name: this.name,
      age: this.age
    };
  }
};

let json = JSON.stringify(user);
alert(json); // "{"name":"John","age":30}"
```
Here, the `toJSON` method ensures that only the `name` and `age` properties are included in the final JSON output.

### Conclusion
- `JSON.stringify` automatically converts objects to JSON format.
- It handles nested objects efficiently.
- The `toJSON` method allows us to customize how an object is converted.
- Using `toJSON`, we can exclude sensitive or unnecessary data while converting objects.

Using these methods makes data handling in JavaScript much simpler and more efficient.

**JSON.stringify in Easy Language**

### What is JSON?
JSON (JavaScript Object Notation) is a format used to store and exchange data. It was originally designed for JavaScript, but now almost every programming language supports it, such as Ruby, PHP, and Java.

### JSON Methods in JavaScript
JavaScript provides two important methods to work with JSON:

1. **JSON.stringify()** – Converts a JavaScript object into a JSON string.
2. **JSON.parse()** – Converts a JSON string back into a JavaScript object.

### Example of JSON.stringify()
```js
let student = {
  name: 'John',
  age: 30,
  isAdmin: false,
  courses: ['html', 'css', 'js'],
  spouse: null
};

let json = JSON.stringify(student);

console.log(typeof json); // Output: string
console.log(json);
```
**Output:**
```json
{
  "name": "John",
  "age": 30,
  "isAdmin": false,
  "courses": ["html", "css", "js"],
  "spouse": null
}
```

### Differences Between JavaScript Objects and JSON
- Strings in JSON **must** use double quotes (`" "`).
- Property names in JSON must also be in double quotes.

### Data Types Supported in JSON
JSON can contain:
- Objects `{ ... }`
- Arrays `[ ... ]`
- Strings
- Numbers
- Boolean values (`true`/`false`)
- `null`

### Example of JSON.stringify() on Different Data Types
```js
console.log(JSON.stringify(1));       // "1"
console.log(JSON.stringify("hello")); // "hello"
console.log(JSON.stringify(true));    // "true"
console.log(JSON.stringify([1, 2, 3])); // "[1,2,3]"
```

### What is Ignored in JSON.stringify()?
Some JavaScript-specific values are ignored while converting an object to JSON:
1. **Functions (methods) in objects**
2. **Symbols**
3. **Properties with `undefined` values**

Example:
```js
let user = {
  sayHi() { console.log("Hello"); },
  [Symbol("id")]: 123,
  something: undefined
};

console.log(JSON.stringify(user)); // Output: {}
```

### Handling Nested Objects
JSON.stringify() automatically converts nested objects too.

Example:
```js
let meetup = {
  title: "Conference",
  room: {
    number: 23,
    participants: ["john", "ann"]
  }
};

console.log(JSON.stringify(meetup));
```
**Output:**
```json
{
  "title": "Conference",
  "room": {
    "number": 23,
    "participants": ["john", "ann"]
  }
}
```

### Circular References Issue
JSON.stringify() does **not** work with circular references.

Example of circular reference:
```js
let room = { number: 23 };
let meetup = { title: "Conference", participants: ["john", "ann"] };

meetup.place = room;  // meetup references room
room.occupiedBy = meetup; // room references meetup

console.log(JSON.stringify(meetup)); // Error: Circular structure detected
```
This happens because `room.occupiedBy` refers to `meetup`, and `meetup.place` refers back to `room`, forming a circular structure.

### Summary
- **JSON.stringify()** converts JavaScript objects to JSON format.
- It ignores functions, symbols, and `undefined` values.
- It supports numbers, strings, booleans, arrays, objects, and `null`.
- Nested objects are automatically converted.
- Circular references cause an error.

Using JSON helps in data storage, API communication, and exchanging data between different programming languages.

**Understanding JSON.stringify and JSON.parse in Simple Terms**

### **What is JSON.stringify?**
JSON.stringify is a method that converts a JavaScript object into a JSON string. This is useful when we need to store or send data in a structured text format.

**Syntax:**
```javascript
let json = JSON.stringify(value[, replacer, space])
```
- **value**: The object to convert.
- **replacer**: (Optional) Defines which properties should be included or transformed.
- **space**: (Optional) Adds spacing for better readability.

### **Filtering Properties with replacer**
The replacer argument can be:
1. An array of properties to include.
2. A function that customizes the output.

#### **Example: Using an Array to Filter Properties**
```javascript
let room = { number: 23 };
let meetup = {
  title: "Conference",
  participants: [{ name: "John" }, { name: "Alice" }],
  place: room
};
room.occupiedBy = meetup;

console.log(JSON.stringify(meetup, ['title', 'participants']));
// Output: {"title":"Conference","participants":[{},{}]}
```
In this case, only `title` and `participants` are included, but `name` is missing from `participants`.

#### **Example: Using a Function to Filter Data**
We can use a function to exclude specific properties like circular references.
```javascript
let room = { number: 23 };
let meetup = {
  title: "Conference",
  participants: [{ name: "John" }, { name: "Alice" }],
  place: room
};
room.occupiedBy = meetup;

console.log(JSON.stringify(meetup, function replacer(key, value) {
  return key === 'occupiedBy' ? undefined : value;
}));
```
This function removes the `occupiedBy` property to avoid circular references.

### **Formatting JSON Output with space**
The `space` parameter helps format JSON for readability.
```javascript
let user = {
  name: "John",
  age: 25,
  roles: { isAdmin: false, isEditor: true }
};

console.log(JSON.stringify(user, null, 2));
```
This prints the JSON with 2 spaces of indentation.

### **Custom toJSON Method**
If an object has a `toJSON` method, `JSON.stringify` calls it before conversion.
```javascript
let room = {
  number: 23,
  toJSON() {
    return this.number;
  }
};

console.log(JSON.stringify(room)); // Output: 23
```

---

### **What is JSON.parse?**
JSON.parse is used to convert a JSON string back into a JavaScript object.

**Syntax:**
```javascript
let value = JSON.parse(str[, reviver])
```
- **str**: The JSON string to parse.
- **reviver**: (Optional) A function to modify the parsed values.

#### **Example: Parsing a JSON String**
```javascript
let jsonData = '{ "name": "John", "age": 35 }';
let user = JSON.parse(jsonData);
console.log(user.name); // Output: John
```

### **Fixing Data Types with reviver**
If we have a date inside JSON, it gets converted to a string. We can use `reviver` to restore it.
```javascript
let str = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';

let meetup = JSON.parse(str, function(key, value) {
  return key === 'date' ? new Date(value) : value;
});

console.log(meetup.date.getDate()); // Now works correctly
```

### **Common JSON Mistakes**
1. Property names must be in **double quotes**:
   ```javascript
   let json = '{ name: "John" }'; // ❌ Incorrect
   let json = '{ "name": "John" }'; // ✅ Correct
   ```
2. **No single quotes** allowed:
   ```javascript
   let json = "{'name': 'John'}"; // ❌ Incorrect
   let json = '{ "name": "John" }'; // ✅ Correct
   ```
3. No functions or special objects like `Date`, use string representation.
4. JSON does not allow **comments**.

### **Summary**
- `JSON.stringify(object)`: Converts an object to a JSON string.
- `JSON.parse(string)`: Converts a JSON string back to an object.
- `replacer` in `stringify`: Filters or transforms values.
- `reviver` in `parse`: Modifies parsed values.
- Use `space` for better formatting.
- Custom `toJSON` method changes how objects are stringified.

By mastering these, you can work efficiently with JSON in JavaScript!

##################################################################
# WeakMap and WeakSet in JavaScript (Easy Language)

## Garbage Collection in JavaScript
In JavaScript, an object is stored in memory as long as it is reachable, meaning there is a reference to it. When an object becomes unreachable, it is automatically removed from memory through **garbage collection**.

### Example:
```js
let john = { name: "John" };

john = null; // Now the object { name: "John" } is removed from memory
```
Here, we first created an object and assigned it to the variable `john`. When we set `john = null`, the object `{ name: "John" }` is no longer reachable and gets **garbage collected**.

---

## Objects Inside Arrays and Maps
### Example with Arrays:
```js
let john = { name: "John" };
let array = [john];

john = null;
```
Even after setting `john = null`, the object `{ name: "John" }` is still inside the array and remains in memory.

### Example with Maps:
```js
let john = { name: "John" };
let map = new Map();
map.set(john, "..." );

john = null;
```
Even after removing the reference (`john = null`), the object is still stored inside the `map`, so it **is not garbage collected**.

---

## WeakMap in JavaScript
Unlike `Map`, a `WeakMap` allows the garbage collector to remove an object if there are no other references to it.

### WeakMap Key Rules:
- **Keys must be objects**, not primitive values (like numbers or strings).
- If an object is used as a key and there are no other references, it **automatically gets deleted** from memory.

### Example:
```js
let john = { name: "John" };
let weakMap = new WeakMap();
weakMap.set(john, "Secret Info");

john = null; // Now the object is removed from WeakMap and memory
```
Here, the `WeakMap` automatically removes `{ name: "John" }` from memory when `john` is set to `null`.

### WeakMap Methods:
- `weakMap.set(key, value)` → Adds a key-value pair
- `weakMap.get(key)` → Gets the value associated with the key
- `weakMap.delete(key)` → Removes the key-value pair
- `weakMap.has(key)` → Checks if a key exists

### Limitations of WeakMap:
- It **does not support iteration** (no `.keys()`, `.values()`, or `.entries()` methods).
- It **does not have a `.size` property**, as keys may get removed anytime.

---

## Where is WeakMap Used?
### 1️⃣ **Storing Temporary Data**
```js
let userVisits = new WeakMap();

function visit(user) {
  let count = userVisits.get(user) || 0;
  userVisits.set(user, count + 1);
}

let john = { name: "John" };
visit(john);
john = null; // Object and its visit count are automatically deleted
```
With `WeakMap`, when `john` is removed, his visit count is also removed automatically.

### 2️⃣ **Caching Data**
```js
let cache = new WeakMap();

function process(obj) {
  if (!cache.has(obj)) {
    let result = "Processed Result";
    cache.set(obj, result);
    return result;
  }
  return cache.get(obj);
}

let obj = { id: 1 };
process(obj);
obj = null; // Cache entry is automatically removed
```
Here, if `obj` is deleted, its cache entry also gets removed automatically.

---

## WeakSet in JavaScript
`WeakSet` is similar to `WeakMap`, but it only stores **objects**, not key-value pairs.

### WeakSet Rules:
- Only **objects** can be added.
- If an object is removed from memory, it is **automatically deleted from the WeakSet**.
- It has only 3 methods: `add()`, `has()`, and `delete()`.

### Example:
```js
let weakSet = new WeakSet();
let john = { name: "John" };

weakSet.add(john);
john = null; // Now the object is automatically removed from WeakSet
```

---

## Conclusion
- `WeakMap` and `WeakSet` allow **automatic memory cleanup** when objects are no longer needed.
- They do **not support iteration** (`.keys()`, `.values()`, `.entries()` methods are unavailable).
- They are useful for **storing temporary data**, **caching**, and **tracking objects without memory leaks**.

🚀 Use `WeakMap` and `WeakSet` whenever you need a **memory-efficient way** to store object-related data! 🚀

**WeakSet and WeakMap in JavaScript (Simple Explanation)**

### WeakSet
A **WeakSet** is similar to a regular **Set**, but with some important differences:

- It **only stores objects** (no primitive values like numbers or strings).
- An object in a **WeakSet** exists only while it is reachable from somewhere else.
- Supports only three methods: `add()`, `has()`, and `delete()`.
- Does **not** have methods like `size`, `keys()`, or any way to iterate over its values.

#### Example:
```javascript
let visitedSet = new WeakSet();

let john = { name: "John" };
let pete = { name: "Pete" };
let mary = { name: "Mary" };

visitedSet.add(john); // John visited
visitedSet.add(pete); // Pete visited
visitedSet.add(john); // John again

console.log(visitedSet.has(john)); // true
console.log(visitedSet.has(mary)); // false

john = null; // John is removed from memory
```
Since `john` is now unreachable, **WeakSet automatically removes it**, saving memory.

### WeakMap
A **WeakMap** is similar to a regular **Map**, but with some differences:

- **Keys must be objects** (cannot be numbers, strings, etc.).
- If an object used as a key is **deleted**, it is **automatically removed** from the WeakMap.
- Does **not** support iteration methods like `keys()`, `values()`, or `entries()`.

#### Example:
```javascript
let weakMap = new WeakMap();
let user = { name: "John" };

weakMap.set(user, "some data"); // Storing data for John

console.log(weakMap.get(user)); // Output: "some data"

user = null; // User is removed from memory
```
Since `user` is now unreachable, **WeakMap automatically deletes its entry**, preventing memory leaks.

### Why Use WeakSet and WeakMap?
1. **Memory Efficiency:** Objects are removed when no longer needed.
2. **No Manual Cleanup Needed:** JavaScript’s garbage collector handles removal.
3. **Best for Temporary Data:** Useful for tracking visited users, caching, etc.

### Limitations
- No size property (`size` does not exist).
- No way to loop through entries (no `forEach`, `keys()`, etc.).
- Only objects can be used as keys in WeakMap and stored in WeakSet.

### Summary
| Feature   | WeakSet  | WeakMap  |
|-----------|---------|---------|
| Stores only objects? | ✅ Yes | ✅ Yes |
| Automatic garbage collection? | ✅ Yes | ✅ Yes |
| Can iterate over values? | ❌ No | ❌ No |
| Can check if an item exists? | ✅ Yes (has) | ✅ Yes (has) |
| Can delete an item? | ✅ Yes (delete) | ✅ Yes (delete) |

**When to Use?**
- Use **WeakSet** when you need to track object existence (e.g., checking if a user visited a site).
- Use **WeakMap** when you need to store temporary data linked to an object (e.g., caching calculations).

By using **WeakMap** and **WeakSet**, we can manage memory efficiently and avoid manual cleanup of objects no longer needed!



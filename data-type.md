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




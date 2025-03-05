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



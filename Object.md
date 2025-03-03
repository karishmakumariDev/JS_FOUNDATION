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


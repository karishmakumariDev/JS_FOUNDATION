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






### Object methods, "this"
- Objects are usually created to represent entities of the real world, like users, orders and so on:
  ```let user = {
  name: "John",
  age: 30
}; ```

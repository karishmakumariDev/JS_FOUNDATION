# Intermediate-Level JavaScript Interview Questions and Answers (Arrays of Objects)

## 1. How do you sort an array of objects by a specific key (e.g., sorting by age)?
### Answer:
You can use the `sort()` method with a custom comparator function:

```js
let students = [
    { name: "Alice", age: 25 },
    { name: "Bob", age: 20 },
    { name: "Charlie", age: 22 }
];

students.sort((a, b) => a.age - b.age);

console.log(students);
```
### Output:
```js
[
    { name: "Bob", age: 20 },
    { name: "Charlie", age: 22 },
    { name: "Alice", age: 25 }
]
```
👉 This sorts the objects in ascending order based on the `age` key.

---

## 2. How do you find an object in an array based on a property value?
### Answer:
Use the `find()` method:

```js
let products = [
    { id: 1, name: "Laptop" },
    { id: 2, name: "Phone" },
    { id: 3, name: "Tablet" }
];

let product = products.find(p => p.id === 3);

console.log(product);
```
### Output:
```js
{ id: 3, name: "Tablet" }
```
👉 `find()` returns the first matching object based on the condition.

---

## 3. How do you filter objects in an array based on a condition?
### Answer:
Use the `filter()` method:

```js
let employees = [
    { name: "John", salary: 60000 },
    { name: "Jane", salary: 45000 },
    { name: "Mike", salary: 50000 }
];

let highSalaryEmployees = employees.filter(emp => emp.salary >= 50000);

console.log(highSalaryEmployees);
```
### Output:
```js
[
    { name: "John", salary: 60000 },
    { name: "Mike", salary: 50000 }
]
```
👉 `filter()` returns all matching objects based on the condition.

---

## 4. How do you transform an array of objects into an array of a specific property?
### Answer:
Use the `map()` method:

```js
let books = [
    { title: "Book A", author: "Author 1" },
    { title: "Book B", author: "Author 2" }
];

let bookTitles = books.map(book => book.title);

console.log(bookTitles);
```
### Output:
```js
["Book A", "Book B"]
```
👉 `map()` extracts a specific property from each object and returns a new array.

---

## 5. How do you remove an object from an array based on a property value?
### Answer:
Use `filter()` to create a new array without the matching object:

```js
let users = [
    { id: 1, name: "Alice" },
    { id: 2, name: "Bob" },
    { id: 3, name: "Charlie" }
];

let updatedUsers = users.filter(user => user.id !== 2);

console.log(updatedUsers);
```
### Output:
```js
[
    { id: 1, name: "Alice" },
    { id: 3, name: "Charlie" }
]
```
👉 This removes the object where `id === 2`.

---

## 6. How do you merge two arrays of objects based on a common key?
### Answer:
Use `map()` and `reduce()` to merge objects with the same `id`:

```js
let students1 = [
    { id: 1, name: "Alice", age: 20 },
    { id: 2, name: "Bob", age: 22 }
];

let students2 = [
    { id: 2, name: "Bob", age: 23 },
    { id: 3, name: "Charlie", age: 21 }
];

let mergedStudents = [...students1, ...students2].reduce((acc, student) => {
    let existing = acc.find(s => s.id === student.id);
    if (existing) {
        existing.age = student.age;  // Update age if ID matches
    } else {
        acc.push(student);
    }
    return acc;
}, []);

console.log(mergedStudents);
```
### Output:
```js
[
    { id: 1, name: "Alice", age: 20 },
    { id: 2, name: "Bob", age: 23 },  // Updated age
    { id: 3, name: "Charlie", age: 21 }
]
```
👉 This ensures that objects with the same `id` are merged.

---

## 7. How do you group an array of objects by a specific key?
### Answer:
Use `reduce()` to group objects into categories:

```js
let people = [
    { name: "Alice", role: "admin" },
    { name: "Bob", role: "user" },
    { name: "Charlie", role: "admin" },
    { name: "David", role: "user" }
];

let groupedByRole = people.reduce((acc, person) => {
    (acc[person.role] = acc[person.role] || []).push(person);
    return acc;
}, {});

console.log(groupedByRole);
```
### Output:
```js
{
    admin: [
        { name: "Alice", role: "admin" },
        { name: "Charlie", role: "admin" }
    ],
    user: [
        { name: "Bob", role: "user" },
        { name: "David", role: "user" }
    ]
}
```
👉 This groups objects based on the `role` key.

---
# Intermediate-Level JavaScript Interview Questions and Answers (Arrays of Objects)

## 1. How do you check if all objects in an array meet a condition?
### Answer:
Use the `every()` method:

```js
let students = [
    { name: "Alice", age: 25 },
    { name: "Bob", age: 20 },
    { name: "Charlie", age: 22 }
];

let allAdults = students.every(student => student.age >= 18);

console.log(allAdults);
```
### Output:
```js
true
```
👉 `every()` returns `true` if all objects satisfy the condition.

---

## 2. How do you find the index of an object in an array based on a property value?
### Answer:
Use the `findIndex()` method:

```js
let products = [
    { id: 1, name: "Laptop" },
    { id: 2, name: "Phone" },
    { id: 3, name: "Tablet" }
];

let index = products.findIndex(p => p.id === 2);

console.log(index);
```
### Output:
```js
1
```
👉 `findIndex()` returns the index of the first matching object.

---

## 3. How do you sum up values of a specific property in an array of objects?
### Answer:
Use the `reduce()` method:

```js
let orders = [
    { orderId: 1, total: 500 },
    { orderId: 2, total: 300 },
    { orderId: 3, total: 200 }
];

let totalAmount = orders.reduce((sum, order) => sum + order.total, 0);

console.log(totalAmount);
```
### Output:
```js
1000
```
👉 `reduce()` accumulates the sum of the `total` property.

---

## 4. How do you clone an array of objects without affecting the original?
### Answer:
Use `map()` with the spread operator:

```js
let users = [
    { id: 1, name: "Alice" },
    { id: 2, name: "Bob" }
];

let clonedUsers = users.map(user => ({ ...user }));

console.log(clonedUsers);
```
### Output:
```js
[
    { id: 1, name: "Alice" },
    { id: 2, name: "Bob" }
]
```
👉 This creates a deep copy, ensuring modifications to `clonedUsers` don’t affect `users`.

---

## 5. How do you shuffle an array of objects randomly?
### Answer:
Use `sort()` with `Math.random()`:

```js
let cards = [
    { suit: "hearts", value: "A" },
    { suit: "spades", value: "K" },
    { suit: "diamonds", value: "Q" }
];

let shuffled = cards.sort(() => Math.random() - 0.5);

console.log(shuffled);
```
### Output:
```js
[
    { suit: "spades", value: "K" },
    { suit: "diamonds", value: "Q" },
    { suit: "hearts", value: "A" }
]
```
👉 This randomizes the order of objects in the array.

---

## JavaScript Array of Objects - `map()` Method Questions

### 1. How do you extract a specific property from an array of objects?
**Answer:**
Use `map()` to get an array of property values.

```js
let users = [
    { id: 1, name: "Alice" },
    { id: 2, name: "Bob" }
];

let names = users.map(user => user.name);
console.log(names);
```
**Output:**
```js
["Alice", "Bob"]
```

---

### 2. How do you transform an array of objects by adding a new property?
**Answer:**
Use `map()` to add a new key-value pair.

```js
let employees = [
    { name: "John", salary: 60000 },
    { name: "Jane", salary: 45000 }
];

let updatedEmployees = employees.map(emp => ({ ...emp, bonus: 5000 }));
console.log(updatedEmployees);
```

**Output:**
```js
[
    { name: "John", salary: 60000, bonus: 5000 },
    { name: "Jane", salary: 45000, bonus: 5000 }
]
```

---

### 3. How do you modify an existing property in an array of objects?
**Answer:**
Use `map()` to update a property.

```js
let products = [
    { name: "Laptop", price: 1000 },
    { name: "Phone", price: 500 }
];

let discountedProducts = products.map(p => ({ ...p, price: p.price * 0.9 }));
console.log(discountedProducts);
```

---

### 4. How do you format an array of objects into a different structure?
**Answer:**
Use `map()` to transform object structure.

```js
let students = [
    { firstName: "Alice", lastName: "Smith" },
    { firstName: "Bob", lastName: "Brown" }
];

let formattedStudents = students.map(s => ({ fullName: `${s.firstName} ${s.lastName}` }));
console.log(formattedStudents);
```

---

### 5. How do you convert an array of objects to an array of strings?
**Answer:**
Use `map()` with template literals.

```js
let cars = [
    { brand: "Toyota", model: "Corolla" },
    { brand: "Honda", model: "Civic" }
];

let carDescriptions = cars.map(car => `${car.brand} - ${car.model}`);
console.log(carDescriptions);
```

---

### 6. How do you generate a unique ID for each object in an array?
**Answer:**
Use `map()` and the index.

```js
let tasks = [
    { task: "Do laundry" },
    { task: "Buy groceries" }
];

let tasksWithIds = tasks.map((t, i) => ({ ...t, id: i + 1 }));
console.log(tasksWithIds);
```

---

### 7. How do you calculate a derived property for each object?
**Answer:**
Use `map()` to compute a new value.

```js
let employees = [
    { name: "John", salary: 60000 },
    { name: "Jane", salary: 50000 }
];

let salariesWithTax = employees.map(e => ({ ...e, afterTax: e.salary * 0.8 }));
console.log(salariesWithTax);
```

---

### 8. How do you uppercase a property value for all objects?
**Answer:**
Use `map()` with `toUpperCase()`.

```js
let users = [
    { name: "alice" },
    { name: "bob" }
];

let capitalizedUsers = users.map(user => ({ ...user, name: user.name.toUpperCase() }));
console.log(capitalizedUsers);
```

---

### 9. How do you get only specific keys from objects in an array?
**Answer:**
Use `map()` and destructuring.

```js
let people = [
    { name: "Alice", age: 25, city: "NY" },
    { name: "Bob", age: 30, city: "LA" }
];

let namesAndAges = people.map(({ name, age }) => ({ name, age }));
console.log(namesAndAges);
```

---

### 10. How do you append an index to each object?
**Answer:**
Use `map()` with the index argument.

```js
let items = [
    { name: "Shirt" },
    { name: "Pants" }
];

let indexedItems = items.map((item, index) => ({ ...item, index }));
console.log(indexedItems);
```

---

### 11. How do you double a numeric property in an array of objects?
**Answer:**
Use `map()` to multiply the property value.

```js
let numbers = [
    { value: 10 },
    { value: 20 }
];

let doubledNumbers = numbers.map(n => ({ ...n, value: n.value * 2 }));
console.log(doubledNumbers);
```

---

### 12. How do you conditionally modify a property using `map()`?
**Answer:**
Use `map()` with a condition.

```js
let employees = [
    { name: "Alice", salary: 40000 },
    { name: "Bob", salary: 60000 }
];

let updatedSalaries = employees.map(e =>
    e.salary < 50000 ? { ...e, salary: e.salary + 5000 } : e
);
console.log(updatedSalaries);
```

---

This document contains a series of JavaScript questions and answers related to using the `map()` method with arrays of objects. Each example demonstrates a different use case for transforming or manipulating arrays using `map()`. 🚀



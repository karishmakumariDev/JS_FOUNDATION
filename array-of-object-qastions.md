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
# JavaScript Array of Objects - Questions and Answers (Using `map()`)

## 1. How do you extract a specific property from an array of objects?
### Answer:
Use `map()` to get an array of property values.

```js
let users = [
    { id: 1, name: "Alice" },
    { id: 2, name: "Bob" }
];

let names = users.map(user => user.name);

console.log(names);
```
### Output:
```js
["Alice", "Bob"]
```
---

## 2. How do you transform an array of objects by adding a new property?
### Answer:
Use `map()` to add a new key-value pair.

```js
let employees = [
    { name: "John", salary: 60000 },
    { name: "Jane", salary: 45000 }
];

let updatedEmployees = employees.map(emp => ({ ...emp, bonus: 5000 }));

console.log(updatedEmployees);
```
### Output:
```js
[
    { name: "John", salary: 60000, bonus: 5000 },
    { name: "Jane", salary: 45000, bonus: 5000 }
]
```
---

## 3. How do you modify an existing property in an array of objects?
### Answer:
Use `map()` to update a property.

```js
let products = [
    { name: "Laptop", price: 1000 },
    { name: "Phone", price: 500 }
];

let discountedProducts = products.map(p => ({ ...p, price: p.price * 0.9 }));

console.log(discountedProducts);
```
### Output:
```js
[
    { name: "Laptop", price: 900 },
    { name: "Phone", price: 450 }
]
```
---

## 4. How do you format an array of objects into a different structure?
### Answer:
Use `map()` to transform object structure.

```js
let students = [
    { firstName: "Alice", lastName: "Smith" },
    { firstName: "Bob", lastName: "Brown" }
];

let formattedStudents = students.map(s => ({ fullName: `${s.firstName} ${s.lastName}` }));

console.log(formattedStudents);
```
### Output:
```js
[
    { fullName: "Alice Smith" },
    { fullName: "Bob Brown" }
]
```
---

## 5. How do you convert an array of objects to an array of strings?
### Answer:
Use `map()` with template literals.

```js
let cars = [
    { brand: "Toyota", model: "Corolla" },
    { brand: "Honda", model: "Civic" }
];

let carDescriptions = cars.map(car => `${car.brand} - ${car.model}`);

console.log(carDescriptions);
```
### Output:
```js
["Toyota - Corolla", "Honda - Civic"]
```
---

## 6. How do you generate a unique ID for each object in an array?
### Answer:
Use `map()` with an index.

```js
let tasks = [
    { task: "Do laundry" },
    { task: "Buy groceries" }
];

let tasksWithIds = tasks.map((t, i) => ({ ...t, id: i + 1 }));

console.log(tasksWithIds);
```
### Output:
```js
[
    { task: "Do laundry", id: 1 },
    { task: "Buy groceries", id: 2 }
]
```
---

## 7. How do you calculate a derived property for each object?
### Answer:
Use `map()` to compute a new value.

```js
let employees = [
    { name: "John", salary: 60000 },
    { name: "Jane", salary: 50000 }
];

let salariesWithTax = employees.map(e => ({ ...e, afterTax: e.salary * 0.8 }));

console.log(salariesWithTax);
```
### Output:
```js
[
    { name: "John", salary: 60000, afterTax: 48000 },
    { name: "Jane", salary: 50000, afterTax: 40000 }
]
```
---

## 8. How do you uppercase a property value for all objects?
### Answer:
Use `map()` with `toUpperCase()`.

```js
let users = [
    { name: "alice" },
    { name: "bob" }
];

let capitalizedUsers = users.map(user => ({ ...user, name: user.name.toUpperCase() }));

console.log(capitalizedUsers);
```
### Output:
```js
[
    { name: "ALICE" },
    { name: "BOB" }
]
```
---

## 9. How do you append an index to each object?
### Answer:
Use `map()` with the index argument.

```js
let items = [
    { name: "Shirt" },
    { name: "Pants" }
];

let indexedItems = items.map((item, index) => ({ ...item, index }));

console.log(indexedItems);
```
### Output:
```js
[
    { name: "Shirt", index: 0 },
    { name: "Pants", index: 1 }
]
```
---

## 10. How do you double a numeric property in an array of objects?
### Answer:
Use `map()` to multiply the property value.

```js
let numbers = [
    { value: 10 },
    { value: 20 }
];

let doubledNumbers = numbers.map(n => ({ ...n, value: n.value * 2 }));

console.log(doubledNumbers);
```
### Output:
```js
[
    { value: 20 },
    { value: 40 }
]
```
---

## 11. How do you conditionally modify a property using `map()`?
### Answer:
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
### Output:
```js
[
    { name: "Alice", salary: 45000 },
    { name: "Bob", salary: 60000 }
]
```

---

## 12. How do you replace a specific value in an array of objects?
### Answer:
Use `map()` with an if condition.

```js
let orders = [
    { id: 1, status: "pending" },
    { id: 2, status: "shipped" }
];

let updatedOrders = orders.map(o => o.id === 1 ? { ...o, status: "completed" } : o);

console.log(updatedOrders);
```
### Output:
```js
[
    { id: 1, status: "completed" },
    { id: 2, status: "shipped" }
]
```
# JavaScript Map Method - Questions & Answers (Array of Objects)

## 13. How do you conditionally modify a property using map()?
**Answer:** Use `map()` with a condition.

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
**Output:**
```js
[
    { name: "Alice", salary: 45000 },
    { name: "Bob", salary: 60000 }
]
```

---

## 14. How do you replace a specific value in an array of objects?
**Answer:** Use `map()` with an if condition.

```js
let orders = [
    { id: 1, status: "pending" },
    { id: 2, status: "shipped" }
];

let updatedOrders = orders.map(o => o.id === 1 ? { ...o, status: "completed" } : o);

console.log(updatedOrders);
```
**Output:**
```js
[
    { id: 1, status: "completed" },
    { id: 2, status: "shipped" }
]
```

---

## 15. How do you invert a boolean property in an array?
**Answer:** Use `map()` to toggle `true/false`.

```js
let users = [
    { name: "Alice", active: true },
    { name: "Bob", active: false }
];

let toggledUsers = users.map(u => ({ ...u, active: !u.active }));

console.log(toggledUsers);
```
**Output:**
```js
[
    { name: "Alice", active: false },
    { name: "Bob", active: true }
]
```

---

## 16. How do you assign a rank based on an array index?
**Answer:** Use `map()` with index calculation.

```js
let students = [
    { name: "Alice" },
    { name: "Bob" }
];

let rankedStudents = students.map((s, i) => ({ ...s, rank: i + 1 }));

console.log(rankedStudents);
```
**Output:**
```js
[
    { name: "Alice", rank: 1 },
    { name: "Bob", rank: 2 }
]
```

---

## 17. How do you convert an array of objects to an array of arrays?
**Answer:** Use `map()` to create key-value pairs.

```js
let products = [
    { name: "Laptop", price: 1000 },
    { name: "Phone", price: 500 }
];

let productPairs = products.map(p => [p.name, p.price]);

console.log(productPairs);
```
**Output:**
```js
[
    ["Laptop", 1000],
    ["Phone", 500]
]
```

---

## 18. How do you pad a string property to a fixed length?
**Answer:** Use `map()` with `padEnd()`.

```js
let items = [
    { name: "Pen" },
    { name: "Notebook" }
];

let paddedItems = items.map(i => ({ ...i, name: i.name.padEnd(10, ".") }));

console.log(paddedItems);
```
**Output:**
```js
[
    { name: "Pen......." },
    { name: "Notebook.." }
]
```

---

These 18 questions should give you deep practice with `map()`. Let me know if you need more! 🚀



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



## 1. What is a Set in JavaScript?

A **Set** is a built-in JavaScript object that lets you store **unique values** of any type, whether primitive or objects. It ensures no duplicates and provides methods to add, delete, and check values.

## 2. How is a Set different from an array?

- **Uniqueness:**  
  A Set only stores **unique** values, while an array can have duplicates.

- **Ordering:**  
  Sets maintain insertion order, but they don't have indexed access like arrays (no numeric indices).

- **Methods:**  
  Sets provide methods like `.add()`, `.has()`, and `.delete()` optimized for unique value management.

- **Performance:**  
  Checking for existence (`.has()`) is generally faster with Sets than searching an array.

## 3. How do you create a new Set?

You can create a Set by using the `Set` constructor:

```js
const mySet = new Set(); // Creates an empty Set

// Or initialize with an iterable like an array:
const numbers = new Set([1, 2, 3, 3, 4]); 
console.log(numbers); // Set { 1, 2, 3, 4 } - duplicates ignored
```
## 4. How do you add elements to a Set?

You use the `.add()` method to add elements to a Set:

```js
const mySet = new Set();
mySet.add(1);
mySet.add('hello');
mySet.add({ key: 'value' });
```
## 5. How do you check if a value exists in a Set?

Use the `.has()` method to check whether a Set contains a specific value:

```js
const mySet = new Set([1, 2, 3]);

console.log(mySet.has(2));  // true
console.log(mySet.has(5));  // false
```
## 6. How do you delete an element from a Set?

Use the `.delete()` method to remove a specific element from a Set:

```js
const mySet = new Set([1, 2, 3]);

mySet.delete(2);

console.log(mySet.has(2)); // false
console.log(mySet);        // Set { 1, 3 }
```
## 7. How do you clear all elements in a Set?

Use the `.clear()` method to remove all elements from a Set:

```js
const mySet = new Set([1, 2, 3]);
mySet.clear();
console.log(mySet.size); // 0
```
## 8. How do you check if a value exists in a Set?

Use the `.has()` method, which returns `true` if the value is in the Set, otherwise `false`:

```js
const mySet = new Set([1, 2, 3]);
console.log(mySet.has(2)); // true
console.log(mySet.has(4)); // false
```
## 9. How do you delete an element from a Set?

Use the `.delete()` method, which removes the specified element from the Set and returns `true` if the element existed, otherwise `false`:

```js
const mySet = new Set([1, 2, 3]);
console.log(mySet.delete(2)); // true
console.log(mySet.has(2));    // false
```
## 10. How do you get the size of a Set?
Use the .size property to get the number of elements in a Set:

```js
const mySet = new Set([1, 2, 3]);
console.log(mySet.size); // 3
```
## 11. How do you iterate over the elements in a Set?
You can use a for...of loop or the .forEach() method to iterate over a Set:

```js
const mySet = new Set([1, 2, 3]);

// Using for...of
for (const value of mySet) {
  console.log(value);
}

// Using forEach
mySet.forEach(value => {
  console.log(value);
});
```
## 12. Are duplicate values allowed in a Set?

No, duplicate values are not allowed in a Set. Each value in a Set must be unique. If you try to add a duplicate value, it will be ignored.

```js
const mySet = new Set();
mySet.add(1);
mySet.add(1);
console.log(mySet.size); // 1
```
## 13. How does JavaScript determine equality for values in a Set?

JavaScript uses the **SameValueZero** algorithm to determine equality in a `Set`. This means:

- `NaN` is considered equal to `NaN`
- `0` and `-0` are considered equal
- Object references are compared by identity, not by content

**Examples:**

```js
const set = new Set();

set.add(NaN);
set.add(NaN);       // Duplicate — ignored
set.add(0);
set.add(-0);        // Treated as the same value
set.add({ a: 1 });
set.add({ a: 1 });  // Different object references — both added

console.log(set.size); // Output: 4
```

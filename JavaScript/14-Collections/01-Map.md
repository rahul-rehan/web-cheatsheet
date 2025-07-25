## 1. What is a Map in JavaScript?

A `Map` is a built-in object in JavaScript that holds key-value pairs and remembers the original insertion order of the keys. Unlike regular objects, `Map` allows keys of any type, including objects, functions, and primitives.

## 2. How is a Map different from a plain JavaScript object?

| Feature                | Map                            | Plain Object (`{}`)                   |
|------------------------|--------------------------------|---------------------------------------|
| Key Types              | Can be any type (objects, functions, etc.) | Only strings and symbols (other keys are coerced) |
| Key Order              | Maintains insertion order      | Order is not guaranteed (partially ordered in ES6+) |
| Size Retrieval         | `map.size`                     | Must be calculated manually           |
| Iteration              | Easier with `map.forEach()` or `for...of` | Requires `Object.keys()`, `Object.entries()`, etc. |
| Performance            | Better for frequent additions/removals | Optimized for static key sets         |

## 3. How do you create a new Map?

You can create a `Map` using the `new Map()` constructor.

#### Example:
```js
const myMap = new Map();

// Add key-value pairs
myMap.set('name', 'Alice');
myMap.set(42, 'The answer');
myMap.set({ id: 1 }, 'Object key');

console.log(myMap.get('name')); // "Alice"
console.log(myMap.size); // 3
```
## 4. What types of values can be used as keys in a Map?

In a `Map`, any value can be used as a key. This includes:
- Primitives: strings, numbers, booleans, symbols
- Objects
- Arrays
- Functions

Unlike plain objects (which convert keys to strings), `Map` keys retain their original type.

## 5. How do you add a key-value pair to a Map?

Use the `.set(key, value)` method:

```js
const map = new Map();
map.set('name', 'Alice');     // string key
map.set(1, 'one');            // number key
map.set({ id: 1 }, 'object'); // object key
```
## 6. How do you retrieve a value from a Map?

To retrieve a value from a `Map`, use the `.get(key)` method:

```js
const map = new Map();
map.set('language', 'JavaScript');

console.log(map.get('language')); // Output: "JavaScript"
```
Note: You must use the exact key reference. For object keys, using a different object with the same structure will not work:

```js
const objKey = { id: 1 };
map.set(objKey, 'value');

console.log(map.get(objKey));      // Output: "value"
console.log(map.get({ id: 1 }));   // Output: undefined (different object reference)
```
## 7. How do you check if a key exists in a Map?

Use the `.has(key)` method to check if a specific key exists in a `Map`:

```js
const map = new Map();
map.set('name', 'Alice');

console.log(map.has('name'));  // true
console.log(map.has('age'));   // false
```
## 8. How do you remove a key-value pair from a Map?

You can remove a key-value pair from a Map by using the `.delete(key)` method, which removes the entry with the specified key.

**Example:**

```js
const map = new Map();
map.set('name', 'Alice');

map.delete('name');
console.log(map.has('name'));  // false
```
## 9. How do you clear all entries in a Map?

You can clear all entries from a Map by using the `.clear()` method, which removes all key-value pairs from the Map.

**Example:**

```js
const map = new Map();
map.set('name', 'Alice');
map.set('age', 30);

map.clear();
console.log(map.size);  // 0
```
## 10. How do you get the size of a Map?

You can get the number of key-value pairs in a Map by using the `.size` property.

```js
const map = new Map();
map.set('a', 1);
map.set('b', 2);

console.log(map.size);  // Output: 2
```
## 11. How do you iterate over the keys and values in a Map?

You can iterate over the entries, keys, or values of a Map using:

- The `.forEach()` method
- The `for...of` loop with `.entries()`, `.keys()`, or `.values()`

**Examples:**

#### Using `.forEach()`:

```js
map.forEach((value, key) => {
  console.log(key, value);
});
```
#### Using `for...of` loop:

```js
// Iterate over key-value pairs
for (const [key, value] of map.entries()) {
  console.log(key, value);
}

// Iterate over keys only
for (const key of map.keys()) {
  console.log(key);
}

// Iterate over values only
for (const value of map.values()) {
  console.log(value);
}
```
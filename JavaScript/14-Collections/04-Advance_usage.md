## 1. Can Set store objects? How is equality determined for objects?

Yes, a `Set` can store objects. However, JavaScript determines object equality by reference, not by value. This means that two different object literals with the same structure are considered distinct.

**Example:**

```js
const set = new Set();

const obj1 = { id: 1 };
const obj2 = { id: 1 };

set.add(obj1);
set.add(obj2); // Different reference, so it will be added

console.log(set.size); // Output: 2
```
## 2. How do you convert a Set to an array and vice versa?

You can convert a `Set` to an array using the spread operator (`...`) or `Array.from()`. To convert an array to a `Set`, simply pass the array to the `Set` constructor. This is useful for removing duplicates or for working with Set-specific methods.

#### Set to Array:
```js
const mySet = new Set([1, 2, 3]);
const array1 = [...mySet];         // Using spread operator
const array2 = Array.from(mySet);  // Using Array.from()
```
#### Array to Set:
```js
const array = [1, 2, 3, 3, 4];
const mySet = new Set(array); // Duplicates are automatically removed
```
## 3. How can you perform set operations like union, intersection, and difference using Set?

JavaScript `Set` does not have built-in methods for union, intersection, or difference, but you can implement them using native operations like spread syntax and filtering.

#### Union:
```js
const a = new Set([1, 2, 3]);
const b = new Set([3, 4, 5]);
const union = new Set([...a, ...b]); // → Set {1, 2, 3, 4, 5}
```
#### Intersection:
```js
const intersection = new Set([...a].filter(x => b.has(x))); // → Set {3}
```
#### Difference:
```js
const difference = new Set([...a].filter(x => !b.has(x))); // → Set {1, 2}
```
## 4. How does Set.prototype.forEach() differ from array's forEach()?

Both `Set.prototype.forEach()` and `Array.prototype.forEach()` allow you to iterate over elements, but they differ slightly in the arguments passed to the callback function:

#### Set.prototype.forEach():
- The callback receives three arguments: `value`, `valueAgain`, and `set`.
- `value` and `valueAgain` are the same (for compatibility with `Map.prototype.forEach()` which provides `value` and `key`).
- Used primarily to iterate over unique values.

```js
const mySet = new Set(['x', 'y']);
mySet.forEach((value, valueAgain, set) => {
  console.log(value); // logs 'x' and 'y'
});
```
#### Array.prototype.forEach():
- The callback receives `element`, `index`, and `array`.

- Used for indexed iteration over ordered elements.

```js
const myArray = ['x', 'y'];
myArray.forEach((element, index, array) => {
  console.log(index, element); // logs: 0 'x', 1 'y'
});
```
#### Key Difference:
`Set.prototype.forEach()` does not provide index information, and its second parameter is not meaningful, while `Array.prototype.forEach()` provides index and full array context.

## Comparison and Best Practices
## 1. When should you use Map instead of a plain object?

Use a `Map` when:
- You need keys of any type (including objects or functions).
- You care about the insertion order of entries.
- You need predictable performance for frequent additions/removals.
- You want built-in methods like `.size`, `.set()`, `.get()`, `.has()`, and `.delete()`.

In contrast, plain objects are ideal for simple key-value storage with string/symbol keys and work well when performance is less critical.

## 2. When should you use Set instead of an array?

Use a `Set` when:
- You need to store **unique** values only.
- You want fast checks for existence (`.has()`).
- You don't care about index-based access or ordering beyond insertion order.
- You want efficient deduplication of data.

Arrays are better for ordered collections and when you need features like sorting, filtering, or index access.

## 3. Can Map and Set be used as JSON values? Why or why not?

No, `Map` and `Set` **cannot** be directly serialized with `JSON.stringify()` because:
- JSON only supports plain objects, arrays, strings, numbers, booleans, and null.
- `Map` and `Set` are complex types and will be ignored or serialized as `{}` or `[]`.

To include them in JSON:
- Convert `Map` to an array of entries: `Array.from(map)` or `[...map]`
- Convert `Set` to an array: `Array.from(set)` or `[...set]`

Then, serialize the arrays instead.
## 4. What are the performance benefits of using Map and Set?

- **Fast Lookups**: `Map` and `Set` provide average constant time (`O(1)`) complexity for operations like `get`, `set`, `has`, and `delete`, compared to potentially linear time (`O(n)`) in plain objects or arrays.
- **Efficient Key Handling**: `Map` can use any type as a key (including objects), avoiding the need for complex workarounds like key stringification in plain objects.
- **No Key Collisions**: `Map` avoids issues related to prototype chain collisions (`__proto__`, `hasOwnProperty`, etc.) that may occur in plain objects.
- **Automatic Uniqueness**: `Set` guarantees unique values, removing the need for manual duplication checks common with arrays.
- **Preserved Insertion Order**: Both `Map` and `Set` maintain the order of inserted items, useful for predictable iteration.

## 5. What are common use cases for Map and Set in real-world applications?

#### 📌 **Map Use Cases:**
- **Caching Results**: Store previously computed results for fast retrieval (e.g., memoization).
- **Storing Metadata**: Associate extra data with DOM nodes or objects without modifying the original object.
- **Tracking User Sessions**: Map user IDs to session data or tokens.
- **Counting Occurrences**: Use keys as items and values as counts.

#### 📌 **Set Use Cases:**
- **Deduplicating Data**: Remove duplicates from an array (`[...new Set(array)]`).
- **Efficient Membership Checks**: Store a list of banned usernames, loaded assets, or visited pages.
- **Tagging Systems**: Maintain a collection of unique tags or labels.
- **Tracking Unique Events**: Record which unique events or actions have occurred.

These structures are essential in modern applications for improving performance, clarity, and reliability of data operations.

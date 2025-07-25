## 1. Can objects be used as keys in a Map? Provide an example.

Yes, objects can be used as keys in a `Map` because `Map` keys can be of any type, including objects.

**Example:**

```js
const map = new Map();
const objKey = { id: 1 };

map.set(objKey, "Object as key");
console.log(map.get(objKey)); // Output: "Object as key"
```
## 2. How do you convert an object to a Map and vice versa?

- **Object to Map:**

```js
const obj = { a: 1, b: 2 };
const map = new Map(Object.entries(obj));
console.log(map); // Map { 'a' => 1, 'b' => 2 }
```
- **Map to Object:**

```js
const map = new Map([['a', 1], ['b', 2]]);
const obj = Object.fromEntries(map);
console.log(obj); // { a: 1, b: 2 }
```
## 3. Can you chain set() calls in a Map?

Yes, the `set()` method of a Map returns the Map object itself, allowing you to chain multiple `set()` calls together.

**Example:**

```js
const map = new Map();
map.set('a', 1)
   .set('b', 2)
   .set('c', 3);

console.log(map);
// Map(3) { 'a' => 1, 'b' => 2, 'c' => 3 }
```
## 4. How do `Map.prototype.forEach()` and `for...of` compare?

- **`Map.prototype.forEach()`**  
  - Iterates over each key-value pair in the Map.  
  - Accepts a callback function with parameters `(value, key, map)`.  
  - Callback is called once for each entry, in insertion order.  
  - Cannot be interrupted (no `break` or `return` from the loop).

- **`for...of` loop**  
  - Iterates over the Map's entries as `[key, value]` pairs.  
  - Allows more flexible control flow (can use `break`, `continue`, `return`).  
  - Syntax: `for (const [key, value] of map) { ... }`.  
  - Also iterates in insertion order.

## 5. What happens if you use the same object as a key in two different maps?

- Each Map instance maintains its own separate internal storage.  
- Using the **same object** as a key in two different Maps stores **independent entries** in each Map.  
- Changes to one Map do not affect the other, even if the keys are identical objects by reference.

```js
const objKey = { id: 1 };

const map1 = new Map();
const map2 = new Map();

map1.set(objKey, 'Value in map1');
map2.set(objKey, 'Value in map2');

console.log(map1.get(objKey)); // Output: "Value in map1"
console.log(map2.get(objKey)); // Output: "Value in map2"
```
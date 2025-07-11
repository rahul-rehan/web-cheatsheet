## 1. What is the result of `function example(x = 5, y = x * 2) {}` when no arguments are passed?

- When `example()` is called without arguments:
  - `x` defaults to `5`.
  - `y` defaults to `x * 2`, which evaluates to `10` because it uses the value of `x`.

#### Example:

```javascript
function example(x = 5, y = x * 2) {
  console.log(x, y);
}

example(); // Output: 5 10
```
## 2. How do you safely assign a default object or array to a parameter without unintended side effects?

- Objects and arrays are **reference types**, so using a default object or array directly in the function parameter can lead to shared references across calls, causing unexpected mutations.

- To avoid this, you should **create a new object or array inside the function body** if none is provided, ensuring each call gets its own separate instance.

#### Unsafe example (shared reference):

```javascript
function addItem(item, list = []) {
  list.push(item);
  return list;
}

const list1 = addItem("a");
const list2 = addItem("b");

console.log(list1); // Output: ["a", "b"]
console.log(list2); // Output: ["a", "b"]  // Both share the same array
```
#### Safe example (new instance per call):
```javascript
function addItem(item, list) {
  if (!list) {
    list = [];
  }
  list.push(item);
  return list;
}

const list1 = addItem("a");
const list2 = addItem("b");

console.log(list1); // Output: ["a"]
console.log(list2); // Output: ["b"]  // Separate arrays
```
This approach prevents unintended side effects caused by shared mutable default values.
#### Or using a default parameter with a function:
```javascript
Copy
Edit
function createList() {
  return [];
}

function addItem(item, list = createList()) {
  list.push(item);
  return list;
}
```
This approach ensures each function call gets a fresh, independent object or array, preventing unintended side effects from shared references.
## 3. What are potential bugs to watch out for when using objects/arrays as default parameter values?

- **Shared Reference Bug:** Objects and arrays are reference types, so if used as default parameters directly, the same instance is shared across all function calls.
- This can lead to **unexpected mutations** where one call's changes affect others.
- Example: Modifying a default array parameter in one call affects the array in subsequent calls.

## 4. Why might developers avoid using default parameters in some codebases?

- **Compatibility concerns:** Older JavaScript environments (pre-ES6) do not support default parameters.
- **Readability:** Some developers prefer explicit checks inside the function body for clarity.
- **Complex default logic:** When defaults depend on conditions or side effects, inline defaults can become confusing.
- **Consistency:** In large or legacy codebases, uniform style might avoid default parameters to maintain consistency.

## 5. Can default parameters be used with arrow functions?

- **Yes**, arrow functions support default parameters just like regular functions.

#### Example:

```javascript
const greet = (name = "Guest") => {
  console.log("Hello, " + name);
};

greet();       // Output: Hello, Guest
greet("Alice"); // Output: Hello, Alice
```
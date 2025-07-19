## 1. What is function borrowing in JavaScript?

**Function borrowing** is a technique where one object uses a method belonging to another object without having that method defined on itself. This allows objects to reuse functions from other objects, promoting code reuse and flexibility.

## 2. How does `call()` enable one object to borrow a method from another object?

The `call()` method allows you to invoke a function with an explicit `this` context. By using `call()`, an object can execute a method defined on another object as if it were its own method, effectively **borrowing** it.

## 3. Example: Borrowing `Array.prototype.slice` using `call()`

```javascript
const arrayLike = {
  0: 'a',
  1: 'b',
  2: 'c',
  length: 3
};

// Borrow Array's slice method to convert array-like object to an array
const result = Array.prototype.slice.call(arrayLike);

console.log(result); // Output: ['a', 'b', 'c']
```
#### In this example:

- `arrayLike` is an object that resembles an array (has numeric keys and a `length` property) but does not have array methods.

- Using `Array.prototype.slice.call(arrayLike)` borrows the `slice` method from arrays and applies it to `arrayLike`.

- This converts the array-like object into a true array.
## 4. Why is function borrowing useful in scenarios involving array-like objects or DOM collections?

- **Array-like objects** (such as `arguments`, NodeLists, or HTMLCollections) often have numeric indices and a `length` property but **do not have array methods** like `forEach`, `slice`, or `map`.
- Function borrowing allows these objects to **reuse array methods** without converting them into real arrays.
- This helps avoid manual iteration and simplifies manipulation of such collections.

## 5. Can you use `call()` to borrow methods like `toString`, `push`, or `join`? Provide examples.

Yes, you can borrow many methods using `call()` as long as the method is compatible with the object's structure.

#### Borrowing `toString`:

```javascript
const obj = { a: 1, b: 2 };
const result = Object.prototype.toString.call(obj);
console.log(result); // Output: [object Object]
```
#### Borrowing `push`:
Since `push` modifies the array and relies on a `length` property and numeric keys, it can be borrowed by array-like objects:

```javascript
const arrayLike = { length: 0 };
Array.prototype.push.call(arrayLike, 'x');
Array.prototype.push.call(arrayLike, 'y');
console.log(arrayLike); // Output: { '0': 'x', '1': 'y', length: 2 }
```
#### Borrowing `join`:
```javascript
const arrayLike = { 0: 'a', 1: 'b', length: 2 };
const joined = Array.prototype.join.call(arrayLike, '-');
console.log(joined); // Output: 'a-b'
```
## 6. What are the limitations of function borrowing using `call()`?

- **Structural requirements:** Borrowed methods expect the target object to have specific properties (e.g., a `length` property for array methods). If these are missing or incorrect, the method may behave unexpectedly or throw errors.

- **No prototype inheritance:** Using `call()` to borrow a method does **not** set up prototype chain inheritance. Only the method is invoked with a different `this` context; prototype methods are not inherited.

- **Mutability concerns:** Some borrowed methods (like `push`) modify the target object. If the object isn’t designed to handle such changes, this can cause bugs or unexpected behavior.

- **Method compatibility:** Not all methods can be borrowed successfully. Some rely on internal mechanisms or expect the object to be a genuine instance of a particular type (e.g., a true array).

- **Performance and readability:** Excessive use of function borrowing can lead to code that is harder to understand and potentially less efficient than using proper data structures or inheritance patterns.

## Advanced Use Cases and Best Practices

## 1. Can `call()` be used with arrow functions? Why or why not?

- **No, `call()` cannot effectively change the `this` context of arrow functions.**
- Arrow functions **do not have their own `this`**; instead, they inherit `this` lexically from the surrounding scope.
- Therefore, using `call()` (or `apply()`/`bind()`) on arrow functions **does not affect the `this` value** inside them.

#### Example:

```javascript
const arrowFunc = () => {
  console.log(this);
};

const obj = { name: 'Alice' };
arrowFunc.call(obj); // Logs the outer `this`, not `obj`
```
## 2. How does `call()` behave with strict mode enabled?

- In **strict mode**, when `call()` is invoked with `null` or `undefined` as the `this` value, the `this` inside the called function remains `null` or `undefined`.
- In contrast, in **non-strict mode**, `this` defaults to the global object (e.g., `window` in browsers).
- Strict mode enforces more predictable and safer handling of the `this` keyword.

#### Example:

```javascript
'use strict';

function showThis() {
  console.log(this);
}

showThis.call(null);      // Logs: null
showThis.call(undefined); // Logs: undefined
```
## 3. How can `call()` be used for partial application of functions?

- `call()` invokes a function immediately with a specified `this` value and individual arguments.
- You can use `call()` to **pass fixed arguments** to a function for immediate execution, which resembles partial application.
- However, unlike `bind()`, `call()` does **not create a new function**; it simply calls the function with the given arguments.

#### Example:

```javascript
function multiply(a, b) {
  return a * b;
}

// Partial application by passing arguments with call()
const result = multiply.call(null, 2, 5); // 10

console.log(result);
```
- For creating reusable partially applied functions, `bind()` is preferred as it returns a new function with preset arguments.
## 4. Is `call()` more performant than `apply()` or `bind()` in certain cases?

- **Yes**, `call()` can be more performant than `apply()` or `bind()` when you know the exact number of arguments beforehand and want to invoke the function immediately.
- `call()` requires listing arguments individually, which can be faster for functions with a fixed number of parameters.
- `apply()` is useful when arguments are in an array, but may have slight overhead due to array processing.
- `bind()` creates a new function and thus has additional overhead compared to immediate invocation methods like `call()` and `apply()`.

## 5. When should you prefer `call()` over other function context manipulation techniques?

- Use `call()` when:
  - You want to **immediately invoke** a function with a specific `this` context.
  - You know the **exact number of arguments** and can pass them individually.
  - You want to avoid the overhead of creating a new bound function (which happens with `bind()`).
- Avoid `call()` when you need to:
  - Pass arguments as an array (`apply()` is better).
  - Create a new function for later invocation with preset context or arguments (`bind()` is better).

## 6. How do you debug issues arising from incorrect `this` binding using `call()`?

- **Check the `this` value** being passed to `call()`: Ensure it's the intended object.
- Use **console logs** inside the function to verify what `this` refers to.
- Confirm the function is not an **arrow function**, as arrow functions ignore `call()` and inherit `this` lexically.
- Use **strict mode** to catch accidental `this` binding to the global object.
- Use debugging tools or breakpoints to inspect the execution context.
- Example debugging step:

```javascript
function greet() {
  console.log(this);
}

const obj = { name: 'Alice' };
greet.call(obj); // Should log obj; if not, check if greet is arrow function or this is incorrect
```
#### Summary
- `call()` can be faster than `apply()` or `bind()` when invoking immediately with known arguments.

- Prefer `call()` for immediate invocation with explicit arguments.

- Debug `this` issues by verifying the passed context, avoiding arrow functions, and using console logs or debugging tools.
## 1. What is function borrowing in JavaScript?

Function borrowing is a technique where one object **uses a method belonging to another object** without having that method defined on itself. This allows objects to reuse functions, improving code reuse and flexibility.

## 2. How can `apply()` be used to borrow a method from one object to use in another?

The `apply()` method can be used to call a function with a specified `this` context and arguments as an array. By passing a different object as the `this` value, one object can **borrow** a method from another object's prototype or instance.

## 3. Example of borrowing `Array.prototype.join` using `apply()`

```javascript
const arrayLike = {
  0: 'apple',
  1: 'banana',
  2: 'cherry',
  length: 3
};

const result = Array.prototype.join.apply(arrayLike, [', ']);

console.log(result); // Output: "apple, banana, cherry"
```
- Here, `arrayLike` is an object that looks like an array (has numeric keys and a `length` property) but doesn't have array methods.

- Using `apply()`, we borrow `join` from `Array.prototype` and call it with `arrayLike` as `this`.

- This converts the array-like object into a string with elements joined by `", "`.

## 4. Why is `apply()` useful when dealing with array-like objects or the `arguments` object?

- Array-like objects (such as the `arguments` object or DOM collections) have numeric indices and a `length` property but **do not have array methods** like `forEach`, `slice`, or `map`.
- `apply()` allows borrowing of array methods by calling them with these objects as `this`, enabling the use of array functionalities without converting the objects to true arrays.
- This avoids manual iteration and simplifies working with such structures.

## 5. Can DOM collections like `NodeList` borrow Array methods using `apply()`? Provide an example.

Yes, DOM collections such as `NodeList` can borrow array methods using `apply()`.

#### Example:

```javascript
const nodeList = document.querySelectorAll('div');

// Borrow Array.prototype.forEach to iterate over NodeList
Array.prototype.forEach.apply(nodeList, [function(node) {
  console.log(node.tagName);
}]);
```
- In this example, `forEach` is borrowed from `Array.prototype` and applied to the `NodeList`.

- This enables iteration over the nodes even though `NodeList` doesn't have `forEach` directly (in some older browsers).
## 6. What are some limitations or risks of using function borrowing?

- **Structural dependency:** Borrowed methods expect the target object to have certain properties (like a valid `length` property). If these are missing or incorrect, it may lead to errors or unexpected behavior.

- **No prototype inheritance:** Using `apply()` or `call()` to borrow a method does **not** transfer prototype chains or inheritance.

- **Mutability concerns:** Some borrowed methods (e.g., `push`, `splice`) modify the target object. If the object is not designed for such changes, this can cause bugs.

- **Compatibility limitations:** Some methods rely on internal behaviors or slots that cannot be mimicked by simply borrowing the method.

- **Code readability and performance:** Overusing function borrowing can make code harder to understand and may have performance implications compared to proper object design.

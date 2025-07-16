## 1. What happens when a constructor function is called without the `new` keyword?

- When a constructor is called **without** `new`, it behaves like a regular function.
- The value of `this` is not bound to a new object:
  - In **non-strict mode**, `this` refers to the **global object** (`window` in browsers).
  - In **strict mode**, `this` is `undefined`, which causes a runtime error when trying to assign properties.


## 2. How can calling a constructor without `new` affect the global object?

- In non-strict mode, properties assigned to `this` inside the constructor will be attached to the **global object**, unintentionally polluting it.

#### Example:

```javascript
function Person(name) {
  this.name = name;
}

Person("Alice"); // Forgot `new`

console.log(name); // Output: Alice (added to global scope)
```
This can lead to bugs and security issues due to unintended side effects.
## 3. How can you enforce the use of `new` in a constructor function?

You can enforce the use of `new` in two common ways:

#### 1. Using `new.target` (ES6+):

- `new.target` is only defined when a function is called with the `new` keyword.
- You can throw an error if it's undefined.

```javascript
function Person(name) {
  if (!new.target) {
    throw new Error("Person must be called with 'new'");
  }
  this.name = name;
}
```
#### 2. Using instanceof to auto-correct:
- You can check if `this` is an instance of the constructor.

- If not, call the constructor again with `new`.

```javascript
function Person(name) {
  if (!(this instanceof Person)) {
    return new Person(name);
  }
  this.name = name;
}
```
✅ These patterns help prevent incorrect usage and ensure the constructor creates and returns the expected object.
## 4. What is a common pattern to handle missing `new` in constructor functions?

A common pattern is to check whether the function was called with `new`, and if not, automatically call it with `new` from inside the function. This prevents incorrect usage and ensures the instance is created properly.

#### Example:

```javascript
function User(name) {
  if (!(this instanceof User)) {
    return new User(name);
  }
  this.name = name;
}
```
- This allows users to call `User("Alice")` or `new User("Alice")` with the same outcome.

- It ensures that `this` is always correctly bound to a new instance.
## 5. Should you use arrow functions as constructor functions? Why or why not?

❌ **No, you should not use arrow functions as constructor functions.**

#### Reasons:

- **Arrow functions do not have their own `this`** — they inherit `this` from the surrounding (lexical) scope.
- **Arrow functions cannot be used with the `new` keyword** — attempting to do so throws a `TypeError`.

#### Example:

```javascript
const Person = (name) => {
  this.name = name;
};

const p = new Person("Alice"); // TypeError: Person is not a constructor
```
✅ Always use regular functions (function declarations or expressions) for constructor functions, as they are designed to work with `new`.

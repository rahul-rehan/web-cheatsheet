## 1. What is the purpose of the `call()` method in JavaScript?

The `call()` method in JavaScript is used to invoke a function with a specific `this` value and arguments provided individually. It allows you to call a function in the context of another object, enabling method borrowing and dynamic function execution.

## 2. What is the syntax of the `call()` method?

```javascript
func.call(thisArg, arg1, arg2, ...);
```
- **`func`**: The function to be called.

- **`thisArg`**: The value to be used as `this` when calling the function.

- **`arg1, arg2, ...`**: Arguments passed to the function.

#### Example:

```javascript
function greet(greeting) {
  console.log(`${greeting}, my name is ${this.name}`);
}

const person = { name: 'Alice' };
greet.call(person, 'Hello'); // Output: Hello, my name is Alice
```
## 3. How does `call()` differ from `apply()` and `bind()`?

| Method   | Description                                                                 | Arguments                     | Returns                     |
|----------|-----------------------------------------------------------------------------|-------------------------------|-----------------------------|
| `call()` | Invokes the function immediately with a specified `this` value and arguments provided individually. | `thisArg, arg1, arg2, ...`    | Return value of the function |
| `apply()`| Similar to `call()`, but arguments are passed as an array or array-like object. | `thisArg, [argsArray]`        | Return value of the function |
| `bind()` | Returns a new function with a specified `this` value and optional arguments. Does **not** invoke the function immediately. | `thisArg, arg1, arg2, ...`    | A new bound function         |

#### Example Usage

```javascript
function greet(greeting) {
  console.log(`${greeting}, my name is ${this.name}`);
}

const person = { name: 'Alice' };

// Using call
greet.call(person, 'Hi');           // Output: Hi, my name is Alice

// Using apply
greet.apply(person, ['Hello']);     // Output: Hello, my name is Alice

// Using bind
const greetPerson = greet.bind(person, 'Hey');
greetPerson();                      // Output: Hey, my name is Alice
```
#### Summary
- `call()`: Invokes the function immediately with individual arguments.

- `apply()`: Invokes the function immediately with arguments as an array.

- `bind()`: Returns a new function with bound this and optional preset arguments.

## 4. What is the first argument of the `call()` method used for?

The **first argument** of the `call()` method is used to **set the `this` value** inside the function when it's called. It determines what object the function should operate on.

```javascript
function showName() {
  console.log(this.name);
}

const user = { name: 'Alice' };
showName.call(user); // 'this' is now set to 'user'
```
## 5. What happens if you pass `null` or `undefined` as the `this` value in `call()`?

If you pass `null` or `undefined` as the `this` value to the `call()` method:

- In **non-strict mode**, `this` defaults to the **global object**:
  - `window` in browsers
  - `global` in Node.js

- In **strict mode**, `this` remains as the value passed (`null` or `undefined`).

#### Example (Non-strict mode):

```javascript
function showThis() {
  console.log(this); // Logs the global object (e.g., window)
}

showThis.call(null);
showThis.call(undefined);
```
#### Example (Strict mode):
```javascript
'use strict';

function showThis() {
  console.log(this); // Logs: null or undefined
}

showThis.call(null);      // Logs: null
showThis.call(undefined); // Logs: undefined
```
#### Summary:

- Non-strict mode: `this` defaults to the global object.

- Strict mode: `this` stays as `null` or `undefined`.
## 6. Provide an example of using `call()` to change the context of `this`

The `call()` method can be used to change the context (`this`) of a function, allowing one object to use a method belonging to another.

#### Example:

```javascript
const person1 = {
  name: 'Alice',
  greet: function(greeting) {
    console.log(`${greeting}, I'm ${this.name}`);
  }
};

const person2 = {
  name: 'Bob'
};

// Using call() to change the context to person2
person1.greet.call(person2, 'Hello'); // Output: Hello, I'm Bob
```
#### In this example:

- `person1` has a `greet` method.

- Using `call()`, we invoke `greet` with `person2` as the `this` context.

- As a result, `this.name` refers to `"Bob"` instead of `"Alice"`.
## 7. Can primitive values be passed as `this` in `call()`? What happens in that case?

Yes, **primitive values** (such as numbers, strings, and booleans) **can be passed** as the `this` value in the `call()` method. When a primitive is passed, JavaScript **automatically wraps** it in its corresponding **object wrapper** type.

#### Behavior:
- **String** becomes a `String` object
- **Number** becomes a `Number` object
- **Boolean** becomes a `Boolean` object

However, `null` and `undefined` are **not converted** — they default to the global object in non-strict mode or remain as-is in strict mode.

#### Example:

```javascript
function showType() {
  console.log(typeof this); // Logs: 'object'
  console.log(this);
}

showType.call('hello'); // 'hello' becomes a String object
showType.call(42);      // 42 becomes a Number object
showType.call(true);    // true becomes a Boolean object
```
#### In strict mode:
```javascript
'use strict';

function showStrictType() {
  console.log(typeof this);
}

showStrictType.call('hello'); // Logs: 'string'
```
In strict mode, primitives are not wrapped, and `this` remains the primitive value itself.

Summary:
- Primitive values can be used as `this` in `call()`.

- In non-strict mode, they are automatically boxed into their object equivalents.

- In strict mode, they remain as primitive values.
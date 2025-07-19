## 1. What is the `apply()` method in JavaScript?

The `apply()` method is a built-in JavaScript function that allows you to call a function with a specified `this` context and arguments provided as an **array (or array-like object)**. It enables dynamic function invocation with flexible arguments.

## 2. What is the syntax of the `apply()` method?

```javascript
function.apply(thisArg, [argsArray])
```
- **`thisArg`**: The value to use as `this` when calling the function.

- **`argsArray`**: An array or array-like object containing the arguments to pass to the function. This parameter can be `null` or omitted if there are no arguments.
## 3. How does `apply()` differ from `call()`?

| Aspect            | `call()`                             | `apply()`                          |
|-------------------|------------------------------------|----------------------------------|
| Argument passing  | Arguments are passed **individually**, separated by commas. | Arguments are passed as a **single array** or array-like object. |
| Typical use case  | When you know the exact number of arguments and want to list them explicitly. | When you have arguments already in an array or array-like structure. |
| Syntax example    | `func.call(thisArg, arg1, arg2)`   | `func.apply(thisArg, [arg1, arg2])` |

**Summary:**  
Both methods invoke a function with a specified `this` context, but differ in how the function's arguments are supplied.
## 4. What type of value should be passed as the second argument to `apply()`?

- The second argument to `apply()` should be an **array** or an **array-like object** (an object with a `length` property and indexed elements).
- This array (or array-like object) contains the list of arguments that will be passed to the function being called.
- If there are no arguments to pass, you can use `null` or `undefined`.

## 5. What is the purpose of the first argument in `apply()`?

- The first argument specifies the value of `this` inside the function when it is invoked.
- It determines the context in which the function runs.
- You can pass any value (object, `null`, `undefined`, primitive), but if `null` or `undefined` is passed in non-strict mode, `this` defaults to the global object.
## 6. What happens when `null` or `undefined` is passed as the first argument in `apply()`?

- In **non-strict mode**, if `null` or `undefined` is passed as the first argument, the `this` value inside the called function defaults to the **global object** (`window` in browsers).
- In **strict mode**, `this` remains exactly `null` or `undefined` as passed.
- This behavior affects how the function accesses or modifies properties via `this`.

## 7. Provide a simple example of using `apply()` to invoke a function with a specific `this` context

```javascript
const person = {
  name: 'Alice',
};

function greet(greeting, punctuation) {
  console.log(greeting + ', ' + this.name + punctuation);
}

greet.apply(person, ['Hello', '!']); // Output: Hello, Alice!
```
- Here, `apply()` calls the `greet` function with `this` set to the `person` object.

- The arguments `'Hello'` and `'!'` are passed as an array to `apply()`.
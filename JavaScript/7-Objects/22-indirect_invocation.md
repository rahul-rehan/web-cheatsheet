## 1. What is indirect invocation using `call()` and `apply()`?

- Indirect invocation refers to calling a function with a specified `this` context using `call()` or `apply()`.
- Both methods allow you to control the value of `this` explicitly during function execution.

**Example:**
```js
function greet() {
  console.log(this.name);
}

const person = { name: "Alice" };
greet.call(person);  // "Alice"
greet.apply(person); // "Alice"
```
## 2. How does `this` change when using `call()` or `apply()`?

- When using `call()` or `apply()`, the value of `this` is **explicitly set** to the first argument provided to the method.
- This overrides the default `this` binding, which normally depends on how the function is invoked.

**Key Differences Between `call()` and `apply()`:**

| Method   | How arguments are passed                      |
|----------|-----------------------------------------------|
| `call()` | As a comma-separated list                     |
| `apply()`| As a single array of arguments                |

**Example:**
```js
function introduce(language) {
  console.log(`${this.name} speaks ${language}`);
}

const person = { name: "Alice" };

introduce.call(person, "English");      // Alice speaks English
introduce.apply(person, ["Spanish"]);   // Alice speaks Spanish
```
- In both cases, `this` refers to the `person` object instead of the global object or being undefined.
## 3. What is the purpose of `Function.prototype.bind()`?

- The `bind()` method creates a **new function** with `this` permanently set to the provided value.
- It does **not immediately invoke** the function—it returns a new function with the bound context.

**Why use `bind()`?**
- To ensure the correct `this` context, especially in callback functions or event handlers.
- Useful in scenarios where a function loses its original context, like when passed to `setTimeout` or used as a standalone callback.

**Example:**
```js
function greet() {
  console.log(this.name);
}

const person = { name: "Bob" };
const boundGreet = greet.bind(person);

boundGreet(); // Output: "Bob"
```
- Here, `greet.bind(person)` returns a new function that always uses `person` as `this`, regardless of how or where it is called.
## 4. Provide an example where `bind()` is used to permanently set the `this` context

```js
const user = {
  name: "Alice",
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

const greetFn = user.greet.bind(user);

setTimeout(greetFn, 1000); // Output after 1 second: "Hello, my name is Alice"
```
- n this example, `bind()` ensures that `this` inside `greet()` always refers to `user`, even when the function is called by `setTimeout`.
## 5. What happens when a bound function is used as a constructor? Does it preserve the bound `this`?

- When a function that has been bound with `bind()` is used as a **constructor** (i.e., called with `new`), the **bound `this` is ignored**.
- Instead, a new object is created and assigned to `this`, just like with any normal constructor call.

**Example:**
```js
function Person(name) {
  this.name = name;
}

const BoundPerson = Person.bind({ name: "Bound Object" });

const p = new BoundPerson("Alice");

console.log(p.name); // Output: "Alice"
```
- Even though `Person` was bound to `{ name: "Bound Object" }`, the `new` keyword overrides that binding.

- This ensures constructors behave predictably and always return a new object (unless another object is explicitly returned).
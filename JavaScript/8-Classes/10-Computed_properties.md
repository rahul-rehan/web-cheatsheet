## 1. What is a computed property in JavaScript?

A computed property is a property of an object whose name (key) is dynamically determined at runtime using an expression rather than a fixed identifier.

## 2. How do you define a computed property in an object literal?

You define a computed property by enclosing an expression in square brackets `[]` inside the object literal. The expression is evaluated, and its result is used as the property name.

## 3. What syntax is used to create a computed property name?

```js
const key = "dynamicKey";
const obj = {
  [key]: "value"
};
```
## 4. Provide an example of a computed property using a variable as a key.

```js
const propName = "color";
const car = {
  [propName]: "red"
};
console.log(car.color); // Output: "red"
```
## 5. Can you use expressions inside the computed property brackets?

Yes, you can use any valid JavaScript expression inside the square brackets to compute the property name dynamically.

**Example:**

```js
const prefix = "user";
const id = 42;
const obj = {
  [prefix + id]: "Alice"
};
console.log(obj.user42); // Output: "Alice"
```
## 6. Are computed property names evaluated at runtime or compile time?

Computed property names are evaluated at runtime. This means the expression inside the square brackets is executed when the object literal is created.

## 7. What is the result of using a symbol as a computed property name?

Using a `Symbol` as a computed property name creates a unique property key that does not clash with string keys and is not enumerable in normal property iterations.

**Example:**

```js
const sym = Symbol("id");
const obj = {
  [sym]: 123
};
console.log(obj[sym]); // 123
console.log(Object.keys(obj)); // [] (symbol-keyed properties are not listed)
```
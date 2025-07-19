## 1. Why are arrow functions not recommended for object methods?

- Arrow functions do **not have their own `this`**; they inherit `this` lexically from the surrounding scope.
- When used as object methods, arrow functions cannot access the object’s own properties via `this`.
- This leads to unexpected behavior because `this` does **not** refer to the object itself.

## 2. What is the value of `this` inside an arrow function used as an object method?

- The value of `this` inside an arrow function used as an object method is inherited from the **outer lexical scope** where the arrow function is defined.
- It **does not** refer to the object instance.

## 3. Example where an object method defined as an arrow function fails to access the object’s properties

```javascript
const person = {
  name: 'Alice',
  greet: () => {
    console.log(`Hello, my name is ${this.name}`); // 'this' does not refer to person
  }
};

person.greet(); // Output: "Hello, my name is undefined"
```
- n this example, `this.name` is `undefined` because `this` is not bound to the `person` object inside the arrow function.
## 4. Why do arrow functions not work as expected when used with `this` inside object methods?

- Arrow functions do **not have their own `this`** context.
- Instead, they **inherit `this` lexically** from the surrounding scope where they are defined.
- When used as object methods, this means `this` inside the arrow function does **not** refer to the object itself.
- As a result, accessing object properties via `this` inside an arrow function method leads to unexpected or incorrect behavior.
- This is unlike regular functions, where `this` is dynamically bound based on how the function is called (e.g., as a method of an object).

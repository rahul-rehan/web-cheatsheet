## 1. Why should you not use arrow functions when defining prototype methods?

- Arrow functions **do not have their own `this`**; they inherit it lexically.
- Prototype methods rely on `this` being **dynamically bound** to the instance invoking the method.
- Using arrow functions breaks this binding, causing prototype methods to fail in accessing instance properties.

## 2. How does lexical scoping of `this` break prototype inheritance when using arrow functions?

- Lexical scoping binds `this` to the scope where the arrow function was defined, not to the object instance.
- Therefore, prototype methods defined as arrow functions cannot correctly reference instance-specific data via `this`.
- This breaks the expected behavior of prototype inheritance where methods operate on the calling object.

## 3. Can you override or extend behavior using arrow functions in prototype-based inheritance?

- No, because arrow functions do not bind `this` dynamically, they are unsuitable for methods that rely on `this` referring to the object instance.
- This limits the ability to override or extend prototype methods correctly with arrow functions.

## 4. Example of a prototype method using a regular function

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log(`Hello, my name is ${this.name}`);
};

const alice = new Person('Alice');
alice.greet(); // Output: "Hello, my name is Alice"
```
- Here, `greet` is a regular function, so `this` correctly refers to the instance (`alice`).
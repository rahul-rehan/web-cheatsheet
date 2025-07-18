## 1. What are private fields in JavaScript classes?

Private fields are class properties that are only accessible within the class they are declared in. They help enforce encapsulation by preventing external code from directly accessing or modifying these fields.

## 2. How do you define a private field in a JavaScript class?

You define a private field by prefixing the field name with a `#` symbol inside the class body.

## 3. What is the syntax difference between a private and a public field?

- **Private field:** Uses `#` before the name (e.g., `#myField`)
- **Public field:** Defined without the `#` (e.g., `myField`)

**Example:**

```js
class Example {
  #privateField;  // Private field
  publicField;    // Public field

  constructor() {
    this.#privateField = 42;
    this.publicField = 100;
  }
}
```
## 4. Can you access a private field directly outside of the class?

No, private fields cannot be accessed or modified directly from outside the class. Attempting to do so will result in a syntax error.

## 5. Why are private fields useful in object-oriented programming?

Private fields help enforce encapsulation by hiding the internal state of an object. This prevents external code from accidentally or intentionally modifying internal data, leading to better data integrity, abstraction, and maintainability.
## 6. What error is thrown if you try to access a private field from outside the class?

If you try to access a private field from outside its class, JavaScript throws a `SyntaxError` or a `TypeError`, indicating that the private field is not accessible.


## 7. Are private fields part of the object instance’s own properties?

Yes, private fields are stored directly on the object instance, but they are not accessible or enumerable like public properties. They exist in a way that is internal and hidden from outside access.

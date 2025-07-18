## 1. How do you define getters and setters using Object.defineProperty()?

You can define getters and setters on an object property by using `Object.defineProperty()` and specifying `get` and/or `set` functions in the property descriptor.

## 2. Example of creating a non-enumerable getter using Object.defineProperty():

```js
const person = {
  firstName: 'John',
  lastName: 'Doe',
};

Object.defineProperty(person, 'fullName', {
  get() {
    return `${this.firstName} ${this.lastName}`;
  },
  enumerable: false,  // makes the getter non-enumerable
});

console.log(person.fullName); // John Doe

// The property 'fullName' won't show up in for...in loops or Object.keys()
for (const key in person) {
  console.log(key); // logs only "firstName" and "lastName"
}
console.log(Object.keys(person)); // ["firstName", "lastName"]
```
## 3. Can you define multiple getters and setters at once? Which method would you use?

Yes, you can define multiple getters and setters at once using the `Object.defineProperties()` method, which allows specifying multiple property descriptors on an object in a single call.

## 4. What are some common use cases for getters and setters in real-world applications?

- **Encapsulation:** Control access to private or internal data by exposing computed or validated properties.
- **Derived values:** Compute values on the fly based on other object properties without storing redundant data.
- **Validation:** Validate or transform values before setting them on an object.
- **Lazy computation:** Calculate property values only when accessed, improving performance.
- **Data binding:** Automatically trigger side effects or UI updates when properties change.

## 5. Are getter and setter functions invoked when accessing the property directly?

Yes. Accessing a property with a getter invokes the getter function transparently, returning its computed value. Similarly, assigning to a property with a setter invokes the setter function. This happens as if the property holds a value, but actually calls the functions behind the scenes.
## 6. What will be the result of `typeof obj.getValue` if `getValue` is a getter?

If `getValue` is defined as a getter property, then `typeof obj.getValue` will return the type of the value that the getter returns, **not** `"function"`. This is because accessing `obj.getValue` calls the getter and returns its value, so `typeof` evaluates the type of that returned value.

For example, if the getter returns a number, `typeof obj.getValue` will be `"number"`.

## 7. Can you override or redefine a getter once it is defined?

Yes, you can override or redefine a getter by using `Object.defineProperty()` again on the same property with a new getter function. This will replace the existing getter with the new one.

However, if the property is non-configurable (`configurable: false`), then you cannot redefine the getter.
## Best Practices and Limitations
## 1. When should you use a getter over a method?

- Use a **getter** when you want to expose a property-like interface that computes or derives a value on access, making the syntax cleaner and more intuitive.
- Getters are ideal when the value should appear as a normal property rather than a function call, improving readability.
- Use methods when the operation involves significant computation, side effects, or requires parameters.

## 2. What are potential drawbacks of overusing getters and setters?

- Excessive use of getters/setters can **hide complexity** and side effects, making code harder to understand and debug.
- Getters that perform expensive computations can lead to **performance issues** if accessed frequently.
- Overusing setters can lead to unexpected mutations and side effects, complicating state management.
- They can also make it less clear when something is a simple property vs. a computed value.

## 3. Can you define a getter or setter in an ES6 class? Show how.

Yes, ES6 classes support getters and setters using the `get` and `set` keywords inside the class body.

```js
class Person {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }

  // Getter for fullName
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  }

  // Setter for fullName
  set fullName(name) {
    const parts = name.split(' ');
    this.firstName = parts[0];
    this.lastName = parts[1] || '';
  }
}

const person = new Person('Jane', 'Doe');
console.log(person.fullName); // "Jane Doe"
person.fullName = 'John Smith';
console.log(person.firstName); // "John"
console.log(person.lastName);  // "Smith"
```
## 4. Are getters/setters supported in all JavaScript environments?

- Getters and setters have been supported since **ECMAScript 5 (ES5)**, which is widely implemented in all modern browsers and JavaScript environments.
- They may not be supported in very old environments or legacy browsers that do not fully implement ES5 features.
- For modern web and Node.js development, getters and setters can be safely used.

## 5. How do getters and setters behave with inheritance?

- Getters and setters are inherited through the prototype chain just like regular properties.
- When a subclass inherits a getter or setter, accessing the property invokes the inherited accessor methods.
- Subclasses can **override** inherited getters and setters by defining new ones with the same property name.
- This allows dynamic and polymorphic behavior in object-oriented designs using getters/setters.

## 1. How do you define a private instance method in a class?

- You define a private instance method by prefixing its name with `#` inside the class body.

## 2. Can a private instance method access private fields of the same class?

- Yes, private instance methods can access private fields and other private methods of the same class.

## 3. Example of a class with a private instance method and its usage internally:

```js
class Counter {
  #count = 0;

  // Private instance method
  #increment() {
    this.#count++;
  }

  // Public method to increment and get the count
  increase() {
    this.#increment(); // Calling the private method internally
    return this.#count;
  }
}

const counter = new Counter();
console.log(counter.increase()); // Output: 1
console.log(counter.increase()); // Output: 2
// console.log(counter.#increment()); // SyntaxError: Private field '#increment' must be declared in an enclosing class
```
## 4. Can a public method inside the same class call a private instance method?

- Yes, public methods inside the same class can call private instance methods directly.

## 5. What are the benefits of using private instance methods in terms of encapsulation?

- They hide internal implementation details from external code.
- They prevent accidental or unauthorized access/modification.
- They allow the class to change internal logic without affecting its public API.

## 6. Can private instance methods be overridden by subclasses? Why or why not?

- No, private instance methods **cannot** be overridden by subclasses because they are only accessible within the class that defines them.
- They are not part of the subclass’s prototype chain and are truly private to the class.

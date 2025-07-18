## 1. Can you use computed property names in ES6 class definitions?

Yes, ES6 classes support computed property names for defining methods dynamically.

## 2. How do you define a method with a computed name inside a class?

You define a method with a computed name by enclosing the expression in square brackets `[]` within the class body.

## 3. Provide an example of using a computed method name in a class.

```js
const methodName = "sayHello";

class Greeter {
  [methodName]() {
    console.log("Hello!");
  }
}

const greeter = new Greeter();
greeter.sayHello(); // Outputs: Hello!
```
## 4. Can static methods in classes use computed names?

Yes, static methods in classes can also use computed property names by enclosing the method name expression in square brackets `[]`.

## 5. What are some use cases for computed properties in class design?

- Defining methods dynamically based on variables or constants.
- Creating APIs that adapt method names based on runtime data.
- Implementing patterns like proxies or decorators where method names depend on external input.
- Avoiding repetitive code when multiple similar methods need to be generated with slight variations.
## 6. Can you define getters/setters with computed property names in classes?

Yes, you can define getters and setters using computed property names by enclosing the property name expression in square brackets `[]` within the class body.

## 7. What limitations exist when using computed properties in class syntax?

- Computed property names must be valid expressions that evaluate to a string or symbol.
- You cannot use computed property names for class fields (public or private) — only for methods, getters, and setters.
- Static and instance methods can have computed names, but some older JavaScript engines may lack support.
- Computed property names cannot be used to define constructor or special methods like `static` blocks.

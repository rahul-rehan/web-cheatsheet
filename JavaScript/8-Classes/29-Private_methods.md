## 1. What is a private method in JavaScript?

A **private method** is a function defined inside a class that cannot be accessed or called from outside the class. It is intended to be used only internally by the class to encapsulate implementation details.

## 2. What syntax is used to declare a private method?

Private methods are declared using the `#` prefix before the method name inside a class:

```js
class MyClass {
  #privateMethod() {
    console.log('This is private');
  }
}
```
## 3. How do private methods differ from public methods?

- **Accessibility**:  
  Private methods can only be accessed within the class where they are declared, while public methods can be accessed from outside the class through instances.

- **Encapsulation**:  
  Private methods help encapsulate internal logic and hide it from external code, whereas public methods define the class’s interface and are meant to be used externally.

- **Syntax**:  
  Private methods are declared with a `#` prefix (e.g., `#myMethod()`), while public methods have no prefix and are accessible on the class instance.
## 4. Why are private methods useful in object-oriented design?

- They encapsulate internal implementation details, preventing external code from depending on or interfering with the internal logic.
- They help maintain a clear and clean public interface by hiding helper functions or sensitive operations.
- They improve code maintainability and reduce the risk of unintended side effects.

## 5. Can private methods be accessed outside the class definition?

No, private methods cannot be accessed from outside the class they are defined in.

## 6. What happens if you try to call a private method from outside the class?

A `SyntaxError` or `TypeError` is thrown, indicating that the private method is not accessible.

## 7. Are private methods enumerable or inherited?

- Private methods are **not enumerable**; they do not appear in property enumerations.
- Private methods are **not inherited** by subclasses. Each class has its own private methods.

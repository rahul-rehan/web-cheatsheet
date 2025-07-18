## 1. Can subclasses directly access private fields of their parent class?

No, subclasses cannot directly access the private fields (`#fieldName`) of their parent class. Private fields are strictly limited to the class where they are declared.


## 2. How do private fields differ from protected fields in other languages like Java or C++?

- **Private fields in JavaScript:** Accessible only within the declaring class, not by subclasses or external code.
- **Protected fields in languages like Java/C++:** Accessible within the declaring class and its subclasses, but not outside.

JavaScript currently does not have a native `protected` access modifier

## 3. What happens if a subclass tries to access a # private field from the parent?

Attempting to access a private field defined in the parent class from a subclass will result in a syntax error or runtime error, because private fields are not inherited or accessible outside their own class.

## 4. How should a parent class expose data to a subclass if private fields can’t be accessed directly?

The parent class should expose the necessary data to subclasses via:

- **Protected or public getter/setter methods**
- **Public or protected methods that internally access private fields**

This approach maintains encapsulation while allowing controlled access for subclasses.

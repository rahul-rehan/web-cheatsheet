## 1. What is prototypal inheritance in JavaScript?

- Prototypal inheritance is a mechanism where objects inherit properties and methods directly from other objects.
- Each object has an internal link to a prototype object, and property/method lookups follow this prototype chain.


## 2. How does JavaScript achieve inheritance without classical classes?

- JavaScript uses **prototypes** instead of classical classes.
- Objects inherit directly from other objects via their prototype links.
- Constructor functions combined with prototypes simulate class-like inheritance.
- ES6 introduced the `class` syntax as syntactic sugar over prototypal inheritance but the underlying mechanism remains prototype-based.

## 3. What is the difference between classical and prototypal inheritance?

| Classical Inheritance                    | Prototypal Inheritance                      |
|-----------------------------------------|---------------------------------------------|
| Based on classes and instances           | Based on objects and prototype chains       |
| Classes define blueprints for instances  | Objects inherit directly from other objects |
| Inheritance happens via class hierarchy  | Inheritance happens via prototype chains    |
| Common in languages like Java, C++       | JavaScript uses this model                    |
| Uses keywords like `class`, `extends`    | Uses `prototype` and `__proto__` internally |
## 4. How does the prototype chain work in JavaScript?

- Every JavaScript object has an internal link to another object called its **prototype**.
- When accessing a property or method, JavaScript first looks for it **directly on the object**.
- If the property is not found, the lookup continues up the **prototype chain**, checking the object's prototype, then that prototype's prototype, and so on until the property is found or the chain ends (`null`).

## 5. What happens when a property is not found directly on an object?

- JavaScript traverses the prototype chain, searching each prototype object in succession.
- If the property is found on a prototype, its value is returned.
- If the property is not found anywhere in the chain, `undefined` is returned.


## 6. How is shared behavior achieved in prototypal inheritance?

- Shared methods and properties are defined on an object's **prototype**.
- All objects inheriting from that prototype share these methods without each having their own copy.
- This promotes memory efficiency and code reuse by allowing many instances to share behavior.

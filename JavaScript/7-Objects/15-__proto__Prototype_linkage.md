## 1. What is the `__proto__` property in JavaScript?

- `__proto__` is a special property (now deprecated but widely supported) that points to the **prototype object** of the current object.
- It allows access to the object's internal prototype, enabling prototype chain traversal.

## 2. How is `__proto__` related to the internal prototype of an object?

- `__proto__` is the **exposed accessor** to the internal `[[Prototype]]` property of an object.
- The internal prototype (`[[Prototype]]`) is not directly accessible in JavaScript but can be accessed or modified via `__proto__`.

## 3. What is the difference between `__proto__` and `prototype`?

| `__proto__`                                         | `prototype`                                            |
|----------------------------------------------------|-------------------------------------------------------|
| A property of **all objects** that points to their prototype object (internal `[[Prototype]]`). | A property of **constructor functions** that points to the object used as the prototype for instances created by that constructor. |
| Used to access or set the prototype of an existing object. | Used to define properties and methods that instances will inherit. |
| Present on objects themselves.                      | Present on function objects (constructors).           |
## 4. How can you access or modify an object’s prototype?

- You can access an object's prototype using:
  - `Object.getPrototypeOf(obj)`
  - The deprecated `obj.__proto__` property (not recommended)

- You can modify an object's prototype using:
  - `Object.setPrototypeOf(obj, newProto)` (but use with caution due to performance impacts)
  - Creating an object with a specific prototype using `Object.create(proto)`

## 5. Why is using `__proto__` discouraged in modern JavaScript?

- `__proto__` is a **non-standard, deprecated** property (though widely supported for legacy reasons).
- It can lead to **performance issues** because modifying the prototype chain dynamically is costly.
- Its behavior may vary between environments.
- Using `__proto__` can make code harder to maintain and less predictable.

## 6. What are the standard alternatives to `__proto__`?

- Use `Object.getPrototypeOf(obj)` to **access** the prototype.
- Use `Object.setPrototypeOf(obj, proto)` to **set** or change the prototype (use sparingly).
- Use `Object.create(proto)` to **create a new object with a specified prototype**.

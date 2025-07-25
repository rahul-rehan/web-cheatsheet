## 1. What is the Reflect object in JavaScript?

The `Reflect` object is a built-in object that provides methods for interceptable JavaScript operations. It offers a set of static methods for performing low-level operations on objects, such as property access, assignment, function calls, and more. It is designed to complement Proxy by providing default implementations of these operations.

## 2. How does Reflect relate to Proxy?

`Reflect` is often used inside Proxy traps to perform the default behavior of the intercepted operation. When you define a Proxy trap, you can delegate the operation to `Reflect` to maintain the default functionality while adding custom behavior. This helps to avoid duplicating the logic and ensures consistent behavior.

## 3. Provide an example of using Reflect.get() inside a Proxy get trap.

```js
const target = { name: 'Alice', age: 25 };

const handler = {
  get(obj, prop, receiver) {
    console.log(`Property "${prop}" was accessed`);
    // Use Reflect.get to perform the default property access
    return Reflect.get(obj, prop, receiver);
  }
};

const proxy = new Proxy(target, handler);

console.log(proxy.name); // Logs: Property "name" was accessed
                         // Outputs: Alice
```
## 4. What is the benefit of using Reflect methods inside traps?

Using `Reflect` methods inside Proxy traps provides a clean, standardized way to perform the default behavior of the operation being intercepted. It helps avoid duplicating the logic for fundamental operations and ensures that traps can delegate to the original behavior easily. This leads to more maintainable and predictable code when customizing object behavior with Proxies.

## 5. Name at least 5 commonly used methods from the Reflect API.

1. `Reflect.get(target, propertyKey, receiver)` – Retrieves a property value.
2. `Reflect.set(target, propertyKey, value, receiver)` – Sets a property value.
3. `Reflect.has(target, propertyKey)` – Checks if a property exists.
4. `Reflect.deleteProperty(target, propertyKey)` – Deletes a property.
5. `Reflect.ownKeys(target)` – Returns an array of all property keys (string and symbol) of the target.

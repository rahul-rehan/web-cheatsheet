## 1. How can Proxies be used for data validation?

Proxies can intercept property writes using the `set` trap, allowing you to validate values before they are assigned.

- You can check the type, range, or format of values.
- If validation fails, you can throw an error or ignore the assignment.
- This enforces constraints without modifying the original object logic.

**Example:**
```js
const validator = {
  set(target, prop, value) {
    if (prop === 'age' && (typeof value !== 'number' || value < 0)) {
      throw new TypeError('Age must be a positive number');
    }
    target[prop] = value;
    return true;
  }
};

const person = new Proxy({}, validator);
person.age = 25; // works
person.age = -5; // throws error
```
## 2. How can Proxies be used for logging or debugging property access?

By using the `get` and `set` traps, Proxies can log every time a property is read or written.

- Useful for tracking how an object is used.
- Helps debug unexpected property accesses or mutations.
- Can log the property name, value, and operation type.

**Example:**
```js
const logger = {
  get(target, prop) {
    console.log(`Getting property "${prop}"`);
    return target[prop];
  },
  set(target, prop, value) {
    console.log(`Setting property "${prop}" to ${value}`);
    target[prop] = value;
    return true;
  }
};

const obj = new Proxy({}, logger);
obj.name = 'Alice'; // Logs: Setting property "name" to Alice
console.log(obj.name); // Logs: Getting property "name"
```
## 3. How can you create a read-only object using Proxy?

You can create a read-only object by using the `set` and `deleteProperty` traps to prevent modifications.

- The `set` trap blocks any attempts to change properties.
- The `deleteProperty` trap prevents properties from being deleted.
- Any modification attempts can throw an error or simply return false.

**Example:**

```js
const readOnlyHandler = {
  set(target, prop, value) {
    console.warn(`Cannot set property "${prop}" - object is read-only.`);
    return false; // Prevent assignment
  },
  deleteProperty(target, prop) {
    console.warn(`Cannot delete property "${prop}" - object is read-only.`);
    return false; // Prevent deletion
  }
};

const obj = { name: 'Alice', age: 30 };
const readOnlyObj = new Proxy(obj, readOnlyHandler);

readOnlyObj.name = 'Bob';    // Warning: Cannot set property "name" - object is read-only.
delete readOnlyObj.age;      // Warning: Cannot delete property "age" - object is read-only.

console.log(readOnlyObj.name); // Outputs: Alice
```
## 4. How can Proxies be used to implement default values for missing properties?

Proxies can intercept property access with the `get` trap and return a default value if the property does not exist on the target object.

**Example:**

```js
const defaultsHandler = {
  get(target, prop) {
    if (prop in target) {
      return target[prop];
    } else {
      return `Default value for "${prop}"`;
    }
  }
};

const obj = { name: 'Alice' };
const proxy = new Proxy(obj, defaultsHandler);

console.log(proxy.name);    // Outputs: Alice
console.log(proxy.age);     // Outputs: Default value for "age"
```
## 5. What are the limitations of using Proxy?

- **Performance Overhead:** Proxies add an extra layer of indirection, which can slow down property access and overall performance compared to direct object usage.

- **Debugging Difficulty:** Errors and stack traces involving proxies can be harder to interpret, making debugging more complex.

- **Limited Browser/Environment Support:** Older JavaScript engines or environments may not support Proxy objects.

- **Incomplete Interception:** Some operations cannot be fully trapped or intercepted by proxies, limiting their control over certain behaviors.

- **Compatibility Issues:** Certain built-in methods or libraries might not work correctly with proxied objects.

- **Security Concerns:** Improper use of proxies can expose sensitive data or create unexpected side effects.

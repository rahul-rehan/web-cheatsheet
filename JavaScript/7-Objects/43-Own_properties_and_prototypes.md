## 1. If you assign a property to an object instance, does it shadow the prototype property?

Yes, assigning a property directly to an object instance **shadows** any property with the same name from the prototype chain.  
The instance property takes precedence and hides the inherited property when accessed.

## 2. How can you check whether a property is shadowing an inherited one?

You can check if a property exists both on the instance (own property) and on its prototype:

```javascript
const obj = Object.create({ inheritedProp: 42 });
obj.inheritedProp = 100; // shadows prototype property

console.log(obj.hasOwnProperty('inheritedProp')); // true (own property)
console.log('inheritedProp' in Object.getPrototypeOf(obj)); // true (prototype property)
```
If the property is an own property and also exists on the prototype, the own property is shadowing the inherited one.
## 3. If you delete an own property, does it reveal a prototype property with the same name?

Yes. When you delete an own property from an object, if the prototype chain contains a property with the same name, that prototype property becomes accessible again.

#### Example:
```javascript
const proto = { prop: 42 };
const obj = Object.create(proto);

obj.prop = 100;  // Own property shadows prototype property
console.log(obj.prop); // 100

delete obj.prop; // Delete own property
console.log(obj.prop); // 42 (prototype property is now visible)
```
## 4. Can an own property be redefined to change its descriptor (e.g., to non-enumerable)?

Yes, an own property can be redefined using `Object.defineProperty()` to change its property descriptor attributes such as `enumerable`, `writable`, or `configurable`, **provided the property is configurable**.

#### Example:
```javascript
const obj = { prop: 1 };

Object.defineProperty(obj, 'prop', {
  enumerable: false
});

console.log(Object.keys(obj)); // [] since 'prop' is now non-enumerable
```
Note: If the property is non-configurable, attempting to redefine its descriptor will throw a `TypeError`.
## Best Practices
## 1. Why is it recommended to always use `hasOwnProperty.call(obj, prop)` in generic utility code?

- Using `hasOwnProperty.call(obj, prop)` ensures that the method is called from `Object.prototype` directly, avoiding issues if the object:
  - Does not inherit from `Object.prototype` (e.g., created with `Object.create(null)`).
  - Has a shadowed or overridden `hasOwnProperty` property.
- This approach guarantees **reliable and safe property ownership checks** across any object type.

## 2. What is the impact of using `for...in` without filtering for own properties?

- Using `for...in` without filtering includes **all enumerable properties**, including those inherited from the prototype chain.
- This can cause:
  - Processing unexpected or unintended inherited properties.
  - Bugs due to acting on prototype properties rather than the object's own data.
  - Security or logic issues if prototype properties are sensitive or unrelated.

## 3. How can misuse of own vs inherited property checks lead to bugs in object iteration or merging?

- Failing to distinguish between own and inherited properties can result in:
  - Overwriting inherited properties accidentally during merges.
  - Processing or copying properties from prototypes unintentionally.
  - Including properties that should be excluded, leading to incorrect logic or data corruption.
- Properly checking with `hasOwnProperty()` or similar safeguards is essential to ensure only intended properties are iterated or merged.

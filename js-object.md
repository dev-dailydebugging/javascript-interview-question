# The Complete Guide of Object in JS

## 1. What is an object in JavaScript?

An object is a collection of related data stored as **key–value pairs**. Keys (also called properties) are strings or symbols, and values can be anything: numbers, strings, arrays, functions, or other objects. Objects are used to represent real-world things like a user, a product, or a car.

## 2. How do you create an object in JavaScript?

The most common way is an **object literal**:

js

```jsx
const user = {  name: "Rahul",  age: 25};
```

Other ways:

js

```jsx
const obj1 = new Object();          // Object constructorconst obj2 = Object.create(null);   // Object.create()function User(name) { this.name = name; }const obj3 = new User("Rahul");     // constructor functionclass Person { constructor(name) { this.name = name; } }const obj4 = new Person("Rahul");   // class
```

## 3. What is the difference between dot notation and bracket notation?

Both are used to access properties.

js

```jsx
user.name;      // dot notationuser["name"];   // bracket notation
```

- **Dot notation**: short and readable, but the key must be a valid identifier written literally.
- **Bracket notation**: the key is written as a string or an expression, so it is more flexible.

## 4. When would you use bracket notation instead of dot notation?

Use bracket notation when:

1. The key is stored in a **variable**:

js

```jsx
   const key = "age";   user[key]; // 25
```

1. The key has **spaces or special characters**:

js

```jsx
   const obj = { "first name": "Rahul" };   obj["first name"];
```

1. The key starts with a **number**: `obj["1abc"]`
2. The key is **computed dynamically**: `obj["user_" + id]`

## 5. How do you add, update, and delete properties from an object?

js

```jsx
const user = { name: "Rahul" };user.age = 25;          // adduser["city"] = "Delhi"; // add (bracket)user.name = "Amit";     // update (same syntax as add)delete user.city;       // delete
```

If the property already exists, assignment updates it. If not, it adds it.

## 6. What is the difference between `Object.keys()`, `Object.values()`, and `Object.entries()`?

| Method | Returns |
| --- | --- |
| `Object.keys(obj)` | Array of keys |
| `Object.values(obj)` | Array of values |
| `Object.entries(obj)` | Array of `[key, value]` pairs |

js

```jsx
const user = { name: "Rahul", age: 25 };Object.keys(user);    // ["name", "age"]Object.values(user);  // ["Rahul", 25]Object.entries(user); // [["name", "Rahul"], ["age", 25]]
```

## 7. What is object destructuring?

Destructuring is a shortcut for pulling properties out of an object into separate variables.

js

```jsx
const user = { name: "Rahul", age: 25 };const { name, age } = user;console.log(name); // "Rahul"console.log(age);  // 25
```

You can also set defaults: `const { city = "Delhi" } = user;`

## 8. How can you rename a property while destructuring?

Use a colon: `originalName: newName`.

js

```jsx
const { name: userName, age: userAge } = user;console.log(userName); // "Rahul"
```

Here the variable is `userName`, not `name`.

## 9. What is the spread operator in objects?

The spread operator (`...`) copies the properties of one object into another. It is used to copy or merge objects.

js

```jsx
const copy = { ...user };const merged = { ...user, city: "Delhi" };   // copy + addconst updated = { ...user, age: 26 };        // copy + override
```

If the same key appears twice, the **later one wins**.

## 10. What is the difference between a reference and a copy of an object?

Objects are stored by **reference**. Assigning an object to another variable does not duplicate it; both variables point to the same object.

js

```jsx
const a = { name: "Rahul" };const b = a;          // reference, not a copyb.name = "Amit";console.log(a.name);  // "Amit" (a changed too)const c = { ...a };   // actual copyc.name = "Sam";console.log(a.name);  // "Amit" (unchanged)
```

## 11. What is a shallow copy? How is it different from a deep copy?

- **Shallow copy**: copies only the top level. Nested objects or arrays are still shared by reference.
- **Deep copy**: copies everything at every level, so nothing is shared.

js

```jsx
const user = { name: "Rahul", address: { city: "Delhi" } };const shallow = { ...user };shallow.address.city = "Mumbai";console.log(user.address.city); // "Mumbai" (shared nested object)const deep = structuredClone(user);deep.address.city = "Pune";console.log(user.address.city); // "Mumbai" (unaffected)
```

## 12. How does `structuredClone()` differ from the spread operator?

| Spread (`{ ...obj }`) | `structuredClone(obj)` |
| --- | --- |
| Shallow copy | Deep copy |
| Nested objects are shared | Nested objects are fully cloned |
| Keeps functions | Throws an error on functions |
| Works only for objects/arrays | Handles Date, Map, Set, and circular references |

Use spread for simple, flat objects. Use `structuredClone()` when you need a fully independent copy.

## 13. What is optional chaining (`?.`) and why is it useful?

Optional chaining safely accesses a nested property. If something along the way is `null` or `undefined`, it returns `undefined` instead of throwing an error.

js

```jsx
const user = { name: "Rahul" };user.address.city;    // TypeError: Cannot read properties of undefineduser.address?.city;   // undefined (no error)user.getName?.();     // safe method calluser.list?.[0];       // safe array access
```

It is especially useful with API data, where fields may be missing.

## 14. What is the difference between `??` and `||`?

- `||` returns the right side if the left is **falsy** (`0`, `""`, `false`, `null`, `undefined`, `NaN`).
- `??` returns the right side only if the left is **`null` or `undefined`**.

js

```jsx
0 || 10;        // 10   (0 is falsy)0 ?? 10;        // 0    (0 is a valid value)"" || "Guest";  // "Guest""" ?? "Guest";  // ""null ?? "Guest"; // "Guest"
```

Use `??` when `0`, `""`, or `false` are valid values you want to keep.

## 15. Why does this return `false`?

js

```jsx
const a = { name: "A" };const b = { name: "A" };console.log(a === b); // false
```

**Answer:** Objects are compared by **reference**, not by their contents. `a` and `b` are two separate objects stored at different memory locations, so `===` returns `false` even though they look identical. It would be `true` only if both variables pointed to the same object (e.g., `const b = a;`).

To compare contents, you need to check property by property, or use something like `JSON.stringify(a) === JSON.stringify(b)` for simple cases.

![1.png](The%20Complete%20Guide%20of%20Object%20in%20JS/1.png)

![2.png](The%20Complete%20Guide%20of%20Object%20in%20JS/2.png)

![3.png](The%20Complete%20Guide%20of%20Object%20in%20JS/3.png)

![4.png](The%20Complete%20Guide%20of%20Object%20in%20JS/4.png)

![5.png](The%20Complete%20Guide%20of%20Object%20in%20JS/5.png)

![6.png](The%20Complete%20Guide%20of%20Object%20in%20JS/6.png)

![7.png](The%20Complete%20Guide%20of%20Object%20in%20JS/7.png)

![8.png](The%20Complete%20Guide%20of%20Object%20in%20JS/8.png)

![9.png](The%20Complete%20Guide%20of%20Object%20in%20JS/9.png)

![10.png](The%20Complete%20Guide%20of%20Object%20in%20JS/10.png)

![11.png](The%20Complete%20Guide%20of%20Object%20in%20JS/11.png)

![12.png](The%20Complete%20Guide%20of%20Object%20in%20JS/12.png)

![13.png](The%20Complete%20Guide%20of%20Object%20in%20JS/13.png)

# **JavaScript   Object  — Intermediate Questions with Answers**

## 1. What is the difference between `Object.assign()` and the spread operator (`...`)?

Both copy properties from one object to another (shallowly), but they differ in how they work.

js

```jsx
const user = { name: "Rahul" };const a = Object.assign({}, user, { age: 25 });const b = { ...user, age: 25 };
```

| `Object.assign(target, ...sources)` | Spread `{ ...obj }` |
| --- | --- |
| **Mutates** the target object | Always creates a **new** object |
| Triggers **setters** on the target | Defines properties directly (no setters) |
| A function call | Syntax, shorter and more readable |

js

```jsx
Object.assign(user, { age: 25 }); // modifies user itself
```

Spread is preferred in modern code, especially in React, because it never mutates the original.

## 2. How does shallow copying work with nested objects?

A shallow copy duplicates only the **top-level** properties. If a property's value is an object or array, only its **reference** is copied, so the original and the copy share the same nested object.

js

```jsx
const user = { name: "Rahul", address: { city: "Delhi" } };const copy = { ...user };copy.name = "Amit";           // does not affect usercopy.address.city = "Mumbai"; // affects user tooconsole.log(user.address.city); // "Mumbai"
```

Primitives (strings, numbers, booleans) are copied by value, while nested objects are copied by reference.

## 3. How can you create a deep copy of an object in JavaScript?

**1. `structuredClone()` (recommended):**

js

```jsx
const deep = structuredClone(user);
```

Handles nested objects, arrays, `Date`, `Map`, `Set`, and circular references. It throws on functions.

**2. `JSON.parse(JSON.stringify(obj))`:**

js

```jsx
const deep = JSON.parse(JSON.stringify(user));
```

Quick, but it loses functions, `undefined`, and symbols, converts `Date` to a string, and fails on circular references.

**3. Manual or library approach:** `_.cloneDeep(obj)` from Lodash, or a recursive function.

## 4. What is the difference between `==` and `===` when comparing objects?

For objects, there is **no practical difference**. Both compare by **reference**, not by content.

js

```jsx
const a = { x: 1 };const b = { x: 1 };const c = a;a == b;   // falsea === b;  // falsea == c;   // truea === c;  // true
```

The difference between `==` and `===` only appears with primitives, where `==` does type coercion (`"5" == 5` is `true`, but `"5" === 5` is `false`).

## 5. How do you merge two objects, and what happens when both have the same property?

Use spread or `Object.assign()`:

js

```jsx
const a = { name: "Rahul", age: 25 };const b = { age: 30, city: "Delhi" };const merged = { ...a, ...b };// { name: "Rahul", age: 30, city: "Delhi" }
```

If both objects have the same key, the **later one overrides the earlier one**. Here `age` becomes `30`. Flip the order (`{ ...b, ...a }`) and `age` stays `25`.

Note that merging is shallow. If both have a nested object under the same key, the later one replaces the earlier one entirely and the two are not combined.

## 6. How do you update a nested object without mutating the original object?

Copy every level along the path you are changing using spread:

js

```jsx
const user = {  name: "Rahul",  address: { city: "Delhi", pin: "110001" }};const updated = {  ...user,  address: {    ...user.address,    city: "Mumbai"  }};console.log(user.address.city);    // "Delhi" (unchanged)console.log(updated.address.city); // "Mumbai"
```

This pattern is very common in React state updates, where mutating state directly can stop the UI from updating. For deeply nested data, you can use `structuredClone()` first and then modify the clone.

## 7. What is the difference between `Object.hasOwn()` and the `in` operator?

- `Object.hasOwn(obj, key)` returns `true` only if the property belongs **directly to the object**.
- `key in obj` returns `true` if the property exists **on the object or anywhere in its prototype chain**.

js

```jsx
const user = { name: "Rahul" };Object.hasOwn(user, "name");      // true"name" in user;                   // trueObject.hasOwn(user, "toString");  // false (inherited)"toString" in user;               // true
```

`Object.hasOwn()` is the modern, safer replacement for `obj.hasOwnProperty(key)`.

## 8. What is the difference between `for...in` and `Object.keys()`?

| `for...in` | `Object.keys(obj)` |
| --- | --- |
| A loop | Returns an **array** of keys |
| Includes **inherited** enumerable properties | Only the object's **own** enumerable properties |
| No array methods available | Works with `map`, `filter`, `forEach`, etc. |

js

```jsx
const parent = { role: "admin" };const user = Object.create(parent);user.name = "Rahul";for (const key in user) console.log(key); // "name", "role"Object.keys(user); // ["name"]
```

Prefer `Object.keys()` (or `Object.entries()`) to avoid accidentally picking up inherited properties.

## 9. How do optional chaining (`?.`) and nullish coalescing (`??`) work together?

Optional chaining safely reads a deep property and returns `undefined` if something is missing. Nullish coalescing then provides a **default value** when the result is `null` or `undefined`.

js

```jsx
const user = { profile: { age: 0 } };const city = user.address?.city ?? "Unknown";console.log(city); // "Unknown"const age = user.profile?.age ?? 18;console.log(age); // 0 (kept, because 0 is not null/undefined)
```

Using `||` instead of `??` here would wrongly replace `0` with `18`.

## 10. What are computed property names in JavaScript objects?

They let you use an **expression** as a property name by wrapping it in square brackets inside an object literal.

js

```jsx
const key = "age";const user = {  name: "Rahul",  [key]: 25,  ["user_"+1]: "first"};// { name: "Rahul", age: 25, user_1: "first" }
```

Common use: updating form state dynamically in React.

js

```jsx
setForm({ ...form, [e.target.name]: e.target.value });
```

## 11. What are getters and setters, and when would you use them?

They are special methods that look like normal properties. A **getter** runs when you read the property, and a **setter** runs when you assign to it.

js

```jsx
const user = {  firstName: "Rahul",  lastName: "Sharma",  get fullName() {    return `${this.firstName}${this.lastName}`;  },  set fullName(value) {    [this.firstName, this.lastName] = value.split(" ");  }};console.log(user.fullName);   // "Rahul Sharma"user.fullName = "Amit Verma"; // calls the setter
```

Use them for **computed values**, **validation** before setting a value, and **hiding internal logic** behind a simple property-like interface.

## 12. What is the difference between `Object.freeze()`, `Object.seal()`, and `Object.preventExtensions()`?

| Method | Add properties | Delete properties | Modify values |
| --- | --- | --- | --- |
| `preventExtensions()` | No | Yes | Yes |
| `seal()` | No | No | Yes |
| `freeze()` | No | No | No |

js

```jsx
const obj = Object.freeze({ name: "Rahul" });obj.name = "Amit"; // ignored (throws in strict mode)obj.age = 25;      // ignoreddelete obj.name;   // ignored
```

All three are **shallow**: nested objects inside a frozen object can still be changed unless they are frozen too. You can check with `Object.isFrozen()`, `Object.isSealed()`, and `Object.isExtensible()`.

## 13. What is a prototype chain, and how does property lookup work?

Every object has a hidden link to another object called its **prototype**. That prototype has its own prototype, and so on, until it reaches `null`. This sequence is the prototype chain.

When you access a property, JavaScript:

1. Looks for it on the object itself.
2. If not found, looks on its prototype.
3. Continues up the chain until found or until it reaches `null`, then returns `undefined`.

js

```jsx
const animal = { eats: true };const dog = Object.create(animal);dog.barks = true;dog.barks; // true (own property)dog.eats;  // true (found on animal, the prototype)dog.fly;   // undefined (not found anywhere in the chain)
```

This is also why `{}.toString()` works: it is inherited from `Object.prototype`.

## 14. What is the difference between `Object.create()` and creating an object using `{}`?

- `{}` creates an object whose prototype is `Object.prototype`.
- `Object.create(proto)` creates an object with the prototype **you choose**.

js

```jsx
const a = {};Object.getPrototypeOf(a) === Object.prototype; // trueconst animal = { eats: true };const dog = Object.create(animal);dog.eats; // true (inherited from animal)const pure = Object.create(null);pure.toString; // undefined (no prototype at all)
```

`Object.create(null)` is useful for creating a clean dictionary-like object with no inherited properties like `toString`.

## 15. How would you remove a property from an object without modifying the original object?

Use **destructuring with rest**, which creates a new object without that property:

js

```jsx
const user = { name: "Rahul", age: 25, city: "Delhi" };const { age, ...rest } = user;console.log(rest); // { name: "Rahul", city: "Delhi" }console.log(user); // unchanged
```

Alternatives:

js

```jsx
// Copy, then delete from the copyconst copy = { ...user };delete copy.age;// Filter entriesconst result = Object.fromEntries(  Object.entries(user).filter(([key]) => key !== "age"));
```

Avoid `delete user.age` directly, since it **mutates** the original object.

# **JavaScript   Object  — Advanced Questions with Answers**

## 1. What is the difference between `prototype`, `__proto__`, and `[[Prototype]]`?

- **`[[Prototype]]`** is the **internal slot** every object has. It points to the object's prototype (or `null`). You cannot access it directly in code; it is how the spec describes the link.
- **`__proto__`** is an **accessor property** (getter/setter on `Object.prototype`) that exposes `[[Prototype]]`. It is legacy; prefer `Object.getPrototypeOf()` and `Object.setPrototypeOf()`.
- **`prototype`** is a property that exists on **functions (constructors and classes)**. It is the object that becomes the `[[Prototype]]` of instances created with `new`.

js

```jsx
function User(name) { this.name = name; }User.prototype.greet = function () { return "Hi " + this.name; };const u = new User("Rahul");Object.getPrototypeOf(u) === User.prototype; // true  ([[Prototype]])u.__proto__ === User.prototype;              // true  (legacy accessor)User.prototype.constructor === User;         // true
```

**Rule of thumb:** `prototype` belongs to the constructor function. `__proto__` and `[[Prototype]]` belong to the instance.

## 2. How does the prototype chain work, and how does JavaScript resolve property lookups?

Every object links to a prototype, which links to its own prototype, until `null`. This is the prototype chain.

**Reads (`obj.key`):**

1. Check the object's own properties.
2. If not found, check `[[Prototype]]`, then its `[[Prototype]]`, and so on.
3. If the chain ends at `null`, return `undefined`.

js

```jsx
const animal = { eats: true };const dog = Object.create(animal);dog.barks = true;dog.barks; // own propertydog.eats;  // found on animaldog.fly;   // undefined
```

**Writes (`obj.key = value`):** normally create or update an **own** property, and do not change the prototype. Exceptions: if the inherited property is a **setter**, the setter runs, and if it is **non-writable**, the assignment fails (silently, or throws in strict mode).

The chain for arrays is: `arr → Array.prototype → Object.prototype → null`.

## 3. What are property descriptors? Explain `writable`, `enumerable`, and `configurable`.

Each property has metadata describing how it behaves. You can read it with `Object.getOwnPropertyDescriptor()` and set it with `Object.defineProperty()`.

js

```jsx
const user = { name: "Rahul" };Object.getOwnPropertyDescriptor(user, "name");// { value: "Rahul", writable: true, enumerable: true, configurable: true }
```

| Attribute | Meaning |
| --- | --- |
| `writable` | Can the value be changed? |
| `enumerable` | Does it show up in `for...in`, `Object.keys()`, and spread? |
| `configurable` | Can it be deleted, or have its descriptor changed? |

js

```jsx
const obj = {};Object.defineProperty(obj, "id", {  value: 1,  writable: false,  enumerable: false,  configurable: false});obj.id = 2;          // ignored (throws in strict mode)delete obj.id;       // failsObject.keys(obj);    // []
```

Accessor properties use `get` and `set` instead of `value` and `writable`. Properties created with `defineProperty` default all flags to `false`, while normal assignments default them to `true`.

## 4. What is the difference between `Object.getOwnPropertyNames()`, `Object.keys()`, and `Reflect.ownKeys()`?

| Method | String keys | Non-enumerable | Symbol keys |
| --- | --- | --- | --- |
| `Object.keys()` | Yes | No | No |
| `Object.getOwnPropertyNames()` | Yes | Yes | No |
| `Reflect.ownKeys()` | Yes | Yes | Yes |

js

```jsx
const sym = Symbol("s");const obj = { a: 1, [sym]: 2 };Object.defineProperty(obj, "hidden", { value: 3, enumerable: false });Object.keys(obj);                  // ["a"]Object.getOwnPropertyNames(obj);   // ["a", "hidden"]Reflect.ownKeys(obj);              // ["a", "hidden", Symbol(s)]
```

All three look only at **own** properties, never inherited ones.

## 5. How do getters and setters work internally, and what are their potential drawbacks?

They are **accessor properties**. Instead of storing a value, the property stores a `get` function and/or a `set` function. When you read the property, the engine calls the getter. When you assign to it, the engine calls the setter with the assigned value.

js

```jsx
const user = {  _age: 25,  get age() { return this._age; },  set age(v) {    if (v < 0) throw new Error("Invalid age");    this._age = v;  }};
```

**Drawbacks:**

- Look like plain properties but run code, so they can hide expensive work or side effects.
- A getter with no setter silently ignores assignments (throws in strict mode).
- Backing fields like `_age` are still publicly accessible unless you use private fields (`#age`).
- Not copied as accessors by spread or `Object.assign()`; the getter's **result** is copied as a plain value.
- Not included in `JSON.stringify` if defined on the prototype, and they can make debugging harder.
- Infinite recursion if you use the same name inside the getter (`return this.age`).

## 6. What is the difference between an own property and an inherited property?

- An **own property** is stored directly on the object.
- An **inherited property** is found via the prototype chain.

js

```jsx
const parent = { role: "admin" };const user = Object.create(parent);user.name = "Rahul";Object.hasOwn(user, "name"); // true  (own)Object.hasOwn(user, "role"); // false (inherited)"role" in user;              // true  (own or inherited)
```

`Object.keys()`, `Object.entries()`, spread, and `JSON.stringify()` use **own enumerable** properties only. `for...in` also includes inherited enumerable ones.

## 7. How does `Object.create(null)` differ from `{}`?

`{}` inherits from `Object.prototype`, so it has `toString`, `hasOwnProperty`, `__proto__`, and so on. `Object.create(null)` has **no prototype at all**.

js

```jsx
const a = {};const b = Object.create(null);"toString" in a; // true"toString" in b; // falseObject.getPrototypeOf(b); // null
```

**Why it matters:**

- It is a clean dictionary, so keys like `"constructor"` or `"toString"` cannot collide with inherited ones.
- It helps avoid prototype pollution.
- Downsides: it has no `toString`, so `${b}` throws a `TypeError`, and `b.hasOwnProperty` does not exist (use `Object.hasOwn(b, key)`).

## 8. How does `Object.freeze()` behave with nested objects, and how can you achieve deep immutability?

`Object.freeze()` is **shallow**. It locks only the top-level properties; nested objects remain mutable.

js

```jsx
const user = Object.freeze({ name: "Rahul", address: { city: "Delhi" } });user.name = "Amit";          // ignoreduser.address.city = "Pune";  // works!
```

**Deep freeze:**

js

```jsx
function deepFreeze(obj) {  Reflect.ownKeys(obj).forEach((key) => {    const value = obj[key];    if (value && typeof value === "object" && !Object.isFrozen(value)) {      deepFreeze(value);    }  });  return Object.freeze(obj);}
```

Other options: immutable libraries like **Immer** or **Immutable.js**, or the immutable-update pattern (always create new objects with spread). Note that frozen `Map` and `Set` can still be changed through their methods, because freezing does not affect internal slots.

## 9. What are `Proxy` and `Reflect` in JavaScript, and how can they be used to intercept object operations?

A **Proxy** wraps an object and lets you intercept operations through **traps** such as `get`, `set`, `has`, `deleteProperty`, `ownKeys`, and `apply`. **Reflect** provides the default behavior of those operations as functions, so a trap can forward to it.

js

```jsx
const target = { name: "Rahul", age: 25 };const proxy = new Proxy(target, {  get(obj, key, receiver) {    console.log(`Reading${String(key)}`);    return Reflect.get(obj, key, receiver);  },  set(obj, key, value, receiver) {    if (key === "age" && typeof value !== "number") {      throw new TypeError("Age must be a number");    }    return Reflect.set(obj, key, value, receiver);  }});proxy.name;       // logs "Reading name"proxy.age = "x";  // throws TypeError
```

**Use cases:** validation, logging, default values, read-only views, reactivity systems (Vue 3 uses Proxy), and API wrappers. **Caveats:** a Proxy adds overhead, and it does not make private fields (`#x`) or internal slots work transparently.

## 10. How does property enumeration order work in JavaScript objects?

For own properties, the order is defined as:

1. **Integer-like keys** (array indices) in **ascending numeric order**.
2. **String keys** in **insertion order**.
3. **Symbol keys** in insertion order (only visible to symbol-aware methods).

js

```jsx
const obj = { b: 1, 2: "x", a: 2, 1: "y" };Object.keys(obj); // ["1", "2", "b", "a"]
```

This order is guaranteed by `Object.keys`, `Object.entries`, `Reflect.ownKeys`, and `JSON.stringify`. `for...in` is also ordered in modern engines, but it includes inherited keys after the own ones. Do not rely on object order for numeric keys when insertion order matters; use a `Map`.

## 11. What are `Symbol` properties, and how do they behave with object enumeration methods?

A `Symbol` is a unique, immutable primitive often used as a collision-free property key.

js

```jsx
const id = Symbol("id");const user = { name: "Rahul", [id]: 101 };
```

| Method | Includes symbols? |
| --- | --- |
| `Object.keys()`, `Object.values()`, `Object.entries()` | No |
| `for...in` | No |
| `JSON.stringify()` | No |
| `Object.getOwnPropertyNames()` | No |
| `Object.getOwnPropertySymbols()` | Only symbols |
| `Reflect.ownKeys()` | Yes |
| Spread `{ ...obj }` and `Object.assign()` | **Yes** (own enumerable symbols are copied) |

Symbols give "semi-hidden" properties, not true privacy. Well-known symbols like `Symbol.iterator` and `Symbol.toPrimitive` let you customize built-in behavior.

## 12. How does `structuredClone()` handle circular references, and what types of values can it not clone?

It handles **circular references correctly**, because it tracks objects it has already cloned.

js

```jsx
const a = { name: "A" };a.self = a;const copy = structuredClone(a);copy.self === copy; // truecopy !== a;         // true
```

**Supported:** primitives, plain objects, arrays, `Date`, `RegExp`, `Map`, `Set`, `ArrayBuffer`, typed arrays, `Error`, `Blob`, and more.

**Cannot clone (throws `DataCloneError`):**

- Functions
- DOM nodes
- Symbols as values

**Things that are lost or changed:**

- Class instances become plain objects (the prototype is not preserved).
- Getters and setters are evaluated and copied as plain values.
- Symbol keys, non-enumerable properties, and property descriptors are not copied.

## 13. What are the differences between `Map` and `Object` regarding key types, iteration, and performance?

| Feature | Object | Map |
| --- | --- | --- |
| Key types | Strings and symbols | **Any value** (objects, functions, numbers) |
| Order | Integer keys first, then insertion order | Strict **insertion order** |
| Size | Manual (`Object.keys(o).length`) | `map.size` |
| Iteration | Needs `Object.keys/entries` | Directly iterable (`for...of`) |
| Inherited keys | Possible collisions (`toString`) | None |
| Serialization | `JSON.stringify` works | Needs conversion |
| Performance | Fine for small, fixed shapes | Better for **frequent additions and deletions** |

js

```jsx
const map = new Map();const key = { id: 1 };map.set(key, "value");map.get(key);    // "value"map.size;        // 1
```

Use **Object** for structured records with known fields and JSON data. Use **Map** for dynamic key-value collections, non-string keys, and frequent updates.

## 14. How would you implement a deep equality check for two complex objects, including arrays and nested objects?

js

```jsx
function deepEqual(a, b, seen = new WeakMap()) {  if (Object.is(a, b)) return true;  if (typeof a !== "object" || typeof b !== "object" || a === null || b === null) {    return false;  }  if (Object.getPrototypeOf(a) !== Object.getPrototypeOf(b)) return false;// Handle circular references  if (seen.get(a) === b) return true;  seen.set(a, b);  if (a instanceof Date) return a.getTime() === b.getTime();  if (a instanceof RegExp) return a.toString() === b.toString();  if (a instanceof Map) {    if (a.size !== b.size) return false;    for (const [k, v] of a) {      if (!b.has(k) || !deepEqual(v, b.get(k), seen)) return false;    }    return true;  }  if (a instanceof Set) {    if (a.size !== b.size) return false;    for (const v of a) if (!b.has(v)) return false;    return true;  }  const keysA = Reflect.ownKeys(a);  const keysB = Reflect.ownKeys(b);  if (keysA.length !== keysB.length) return false;  return keysA.every(    (key) => Object.hasOwn(b, key) && deepEqual(a[key], b[key], seen)  );}deepEqual({ a: [1, { b: 2 }] }, { a: [1, { b: 2 }] }); // true
```

Key points: use `Object.is` for `NaN` handling, compare prototypes, handle special types, and track visited pairs to avoid infinite loops. In production, prefer a tested library like Lodash's `_.isEqual`.

## 15. How would you safely merge deeply nested objects while handling arrays, `undefined` values, and potentially unsafe property keys?

The main concerns are:

- **Prototype pollution:** keys like `__proto__`, `constructor`, and `prototype` must be blocked.
- **Arrays:** decide on a strategy (replace, concatenate, or merge by index).
- **`undefined`:** decide whether it overrides or is skipped.
- **Mutation:** do not modify the inputs.

js

```jsx
const UNSAFE_KEYS = new Set(["__proto__", "constructor", "prototype"]);const isPlainObject = (v) =>  v !== null &&  typeof v === "object" &&  [Object.prototype, null].includes(Object.getPrototypeOf(v));function safeMerge(target, source) {  const result = Array.isArray(target) ? [...target] : { ...target };  for (const key of Object.keys(source)) {    if (UNSAFE_KEYS.has(key)) continue;           // block pollution    const srcVal = source[key];    const tgtVal = result[key];    if (srcVal === undefined) continue;           // skip undefined    if (Array.isArray(srcVal)) {      result[key] = [...srcVal];                  // arrays: replace    } else if (isPlainObject(srcVal) && isPlainObject(tgtVal)) {      result[key] = safeMerge(tgtVal, srcVal);    // recurse    } else if (isPlainObject(srcVal)) {      result[key] = safeMerge({}, srcVal);        // clone, don't share refs    } else {      result[key] = srcVal;    }  }  return result;}const a = { user: { name: "Rahul", tags: ["a"] } };const b = { user: { age: 25, tags: ["b"], name: undefined }, __proto__: { hacked: true } };safeMerge(a, b);// { user: { name: "Rahul", tags: ["b"], age: 25 } }
```

Extra hardening: use `Object.create(null)` for results, use `Object.hasOwn` to check keys, and add a depth limit for untrusted input. For production code, use a maintained library (such as `deepmerge`) and keep it updated, since many real CVEs came from naive merge functions.

# 🚀 **Follow @daily.debugging for complete frontend resources and interview preparation.**
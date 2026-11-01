# The Complete Guide of this Keywords

## 1. What is the `this` keyword in JavaScript?

`this` is a special keyword that refers to the **object that is currently executing the code**, often called the "context." Its value is not fixed when you write the function. It depends on **how the function is called**.

js

```jsx
const user = {  name: "Aman",  greet() {    console.log(this.name);  }};user.greet(); // "Aman" (this = user)
```

## 2. How is the value of `this` determined in JavaScript?

It is decided at **call time** (except for arrow functions), by the following rules in order of priority:

1. **`new` binding:** `new Fn()` makes `this` the newly created object.
2. **Explicit binding:** `call()`, `apply()`, or `bind()` set `this` manually.
3. **Implicit binding:** `obj.method()` makes `this` the object before the dot.
4. **Default binding:** a plain call `fn()` makes `this` the global object (non-strict) or `undefined` (strict).
5. **Arrow functions:** have no rules of their own; they use `this` from the surrounding scope.

## 3. What does `this` refer to inside an object method?

It refers to the **object that called the method**, meaning whatever is to the left of the dot at call time.

js

```jsx
const car = {  brand: "Tata",  show() {    console.log(this.brand);  }};car.show(); // "Tata" (this = car)
```

## 4. What does `this` refer to inside a regular function in non-strict mode?

It refers to the **global object**: `window` in browsers, and `globalThis` in Node.js.

js

```jsx
function show() {  console.log(this);}show(); // window (browser, non-strict)
```

## 5. What does `this` refer to inside a regular function in strict mode?

It is **`undefined`**. Strict mode prevents `this` from defaulting to the global object.

js

```jsx
"use strict";function show() {  console.log(this);}show(); // undefined
```

## 6. How does `this` behave differently in regular functions and arrow functions?

| Regular function | Arrow function |
| --- | --- |
| `this` depends on **how it is called** | `this` depends on **where it is written** |
| Gets a new `this` on every call | Uses `this` from the surrounding scope |
| `call`, `apply`, `bind` can change `this` | They cannot change `this` |
| Can be used with `new` | Cannot be used with `new` |

js

```jsx
const user = {  name: "Aman",  regular() {    setTimeout(function () {      console.log(this.name); // undefined (this is not user)    }, 100);  },  arrow() {    setTimeout(() => {      console.log(this.name); // "Aman" (this inherited from arrow())    }, 100);  }};
```

## 7. Do arrow functions have their own `this`? Why or why not?

**No.** Arrow functions do not create their own `this` binding. They capture `this` from the **enclosing lexical scope** at the time they are defined, similar to how they capture any other outer variable.

**Why:** they were designed to solve the problem of losing `this` in callbacks (like `setTimeout` or `map`), so you no longer need `const self = this` or `.bind(this)`.

Because of this, arrow functions are a poor choice for **object methods** and **constructors**, where you want `this` to point to the object.

## 8. What happens to `this` when you assign an object method to another variable and call it?

The method **loses its context**. A standalone call has no object before the dot, so default binding applies: `this` becomes the global object (non-strict) or `undefined` (strict).

js

```jsx
const user = {  name: "Aman",  greet() {    console.log(this.name);  }};const fn = user.greet;fn(); // this is no longer user
```

**Fixes:**

js

```jsx
const fn1 = user.greet.bind(user);fn1(); // "Aman"const fn2 = () => user.greet();fn2(); // "Aman"
```

This is a common bug when passing methods as callbacks, for example `button.addEventListener("click", user.greet)`.

## 9. What is the difference between `call()`, `apply()`, and `bind()`?

All three set `this` explicitly.

| Method | Runs immediately? | Arguments | Returns |
| --- | --- | --- | --- |
| `call(thisArg, a, b)` | Yes | Passed **individually** | Function's result |
| `apply(thisArg, [a, b])` | Yes | Passed as an **array** | Function's result |
| `bind(thisArg, a, b)` | **No** | Passed individually (can be partial) | A **new function** |

js

```jsx
function intro(city, country) {  console.log(`${this.name} from${city},${country}`);}const user = { name: "Aman" };intro.call(user, "Delhi", "India");intro.apply(user, ["Delhi", "India"]);const bound = intro.bind(user, "Delhi");bound("India");
```

## 10. Does `bind()` execute a function immediately?

**No.** `bind()` returns a **new function** with `this` permanently set. You must call that new function yourself.

js

```jsx
function greet() {  console.log(this.name);}const user = { name: "Aman" };const bound = greet.bind(user); // nothing printed yetbound();                        // "Aman"
```

Once bound, the `this` value cannot be changed by another `bind`, `call`, or `apply`.

## 11. What is the output of this code?

js

```jsx
const user = {  name: "Aman",  greet() {    console.log(this.name);  },};user.greet();
```

**Output:** `Aman`

**Reason:** `greet()` is called as `user.greet()`, so `this` refers to `user`.

## 12. What is the output of this code?

js

```jsx
"use strict";function show() {  console.log(this);}show();
```

**Output:** `undefined`

**Reason:** `show()` is a plain function call, with no object before the dot. In strict mode, default binding does not fall back to the global object, so `this` is `undefined`.

## 13. What is the output of this code?

js

```jsx
const user = {  name: "Aman",  greet: () => {    console.log(this.name);  },};user.greet();
```

**Output:** not `"Aman"`. It prints `undefined` in most setups. In a browser script it prints an empty string (`""`), because `this` is `window` and `window.name` is an empty string by default.

**Reason:** the arrow function does not get `this` from `user`. An object literal does not create a scope, so the arrow function takes `this` from the surrounding scope, which here is the top level (global in a browser, or `module.exports` in Node, where `name` does not exist).

**Fix:** use a regular method.

js

```jsx
greet() {  console.log(this.name); // "Aman"}
```

## 14. What is the output of this code?

js

```jsx
const user = {  name: "Aman",  greet() {    console.log(this.name);  },};const greetFn = user.greet;greetFn();
```

**Output:** not `"Aman"`. In a browser (non-strict) it prints an empty string (`""`) because `this` is `window`. In Node.js it prints `undefined`.

**Reason:** `greetFn` is called as a plain function, so the link to `user` is lost and default binding applies. In strict mode or inside a class, `this` would be `undefined`, and `this.name` would throw a `TypeError`.

**Fix:** `const greetFn = user.greet.bind(user);`

## 15. What is the output of this code?

js

```jsx
function greet() {  console.log(this.name);}const user = { name: "Aman" };greet.call(user);
```

**Output:** `Aman`

**Reason:** `call(user)` explicitly sets `this` to `user` and runs `greet()` immediately, so `this.name` is `"Aman"`.

![1.png](The%20Complete%20Guide%20of%20this%20Keywords/1.png)

![2.png](The%20Complete%20Guide%20of%20this%20Keywords/2.png)

![3.png](The%20Complete%20Guide%20of%20this%20Keywords/3.png)

![4.png](The%20Complete%20Guide%20of%20this%20Keywords/4.png)

![5.png](The%20Complete%20Guide%20of%20this%20Keywords/5.png)

![6.png](The%20Complete%20Guide%20of%20this%20Keywords/6.png)

![7.png](The%20Complete%20Guide%20of%20this%20Keywords/7.png)

![8.png](The%20Complete%20Guide%20of%20this%20Keywords/8.png)

![9.png](The%20Complete%20Guide%20of%20this%20Keywords/9.png)

![10.png](The%20Complete%20Guide%20of%20this%20Keywords/10.png)

![11.png](The%20Complete%20Guide%20of%20this%20Keywords/11.png)

![12.png](The%20Complete%20Guide%20of%20this%20Keywords/12.png)

![13.png](The%20Complete%20Guide%20of%20this%20Keywords/13.png)

# **JavaScript this Keywords  — Intermediate Questions with Answers**

## 1. What happens to `this` when you extract a method from an object and call it separately?

The method **loses its context**. A standalone call has no object before the dot, so default binding applies: `this` becomes the global object (non-strict) or `undefined` (strict).

js

```jsx
const user = {  name: "Aman",  greet() {    console.log(this.name);  }};const fn = user.greet;fn(); // this is no longer user
```

**Fix:** `user.greet.bind(user)` or wrap it: `() => user.greet()`.

## 2. Why does `this` behave differently inside an arrow function nested within an object method?

Arrow functions have no `this` of their own. They use the `this` of the **enclosing function**, which here is the method. Since the method was called as `user.greet()`, its `this` is `user`, and the nested arrow function inherits it.

js

```jsx
const user = {  name: "Aman",  greet() {    const inner = () => console.log(this.name);    inner(); // "Aman"  }};user.greet();
```

If `inner` were a regular function, it would be a plain call and `this` would be lost.

## 3. How does `this` behave when a regular function is passed as a callback to `setTimeout()`?

The callback is called by the timer, not as `obj.method()`, so `this` is the **global object** in non-strict mode. In browsers, `setTimeout` calls the function with `this` as `window`, and in strict mode `this` is `undefined` (in Node.js it is the `Timeout` object, which is a quirk worth knowing).

js

```jsx
const user = {  name: "Aman",  greet() {    console.log(this.name);  }};setTimeout(user.greet, 100);                 // context lostsetTimeout(user.greet.bind(user), 100);      // "Aman"setTimeout(() => user.greet(), 100);         // "Aman"
```

## 4. What is the difference between implicit binding, explicit binding, and default binding?

| Binding | How `this` is set | Example |
| --- | --- | --- |
| **Implicit** | The object before the dot at call time | `user.greet()` → `this = user` |
| **Explicit** | Manually set with `call`, `apply`, or `bind` | `greet.call(user)` |
| **Default** | No object, plain call | `greet()` → global object (non-strict) or `undefined` (strict) |

Priority order: `new` binding > explicit > implicit > default. Arrow functions ignore all of these and use lexical `this`.

## 5. Can you change the value of `this` inside an arrow function using `call()`, `apply()`, or `bind()`? Why?

**No.** An arrow function does not have its own `this`, so there is nothing for these methods to change. `call` and `apply` pass the `this` argument, but the arrow function ignores it. `bind` still returns a new function, but its `this` stays the same as the lexical one.

js

```jsx
const arrow = () => console.log(this === globalThis);const user = { name: "Aman" };arrow.call(user); // still uses the outer `this`, not user
```

Any other arguments you pass (for example in `call(user, a, b)`) still work. Only the `this` part is ignored.

## 6. How does `this` behave inside a constructor function when called with the `new` keyword?

`new` does four things:

1. Creates a new empty object.
2. Links its prototype to `Constructor.prototype`.
3. Calls the function with `this` set to that new object.
4. Returns the new object (unless the function explicitly returns another **object**).

js

```jsx
function User(name) {  this.name = name; // this = the new object}const u = new User("Aman");console.log(u.name); // "Aman"
```

If you forget `new`, `this` is the global object (non-strict) or `undefined` (strict, which throws an error).

## 7. What happens if you use `new` with a function that has been created using `bind()`?

`new` **overrides** the `this` that `bind()` set. The bound function's `this` is ignored, and a fresh object is created as usual. Any **pre-filled arguments** from `bind` are still applied.

js

```jsx
function User(name, age) {  this.name = name;  this.age = age;}const BoundUser = User.bind({ name: "Default" }, "Aman");const u = new BoundUser(25);console.log(u.name); // "Aman"console.log(u.age);  // 25
```

Also, `u instanceof User` is `true`.

## 8. How does `this` behave in JavaScript class methods when the method is detached from its instance?

Class bodies always run in **strict mode**, so a detached method gets `this` as **`undefined`** (not the global object). Accessing a property on it throws a `TypeError`.

js

```jsx
class User {  constructor(name) {    this.name = name;  }  greet() {    console.log(this.name);  }}const u = new User("Aman");const fn = u.greet;fn(); // TypeError: Cannot read properties of undefined (reading 'name')
```

**Fixes:**

js

```jsx
// 1. Bind in the constructorthis.greet = this.greet.bind(this);// 2. Class field with an arrow functiongreet = () => console.log(this.name);
```

This is a very common issue with React class component event handlers.

## 9. What is the output?

js

```jsx
const anotherUser = { name: "Riya" };anotherUser.greet = user.greet;anotherUser.greet();
```

**Output:** `Riya`

**Reason:** `this` depends on the call site, not on where the method was defined. The call is `anotherUser.greet()`, so `this` is `anotherUser`.

## 10. What is the output?

js

```jsx
const user = {  name: "Aman",  greet() {    const inner = () => console.log(this.name);    inner();  },};user.greet();
```

**Output:** `Aman`

**Reason:** `inner` is an arrow function, so it uses `this` from `greet()`. Since `greet` was called as `user.greet()`, `this` is `user`.

## 11. What is the output?

js

```jsx
const fn = user.greet.bind({ name: "Riya" });fn.call({ name: "Rahul" });
```

**Output:** `Riya`

**Reason:** `bind()` permanently fixes `this`. A later `call()` (or `apply()` or another `bind()`) cannot override it, so `this.name` stays `"Riya"`.

## 12. What is the output?

js

```jsx
function User(name) {  this.name = name;}const BoundUser = User.bind({ name: "Default" });const user = new BoundUser("Aman");console.log(user.name);
```

**Output:** `Aman`

**Reason:** `new` takes priority over `bind()`. The bound `this` (`{ name: "Default" }`) is ignored, a new object is created, and the constructor sets `name` to `"Aman"` on it.

## 13. What is the output?

js

```jsx
const user = {  name: "Aman",  greet() {    return function () {      console.log(this.name);    };  },};user.greet()();
```

**Output:** not `"Aman"`. In a browser (non-strict) it prints an empty string (`""`) because `this` is `window`. In Node.js it prints `undefined`.

**Reason:** `user.greet()` returns a regular function, which is then called as `()` with no object before it. That is a plain call, so default binding applies. The inner function does not inherit `this` from `greet`.

**Fix:** return an arrow function instead: `return () => console.log(this.name);` (this prints `Aman`).

## 14. What is the output?

js

```jsx
"use strict";const user = {  name: "Aman",  greet() {    function inner() {      console.log(this);    }    inner();  },};user.greet();
```

**Output:** `undefined`

**Reason:** `inner()` is a plain function call, and in strict mode default binding gives `undefined`. It does not matter that it is defined inside a method, because regular functions get `this` from how they are called, not where they are written.

## 15. What is the output?

js

```jsx
const wrapper = user.greet;wrapper.apply({ name: "Riya" });
```

**Output:** `Riya`

**Reason:** `apply()` explicitly sets `this` to `{ name: "Riya" }` and runs the function immediately, so `this.name` is `"Riya"`. It does not matter that the function was originally defined on `user`.

# **JavaScript this Keywords  — Advanced Questions with Answers**

## 1. How does JavaScript determine the value of `this` when a function is invoked? Explain default, implicit, explicit, and constructor binding, including their precedence.

For a regular function, `this` is decided **at call time** by looking at how the function was called.

| Binding | When it applies | `this` value |
| --- | --- | --- |
| **Default** | Plain call: `fn()` | Global object (non-strict) or `undefined` (strict) |
| **Implicit** | Called on an object: `obj.fn()` | `obj` (the object before the dot) |
| **Explicit** | `fn.call(x)`, `fn.apply(x)`, `fn.bind(x)()` | `x` |
| **Constructor** | `new fn()` | The newly created object |

**Precedence (highest to lowest):**

1. `new` binding
2. Explicit binding (`bind` / `call` / `apply`)
3. Implicit binding
4. Default binding

js

```jsx
function Show() { console.log(this.name); }const obj = { name: "obj", Show };const other = { name: "other" };obj.Show();                       // "obj"   (implicit)obj.Show.call(other);             // "other" (explicit beats implicit)const bound = obj.Show.bind(other);new bound();                      // undefined (new beats bind; new object has no name)
```

**Arrow functions** sit outside this system. They have no `this` of their own and use the one from the surrounding scope.

## 2. What happens when `call()`, `apply()`, and `bind()` are used on an arrow function? Why?

The `this` argument is **ignored**. An arrow function has no `this` binding of its own, so there is nothing to override. It always uses the `this` captured from where it was defined.

js

```jsx
const user = { name: "Aman" };function outer() {  const arrow = () => this.name;  return [arrow.call(user), arrow.apply(user), arrow.bind(user)()];}outer.call({ name: "Riya" }); // ["Riya", "Riya", "Riya"]
```

Details:

- `call` and `apply` run the function, but the first argument is discarded. Remaining arguments are still passed normally.
- `bind` returns a new function, but its `this` is unchanged. Partial arguments still work.
- Arrow functions also cannot be used with `new`.

## 3. How does `this` behave in inherited methods? If a child object calls a method inherited from its prototype, which object does `this` refer to?

`this` refers to the **object the method was called on** (the receiver), not the object where the method is defined. A method found through the prototype chain still gets `this` = the child.

js

```jsx
const parent = {  greet() {    console.log(this.name);  }};const child = Object.create(parent);child.name = "Riya";child.greet(); // "Riya" (this = child, not parent)
```

An important side effect: assignments inside an inherited method create the property on the **child** (an own property), and do not modify the prototype.

js

```jsx
const parent = { count: 0, inc() { this.count++; } };const child = Object.create(parent);child.inc();console.log(child.count);  // 1 (own property created on child)console.log(parent.count); // 0
```

## 4. What happens to `this` when a class method is passed as a callback? How can you preserve the correct context?

The method is detached from its instance, so the call becomes a plain call. Class bodies are strict mode, so `this` is `undefined`, and accessing a property throws a `TypeError`.

js

```jsx
class Counter {  count = 0;  inc() { this.count++; }}const c = new Counter();setTimeout(c.inc, 100); // TypeError (this is undefined)
```

**Ways to preserve context:**

js

```jsx
// 1. Bind at the call sitesetTimeout(c.inc.bind(c), 100);// 2. Wrap in an arrow functionsetTimeout(() => c.inc(), 100);// 3. Bind once in the constructorconstructor() { this.inc = this.inc.bind(this); }// 4. Arrow function as a class fieldinc = () => { this.count++; };
```

Option 4 is the most convenient, but it creates a separate function **per instance** instead of sharing one on the prototype. It also cannot be overridden via `super.inc()` in subclasses.

## 5. How does `this` behave differently in getters, setters, and regular methods?

The rule is the same: `this` is the object the property is **accessed on** (the receiver). The difference is in how they are triggered.

- **Regular method:** invoked explicitly with `obj.method()`. Detaching it loses `this`.
- **Getter/setter:** invoked implicitly on property read/write (`obj.prop` or `obj.prop = v`). There is no call syntax, so you cannot detach them accidentally in the same way. `this` is the object being read or written, even if the accessor is inherited.

js

```jsx
const base = {  get label() { return `Name:${this.name}`; },  set label(v) { this.name = v; }};const user = Object.create(base);user.label = "Aman"; // setter: this = user, creates user.nameuser.label;          // getter: this = user → "Name: Aman"
```

Other points:

- With `Reflect.get(target, key, receiver)` or a `Proxy`, `this` in the getter is the **receiver** you pass.
- In a **static** getter, `this` is the class itself.
- If you define the accessor as an arrow function (for example, via `Object.defineProperty`), `this` is not the object, which is almost never what you want.
- Destructuring (`const { label } = user`) reads the value, calling the getter with `this = user` at that moment, and stores the result.

## 6. What happens when a bound function is used with the `new` keyword? Does the bound `this` value still apply?

**No.** When a bound function is called with `new`, the bound `this` is **ignored**. A new object is created and used as `this`. Any **pre-bound arguments** still apply, and the prototype link goes to the original function's `prototype`.

js

```jsx
function Person(name, age) {  this.name = name;  this.age = age;}const Bound = Person.bind({ name: "Default" }, "Aman");const p = new Bound(25);console.log(p.name);              // "Aman"console.log(p.age);               // 25console.log(p instanceof Person); // true
```

## 7. How does `this` behave in nested regular functions, arrow functions, and closures? How would you preserve the outer context without using `.bind()`?

- **Nested regular function:** gets its own `this` based on how it is called. A plain call means the global object or `undefined`, not the outer `this`.
- **Arrow function:** uses the `this` of the enclosing scope.
- **Closure:** closures capture **variables**, not `this`. Since `this` is not a variable, a regular inner function does not capture it.

js

```jsx
const user = {  name: "Aman",  run() {    function inner() { console.log(this?.name); }    inner(); // lost context  }};
```

**Ways to preserve the outer `this` without `.bind()`:**

js

```jsx
// 1. Arrow function (best)run() {  const inner = () => console.log(this.name);  inner();}// 2. Store this in a variable (older pattern)run() {  const self = this;  function inner() { console.log(self.name); }  inner();}// 3. thisArg parameter of array methodsthis.items.forEach(function (item) {  console.log(this.name, item);}, this);// 4. call() / apply() at the call siteinner.call(this);
```

## 8. What is the difference between `this` in JavaScript modules and in classic browser scripts? Consider strict mode and top-level `this`.

|  | Classic script | ES module (`type="module"`) |
| --- | --- | --- |
| Strict mode | **Off** by default | **Always on** |
| Top-level `this` | `window` (`globalThis`) | **`undefined`** |
| Top-level `var` / function declarations | Become properties of `window` | Stay module-scoped |
| Plain function call `fn()` | `this` = `window` (non-strict) | `this` = `undefined` |

html

```html
<script>  console.log(this === window); // true  function f() { return this; }  f();                          // window</script><script type="module">  console.log(this);            // undefined  function f() { return this; }  f();                          // undefined</script>
```

In **Node.js CommonJS** files, top-level `this` is `module.exports` (initially `{}`), while in Node ES modules (`.mjs` or `"type": "module"`) it is `undefined`. This explains why arrow functions defined at the top level of an object literal behave differently across environments.

## 9. What is the output?

js

```jsx
const admin = {  name: "Riya",  __proto__: user,};admin.greet();
```

**Output:** `Riya`

**Reason:** `greet` is found on `user` through the prototype chain, but it is called as `admin.greet()`, so `this` is `admin`.

## 10. What is the output?

js

```jsx
const bound = user.greet.bind({ name: "Riya" });const secondBound = bound.bind({ name: "Rahul" });secondBound();
```

**Output:** `Riya`

**Reason:** the first `bind` fixes `this` permanently. Binding a bound function again does not change `this`; only the first `bind` counts.

## 11. What is the output?

js

```jsx
const user = {  name: "Aman",  greet: () => {    console.log(this.name);  },};user.greet.call({ name: "Riya" });
```

**Output:** not `"Riya"` and not `"Aman"`. It prints an empty string (`""`) in a browser script, `undefined` in Node CommonJS, and throws a `TypeError` in an ES module (where top-level `this` is `undefined`).

**Reason:** the arrow function ignores `call()` and uses the top-level `this` from where it was defined. An object literal does not create a `this` scope.

## 12. What is the output?

js

```jsx
function Person(name) {  this.name = name;}const BoundPerson = Person.bind({ name: "Default" });const person = new BoundPerson("Aman");console.log(person.name);
```

**Output:** `Aman`

**Reason:** `new` overrides the bound `this`. A fresh object is created, and the constructor sets `name` to `"Aman"` on it.

## 13. What is the output?

js

```jsx
const user = new User("Aman");const greet = user.greet;greet();
```

**Output:** `TypeError: Cannot read properties of undefined (reading 'name')`

**Reason:** `greet` is a plain call, and class bodies run in strict mode, so `this` is `undefined`. Accessing `.name` on `undefined` throws.

## 14. What is the output?

js

```jsx
const user = {  name: "Aman",  greet() {    return () => {      console.log(this.name);    };  },};const greet = user.greet.call({ name: "Riya" });greet();
```

**Output:** `Riya`

**Reason:** `greet()` is invoked with `call({ name: "Riya" })`, so inside it `this` is that object. The returned arrow function captures that `this` permanently. Calling `greet()` later does not change it.

## 15. What is the output?

js

```jsx
const user = {  name: "Aman",  regular() {    return this.name;  },  arrow: () => this.name,};const other = { name: "Riya" };console.log(user.regular.call(other));console.log(user.arrow.call(other));
```

**Output:**

```
Riya
```

followed by a second line that depends on the environment:

- Browser classic script: an empty string (`""`), since `this` is `window` and `window.name` defaults to `""`.
- Node.js CommonJS: `undefined`, since `this` is `module.exports` (`{}`).
- ES module: a `TypeError`, since top-level `this` is `undefined`.

**Reason:** the regular method uses `call(other)`, so `this` is `other` and it returns `"Riya"`. The arrow function ignores `call()` and uses the top-level `this`, which has no `name` property matching `"Aman"` or `"Riya"`.

# 🚀 **Follow @daily.debugging for complete frontend resources and interview preparation.**
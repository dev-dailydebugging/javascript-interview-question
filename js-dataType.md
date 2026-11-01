# The Complete of Guide of Data Type

# **1. What are data types in JavaScript?**

A data type tells JavaScript what kind of value a variable holds, and what operations can be performed on it. JavaScript has two broad categories: **primitive types** (simple, immutable values) and **non-primitive types** (objects, which can hold collections of values and more complex structures).

# **2. How many primitive data types are there in JavaScript?**

There are **7 primitive data types** in JavaScript:

- String
- Number
- Boolean
- Undefined
- Null
- BigInt
- Symbol

# **3. What are the 7 primitive data types?**

1. **String** — textual data, e.g. `"hello"`
2. **Number** — numeric data (integers and decimals), e.g. `42`, `3.14`
3. **Boolean** — logical true/false, e.g. `true`, `false`
4. **Undefined** — a variable declared but not assigned a value
5. **Null** — an intentional absence of value
6. **BigInt** — for integers larger than `Number` can safely represent, e.g. `123n`
7. **Symbol** — a unique, immutable identifier, e.g. `Symbol("id")`

# **4. What is the difference between primitive and non-primitive data types?**

| **Aspect** | **Primitive** | **Non-Primitive** |
| --- | --- | --- |
| Storage | Stored directly by value | Stored by reference |
| Mutability | Immutable (value can't be changed, only reassigned) | Mutable (contents can be changed) |
| Copying | Copying creates a new independent value | Copying copies the reference, not the data |
| Examples | String, Number, Boolean, Null, Undefined, BigInt, Symbol | Object, Array, Function |
| `typeof` | Returns specific type names | Mostly returns `"object"` (except functions) |

Example:

```jsx
let a = 10;
let b = a;
b = 20;
console.log(a); // 10 (unaffected, primitive)

let obj1 = { value: 10 };
let obj2 = obj1;
obj2.value = 20;
console.log(obj1.value); // 20 (affected, same reference)
```

# **5. What is a String in JavaScript?**

A **String** represents textual data, written inside single quotes `'...'`, double quotes `"..."`, or backticks ``...`` (template literals, which allow embedded expressions). Strings are immutable — once created, their characters cannot be changed in place.

```jsx
let name = "Poojan";
let greeting = `Hello, ${name}!`;
```

# **6. What is the Number data type? Can it store both integers and decimals?**

**Number** represents all numeric values in JavaScript — there's no separate type for integers vs. floats. Yes, it stores both integers (`10`) and decimals (`10.5`), as well as special values like `Infinity`, `-Infinity`, and `NaN`. Internally, numbers are stored as 64-bit floating-point (IEEE 754) values.

```jsx
let a = 10;      // integer
let b = 10.5;    // decimal
let c = -3;      // negative integer
```

# **7. What is `NaN` in JavaScript?**

`NaN` stands for **Not-a-Number**. It's a special Number value that represents the result of an invalid or undefined mathematical operation.

```jsx
console.log(0 / 0);        // NaN
console.log("abc" * 2);    // NaN
```

A quirky fact: `NaN` is the only value in JavaScript that is not equal to itself (`NaN === NaN` is `false`). To check for it, use `Number.isNaN(value)`.

# **8. What is the difference between `null` and `undefined`?**

|  | **`undefined`** | **`null`** |
| --- | --- | --- |
| Meaning | Variable declared but not yet assigned a value | Intentional absence of a value, explicitly set |
| Set by | JavaScript automatically | The developer explicitly |
| Type (`typeof`) | `"undefined"` | `"object"` (a long-standing JS quirk) |
| Example | `let x; // x is undefined` | `let y = null; // y is intentionally empty` |

# **9. What is the Boolean data type?**

**Boolean** represents one of two logical values: `true` or `false`. It's commonly used in conditions, comparisons, and control flow.

```jsx
let isLoggedIn = true;
let hasAccess = false;

console.log(5 > 3); // true
```

# **10. What is BigInt, and why is it used?**

**BigInt** is a primitive type introduced to represent integers larger than the safe limit for the `Number` type (`Number.MAX_SAFE_INTEGER`, which is 2^53 − 1). It's used when you need precise, arbitrarily large integer values, such as in cryptography or high-precision calculations.

```jsx
let big = 9007199254740993n; // 'n' suffix makes it a BigInt
let big2 = BigInt(9007199254740993);
```

# **11. What is Symbol in JavaScript?**

**Symbol** is a primitive type that creates a unique and immutable value, primarily used as a special identifier for object properties — guaranteeing no naming collisions, even if two symbols have the same description.

```jsx
let sym1 = Symbol("id");
let sym2 = Symbol("id");
console.log(sym1 === sym2); // false, each Symbol is unique
```

# **12. What is an Object in JavaScript?**

An **Object** is a non-primitive data type used to store collections of related data as key-value pairs. Objects can hold multiple values of different types, including other objects and functions, and are mutable and stored by reference.

```jsx
let person = {
  name: "Poojan",
  age: 25,
  isDeveloper: true
};
```

Arrays and functions are technically specialized types of objects in JavaScript.

# **13. What is the `typeof` operator used for?**

The `typeof` operator returns a string indicating the data type of a value or variable. It's commonly used to check types before performing operations, or for debugging.

```jsx
typeof "hello";   // "string"
typeof 42;        // "number"
typeof true;      // "boolean"
typeof undefined; // "undefined"
typeof {};        // "object"
```

# **14. What will these return?**

```jsx
typeof null       // "object"
typeof undefined  // "undefined"
typeof []         // "object"
typeof NaN        // "number"
```

- `typeof null` → `"object"` — a famous, long-standing bug in JavaScript kept for backward compatibility.
- `typeof undefined` → `"undefined"` — as expected.
- `typeof []` → `"object"` — arrays are a type of object (use `Array.isArray([])` to check specifically for arrays).
- `typeof NaN` → `"number"` — because `NaN` is technically a value of the Number type, just an invalid one.

# **15. Is JavaScript statically typed or dynamically typed? Explain with an example.**

JavaScript is **dynamically typed**, meaning variable types are determined at runtime and can change during program execution — you don't declare a type when creating a variable, and the same variable can hold different types of values over its lifetime.

```jsx
let value = 42;        // value is a Number
console.log(typeof value); // "number"

value = "Hello";       // now value is a String
console.log(typeof value); // "string"

value = true;          // now value is a Boolean
console.log(typeof value); // "boolean"
```

![1.png](The%20Complete%20of%20Guide%20of%20Data%20Type/1.png)

![2.png](The%20Complete%20of%20Guide%20of%20Data%20Type/2.png)

![3.png](The%20Complete%20of%20Guide%20of%20Data%20Type/3.png)

![4.png](The%20Complete%20of%20Guide%20of%20Data%20Type/4.png)

![5.png](The%20Complete%20of%20Guide%20of%20Data%20Type/5.png)

![6.png](The%20Complete%20of%20Guide%20of%20Data%20Type/6.png)

![7.png](The%20Complete%20of%20Guide%20of%20Data%20Type/7.png)

![8.png](The%20Complete%20of%20Guide%20of%20Data%20Type/8.png)

![9.png](The%20Complete%20of%20Guide%20of%20Data%20Type/9.png)

![10.png](The%20Complete%20of%20Guide%20of%20Data%20Type/10.png)

![11.png](The%20Complete%20of%20Guide%20of%20Data%20Type/11.png)

![12.png](The%20Complete%20of%20Guide%20of%20Data%20Type/12.png)

![13.png](The%20Complete%20of%20Guide%20of%20Data%20Type/13.png)

![14.png](The%20Complete%20of%20Guide%20of%20Data%20Type/14.png)

![15.png](The%20Complete%20of%20Guide%20of%20Data%20Type/15.png)

# **JavaScript  Data Type  — Intermediate Questions with Answers**

# **1. What is the difference between primitive and reference values in JavaScript?**

| **Aspect** | **Primitive Values** | **Reference Values** |
| --- | --- | --- |
| Types | String, Number, Boolean, Undefined, Null, BigInt, Symbol | Object, Array, Function |
| Storage | Stored directly in the variable (on the stack) | Variable stores a reference (pointer) to the value in memory (heap) |
| Copying | Copying creates a completely independent value | Copying copies the reference, so both variables point to the same data |
| Mutability | Immutable | Mutable |
| Comparison | Compared by value | Compared by reference (memory address) |

# **2. How are primitive values stored and how are objects handled when assigned to another variable?**

Primitive values are stored **directly** in the variable itself. When you assign a primitive to another variable, JavaScript copies the actual value — the two variables become completely independent.

Objects, on the other hand, are stored in memory (the heap), and the variable only holds a **reference** (an address) pointing to that memory location. When you assign an object to another variable, you're copying the reference, not the object itself — so both variables end up pointing to the same underlying object.

```jsx
let a = 5;
let b = a; // b gets a copy of the value 5

let obj1 = { x: 1 };
let obj2 = obj1; // obj2 gets a copy of the reference, not a new object
```

# **3. What will be the output? Why?**

```jsx
let a = 10;
let b = a;

b = 20;

console.log(a);
console.log(b);
```

**Output:**

```
10
20
```

**Why:** `a` is a primitive (`Number`). When `b = a` runs, `b` gets its own independent copy of the value `10`. Reassigning `b` to `20` has no effect on `a`, since they no longer share any connection after the copy.

# **4. What will be the output? Why?**

```jsx
const user1 = { name: "Rahul" };
const user2 = user1;

user2.name = "Aman";

console.log(user1.name);
```

**Output:**

```
Aman
```

**Why:** `user1` and `user2` are objects, so `user2 = user1` copies the **reference**, not the object itself. Both variables point to the exact same object in memory. Modifying `user2.name` modifies the shared object, so the change is visible through `user1` too. Note: `const` only prevents reassigning the variable itself (e.g. `user2 = {}` would fail) — it does not make the object's contents immutable.

# **5. Why does `typeof null` return `"object"`?**

This is a well-known **historical bug** in JavaScript. In the original 1995 implementation, values were represented internally with a type tag, and objects had the type tag `0`. `null` was represented as the null pointer (essentially all zeros), which happened to match the object type tag — causing `typeof null` to incorrectly return `"object"`. This behavior has stuck around ever since because fixing it would break existing code across the web, so it was never patched despite being widely acknowledged as a mistake.

# **6. Why does `typeof []` return `"object"`? How can you check whether a value is actually an array?**

Arrays are a specialized kind of object in JavaScript — under the hood, they're objects with numeric keys, a `length` property, and array-specific methods on their prototype. Since `typeof` only distinguishes broad categories (and treats all non-function objects as `"object"`), it can't tell arrays apart from plain objects.

To check specifically for an array, use:

```jsx
Array.isArray([]);        // true
Array.isArray({});        // false
```

# **7. What is the difference between `typeof` and `Array.isArray()`?**

|  | **`typeof`** | **`Array.isArray()`** |
| --- | --- | --- |
| Purpose | Returns the general type of any value | Specifically checks if a value is an array |
| Result for arrays | `"object"` (not useful for distinguishing arrays) | `true` |
| Result for objects | `"object"` | `false` |
| Use case | Broad type checking (string, number, boolean, etc.) | Precise array detection |

```jsx
typeof [];           // "object"
Array.isArray([]);   // true
typeof {};           // "object"
Array.isArray({});   // false
```

# **8. What are truthy and falsy values in JavaScript? Give examples.**

When a value is used in a boolean context (like an `if` condition), JavaScript converts it to `true` or `false`.

- **Truthy** values evaluate to `true` — e.g. `"hello"`, `42`, `[]` (empty array), `{}` (empty object), `1`.
- **Falsy** values evaluate to `false` — a specific, limited set (see next question).

```jsx
if ("hello") console.log("truthy"); // runs
if (0) console.log("falsy");        // doesn't run
```

# **9. What are all the falsy values in JavaScript?**

There are exactly **8 falsy values** in JavaScript:

1. `false`
2. `0` (and `0`)
3. `""` (empty string)
4. `null`
5. `undefined`
6. `NaN`
7. `0n` (BigInt zero)
8. `document.all` (a rare, legacy special case in browsers)

Everything else — including `"0"`, `"false"`, `[]`, and `{}` — is truthy.

# **10. What is type coercion? Explain with examples.**

**Type coercion** is JavaScript's automatic (implicit) conversion of a value from one data type to another, typically when an operator is used with mismatched types.

```jsx
console.log("5" + 2);
console.log("5" - 2);
```

**Output:**

```
"52"
3
```

**Why:**

- `"5" + 2` → the `+` operator, when either operand is a string, converts the other to a string and **concatenates**: `"5" + "2"` → `"52"`.
- `"5" - 2` → the  operator has no string-concatenation meaning, so JavaScript **coerces** `"5"` into the number `5`, then subtracts: `5 - 2` → `3`.

# **11. What is the difference between `==` and `===`?**

|  | **`==` (loose equality)** | **`===` (strict equality)** |
| --- | --- | --- |
| Type conversion | Converts operands to the same type before comparing | No conversion — types must already match |
| Example | `"5" == 5` → `true` | `"5" === 5` → `false` |
| Recommended use | Generally avoided due to unpredictable coercion rules | Preferred for predictable, safe comparisons |

```jsx
"5" == 5;    // true (coerced)
"5" === 5;   // false (different types)
null == undefined;   // true
null === undefined;  // false
```

# **12. What is the difference between `null`, `undefined`, and `NaN`?**

|  | **`null`** | **`undefined`** | **`NaN`** |
| --- | --- | --- | --- |
| Meaning | Intentional absence of value | Variable declared but not assigned | Result of an invalid numeric operation |
| Set by | Developer, explicitly | JavaScript, automatically | JavaScript, as the result of bad math |
| `typeof` | `"object"` | `"undefined"` | `"number"` |
| Example | `let x = null;` | `let x; // undefined` | `0 / 0 // NaN` |

# **13. Why is `NaN` considered a Number? What does this return?**

```jsx
typeof NaN
```

**Output:**

```
"number"
```

**Why:** Despite meaning "Not-a-Number," `NaN` is technically a special value **within** the Number type — it represents an invalid or unrepresentable numeric result (like `0/0` or `parseInt("abc")`), but it's still classified as a Number under the hood, per the IEEE 754 floating-point standard which reserves specific bit patterns for "not a number" results.

# **14. What is the difference between `Object.is()` and `===`? Give examples where their results differ.**

`Object.is()` behaves almost identically to `===`, but fixes two specific edge cases:

```jsx
NaN === NaN;          // false
Object.is(NaN, NaN);  // true

+0 === -0;             // true
Object.is(+0, -0);     // false
```

In every other case, `Object.is()` and `===` behave the same way. `Object.is()` is mainly useful in scenarios like deep-equality checks or React's internal change-detection logic, where these edge cases matter.

# **15. What happens when you use `const` with an object or array? Can its properties/elements still be changed?**

`const` only makes the **variable binding** immutable — it prevents the variable from being **reassigned** to point to a different value. It does **not** freeze the contents of an object or array. So properties and elements can still be added, removed, or modified.

```jsx
const arr = [1, 2, 3];
arr.push(4);        // allowed — modifies the array in place
console.log(arr);   // [1, 2, 3, 4]

arr = [5, 6];        // ❌ TypeError: Assignment to constant variable.

const obj = { name: "Rahul" };
obj.name = "Aman";  // allowed
obj.age = 25;        // allowed
```

# **JavaScript  Data Type  — Advanced Questions with Answers**

# **1. What exactly happens during JavaScript's type coercion? Explain the internal conversion process when JavaScript converts one type into another.**

Internally, JavaScript type coercion is driven by a set of **abstract operations** defined in the ECMAScript specification. When an operator or context needs a value of a particular type, the engine calls one of these internal conversion routines:

- **`ToPrimitive`** — converts an object into a primitive value (string, number, or boolean).
- **`ToString`** — converts any value into a string.
- **`ToNumber`** — converts any value into a number.
- **`ToBoolean`** — converts any value into a boolean.

The engine decides *which* conversion to apply based on the operator and the "preferred type" hint it passes along. For example:

- The `+` operator, when operands aren't both numbers, first converts objects via `ToPrimitive` (with hint `"default"`), then decides between string concatenation or numeric addition based on the resulting primitive types.
- Comparison operators like `<` or `>` use `ToPrimitive` with hint `"number"`.
- Template literals and explicit `String()` calls use `ToPrimitive` with hint `"string"`.

So coercion isn't random — it's a well-defined pipeline: **check the operator → determine the hint → call `ToPrimitive` if needed → then apply `ToString`/`ToNumber`/`ToBoolean` as required by the operation.**

# **2. What is `ToPrimitive` in JavaScript? Explain how JavaScript converts an object into a primitive value.**

```jsx
const obj = {
  valueOf() {
    return 10;
  }
};

console.log(obj + 5);
```

**Output:**

```
15
```

**Explanation:** `ToPrimitive` is the internal abstract operation that converts an object into a primitive value so operators (like `+`) can work with it. It follows an order depending on the "hint" it receives:

- **hint `"number"`:** try `valueOf()` first, then `toString()`.
- **hint `"string"`:** try `toString()` first, then `valueOf()`.
- **hint `"default"`** (used by `+`, `==`, etc. when no specific type is implied): try `valueOf()` first, then `toString()`.

In the example, `obj + 5` triggers `ToPrimitive` with hint `"default"`. JavaScript calls `obj.valueOf()`, which returns the primitive number `10`. Since a primitive was successfully returned, `toString()` is never called. The expression then becomes `10 + 5`, which is `15`.

# **3. What is the difference between `ToString`, `ToNumber`, and `ToBoolean`? Explain when JavaScript performs each conversion.**

| **Conversion** | **Purpose** | **Triggered by** |
| --- | --- | --- |
| `ToString` | Converts a value into its string representation | Template literals, `String(x)`, `+` with a string operand, implicit string contexts |
| `ToNumber` | Converts a value into a numeric representation | Arithmetic operators (`-`, `*`, `/`), `Number(x)`, comparisons (`<`, `>`), unary `+` |
| `ToBoolean` | Converts a value into `true`/`false` | Conditions (`if`, `while`), logical operators (`&&`, ` |

Examples:

```jsx
String(123);      // ToString → "123"
Number("42");     // ToNumber → 42
Boolean(0);        // ToBoolean → false
if ("hello") {}    // ToBoolean applied implicitly
"5" * 2;           // ToNumber applied to "5" → 10
```

# **4. Explain the complete difference between `==` and `===`.**

```jsx
console.log(0 == false);
console.log("" == false);
console.log(null == undefined);
console.log(null === undefined);
```

**Output:**

```
true
true
true
false
```

**Why these differ:**

- `0 == false` → `false` is coerced to `0` via `ToNumber`, so `0 == 0` → `true`.
- `"" == false` → both sides are coerced to numbers: `""` → `0`, `false` → `0`, so `0 == 0` → `true`.
- `null == undefined` → this is a **special case written directly into the spec**: `null` and `undefined` are defined to be loosely equal to each other, and to nothing else (no coercion actually happens here — it's a hardcoded rule).
- `null === undefined` → `===` never coerces, and since `null` and `undefined` are different types, they are never strictly equal, hence `false`.

In short: `==` (loose equality) coerces operands to a common type before comparing, following specific, sometimes surprising spec rules, while `===` (strict equality) compares both type and value with zero coercion.

# **5. What is the difference between `===`, `Object.is()`, and `SameValueZero`?**

```jsx
console.log(NaN === NaN);
console.log(Object.is(NaN, NaN));

console.log(+0 === -0);
console.log(Object.is(+0, -0));
```

**Output:**

```
false
true
true
false
```

**Explanation:** JavaScript actually has three related-but-distinct equality algorithms:

- **`===` (Strict Equality Comparison)**: treats `NaN` as never equal to itself, and treats `+0` and `0` as equal.
- **`Object.is()` (SameValue algorithm)**: treats `NaN` as equal to itself, and distinguishes `+0` from `0`. It's designed to match mathematical "sameness" more precisely.
- **`SameValueZero`**: identical to `Object.is()`'s SameValue algorithm, **except** it treats `+0` and `0` as equal (like `===` does). This algorithm is used internally by things like `Array.prototype.includes()` and `Map`/`Set` key comparisons — which is why `[NaN].includes(NaN)` returns `true`, unlike `indexOf`.

# **6. Why does this return `false`? Explain reference equality versus value equality.**

```jsx
console.log({} === {});
console.log([] === []);
```

**Output:**

```
false
false
```

**Why:** Objects and arrays are **reference types**. `===` for objects checks whether both operands point to the **exact same location in memory**, not whether their contents look the same. Each `{}` and `[]` literal creates a brand-new, distinct object in memory, so even though they look identical structurally, they are different references — hence `false`.

This is **reference equality** (compares identity/memory address), as opposed to **value equality** (compares contents), which JavaScript doesn't provide natively for objects — you'd need a custom deep-comparison function or a library like Lodash's `isEqual`.

```jsx
const a = {};
const b = a;
console.log(a === b); // true — same reference
```

# **7. How does JavaScript handle Number precision? Explain why `0.1 + 0.2` doesn't produce exactly `0.3`.**

```jsx
console.log(0.1 + 0.2);
```

**Output:**

```
0.30000000000000004
```

**Why:** JavaScript represents all numbers using the **IEEE 754 double-precision floating-point standard** (64 bits). This format cannot represent most decimal fractions (like `0.1` or `0.2`) *exactly* in binary — similar to how `1/3` can't be written exactly in decimal. Instead, these values are stored as the closest possible binary approximation. When `0.1` and `0.2` (each already slightly imprecise) are added, their tiny rounding errors combine, producing a result that's very close to, but not exactly, `0.3`.

```jsx
Number.MAX_SAFE_INTEGER  // 9007199254740991 (2^53 - 1)
Number.MIN_SAFE_INTEGER  // -9007199254740991
```

These represent the largest and smallest integers that can be represented **exactly** and safely in the double-precision format without losing precision. Beyond this range, integers may not be represented accurately (e.g., `9007199254740993` and `9007199254740992` can end up being treated as equal).

# **8. What is the difference between `Number`, `BigInt`, and `Number.MAX_SAFE_INTEGER`? Explain when `BigInt` should be used and why this causes an error.**

```jsx
console.log(10n + 5);
```

**Output:**

```
TypeError: Cannot mix BigInt and other types, use explicit conversions
```

**Explanation:**

- **`Number`** uses IEEE 754 double-precision floats, and can safely represent integers only up to `Number.MAX_SAFE_INTEGER` (2^53 − 1).
- **`BigInt`** is a separate primitive type designed to represent arbitrarily large integers with full precision, denoted with an `n` suffix (e.g., `10n`).
- **`Number.MAX_SAFE_INTEGER`** is simply a constant on the `Number` type marking the upper safe boundary for regular numbers — it's not related to BigInt directly, but is the threshold beyond which you'd typically switch to `BigInt`.

The error occurs because JavaScript **deliberately disallows implicit mixing** of `BigInt` and `Number` in arithmetic — since converting between them could silently lose precision, the spec requires you to convert explicitly:

```jsx
console.log(10n + BigInt(5));  // 15n
console.log(Number(10n) + 5);  // 15
```

Use `BigInt` when working with values beyond safe integer range — e.g., cryptographic keys, high-precision IDs, or large financial calculations.

# **9. Explain `Symbol` in depth. Why is `Symbol("id") === Symbol("id")` `false`? Also explain how Symbols can be used as object property keys.**

```jsx
Symbol("id") === Symbol("id")  // false
```

**Why:** Every call to `Symbol()` creates a **brand-new, completely unique value**, regardless of the description string passed in. The description (`"id"`) is purely for debugging/readability — it plays no role in equality. Internally, each Symbol is guaranteed by the engine to be distinct from every other Symbol ever created, which is the entire point of the type: guaranteed uniqueness, even for identical-looking symbols.

**As object property keys:** Symbols can be used as unique, collision-free property keys — useful for adding "hidden" or special metadata to objects without risking clashes with string keys (including from other code/libraries).

```jsx
const id = Symbol("id");
const user = {
  name: "Rahul",
  [id]: 12345 // symbol as a computed property key
};

console.log(user[id]);        // 12345
console.log(Object.keys(user)); // ["name"] — symbol keys are excluded from normal enumeration
```

# **10. How does JavaScript convert objects to primitive values? Explain the order involving `Symbol.toPrimitive`, `valueOf()`, and `toString()`.**

```jsx
const obj = {
  valueOf() {
    return 10;
  },
  toString() {
    return "20";
  }
};

console.log(obj + 5);
```

**Output:**

```
15
```

**Explanation:** When converting an object to a primitive, JavaScript follows this priority order:

1. **`Symbol.toPrimitive`** — if the object defines this method, it's called first and its return value is used directly, overriding everything else.
2. **`valueOf()`** — called next (for hints `"number"` or `"default"`), if it returns a primitive, that's used.
3. **`toString()`** — used as a fallback if `valueOf()` doesn't return a primitive (or is missing), and always tried first for hint `"string"`.

In this example, there's no `Symbol.toPrimitive`, so JavaScript proceeds to `valueOf()`, which returns the primitive `10`. Since a valid primitive was returned, `toString()` is never reached. So `obj + 5` becomes `10 + 5` → `15`.

If `valueOf()` were removed or returned a non-primitive (like an object), JavaScript would fall back to `toString()`, and the result would instead use `"20"`, producing `"205"` (string concatenation).

# **11. What happens when different types are used with the `+` operator?**

```jsx
console.log(1 + "2");
console.log(1 + 2);
console.log(true + 1);
console.log(null + 1);
console.log(undefined + 1);
```

**Output:**

```
"12"
3
2
1
NaN
```

**Explanation:**

- `1 + "2"` → since one operand is a string, `+` performs **string concatenation**: `1` is converted to `"1"`, giving `"12"`.
- `1 + 2` → both are numbers, so plain **numeric addition**: `3`.
- `true + 1` → `true` is coerced via `ToNumber` to `1`, so `1 + 1` → `2`.
- `null + 1` → `null` is coerced via `ToNumber` to `0`, so `0 + 1` → `1`.
- `undefined + 1` → `undefined` is coerced via `ToNumber` to `NaN`, so `NaN + 1` → `NaN` (any arithmetic involving `NaN` yields `NaN`).

# **12. Explain why these results are different. Discuss object-to-primitive conversion and the `+` operator.**

```jsx
console.log([] + []);
console.log([] + {});
console.log({} + []);
```

**Output (in a script/expression context):**

```
""
"[object Object]"
"[object Object]"
```

*(Note: `{} + []` typed directly at the start of a statement in a console/REPL can be parsed differently — as an empty block followed by `+[]` — giving `0`. As an expression, e.g. inside `console.log(...)`, it consistently gives `"[object Object]"`.)*

**Explanation:** Both operands of `+` go through `ToPrimitive` with hint `"default"` when they're objects/arrays:

- `[]` → `ToPrimitive` calls `valueOf()` (returns the array itself, not a primitive, so it's skipped) then `toString()`, which joins array elements — for an empty array, that's `""`.
- `{}` → `valueOf()` returns the object itself (not primitive, skipped), so `toString()` is used, giving the default `"[object Object]"`.

So:

- `[] + []` → `"" + ""` → `""`
- `[] + {}` → `"" + "[object Object]"` → `"[object Object]"`
- `{} + []` (as an expression) → `"[object Object]" + ""` → `"[object Object]"`

# **13. What is the difference between shallow copy and deep copy? Explain the effect of references.**

```jsx
const user1 = {
  name: "Rahul",
  address: {
    city: "Delhi"
  }
};

const user2 = { ...user1 };

user2.address.city = "Mumbai";

console.log(user1.address.city);
```

**Output:**

```
Mumbai
```

**Why:** The spread operator (`{ ...user1 }`) performs a **shallow copy** — it copies only the top-level properties. `name` (a primitive string) is copied by value, so it's independent. But `address` is an object, so only its **reference** is copied — `user2.address` and `user1.address` point to the exact same nested object in memory. Modifying `user2.address.city` therefore also affects `user1.address.city`, since there's really only one `address` object being shared.

A **deep copy** would recursively duplicate every nested object/array so there's no shared reference anywhere, e.g.:

```jsx
const user2 = structuredClone(user1); // true deep copy
// or: JSON.parse(JSON.stringify(user1)) — with caveats (loses functions, dates, etc.)
```

# **14. Are functions, arrays, and dates separate data types? Explain the `typeof` results and their relationship to `Object`.**

```jsx
typeof function() {}   // "function"
typeof []               // "object"
typeof new Date()       // "object"
```

**Explanation:** Functions, arrays, and dates are **not** separate primitive data types — they are all specialized kinds of **objects** under the hood, each with their own internal behavior and prototype methods (`Array.prototype`, `Date.prototype`, `Function.prototype`).

- **Functions** get a special-cased `typeof` result — `"function"` — because they're *callable* objects, and the spec explicitly carves this out for practical usefulness (since checking for callability is extremely common).
- **Arrays** and **Dates** don't get this special treatment — `typeof` reports them simply as `"object"`, since from `typeof`'s perspective, they're just objects (their special array/date behavior comes from their prototype chain, not a distinct primitive type).

To distinguish them more precisely, you'd use `Array.isArray()`, `instanceof Date`, or `Object.prototype.toString.call(value)` (which returns things like `"[object Array]"` or `"[object Date]"`).

# **15. Explain this complete output-based problem.**

```jsx
console.log(typeof null);
console.log(typeof NaN);
console.log(typeof []);
console.log(typeof {});
console.log(typeof function () {});

console.log([] == false);
console.log([] === false);

console.log(null == undefined);
console.log(null === undefined);

console.log(NaN === NaN);
console.log(Object.is(NaN, NaN));

console.log(0.1 + 0.2 === 0.3);
```

**Output:**

```
"object"
"number"
"object"
"object"
"function"

true
false

true
false

false
true

false
```

# 🚀 **Follow @daily.debugging for complete frontend resources and interview preparation.**
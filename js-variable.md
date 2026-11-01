# The Complete Guide of Variable

# 1. What is a variable in JavaScript?

A variable is a container that stores a value (like a number, text, or object) so you can use it later in your code.

# 2. Why do we use variables?

To store, reuse, and manage data instead of writing the same value again and again, and to make code easier to update.

# 3. Three keywords to declare variables

`var`, `let`, and `const`.

# 4. Difference between `var`, `let`, and `const`

- `var` — function-scoped, can be redeclared and updated, hoisted (old way)
- `let` — block-scoped, can be updated but not redeclared in same scope
- `const` — block-scoped, cannot be updated or redeclared (value stays constant)

# 5. Declare a variable using `let`

```jsx
let age = 25;
```

# 6. Declare a constant using `const`

```jsx
const name = "Poojan";
```

# 7. Can a `let` variable be reassigned?

Yes.

```jsx
let x = 5;
x = 10; // works
```

# 8. Can a `const` variable be reassigned?

No, it will throw an error.

```jsx
const x = 5;
x = 10; // ❌ Error
```

# 9. Can a `var` variable be redeclared?

Yes, `var` allows redeclaration without error.

```jsx
var x = 1;
var x = 2; // works
```

# 10. Can a `let` variable be redeclared in the same scope?

No.

```jsx
let x = 1;
let x = 2; // ❌ Error
```

# 11. What is variable initialization?

Giving a variable its first value when you declare it.

```jsx
let score = 0; // initialization
```

# 12. What is variable reassignment?

Changing the value of a variable after it's already been declared.

```jsx
score = 10; // reassignment
```

# 13. What is block scope?

A variable declared inside `{ }` (like an `if` block or loop) is only accessible within that block. `let` and `const` follow block scope; `var` does not.

# 14. Why is `const` preferred over `let`?

It prevents accidental reassignment, making code safer and more predictable. You use `let` only when you know the value will change.

# 15. When should you use `let` instead of `const`?

When the variable's value needs to change later, like a counter, loop index, or a value that updates based on user input.

![58A93598-4F2B-4220-916A-F519CE68D249.PNG](The%20Complete%20Guide%20of%20Variable/58A93598-4F2B-4220-916A-F519CE68D249.png)

![FAD96306-F8F3-4DE4-A581-0569C2285721.PNG](The%20Complete%20Guide%20of%20Variable/FAD96306-F8F3-4DE4-A581-0569C2285721.png)

![D53BE675-C1B5-4531-894E-AA1D89D5C735.PNG](The%20Complete%20Guide%20of%20Variable/D53BE675-C1B5-4531-894E-AA1D89D5C735.png)

![6B47A7A4-9250-435C-A8CF-7A4B9A2D5383.PNG](The%20Complete%20Guide%20of%20Variable/6B47A7A4-9250-435C-A8CF-7A4B9A2D5383.png)

![A386BDC5-B8A3-48D5-8F8C-05037551FF3B.PNG](The%20Complete%20Guide%20of%20Variable/A386BDC5-B8A3-48D5-8F8C-05037551FF3B.png)

![90069688-E404-4CD1-8D3B-B9A37270D4CF.PNG](The%20Complete%20Guide%20of%20Variable/90069688-E404-4CD1-8D3B-B9A37270D4CF.png)

![75498B96-49D4-4A79-BCCE-C0E397C06636.PNG](The%20Complete%20Guide%20of%20Variable/75498B96-49D4-4A79-BCCE-C0E397C06636.png)

![DB681572-37E9-4B12-82C6-DC8A64C1E01B.PNG](The%20Complete%20Guide%20of%20Variable/DB681572-37E9-4B12-82C6-DC8A64C1E01B.png)

![2EA828AB-02B1-49FE-83FA-8822EEE0008E.PNG](The%20Complete%20Guide%20of%20Variable/2EA828AB-02B1-49FE-83FA-8822EEE0008E.png)

![E5FAE914-1370-4BB0-90B3-B946677283B5.PNG](The%20Complete%20Guide%20of%20Variable/E5FAE914-1370-4BB0-90B3-B946677283B5.png)

![9973AA21-40CB-41E8-8258-CDB074CA98E9.PNG](The%20Complete%20Guide%20of%20Variable/9973AA21-40CB-41E8-8258-CDB074CA98E9.png)

![46F3F200-206D-4C3A-A773-7FF872C60D52.PNG](The%20Complete%20Guide%20of%20Variable/46F3F200-206D-4C3A-A773-7FF872C60D52.png)

![E483F859-7674-4EE7-A8B0-BEA4F96A89B0.PNG](The%20Complete%20Guide%20of%20Variable/E483F859-7674-4EE7-A8B0-BEA4F96A89B0.png)

![A7C0DDDC-13F1-4516-BE7B-E35C0A2BF253.PNG](The%20Complete%20Guide%20of%20Variable/A7C0DDDC-13F1-4516-BE7B-E35C0A2BF253.png)

# **JavaScript  Variables — Intermediate Questions with Answers**

# 1. What is the difference between variable scope and lexical scope?

- **Variable scope** is the *region* of code where a variable can be accessed (global, function, or block).
- **Lexical scope** is the *rule* JavaScript uses to decide that region: a variable’s scope is determined by where it is **written** in the source code, not by how functions are called at runtime.

In short: “scope” = where it’s visible; “lexical scope” = the rule that scope is based on the code’s physical nesting.

---

# 2. How does the JavaScript scope chain work when accessing a variable?

When you use a variable, JavaScript searches for it using the **scope chain**:

1. Check the **current (innermost)** scope.
2. If not found, move to the **parent** scope.
3. Keep moving outward until the **global** scope.
4. If still not found, throw a `ReferenceError`.

This is why inner functions can read outer variables, but not the other way around.

---

# 3. Can `let` and `const` variables be hoisted? Explain with an example.

Yes, `let` and `const` are **hoisted**, but **not initialized**.[stackoverflow](https://stackoverflow.com/questions/500431/what-is-the-scope-of-variables-in-javascript/500459)

- They exist from the top of their block, but you cannot use them until their declaration line.
- Before that line, they are in the **Temporal Dead Zone (TDZ)**.[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)

Example:

```
jsconsole.log(x);// ReferenceError: Cannot access 'x' before initializationlet x=10;
```

With `var`, it would log `undefined` instead of throwing, because `var` is hoisted **and** initialized to `undefined`.[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)

---

# 4. Why does accessing a `let` or `const` variable before declaration throw a ReferenceError?

Because although the binding exists (hoisted), it is **uninitialized** until the declaration line runs.

Accessing it in the TDZ is forbidden, so JavaScript throws a `ReferenceError` to prevent using a variable before it’s properly set up.[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)

---

# 5. What exactly happens during the Temporal Dead Zone (TDZ)?

TDZ is the time **from the start of the block** until the `let`/`const` declaration is evaluated.stackoverflow+1

- The variable is “known” to the engine but **cannot be read or written**.[stackoverflow](https://stackoverflow.com/questions/500431/what-is-the-scope-of-variables-in-javascript/500459)
- Any access in this zone throws `ReferenceError: Cannot access 'x' before initialization`.[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)

It protects you from subtle bugs caused by using variables before they’re intentionally created.[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)

---

# 6. What is variable shadowing in JavaScript?

**Shadowing** happens when an inner scope declares a variable with the **same name** as one in an outer scope.

Inside the inner scope, the inner variable “hides” (shadows) the outer one.

Example:

```
jslet x=1;{let x=2;// shadows outer x  console.log(x);// 2}console.log(x);// 1
```

---

# 7. Can `let` and `const` shadow variables declared with `var`?

Yes. `let`/`const` in an inner block can shadow a `var` from an outer function/global scope, because they create a new binding in the inner scope.[stackoverflow](https://stackoverflow.com/questions/500431/what-is-the-scope-of-variables-in-javascript/500459)

Inside that inner block, references resolve to the `let`/`const`, not the outer `var`.

---

# 8. What happens when a variable is declared with the same name in nested blocks?

- With `let`/`const`: each block gets its **own separate** variable; the inner one shadows the outer within that block.stackoverflow+1
- With `var`: there is **no block scope**; redeclaring `var` in nested blocks refers to the **same** function/global variable (no new binding).stackoverflow+1

---

# 9. What is the difference between redeclaration and reassignment?

- **Redeclaration**: declaring the same variable name again in the same scope (e.g., `var x; var x;`).[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)
    - `var` allows redeclaration in the same scope; `let`/`const` do **not** (SyntaxError).[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)
- **Reassignment**: giving a variable a new value (e.g., `x = 5;`).[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)
    - `var` and `let` allow reassignment; `const` does **not** (TypeError if you try to reassign).[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)

---

# 10. Why can a `const` object be modified even though a `const` variable cannot be reassigned?

`const` prevents **reassigning the variable** to a different value, but it does **not** make the value itself immutable.[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)

- For objects/arrays, you can still change their **properties/elements**; you just can’t point the variable to a new object.[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)

Example:

```
jsconst obj={a:1};obj.a=2;// OK (mutate property)obj={};// TypeError (reassign variable)
```

---

# 11. What is the difference between primitive values and object references when using `const`?

- **Primitives** (number, string, boolean, etc.): `const` means the value cannot change.[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)
- **Objects/arrays**: `const` means the **reference** cannot change, but the object’s contents can.[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)

So `const arr = [1]; arr.push(2);` is allowed; `arr = [3];` is not.[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)

---

# 12. What happens when you assign a value to an undeclared variable?

In non-strict mode, assigning to an undeclared variable **creates a global variable** (on the global object), which is usually a bug.[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)

Example:

```
jsfunctionf(){  x=10;// creates global x (non-strict mode)}
```

---

# 13. How does strict mode affect assignment to undeclared variables?

In **strict mode** (`"use strict";`), assigning to an undeclared variable throws a `ReferenceError` instead of creating a global.[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)

This helps catch typos and accidental globals early.[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)

---

# 14. What happens when `var` is declared inside a loop compared with `let`?

- `var i` in a loop: one shared variable for the whole function/global scope; all closures see the **final** value.stackoverflow+1
- `let i` in a loop: a **new binding per iteration**; closures capture the value for that specific iteration.stackoverflow+2

This is why `let` is safer for loops with callbacks or async code.[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)

---

# 15. Why are `let` and `const` considered safer than `var` in modern JavaScript?

Because they:

- Have **block scope** (no accidental leaks outside `{}`).stackoverflow+2
- Disallow **redeclaration** in the same scope (fewer name clashes).[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)
- Enforce **TDZ**, preventing use before declaration.[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)
- Encourage immutability with `const`, reducing bugs from unintended changes.[geeksforgeeks](https://www.geeksforgeeks.org/javascript/javascript-scope/)

Modern guidance: **default to `const`**, use `let` when you must reassign, and **avoid `var`**.

# **JavaScript  Variables — Advanced Questions with Answers**

# 1. Explain the exact lifecycle of a `let`/`const` variable from entering a block to after its declaration.

When JavaScript enters a block (like `{ ... }`, `if`, `for`), it does two steps for `let`/`const`:[stackinterview](https://stackinterview.dev/guides/javascript-interview-questions-2026)

1. **Creation**: The variable name is registered in that block’s scope, but it is **not initialized** yet.[stackinterview](https://stackinterview.dev/guides/javascript-interview-questions-2026)
2. **Temporal Dead Zone (TDZ)**: From the start of the block until the line with `let x = ...` or `const x = ...`, the variable exists but **cannot be accessed**. Any access here throws `ReferenceError`.[stackinterview](https://stackinterview.dev/guides/javascript-interview-questions-2026)
3. **Initialization**: When the declaration line runs, the variable gets its value and becomes usable.

So the lifecycle is: *created → TDZ (unusable) → initialized (usable)*.[stackinterview](https://stackinterview.dev/guides/javascript-interview-questions-2026)

---

# 2. Predict the output and explain why:

```
jsfor(var i=0; i<3; i++){setTimeout(()=> console.log(i),0);}
```

**Output:** `3 3 3`scrimba+2

**Why?**

`var i` is **function-scoped** (or global if not in a function). All three `setTimeout` callbacks share the **same** `i`. By the time the callbacks run, the loop has finished and `i` is `3`.scrimba+1

**Now with `let`:**

```
jsfor(let i=0; i<3; i++){setTimeout(()=> console.log(i),0);}
```

**Output:** `0 1 2`scrimba+2

**Why?**

`let i` is **block-scoped**, and in a `for` loop, JavaScript creates a **new binding of `i` for each iteration**. Each callback captures its own `i` value for that iteration.scrimba+2

---

# 3. What is the Temporal Dead Zone (TDZ) at the engine level, and how is it different from “not defined”?

- **TDZ**: The variable is *known* to the engine (its name exists in the scope), but it is **uninitialized** until the declaration line runs. Accessing it in TDZ throws:
    
    `ReferenceError: Cannot access 'x' before initialization`.[stackinterview](https://stackinterview.dev/guides/javascript-interview-questions-2026)
    
- **“Not defined”**: The variable name does **not exist** in any scope. Accessing it throws:
    
    `ReferenceError: x is not defined`.[stackinterview](https://stackinterview.dev/guides/javascript-interview-questions-2026)
    

**Example of TDZ error:**

```
js{  console.log(x);// ReferenceError: Cannot access 'x' before initializationlet x=10;}
```

The name `x` exists in this block, but you’re using it before its declaration line.

---

# 4. Can you create a block-scoped variable dynamically (e.g., inside an `if` that may or may not run) using `let`/`const`?

Yes, you can declare `let`/`const` inside an `if` block, but the variable is **only available inside that block**.

```
jsif(true){let x=5;  console.log(x);// 5}console.log(x);// ReferenceError: x is not defined
```

If the `if` block doesn’t run, the declaration never executes, so the variable doesn’t exist at all. Trying to use it outside (or even inside, if the block didn’t run) will cause a `ReferenceError`.

---

# 5. What is the difference between these two snippets?

```
js// Avar x=1;functionfoo(){  console.log(x);var x=2;}foo();// Blet y=1;functionbar(){  console.log(y);let y=2;}bar();
```

**Snippet A output:** `undefined`

- Inside `foo`, `var x` is **hoisted** to the top of the function and initialized as `undefined`.
- The `console.log(x)` uses this local `x` (still `undefined`) before `x = 2` runs.
- So it logs `undefined`, not `1`.

**Snippet B output:** `ReferenceError: Cannot access 'y' before initialization`[stackinterview](https://stackinterview.dev/guides/javascript-interview-questions-2026)

- `let y` inside `bar` is hoisted but **uninitialized** (TDZ).
- `console.log(y)` tries to read `y` in TDZ → throws `ReferenceError`.

Key idea: `var` = hoisted + initialized (`undefined`); `let` = hoisted + uninitialized (TDZ).[stackinterview](https://stackinterview.dev/guides/javascript-interview-questions-2026)

---

# 6. How do closures interact differently with `var` vs `let` in loops?

With `var`, all closures share the same variable. With `let`, each iteration gets its own variable.

**Problem with `var`:**

```
jsconst funcs=[];for(var i=0; i<3; i++){  funcs.push(()=> console.log(i));}funcs[0]();// 3funcs[1]();// 3funcs[2]();// 3
```

All functions see the final `i = 3`.scrimba+2

**Fix with `let`:**

```
jsconst funcs=[];for(let i=0; i<3; i++){  funcs.push(()=> console.log(i));}funcs[0]();// 0funcs[1]();// 1funcs[2]();// 2
```

Each closure captures its own `i` for that iteration.scrimba+2

---

# 7. What happens when you redeclare a variable with the same name using `var`, `let`, and `const` in the same scope?

- **`var` then `var` (same scope):** Allowed.
    
    ```
    jsvar x=1;var x=2;// OK, same x
    ```
    
- **`let` then `let` (same scope):** Not allowed → `SyntaxError`.
    
    ```
    jslet y=1;let y=2;// SyntaxError: Identifier 'y' has already been declared
    ```
    
- **`var` then `let` in a nested block:** Allowed, because `let` is block-scoped and creates a new binding inside the block.
    
    ```
    jsvar a=1;{let a=2;// new 'a' inside this block only}
    ```
    
- **`let` then `var` in a nested block:** Also allowed, because the `var` is in a different (inner) block, but note `var` is function-scoped, so it can affect the outer function scope.
    
    ```
    jslet b=1;{var b=2;// still same 'b' in function/global scope, can cause conflicts}
    ```
    

Rule of thumb: avoid mixing `var` and `let`/`const` with the same name.

---

# 8. Why does this code throw, and how would you fix it without changing the `const`?

```
jsconst config={apiUrl:"https://api.example.com"};config={apiUrl:"https://new-api.example.com"};// ?
```

This throws `TypeError: Assignment to constant variable.` because `config` is a **constant binding**; you cannot reassign it to a new object.[iangabaraev](https://iangabaraev.com/learn/full-stack-interview-prep/)

**What you *can* do:** mutate the object’s properties.

```
jsconfig.apiUrl="https://new-api.example.com";// ✅ OK
```

`const` stops reassignment of the variable, not mutation of the object.[iangabaraev](https://iangabaraev.com/learn/full-stack-interview-prep/)

---

# 9. Explain the difference between “immutable binding” and “immutable value” in the context of `const`.

- **Immutable binding** (`const`): The variable’s **reference** cannot change. You cannot assign a new value to that variable.stackinterview+1
- **Immutable value**: The actual data cannot change. Primitives like numbers are inherently immutable, but objects/arrays are **mutable** unless you freeze them.

**Primitive example:**

```
jsconst num=5;num=10;// TypeError: cannot reassign
```

Here both the binding and the value are effectively immutable (you can’t change `5` anyway).[stackinterview](https://stackinterview.dev/guides/javascript-interview-questions-2026)

**Object example:**

```
jsconst obj={a:1};obj.a=2;// ✅ allowed (object is mutable)obj={};// ❌ TypeError (binding is immutable)
```

`const` gives you an immutable binding to a mutable value.stackinterview+1

---

# 10. What is the effect of declaring a variable with `var` at the top level of a script vs inside a function?

- **Top-level `var` in a script (browser):** Creates a property on the global object (`window`).
    
    ```
    jsvar x=1;console.log(window.x);// 1
    ```
    
- **`var` inside a function:** The variable is local to that function and not on `window`.

**`let`/`const` at top level:**

- They are **global to the module/script**, but **do not** create properties on `window`.
    
    ```
    jslet y=2;console.log(window.y);// undefined
    ```
    

This makes `let`/`const` safer for global variables.

---

# 11. Predict the output:

```
jsconsole.log(a);console.log(b);console.log(c);var a=1;let b=2;const c=3;
```

**Output:**

```
textundefinedReferenceError: Cannot access 'b' before initializationReferenceError: Cannot access 'c' before initialization
```

**Why?**

- `var a` is hoisted and initialized to `undefined`, so `console.log(a)` → `undefined`.[stackinterview](https://stackinterview.dev/guides/javascript-interview-questions-2026)
- `let b` and `const c` are hoisted but in **TDZ** until their declaration lines. Accessing them before that throws `ReferenceError`.[stackinterview](https://stackinterview.dev/guides/javascript-interview-questions-2026)

---

# 12. How does strict mode change the behavior of assigning to an undeclared variable?

**Without strict mode:**

```
jsfunctionf(){  x=10;// creates global x}f();console.log(x);// 10
```

Assigning to `x` without declaring it creates a **global variable** (bad practice).

**With strict mode:**

```
js"use strict";functionf(){  x=10;// ReferenceError: x is not defined}f();
```

Now it throws `ReferenceError` instead of creating a global. This helps catch typos and accidental globals.

---

# 13. Can `let` or `const` be used to avoid the classic IIFE pattern that was needed with `var`?

Yes. Before ES6, people used IIFEs (Immediately Invoked Function Expressions) to create block-like scope with `var`.

**Old `var` + IIFE pattern:**

```
jsfor(var i=0; i<3; i++){(function(j){setTimeout(()=> console.log(j),100);})(i);}// logs 0, 1, 2
```

The IIFE creates a new scope so each callback gets its own `j`.dev+1

**Modern `let` version (no IIFE needed):**

```
jsfor(let i=0; i<3; i++){setTimeout(()=> console.log(i),100);}// logs 0, 1, 2
```

`let` gives block scope and a new binding per iteration, so no IIFE is needed.scrimba+2

---

# 14. What happens in this code and why?

```
js{  console.log(x);let x=10;}
```

This throws: `ReferenceError: Cannot access 'x' before initialization`.

**Why?**

Inside the block, `let x` is hoisted but in **TDZ** until `let x = 10;` runs. The `console.log(x)` is in TDZ, so it errors.

**If you move `console.log(x)` after the declaration:**

```
js{let x=10;  console.log(x);// 10}
```

Now it works, because `x` is initialized before use.

---

# 15. Design a small snippet where the same variable name exists in global scope, function scope, and block scope (with `let`). Show how shadowing works.

```
jslet x="global";functionouter(){let x="function";{let x="block";    console.log(x);// "block"}  console.log(x);// "function"}outer();console.log(x);// "global"
```

**Explanation:**

- The innermost `let x` (“block”) **shadows** the function and global `x` inside that block.
- Inside `outer` but outside the block, `x` refers to the function-level `x`.
- Outside `outer`, `x` refers to the global `x`.

This shows how JavaScript picks the nearest (innermost) declaration with that name.

# 🚀 **Follow @daily.debugging for complete frontend resources and interview preparation.**
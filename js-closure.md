# The Complete Guide of Scope and Closure

## 1. Global Scope

### 1.1 What is Global Scope in JavaScript?

Global Scope is the outermost scope in a program. Any variable declared here is accessible from anywhere in the code — inside functions, blocks, or nested scopes — unless shadowed by a local variable of the same name.

### 1.2 How do you create a global variable?

Declare a variable outside of any function or block, using `var`, `let`, `const`, or (in non-strict mode) simply by assigning to an undeclared name:

js

```jsx
let count = 10; // global variable
```

### 1.3 Can a function access a variable declared in the global scope?

Yes. Functions can read and modify global variables because of lexical scoping — inner scopes always have access to outer scopes.

### 1.4 What is the difference between a global variable and a local variable?

A global variable is declared outside any function/block and lives for the entire program's execution, accessible everywhere. A local variable is declared inside a function or block and only exists/accessible within that function or block.

### 1.5 What problems can too many global variables cause?

- Naming collisions between different parts of code or libraries
- Unintended overwrites since any code can modify them
- Harder debugging, since state changes could come from anywhere
- Memory isn't freed until the program ends
- Increased coupling, making code harder to test and maintain

## 2. Function Scope

### 2.1 What is Function Scope?

Function Scope means a variable declared inside a function is only accessible within that function — including any nested functions inside it — and not outside it.

### 2.2 Which variables are function-scoped in JavaScript?

Variables declared with `var` are function-scoped (not block-scoped).

### 2.3 Can a variable declared inside a function be accessed outside the function?

No. It exists only within the function's local scope and is destroyed once the function finishes executing (unless captured by a closure).

### 2.4 What happens if you try to access a function-scoped variable outside the function?

JavaScript throws a `ReferenceError` because the variable is not defined in that outer scope.

### 2.5 What is the difference between function scope and global scope?

Function scope limits variable access to within a single function, while global scope makes a variable accessible throughout the entire program.

## 3. Block Scope

### 3.1 What is Block Scope?

Block Scope means a variable is only accessible within the nearest enclosing pair of curly braces `{ }` — such as an `if` block, `for` loop, or standalone block.

### 3.2 Which keywords support block scope: var, let, or const?

`let` and `const` support block scope. `var` does not.

### 3.3 Is var block-scoped?

No, `var` is function-scoped (or global-scoped if declared outside a function), not block-scoped.

### 3.4 What happens when let is declared inside an if block?

The variable is only accessible within that `if` block. Trying to access it outside results in a `ReferenceError`.

js

```jsx
if (true) {  let x = 5;}console.log(x); // ReferenceError
```

### 3.5 What is the difference between var and let regarding scope?

`var` ignores block boundaries and is scoped to the nearest function (or global scope), while `let` respects block boundaries and is confined to the block it's declared in.

## 4. Lexical Scope

### 4.1 What is Lexical Scope?

Lexical Scope means the scope of a variable is determined by its physical location in the source code — where it's written — not by how or where the function is called.

### 4.2 How does JavaScript determine where a variable can be accessed?

JavaScript looks at the nesting structure of the code at the time it's written. Each function/block can access variables from its own scope and any enclosing (outer) scopes, following that fixed structure.

### 4.3 Can an inner function access variables from its outer function?

Yes. This is a direct result of lexical scoping — inner functions have access to their outer function's variables.

### 4.4 Can an outer function access variables declared inside an inner function?

No. Scope access only flows outward-to-inward, not inward-to-outward.

### 4.5 What is the relationship between Lexical Scope and Closures?

Lexical scope is the rule that determines *which* variables a function can see based on where it's defined. A closure is the *mechanism* that lets a function retain access to those lexically scoped variables even after the outer function has finished executing.

## 5. Closures

### 5.1 What is a Closure in JavaScript?

A closure is a function that retains access to variables from its outer (enclosing) lexical scope, even after that outer function has returned/finished executing.

### 5.2 How is a Closure created?

A closure is created automatically whenever a function is defined inside another function, and the inner function references variables from the outer function.

js

```jsx
function outer() {  let count = 0;  return function inner() {    count++;    return count;  };}
```

### 5.3 Why can an inner function remember variables from its outer function?

Because the inner function keeps a reference to its outer function's scope (not just a copy of the values), JavaScript's garbage collector doesn't free that scope as long as the inner function still exists.

### 5.4 What are some real-world uses of Closures?

- Data privacy/encapsulation (private variables via module pattern)
- Function factories (creating specialized functions from a general one)
- Memoization/caching results
- Event handlers and callbacks that need to remember state
- `setTimeout`/`setInterval` callbacks retaining context

### 5.5 What is the difference between Lexical Scope and Closure?

Lexical scope is the *rule* — defined by where code is physically written — that determines variable visibility. A closure is the actual *function object* that uses that rule to keep variables alive and accessible beyond their normal lifetime.

![1.png](The%20Complete%20Guide%20of%20Scope%20and%20Closure/1.png)

![2.png](The%20Complete%20Guide%20of%20Scope%20and%20Closure/2.png)

![3.png](The%20Complete%20Guide%20of%20Scope%20and%20Closure/3.png)

![4.png](The%20Complete%20Guide%20of%20Scope%20and%20Closure/4.png)

![5.png](The%20Complete%20Guide%20of%20Scope%20and%20Closure/5.png)

![6.png](The%20Complete%20Guide%20of%20Scope%20and%20Closure/6.png)

![7.png](The%20Complete%20Guide%20of%20Scope%20and%20Closure/7.png)

![8.png](The%20Complete%20Guide%20of%20Scope%20and%20Closure/8.png)

![9.png](The%20Complete%20Guide%20of%20Scope%20and%20Closure/9.png)

![10.png](The%20Complete%20Guide%20of%20Scope%20and%20Closure/10.png)

# **JavaScript  Scope and Closures  — Intermediate Questions with Answers**

## 1. Scope

### 1. What happens when JavaScript cannot find a variable in the current scope?

JavaScript looks up the **scope chain** — it checks the enclosing (parent) scope, then that scope's parent, and so on until it reaches the global scope. If the variable isn't found anywhere in the chain, it throws a `ReferenceError`.

### 2. Explain the Scope Chain with an example.

The scope chain is the ordered list of scopes JavaScript searches through — from innermost to outermost — when resolving a variable.

js

```jsx
let a = 'global';function outer() {  let b = 'outer';  function inner() {    let c = 'inner';    console.log(a, b, c); // 'global' 'outer' 'inner'  }  inner();}outer();
```

Here, `inner()` can access `c` (its own), `b` (from `outer`), and `a` (from global) — each lookup walks up the chain.

### 3. How does JavaScript resolve a variable name?

It starts at the scope where the variable is referenced, checks if it's declared there, and if not, moves up to the next outer scope (following lexical/static structure, not the call stack), repeating until found or the global scope is exhausted.

### 4. What is the difference between Lexical Scope and Scope Chain?

Lexical Scope is the *rule* — scope is fixed by where code is physically written. The Scope Chain is the *structure/mechanism* built from that rule: the actual ordered sequence of scopes JavaScript traverses to resolve a variable.

### 5. Can two different scopes have variables with the same name?

Yes. Each scope maintains its own variable bindings, so the same name can exist independently in multiple scopes without conflict — the inner one simply shadows the outer one when accessed from inside.

### 6. What is variable shadowing?

Shadowing happens when a variable declared in an inner scope has the same name as one in an outer scope. Inside the inner scope, references to that name resolve to the inner variable, "hiding" the outer one.

js

```jsx
let x = 'outer';function test() {  let x = 'inner';  console.log(x); // 'inner'}
```

### 7. What is the difference between shadowing and redeclaration?

Shadowing occurs **across different scopes** — an inner-scope variable temporarily hides an outer-scope variable of the same name, and both still exist. Redeclaration happens **within the same scope**, declaring a variable with a name already used there — which is a `SyntaxError` for `let`/`const`, but allowed (and harmless) for `var`.

## 2. Global & Function Scope

### 8. What happens when you declare `var`, `let`, and `const` in the global scope?

- `var` creates a property on the global object (`window` in browsers) and is hoisted with an initial value of `undefined`.
- `let` and `const` create global bindings that are hoisted but stay in the "temporal dead zone" until their declaration line runs — they are **not** attached to the global object.

### 9. What is the difference between a global variable declared with `var` and one declared with `let`?

A `var` global becomes an accessible property of the global object (e.g. `window.x`), can be redeclared, and is hoisted with `undefined`. A `let` global is not attached to the global object, cannot be redeclared in the same scope, and is inaccessible before its declaration line (temporal dead zone).

### 10. Can a function access a variable from its parent function?

Yes, via lexical scoping — a nested function can read (and modify, if mutable) any variable declared in its parent function's scope.

### 11. Can the parent function access a variable declared inside its child function?

No. Scope only flows outward-to-inward. A variable declared inside a child function is private to that function and invisible to the parent.

### 12. What happens when a local variable has the same name as a global variable?

The local variable shadows the global one within that local scope. Any reference to the name inside the function uses the local variable; the global variable remains unchanged and is only accessible again once the function exits (or from outside the function).

## 3. Block Scope

### 13. Why is `var` not block-scoped?

By design, `var` was scoped to functions (or global scope) from JavaScript's earliest versions. It ignores block boundaries like `{}`, `if`, and `for` — it only respects function boundaries.

### 14. Why are `let` and `const` block-scoped?

`let` and `const` were introduced in ES6 specifically to give developers block-level scoping, tying the variable's lifetime and visibility to the nearest enclosing `{}` rather than the nearest function.

### 15. What happens when `let` or `const` is declared inside an `if` block?

The variable is confined to that `if` block. It cannot be accessed before its declaration (temporal dead zone) or after the block ends — attempting either throws a `ReferenceError`.

### 16. Can a `for` loop create a separate scope?

Yes. With `let`/`const`, each iteration of a `for` loop gets its own fresh block scope for the loop variable, distinct from the scope outside the loop.

### 17. Why does `let` behave differently from `var` inside loops?

With `var`, there's a single shared variable across all iterations (function-scoped), so closures created inside the loop all reference the same final value. With `let`, each iteration creates a **new binding**, so closures capture the value specific to that iteration.

js

```jsx
for (let i = 0; i < 3; i++) {  setTimeout(() => console.log(i)); // 0, 1, 2}for (var j = 0; j < 3; j++) {  setTimeout(() => console.log(j)); // 3, 3, 3}
```

## 4. Lexical Scope

### 18. What does "lexical" mean in Lexical Scope?

"Lexical" refers to the source code text itself — specifically, where things are physically written. Lexical scope means scope is determined by the code's written structure, not by runtime behavior.

### 19. Is Lexical Scope determined at runtime or when the code is written?

It's determined when the code is **written** (at parse time), based on nesting structure — not at runtime, and not by how or where a function is called.

### 20. Can a function access variables based on where it is called?

No. JavaScript uses lexical (static) scoping, not dynamic scoping — the *call site* has no bearing on which variables a function can see.

### 21. Can a function access variables based on where it is defined?

Yes. A function's accessible variables are fixed by its **definition location** in the source code — it can access its own scope plus every enclosing scope at the point it was defined.

### 22. Explain Lexical Scope using nested functions.

js

```jsx
function grandparent() {  let a = 1;  function parent() {    let b = 2;    function child() {      let c = 3;      console.log(a, b, c); // 1 2 3 — all visible    }    child();  }  parent();}
```

`child` can see `a`, `b`, and `c` because it's lexically nested inside `parent` and `grandparent` — its scope is fixed by where it's written, not by when/how it's invoked.

## 5. Closures

### 23. How does a Closure work internally?

When a function is created, it keeps an internal reference to its lexical environment (the scope it was defined in). Even after the outer function returns, that environment isn't garbage-collected as long as the inner function still holds a reference to it — the inner function "closes over" those variables.

### 24. Why doesn't a variable disappear when the outer function finishes executing?

Normally a function's local variables are destroyed when it returns. But if an inner function references those variables and is itself returned/retained, JavaScript keeps that variable environment alive in memory because it's still reachable through the inner function's closure.

### 25. Can a Closure access and modify variables from its outer scope?

Yes. A closure holds a live reference (not a copy) to the outer variables, so it can both read and reassign them, and those changes persist across calls.

### 26. Can multiple functions share the same Closure?

Yes, if they're created within the same outer function call, they share the same closed-over environment.

js

```jsx
function outer() {  let count = 0;  return {    increment: () => ++count,    getCount: () => count,  };}
```

Here `increment` and `getCount` share the same `count` variable.

### 27. What is a practical use case of Closures?

Creating counters, memoized/cached functions, event handler callbacks that need to remember state, and function factories (e.g. a function that generates specialized functions, like `multiplyBy(5)`).

### 28. How can Closures be used for data privacy?

Variables declared inside a function are inaccessible from outside, but an inner returned function can still interact with them — giving controlled, private access without exposing the variable directly (the "module pattern").

js

```jsx
function createBankAccount(balance) {  return {    deposit: (amt) => (balance += amt),    getBalance: () => balance,  };}
```

`balance` can't be accessed or modified except through the exposed methods.

### 29. What are the advantages of using Closures?

- Encapsulation/data privacy without classes
- Preserving state between function calls without global variables
- Enabling function factories and currying
- Supporting memoization/caching
- Keeping code modular and avoiding global namespace pollution

### 30. Can excessive use of Closures cause memory-related problems?

Yes. Since closures keep their outer variables alive as long as the inner function exists, holding onto many closures (especially ones referencing large objects/DOM nodes) can prevent garbage collection and lead to memory bloat or leaks if not cleaned up properly.

## 6. Output-Based Questions 🔥

### 31. What will be the output?

js

```jsx
let x = 10;function outer() {  let x = 20;  function inner() {    console.log(x);  }  inner();}outer();
```

**Output: `20`**

`inner` is lexically defined inside `outer`, so it resolves `x` to the nearest enclosing scope first — `outer`'s `x = 20` — never reaching the global `x = 10`.

### 32. What will be the output?

js

```jsx
let x = 10;function outer() {  let x = 20;  return function () {    console.log(x);  };}const fn = outer();fn();
```

**Output: `20`**

Even though `outer()` has already finished executing by the time `fn()` is called, the returned function forms a closure over `outer`'s scope, retaining access to `x = 20`.

### 33. What will be the output?

js

```jsx
var x = 1;function test() {  var x = 2;  console.log(x);}test();console.log(x);
```

**Output:**

```
2
1
```

`var x` inside `test()` is a separate, function-scoped variable that shadows the global `x`. It doesn't affect the global `x`, so logging it outside still shows `1`.

### 34. What will be the output?

js

```jsx
function counter() {  let count = 0;  return function () {    count++;    console.log(count);  };}const c1 = counter();c1();c1();
```

**Output:**

```
1
2
```

`c1` is a closure over the same `count` variable created in that one call to `counter()`. Each call to `c1()` increments and remembers the same persistent `count`.

### 35. What will be the output?

js

```jsx
function createCounter() {  let count = 0;  return () => ++count;}const a = createCounter();const b = createCounter();console.log(a());console.log(a());console.log(b());
```

**Output:**

```
1
2
1
```

`a` and `b` come from **separate calls** to `createCounter()`, so each gets its own independent `count` closure. `a()` incrementing twice doesn't affect `b`'s separate `count`, which starts fresh at `0` → `1`.

# **JavaScript  Scope and Closures  — Advanced Questions with Answers**

## 1. Scope & Scope Chain

### 1. How does the JavaScript engine resolve a variable through the scope chain?

When code references a variable, the engine starts at the current lexical environment and checks its Environment Record. If not found, it follows the environment's internal link to its outer (parent) environment, and repeats this walk until the variable is found or the global environment is exhausted (throwing a `ReferenceError`).

### 2. What is the difference between Lexical Environment and Execution Context?

An **Execution Context** is the broader runtime container created whenever code runs (global, function, or eval) — it holds the Lexical Environment, Variable Environment, `this` binding, and more. A **Lexical Environment** is just one part of that context: the structure that maps identifiers to variable bindings and links to its outer environment.

### 3. What is an Environment Record?

It's the internal data structure inside a Lexical Environment that actually stores the variable and function bindings declared in that scope (e.g. `{ x: 10, count: 0 }`) along with their mutability.

### 4. How are nested lexical environments represented internally?

As a chain of Lexical Environment objects, each holding an Environment Record plus a reference to its **outer environment**. This linked structure is exactly what forms the scope chain — nested functions' environments point back to the environment they were defined within.

### 5. What happens when a variable exists in multiple levels of the scope chain?

The engine resolves to the **nearest** one — the first match found while walking from the innermost scope outward. Outer declarations of the same name are shadowed and never reached from the inner scope.

### 6. How does variable shadowing affect scope resolution?

Shadowing stops the scope chain lookup early — once a matching name is found in a closer scope, the engine uses that binding and never continues searching outer scopes, even if they also declare a variable with the same name.

### 7. Can a function's scope change after it has been created?

No. A function's lexical scope is fixed permanently at the moment it's defined, based on its position in the source code. Calling the function from a different location, or reassigning variables it closes over, does not alter *which* scopes it can see — only their values.

### 8. Why doesn't JavaScript use dynamic scoping?

Dynamic scoping (resolving variables based on the call stack/caller's scope) makes code unpredictable and hard to reason about, since a function's behavior would depend on where it's called from rather than where it's written. JavaScript (like most modern languages) uses lexical scoping so a function's variable access is fixed and predictable purely from reading its definition.

## 2. Closures — Deep Understanding

### 9. What exactly does a Closure contain?

A closure consists of a function paired with a reference to the lexical environment(s) in which it was defined — giving it access to every variable in scope at its creation point, not just the immediate one.

### 10. Does a Closure store a copy of the outer variables or a reference to them?

A **reference**, not a copy. This is why a closure sees updated values if the outer variable changes after the closure is created.

### 11. What happens to the outer function's variables after the outer function finishes execution?

Normally they'd be destroyed. But if an inner function (closure) still references them, the JavaScript engine keeps that Lexical Environment alive in memory instead of garbage-collecting it, because it's still reachable.

### 12. Can a Closure access variables that were declared after the inner function?

Yes, as long as they're in the same enclosing scope and declared before the closure is actually *invoked* (not before it's *defined*). Since it holds a live reference to the environment, any variable added to that environment later is visible too — subject to the temporal dead zone for `let`/`const`.

### 13. Can multiple Closures share the same lexical environment?

Yes — if multiple inner functions are created within the same execution of an outer function, they all close over the exact same Environment Record, and any of them can read or modify shared variables.

### 14. What happens when multiple functions modify the same closed-over variable?

Since they share a reference to the same Environment Record, any modification by one function is immediately visible to the others — there's a single shared piece of state, not independent copies.

### 15. Can a Closure access variables from multiple outer scopes?

Yes. A closure retains links through the entire chain of lexical environments it was nested in at creation time — it can access variables from its immediate parent, grandparent, and so on, up to the global scope.

### 16. How does a Closure maintain state between function calls?

Because the closure holds a persistent reference to its Environment Record (rather than re-creating it), variables inside that environment retain their values between separate invocations of the closure.

### 17. Can a Closure exist without an outer function?

Technically every function forms a closure over its containing scope, even the global scope — but the "outer function" in question doesn't need to be a *named* function. It could be a block, a module, or an IIFE; what matters is that there's an enclosing lexical environment, not specifically a function keyword.

### 18. What is the relationship between Closures and Garbage Collection?

Garbage collection normally reclaims memory for variables no longer reachable. Closures keep their outer environment reachable (via a live reference) even after the outer function returns, which **prevents** that environment from being garbage collected until every closure referencing it is itself no longer reachable.

## 3. Closures & Memory

### 19. How can Closures cause memory leaks?

If a closure retains a reference to a large object, DOM node, or environment that's never released (e.g. stored in a long-lived array, event listener, or global variable), that memory can't be reclaimed even though it's no longer actually needed — leading to a buildup over time.

### 20. When can a closed-over variable be garbage collected?

Once **no closures or references** point to the Lexical Environment containing it anymore — i.e., every function that could access it has itself become unreachable (e.g., removed from the DOM, cleared from arrays, or gone out of scope).

### 21. What happens if a Closure keeps a reference to a large object?

The object stays in memory for as long as the closure exists and is reachable, even if the rest of the program no longer needs it — potentially wasting significant memory, especially if many such closures accumulate.

### 22. How can you prevent unnecessary memory retention caused by Closures?

- Avoid capturing large objects in closures you don't need long-term
- Explicitly set references to `null` when done with them
- Remove event listeners when elements/components are destroyed
- Limit closure lifetime by not storing closures in long-lived global structures unnecessarily
- Use `WeakMap`/`WeakRef` when appropriate for object references

### 23. Why can event listeners sometimes cause memory leaks involving Closures?

An event listener callback is often a closure over variables (including DOM elements) from its enclosing scope. If the listener is never removed (`removeEventListener`), the browser can't garbage-collect the associated DOM nodes or captured variables — even after the element is no longer visibly used — because the still-active listener keeps them reachable.

## 4. Closures & Loops 🔥

### 24. Why does `var` behave differently from `let` inside loops with Closures?

`var` is function-scoped, so there's only **one** shared binding for the loop variable across all iterations — every closure created inside the loop ends up referencing that same final value. `let` creates a **fresh binding per iteration**, so each closure captures its own iteration-specific value.

### 25. Explain the classic `var` inside `setTimeout` loop problem.

js

```jsx
for (var i = 0; i < 3; i++) {  setTimeout(() => console.log(i), 1000);}
```

Because `var i` is a single shared variable across the whole loop, by the time the `setTimeout` callbacks actually run (after the loop has finished), `i` has already reached `3`. All three callbacks log `3`, not `0, 1, 2` as might be expected.

### 26. How can you fix the `var` + Closure problem using `let`?

Simply replace `var` with `let`:

js

```jsx
for (let i = 0; i < 3; i++) {  setTimeout(() => console.log(i), 1000);}
```

`let` creates a new binding for `i` on each iteration, so each callback closes over its own separate value — logging `0, 1, 2`.

### 27. How can an IIFE solve the `var` loop problem?

By wrapping the loop body in an Immediately Invoked Function Expression, you create a new function scope per iteration that captures the current value of `i` as a parameter:

js

```jsx
for (var i = 0; i < 3; i++) {  (function (j) {    setTimeout(() => console.log(j), 1000);  })(i);}
```

Each IIFE call gets its own `j`, solving the shared-variable problem without needing `let`.

### 28. Why does `let` create a new binding for each loop iteration?

This is a specific behavior defined in the ECMAScript spec for `for` loops using `let`: at the start of each iteration, the engine creates a fresh copy of the loop variable's binding (initialized from the previous iteration's value), effectively giving each pass through the loop its own independent variable.

## 5. Closures & Async JavaScript

### 29. How do Closures work with `setTimeout()`?

The callback passed to `setTimeout` is itself a closure — it retains access to variables from its surrounding scope at the time it was defined, even though it doesn't execute until later (after the enclosing function has already returned).

### 30. How do Closures work with Promises?

`.then()`/`.catch()` callbacks are closures over the scope in which the Promise chain was written, letting them access outer variables when they eventually run — regardless of how much time passes before the promise resolves/rejects.

### 31. How do Closures interact with `async/await`?

The code after an `await` runs as a continuation that closes over the same local variables as the rest of the `async` function — it behaves like a closure spanning the pause, referencing outer/local variables normally even though execution suspends at each `await`.

### 32. What happens when an asynchronous callback accesses a variable from its outer scope?

It reads whatever the **current value** of that variable is at the moment the callback actually executes — not the value at the time the callback was defined — because it holds a live reference to the variable's binding, not a snapshot.

### 33. Why can changing a variable affect the value observed by an asynchronous callback?

Because the callback closes over the variable itself, not a copy of its value. If the variable is reassigned between when the callback is created and when it runs, the callback will see the updated value at execution time (this is exactly the root cause of the classic `var` loop bug above).

## 6. Advanced Output Questions 🔥

### 34. What is the output and why?

js

```jsx
for (var i = 0; i < 3; i++) {  setTimeout(() => {    console.log(i);  }, 1000);}
```

**Output:**

```
3
3
3
```

`var i` is function/global-scoped, so all three `setTimeout` callbacks share the exact same `i`. By the time they run (1 second later, after the loop has already finished), `i` equals `3`.

### 35. What is the output?

js

```jsx
for (let i = 0; i < 3; i++) {  setTimeout(() => {    console.log(i);  }, 1000);}
```

**Output:**

```
0
1
2
```

`let` creates a new binding of `i` for each iteration, so each callback closes over its own separate value.

### 36. What is the output?

js

```jsx
function outer() {  let x = 10;  return function inner() {    x++;    return x;  };}const a = outer();const b = outer();console.log(a());console.log(a());console.log(b());
```

**Output:**

```
11
12
11
```

`a` and `b` come from separate calls to `outer()`, so each has its own independent `x`. Calling `a()` twice increments `a`'s private `x` from 10 → 11 → 12, while `b`'s `x` remains untouched, starting fresh at 10 → 11.

### 37. What is the output?

js

```jsx
function outer() {  let count = 0;  function a() {    count++;    console.log(count);  }  function b() {    count++;    console.log(count);  }  return { a, b };}const obj = outer();obj.a();obj.b();obj.a();
```

**Output:**

```
1
2
3
```

`a` and `b` are both created within the same call to `outer()`, so they **share** the same closed-over `count` variable. Each call — regardless of which function — increments the same shared counter.

### 38. What is the output?

js

```jsx
let x = 10;function outer() {  let x = 20;  function inner() {    console.log(x);  }  return inner;}const fn = outer();x = 30;fn();
```

**Output: `20`**

`inner` closes over `outer`'s local `x` (20), which is a completely separate variable from the global `x`. Reassigning the *global* `x` to `30` has no effect on `outer`'s private `x`, so `fn()` still logs `20`.

## 7. Expert-Level Conceptual Questions

### 39. Explain how Closures, Lexical Scope, and Execution Context are connected.

Lexical Scope defines *which* variables a function can theoretically see, based on where it's written in the code. An Execution Context is created each time that function actually runs, containing its Lexical Environment. A Closure is what happens when a function retains a reference to the Lexical Environment of an outer Execution Context even after that outer context has been popped off the call stack — bridging "scope rules" with "runtime memory" so the function keeps working correctly later.

### 40. Why is a Closure considered a combination of a function and its surrounding lexical environment?

Because a closure isn't just executable code — it's a bundle of the function's logic plus a live, persistent reference to every variable binding in the scopes where it was defined. Without that captured environment, the function would have no idea what its free (non-local) variables refer to.

### 41. How does the JavaScript engine keep closed-over variables alive?

Instead of destroying a function's Lexical Environment when it returns, the engine checks whether any inner function still references that environment. If so, the environment is kept in memory (not garbage collected), because it remains reachable through the closure's internal `[[Environment]]` reference.

### 42. What is the difference between Closure and Scope?

Scope is a *static/conceptual* rule about variable visibility, fixed by code structure. A Closure is a *concrete runtime object* — an actual function value carrying a live reference to its defining environment — that exploits scope rules to keep variables alive and accessible beyond their normal lifetime.

### 43. Is every function a Closure? Explain with examples.

In a strict technical sense, yes — every function forms a closure over its lexical environment (even if that's just the global scope), because every function retains a link to where it was defined. However, colloquially "closure" is usually reserved for cases where this matters practically — i.e., when a function is used *outside* the scope it was defined in and still accesses outer variables:

js

```jsx
function greet() {  console.log('hi'); // technically closes over global scope, but trivial}function makeGreeter(name) {  return function () {    console.log(`hi${name}`); // meaningful closure — captures `name`  };}
```

### 44. Can a Closure capture variables that are no longer directly used?

Yes. In many engines, if a variable is declared in the same scope as one that *is* used by the closure, the entire Environment Record may be retained together — meaning unused variables in that scope can also stay in memory as an unintended side effect, potentially contributing to memory bloat.

### 45. How do Closures enable the Module Pattern?

The Module Pattern wraps related variables and functions inside an IIFE (or module), exposing only selected functions publicly while keeping other variables private via closures:

js

```jsx
const CounterModule = (function () {  let count = 0;  return {    increment: () => ++count,    getCount: () => count,  };})();
```

`count` is inaccessible from outside except through the exposed methods, which close over it.

### 46. How can Closures be used to implement private variables?

By declaring the variable inside a function and only exposing getter/setter functions that close over it, rather than the variable itself — external code has no direct reference to the variable and can only interact with it through the controlled interface.

### 47. How would you implement a private counter using Closure without using a class?

js

```jsx
function createCounter(initial = 0) {  let count = initial;  return {    increment: () => ++count,    decrement: () => --count,    getValue: () => count,  };}const counter = createCounter();counter.increment(); // 1counter.increment(); // 2counter.getValue();  // 2
```

`count` is fully private — there's no way to access or modify it except through the exposed methods.

### 48. What are the performance considerations of using many Closures?

- Each closure retains a reference to its outer environment, so many long-lived closures can increase memory usage (preventing garbage collection of otherwise-unused scopes)
- Deep/complex scope chains can slightly slow variable lookup, since the engine may need to traverse multiple levels
- Creating large numbers of closures repeatedly (e.g., inside hot loops) can add overhead from repeated function/environment allocation
- In most typical applications this cost is negligible, but it matters in performance-critical or memory-constrained code (e.g., handling thousands of DOM event listeners or large data-processing loops)

# 🚀 **Follow @daily.debugging for complete frontend resources and interview preparation.**
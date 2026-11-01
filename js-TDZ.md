# The Complete of Guide of Temporal Dead Zone(TDZ)

## 1. What is the Temporal Dead Zone (TDZ) in JavaScript?

The TDZ is the period between the start of a block/scope and the point where a `let` or `const` variable is actually declared in the code. During this period, the variable exists in memory but cannot be accessed. Trying to use it throws a `ReferenceError`.

## 2. Which JavaScript keywords are affected by the Temporal Dead Zone?

`let`, `const`, and `class` declarations are all affected by the TDZ. `var` is not.

## 3. Does the Temporal Dead Zone apply to `var`? Why or why not?

No. `var` declarations are hoisted and automatically initialized with `undefined` at the top of their scope. So even before the actual line of declaration, the variable already has a usable value (`undefined`) instead of being in a "dead" state. That's why `var` has no TDZ.

## 4. Are `let` and `const` hoisted in JavaScript?

Yes. Their declarations are hoisted to the top of the block scope, just like `var`. What's different is that they are *not* initialized during hoisting — `var` gets `undefined`, but `let`/`const` get nothing until their actual declaration line runs.

## 5. If `let` and `const` are hoisted, why can't we access them before their declaration?

Because hoisting only reserves the variable's name in scope — it doesn't give it a value. Until the line with the actual declaration executes, the variable stays in an "uninitialized" state. JavaScript deliberately throws an error if you try to read it in this state, which is exactly what creates the TDZ.

## 6. When does the Temporal Dead Zone start?

It starts at the beginning of the enclosing block/scope (e.g., when the `{ }` block begins execution).

## 7. When does the Temporal Dead Zone end?

It ends the moment the `let`/`const` declaration line is actually executed and the variable is assigned an initial value (even `undefined` for `let x;`).

## 8. What happens when you access a `let` variable inside its TDZ?

JavaScript throws a `ReferenceError: Cannot access 'x' before initialization`.

## 9. What error do you get when accessing a `const` variable before initialization?

The same error type: `ReferenceError: Cannot access 'x' before initialization`. `let` and `const` behave identically with respect to the TDZ — the only extra rule for `const` is that once initialized, it can't be reassigned.

## 10. What is the difference between declaration and initialization?

- **Declaration**: telling the engine "this variable name exists in this scope" (e.g., `let x`).
- **Initialization**: actually assigning it a value in memory (e.g., `x = 10`, or even `x = undefined`).

For `var`, declaration and initialization (to `undefined`) happen together during hoisting. For `let`/`const`, declaration happens during hoisting, but initialization happens only when the code reaches that line — the gap between the two is the TDZ.

## 11. What is the difference between TDZ and hoisting?

- **Hoisting** is the general mechanism where variable/function declarations are moved to the top of their scope during the compile phase.
- **TDZ** is a *consequence* of hoisting specifically for `let`/`const`: because they're hoisted but not initialized, there's a "dead zone" window where accessing them is illegal. `var` is hoisted too, but since it's auto-initialized, it has no TDZ. So TDZ isn't a separate feature — it's a side effect of how `let`/`const` hoisting works differently from `var`.

## 12. Why does this code throw an error?

No code snippet was included in your message, so I can't point to a specific line. But the general pattern that causes this error looks like:

js

```jsx
console.log(x); // ReferenceError: Cannot access 'x' before initializationlet x = 5;
```

This throws because `x` is hoisted to the top of the scope but stays uninitialized until `let x = 5;` runs. The `console.log(x)` line executes while `x` is still in the TDZ, so accessing it triggers the error. If you paste your actual code, I can explain exactly why it fails.

![1.png](The%20Complete%20of%20Guide%20of%20Temporal%20Dead%20Zone(TDZ)/1.png)

![2.png](The%20Complete%20of%20Guide%20of%20Temporal%20Dead%20Zone(TDZ)/2.png)

![3.png](The%20Complete%20of%20Guide%20of%20Temporal%20Dead%20Zone(TDZ)/3.png)

![4.png](The%20Complete%20of%20Guide%20of%20Temporal%20Dead%20Zone(TDZ)/4.png)

![5.png](The%20Complete%20of%20Guide%20of%20Temporal%20Dead%20Zone(TDZ)/5.png)

![6.png](The%20Complete%20of%20Guide%20of%20Temporal%20Dead%20Zone(TDZ)/6.png)

![7.png](The%20Complete%20of%20Guide%20of%20Temporal%20Dead%20Zone(TDZ)/7.png)

![8.png](The%20Complete%20of%20Guide%20of%20Temporal%20Dead%20Zone(TDZ)/8.png)

# **JavaScript  TDZ  — Intermediate Questions with Answers**

## 1. Why does this code throw a `ReferenceError` even though `x` exists in the outer scope?

js

```jsx
let x = 10;{  console.log(x);  let x = 20;}
```

This throws `ReferenceError: Cannot access 'x' before initialization`.

Even though an outer `x` exists, JavaScript uses **lexical (block) scoping**. Because the inner block has its own `let x = 20;`, the entire block treats `x` as belonging to that inner scope from the very start of the block — this is sometimes called "shadowing." The inner `x` is hoisted to the top of the `{ }` block but stays uninitialized until `let x = 20;` runs. So `console.log(x)` inside the block refers to the **inner** `x`, which is still in its TDZ — it does *not* fall back to the outer `x`.

## 2. Where exactly does the TDZ begin and end for a `let` variable?

js

```jsx
{// ?  let name = "Rahul";// ?}
```

- **TDZ begins**: at the very start of the enclosing block `{`.
- **TDZ ends**: exactly at the line `let name = "Rahul";`, once that statement finishes executing and `name` is assigned a value.

So the first `// ?` (before the declaration) is inside the TDZ — accessing `name` there throws an error. The second `// ?` (after the declaration) is outside the TDZ — `name` is now safely usable.

## 3. What happens during the creation phase for `let`, `const`, and `var`?

js

```jsx
var → created + initializedlet → created + uninitializedconst → created + uninitialized
```

During the **creation phase** (before any code actually runs in a scope), the JS engine scans for all declarations:

- **`var`**: memory is allocated for it, and it is immediately initialized to `undefined`. This is why you can reference a `var` before its line and get `undefined` instead of an error.
- **`let`**: memory is allocated (the binding is "created"), but it is left **uninitialized** — it's in the TDZ. No value, not even `undefined`, is assigned yet.
- **`const`**: behaves exactly like `let` during creation — created but uninitialized, sitting in the TDZ until the declaration line runs.

The key distinction: "created" just means the engine knows the name exists in that scope. "Initialized" means it actually has a value. `var` gets both immediately; `let`/`const` only get "created" up front, and "initialized" later when their declaration line executes.

## 4. Why does `typeof` throw a `ReferenceError` in this example?

js

```jsx
console.log(typeof x);let x = 10;
```

Normally, `typeof someUndeclaredVariable` is safe and returns `"undefined"` without throwing — this is a special leniency of `typeof`. But here, `x` **is** declared in the current scope (via `let`), just later. Because `x` is hoisted and sits in the TDZ from the start of the scope, referencing it in *any* way — including through `typeof` — before its declaration triggers `ReferenceError: Cannot access 'x' before initialization`.

Compare with:

js

```jsx
console.log(typeof x);
```

If `x` is **never declared anywhere** in scope, `typeof x` simply returns `"undefined"` — no error. The difference: in the first case, `x` exists in the TDZ (dangerous to touch); in the second, `x` doesn't exist at all in any accessible scope (safe for `typeof` to report as `"undefined"`).

## 5. Does TDZ exist only when a variable is accessed before its declaration?

TDZ is **not about access at all** — it's about a **fixed zone in time and scope**, defined purely by the variable's position in the code. The TDZ exists for every `let`/`const`/`class` variable, whether or not you ever try to access it. It exists from the moment the block starts until the declaration line runs.

- If you never touch the variable during that window, nothing happens — the TDZ passes silently.
- If you *do* try to access it during that window, only then does the error surface.

So: TDZ is a property of **scope + code position** (it always exists structurally), while the `ReferenceError` is merely the **consequence** of accessing the variable while that zone is active. Access doesn't create the TDZ — it just reveals it.

## 6. What happens in this example?

js

```jsx
let x = 10;function test() {  console.log(x);  let x = 20;}test();
```

This throws `ReferenceError: Cannot access 'x' before initialization`.

**Why doesn't JavaScript use the outer `x`?** Because `test()` has its own `let x = 20;` declared inside it, that declaration is hoisted to the top of the function's scope. From the engine's perspective, `x` inside `test` refers to the *local* `x` throughout the entire function body — the outer `x = 10` is completely shadowed and never considered inside `test`. So `console.log(x)` tries to read the local `x`, which is still in its TDZ at that point, and throws.

## 7. What happens when a function is called before a `let` variable used inside it is initialized?

js

```jsx
function test() {  console.log(x);}test();let x = 100;
```

Step-by-step:

1. During the creation phase of the global scope, `x` (via `let`) is hoisted but left uninitialized — it enters the TDZ. `test` (function declaration) is also hoisted and fully initialized (functions are hoisted with their full body).
2. `test()` is called. Execution enters the function body.
3. Inside `test`, `console.log(x)` looks up `x`. Since `test` has no local `x`, it looks in the outer (global) scope via its closure.
4. At this point in time, the global `x` has **not yet** reached its declaration line (`let x = 100;` hasn't executed yet) — it's still in the TDZ.
5. Result: `ReferenceError: Cannot access 'x' before initialization`.

The key point: TDZ is about **when the code runs**, not where the function is *defined*. Since `test()` is invoked before `let x = 100;` executes, `x` is still dead at that moment.

## 8. Can a `let` variable be accessed before its declaration if the access happens inside another function?

js

```jsx
function test() {  console.log(x);}let x = 10;test();
```

Yes — this works fine and logs `10`.

**Why does this work while the previous example doesn't?** The difference is entirely about **execution timing**, not where `test` is defined relative to `x`. Here, `test()` is *called* only after `let x = 10;` has already executed. By the time the function body actually runs and tries to read `x`, the TDZ for `x` has already ended (it's initialized).

In Q7, `test()` was called *before* `let x = 100;` ran, so `x` was still in its TDZ at call-time. Here, the call happens *after* the declaration line, so there's no TDZ issue. Function bodies only care about the state of variables at the *moment they execute*, not at the moment they're defined.

## 9. How does lexical scope contribute to the Temporal Dead Zone?

js

```jsx
let a = 10;{  console.log(a);  let a = 20;}
```

This throws a `ReferenceError`.

Lexical scoping means variable resolution is based on **where a variable is declared in the source code structure** (nesting of blocks/functions), not on execution order or outer values. Because the inner `{ }` block declares its own `let a = 20;`, that block's `a` is a completely separate binding from the outer `a`. Due to lexical scoping rules, any reference to `a` *within that block* automatically resolves to the block's **own** `a` — never the outer one — for the entire block, from top to bottom.

This means the inner `a` shadows the outer one starting from the very first line of the block, entering the TDZ immediately. So `console.log(a)` inside the block tries to access the *shadowed, not-yet-initialized* inner `a`, causing the TDZ error — lexical scope is precisely what causes the lookup to stop at the inner `a` instead of "seeing through" to the outer one.

## 10. What is the difference between these two errors?

js

```jsx
console.log(x);let x = 10;
```

vs.

js

```jsx
console.log(y);
```

**First case**: `ReferenceError: Cannot access 'x' before initialization`. This is a **TDZ error**. `x` is a real, declared variable (via `let`) in this scope — the engine knows it exists (it was hoisted), but it hasn't been initialized yet at the point of access. The variable exists but is "dead."

**Second case**: `ReferenceError: y is not defined`. This is a **plain undeclared-variable error**. `y` was never declared anywhere in any accessible scope — the engine has no record of it at all, so there's no TDZ, no hoisting, nothing. It simply doesn't exist.

The distinction: "before initialization" means the variable is known but not ready. "Is not defined" means the variable was never declared in the first place. Same error type (`ReferenceError`), but different messages and different underlying causes.

## 11. What happens when `const` is declared but not initialized?

js

```jsx
const x;
```

This throws: `SyntaxError: Missing initializer in const declaration`.

This is **not** a TDZ error — it's a **syntax error**, caught at parse time, before the code even runs. `const` bindings are required by the language grammar to be initialized at the moment of declaration, since they can never be reassigned afterward. Writing `const x;` with no value is grammatically invalid JavaScript, so the engine rejects it before execution even begins — this happens earlier and is a different category of error than the runtime `ReferenceError` you get from TDZ violations.

## 12. How does TDZ work with default function parameters?

js

```jsx
function test(a = b, b = 10) {  console.log(a);}test();
```

This throws `ReferenceError: Cannot access 'b' before initialization`.

Function parameters are evaluated **left to right**, and each parameter is treated similarly to a `let` declaration within the function's parameter scope. When `test()` is called with no arguments:

1. `a = b` is evaluated first. Since no argument was passed, JS tries to evaluate the default value `b`.
2. But `b` is declared later (as the second parameter) and hasn't been initialized yet — it's still in the TDZ at this point, because parameter initialization happens in declaration order.
3. Accessing `b` while it's in this TDZ throws the error.

**Why does `b` cause a problem?** Because `a`'s default value tries to reference `b` *before* `b` has been assigned any value (even its own default of `10`). If the parameter order were reversed (`function test(b = 10, a = b)`), it would work fine, since `b` would already be initialized by the time `a`'s default is evaluated.

## 13. Can TDZ occur in a `for` loop?

js

```jsx
for (let i = 0; i < 3; i++) {  console.log(i);}
```

Yes, TDZ technically applies to `i` here too, but it resolves so early that it's invisible in normal use.

- `i` is declared with `let` in the loop's initializer, so it's hoisted and starts in the TDZ.
- The TDZ ends as soon as `let i = 0` executes — which happens immediately, before the condition check or loop body runs.
- By the time `console.log(i)` executes inside the loop body, `i` has long since been initialized (and even gets a **fresh binding per iteration** with `let`, which is why closures in loops work correctly with `let` but not `var`).

So there's no error here — the TDZ exists only for a brief instant before `let i = 0` runs, and normal loop execution never accesses `i` during that instant. TDZ *could* only surface if you somehow referenced `i` from an even earlier point (which isn't possible in this loop's structure).

## 14. What happens when `let` and `var` use the same variable name in nested scopes?

js

```jsx
var x = 10;{  console.log(x);  let x = 20;}
```

This throws `ReferenceError: Cannot access 'x' before initialization`.

Even though the outer `x` is a `var` (already initialized to `10`), the inner block declares its own `let x = 20;`. Due to lexical scoping and shadowing, the inner block's `x` (the `let` one) takes over the entire block from top to bottom — the outer `var x` is completely shadowed and invisible inside the block. Since the inner `x` is a `let` binding, it follows TDZ rules: it's hoisted but uninitialized until its declaration line runs. So `console.log(x)` at the top of the block tries to access this shadowed, not-yet-initialized `let x`, and the TDZ error fires — the `var`/`let` distinction outside doesn't matter; what matters is that a `let` declaration exists *somewhere* in that same block.

## 15. Explain this code step-by-step:

js

```jsx
let x = 10;{  console.log(x);  if (true) {    let x = 20;    console.log(x);  }}
```

This throws `ReferenceError: Cannot access 'x' before initialization` on the **first** `console.log(x)`.

Step-by-step:

1. Outer scope: `let x = 10;` runs, so the outer `x` is `10`.
2. Enters the `{ }` block. This block does **not** declare its own `x` directly — but it *contains* an `if` block that does declare `let x = 20;`. Each `{ }` creates its own scope, so the `if` block's `x` is scoped only to the `if` block, **not** to the outer `{ }` block.
3. So the first `console.log(x)` (inside the outer `{ }` block, but outside the `if` block) actually looks up the chain and finds the **outer** `x` (value `10`) — since the `if` block's `let x` hasn't shadowed this level.

# **JavaScript  TDZ  — Advanced Questions with Answers**

## 1. Nested Shadowing + TDZ

js

```jsx
let x = 10;{  let x = x + 1;  console.log(x);}
```

**Throws** `ReferenceError: Cannot access 'x' before initialization`.

Inside the block, `let x = x + 1;` declares a new, block-scoped `x`. Because of hoisting, this inner `x` is already "created" (but uninitialized) for the *entire* block, from the very first line. So when the right-hand side `x + 1` is evaluated, the `x` being read is the **inner** `x` (still in its TDZ) — not the outer `x = 10`. Reading a TDZ variable throws immediately, so the code never even reaches the assignment or the `console.log`.

## 2. Function Scope + TDZ

js

```jsx
let value = 100;function test() {  console.log(value);  let value = 200;}test();
```

**Throws** `ReferenceError: Cannot access 'value' before initialization`.

Inside `test()`, `let value = 200;` creates a local `value` that is hoisted to the top of the function body. This local declaration shadows the outer `value` for the *entire* function, so `console.log(value)` tries to read the **local** `value`, which is still uninitialized (in its TDZ) at that point — it never looks outward to the outer `value = 100`.

## 3. Closure Created During TDZ

js

```jsx
let getValue;{  getValue = () => value;  let value = 42;}console.log(getValue());
```

**Output: `42`** — no error.

Defining the arrow function `() => value` does **not** access `value` — it only creates a closure that *references* the variable, to be evaluated later when the function is actually called. So creating the closure while `value` is still in its TDZ is perfectly fine, since no read happens at that moment.

By the time `getValue()` is finally called (outside the block, on the last line), the block has already fully executed — including `let value = 42;` — so `value` has long since exited its TDZ and holds `42`. The closure captures the *binding* (not a snapshot), and by call-time that binding is initialized.

## 4. Closure Called Before Initialization

js

```jsx
let fn;{  fn = () => value;  fn();  let value = 10;}
```

**Throws** `ReferenceError: Cannot access 'value' before initialization`.

Same closure-creation logic as Q3 applies — defining `fn` doesn't touch `value`. But here, `fn()` is **called immediately**, *before* `let value = 10;` has executed. At the moment of the call, `value` is still in its TDZ (the block hasn't reached its declaration line yet), so evaluating the closure body throws.

**Why is this different from Q3?** It's purely about **timing of invocation**: in Q3, the closure was called only after the block (and its `let value = 42`) had fully finished executing. Here, the closure is called *while still inside the TDZ window* for `value`. Same closure mechanics, different execution timing — that's the entire difference.

## 5. `typeof` + TDZ

js

```jsx
{  console.log(typeof value);  let value = 10;}
```

**Throws** `ReferenceError: Cannot access 'value' before initialization`.

Normally `typeof` is "safe" for undeclared variables and returns `"undefined"`. But that leniency only applies when the variable **doesn't exist anywhere** in scope. Here, `value` **does** exist (declared via `let` later in the same block) and is hoisted to the top of the block, sitting in the TDZ. Since `value` is a known-but-uninitialized binding, `typeof` cannot safely resolve it and instead throws, just like any other reference would.

## 6. TDZ + `var` Shadowing

js

```jsx
var x = 10;{  console.log(x);  let x = 20;}
```

**Throws** `ReferenceError: Cannot access 'x' before initialization`.

**Why doesn't it access the outer `var x`?** Because the inner block contains its own `let x = 20;`. Due to lexical scoping, that declaration is hoisted to the top of the block and shadows the outer `x` for the block's *entire* body — the outer `var x` becomes completely inaccessible inside this block. So `console.log(x)` resolves to the inner, TDZ-bound `x`, not the outer `var`. The type of the outer declaration (`var` vs `let`) doesn't matter — what matters is that a `let` exists in the same block, which triggers shadowing from the top down.

## 7. TDZ + Destructuring

js

```jsx
let a = 10;{  let [a] = [a];  console.log(a);}
```

**Throws** `ReferenceError: Cannot access 'a' before initialization`.

**Which `a` does the RHS refer to?** The **new, local** `a` — not the outer one. The entire `let [a] = [a];` statement is one declaration for the block-scoped `a`, which is hoisted (and TDZ'd) across the whole block *before* the statement even runs. When the right-hand side `[a]` is evaluated (to build the array being destructured), it looks up `a` in the current lexical scope, finds the local, hoisted-but-uninitialized `a`, and throws — exactly like Q1's `let x = x + 1`.

## 8. TDZ + Object Destructuring

js

```jsx
let name = "Rahul";{  let { name } = { name };  console.log(name);}
```

**Throws** `ReferenceError: Cannot access 'name' before initialization`.

Same reasoning as Q7. The shorthand `{ name }` on the right-hand side is evaluated in the block's scope, where the local `let name` has already been hoisted (and is uninitialized). So the RHS `name` resolves to the **local**, TDZ-bound `name` — not the outer `"Rahul"` — and throws before the assignment or `console.log` ever runs.

## 9. TDZ + Default Parameters

js

```jsx
function test(a = b, b = 20) {  console.log(a, b);}test();
```

**Throws** `ReferenceError: Cannot access 'b' before initialization`.

**Why does parameter order matter?** Parameters are initialized strictly **left to right**, each behaving like a `let` binding in a shared parameter scope. When `test()` runs with no arguments:

1. `a`'s default (`b`) is evaluated first — but `b` (the second parameter) hasn't been initialized yet at this point, so it's still in its TDZ.
2. Accessing `b` here throws immediately.

If the order were swapped (`function test(b = 20, a = b)`), it would work fine, since `b` would already be initialized before `a`'s default tries to use it. Parameter defaults can only safely reference *earlier* parameters, never later ones.

## 10. Parameter Scope + Function Body

js

```jsx
let x = 10;function test(x = 20) {  console.log(x);  let x = 30;}test();
```

**This is invalid JavaScript** — it throws a `SyntaxError: Identifier 'x' has already been declared`.

Function parameters and top-level `let`/`const` declarations in the function body **share the same scope**. You're allowed to shadow an outer variable with a parameter, but you **cannot** redeclare a parameter name using `let`/`const` inside the function body — that's a straight-up duplicate-declaration syntax error, caught before the function ever runs. (This is different from `var`, which *can* coexist with a same-named parameter without erroring, since `var` redeclarations are tolerated.)

## 11. Class TDZ

js

```jsx
const obj = new Person();class Person {  constructor() {    this.name = "Rahul";  }}
```

**Throws** `ReferenceError: Cannot access 'Person' before initialization`.

**Why does `class` behave differently from a function declaration?** Function declarations are fully hoisted — both their name *and* their entire body/implementation are available from the top of the scope, so calling them before their line in the code works fine. `class` declarations, however, follow the **same hoisting rules as `let`/`const`**: the name is hoisted, but the class itself stays uninitialized until its declaration line executes. So instantiating it earlier (`new Person()`) hits the TDZ and throws — this is a deliberate design choice to prevent using a class before its full body (including any class-field initializers) is ready.

## 12. Class + `typeof`

js

```jsx
console.log(typeof Person);class Person {}
```

**Throws** `ReferenceError: Cannot access 'Person' before initialization`.

**Why can `typeof` still throw here?** As established earlier, `typeof`'s "safe" behavior (returning `"undefined"` without erroring) only applies to variables that are **entirely undeclared** in any accessible scope. `Person` **is** declared (via `class` later in the same scope) and is hoisted into a TDZ binding. Since the engine knows `Person` exists but isn't ready, `typeof` cannot bypass the TDZ check — it throws just like any other reference would.

## 13. TDZ + `switch`

js

```jsx
let x = 10;switch (x) {  case 10:    console.log(x);    let x = 20;    break;}
```

**Throws** `ReferenceError: Cannot access 'x' before initialization`.

An important, often-missed detail: **all `case` clauses in a single `switch` share one block scope** — the entire `switch { ... }` is treated as one block, not a separate block per `case`. So `let x = 20;` inside the `case 10:` clause is hoisted to the top of the *whole switch block*, shadowing the outer `x = 10` throughout. That means `console.log(x)` — even though it appears *before* the `let x = 20;` line in the same case — is still referencing the shadowed, TDZ-bound inner `x`, and throws.

## 14. TDZ + `for` Loop Closure

js

```jsx
for (let i = 0; i < 3; i++) {  setTimeout(() => console.log(i), 0);}
```

**Output:**

```
0
1
2
```

**Does TDZ have anything to do with this?** No — this behavior comes from a **different feature of `let`**, not TDZ. TDZ is about accessing a variable before it's initialized; here, `i` is always fully initialized by the time each closure runs.

The real mechanism is **per-iteration bindings**: with `let` in a `for` loop, JavaScript creates a **brand-new, independent binding of `i` for each iteration**, copying forward the previous value at the start of each loop cycle. So each `setTimeout` callback closes over its *own* iteration's `i` (0, then 1, then 2), rather than one single shared `i` that ends up at `3` after the loop finishes (which is what happens with `var`, since `var` has function/global scope and only one shared binding across all iterations).
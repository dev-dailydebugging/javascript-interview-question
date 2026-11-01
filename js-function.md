# The Complete Guide of Function

## 1. What is a function in JavaScript?

- A function is a reusable block of code that performs a specific task.
- It runs only when it is called.
- Functions help avoid repeating code and keep programs organized.
- In JavaScript, functions are objects, so they can be stored in variables, passed around, and returned.

## 2. How do you declare a function?

- Use the `function` keyword, a name, parentheses for parameters, and a body in curly braces.

js

```jsx
function greet(name) {  console.log("Hello, " + name);}
```

## 3. How do you call/invoke a function?

- Write the function name followed by parentheses, passing any arguments inside.

js

```jsx
greet("Poojan"); // Hello, Poojan
```

- Without the parentheses, you only reference the function and don't run it.

## 4. What are parameters and arguments?

- **Parameters** are the variable names listed in the function definition.
- **Arguments** are the actual values passed when the function is called.

js

```jsx
function add(a, b) {   // a, b → parameters  return a + b;}add(2, 3);             // 2, 3 → arguments
```

## 5. What is the purpose of the `return` statement?

- It sends a value back to the place where the function was called.
- It immediately stops the execution of the function.
- Any code written after `return` inside the function does not run.

js

```jsx
function square(n) {  return n * n;}const result = square(4); // 16
```

## 6. What happens if a function doesn't have a `return` statement?

- The function returns `undefined` by default.
- The same happens if `return` is used without a value.

js

```jsx
function sayHi() {  console.log("Hi");}console.log(sayHi()); // Hi, then undefined
```

## 7. What is a function declaration?

- It is a function defined with the `function` keyword and a required name.
- It is **hoisted**, so it can be called before it appears in the code.

js

```jsx
function multiply(a, b) {  return a * b;}
```

## 8. What is a function expression?

- It is a function created and assigned to a variable.
- The function can be named or anonymous.
- It is **not fully hoisted**: the variable exists before the line runs, but its value is not the function yet.

js

```jsx
const multiply = function (a, b) {  return a * b;};
```

## 9. What is the difference between a function declaration and a function expression?

- **Syntax:** a declaration starts with `function name() {}`, while an expression is assigned to a variable (`const name = function() {}`).
- **Hoisting:** declarations can be called before they are defined. Expressions cannot, and calling one early throws an error with `const`/`let`, or a TypeError with `var`.
- **Name:** a declaration must have a name. An expression can be anonymous.
- **Usage:** expressions are handy for callbacks and for storing functions in variables.

js

```jsx
sayHello();                  // Worksfunction sayHello() {}sayBye();                    // Errorconst sayBye = function () {};
```

## 10. What is an arrow function?

- It is a shorter syntax for writing function expressions, introduced in ES6.
- It uses the `=>` symbol.
- With a single expression, `return` and the braces can be omitted (implicit return).
- It does not have its own `this`. It uses `this` from the surrounding scope.
- It cannot be used as a constructor.

js

```jsx
const add = (a, b) => a + b;const double = n => n * 2;
```

## 11. What is an anonymous function?

- It is a function without a name.
- It is commonly used as a callback or assigned to a variable.

js

```jsx
setTimeout(function () {  console.log("Runs after 1 second");}, 1000);const nums = [1, 2, 3].map(n => n * 2); // arrow function, also anonymous
```

## 12. What are default parameters?

- They let a parameter have a fallback value when no argument (or `undefined`) is passed.

js

```jsx
function greet(name = "Guest") {  console.log("Hello, " + name);}greet();          // Hello, Guestgreet("Poojan");  // Hello, Poojan
```

- Defaults apply only for `undefined`, not for `null` or `0`.

## 13. What are rest parameters (`...args`)?

- They collect all remaining arguments into a real **array**.
- They must be the **last** parameter in the list.

js

```jsx
function sum(...numbers) {  return numbers.reduce((total, n) => total + n, 0);}sum(1, 2, 3, 4); // 10
```

## 14. Can a function accept multiple arguments?

- Yes, a function can accept any number of arguments.
- Separate multiple parameters with commas.
- You can also pass more arguments than parameters. The extras are ignored unless you use rest parameters or `arguments`.

js

```jsx
function introduce(name, age, city) {  console.log(`${name},${age},${city}`);}introduce("Poojan", 25, "Delhi");
```

## 15. Can a function return another value or function?

- Yes, a function can return any value: number, string, object, array, or another function.
- A function that returns a function is the basis of **closures** and **higher-order functions**.

js

```jsx
function multiplier(factor) {  return function (n) {    return n * factor;  };}const triple = multiplier(3);triple(5); // 15
```

remove poojan and use diifrent name

Swapping out the example name in the code samples.

## 1. What is a function in JavaScript?

- A function is a reusable block of code that performs a specific task.
- It runs only when it is called.
- Functions help avoid repeating code and keep programs organized.
- In JavaScript, functions are objects, so they can be stored in variables, passed around, and returned.

## 2. How do you declare a function?

- Use the `function` keyword, a name, parentheses for parameters, and a body in curly braces.

js

```jsx
function greet(name) {  console.log("Hello, " + name);}
```

## 3. How do you call/invoke a function?

- Write the function name followed by parentheses, passing any arguments inside.

js

```jsx
greet("Rahul"); // Hello, Rahul
```

- Without the parentheses, you only reference the function and don't run it.

## 4. What are parameters and arguments?

- **Parameters** are the variable names listed in the function definition.
- **Arguments** are the actual values passed when the function is called.

js

```jsx
function add(a, b) {   // a, b → parameters  return a + b;}add(2, 3);             // 2, 3 → arguments
```

## 5. What is the purpose of the `return` statement?

- It sends a value back to the place where the function was called.
- It immediately stops the execution of the function.
- Any code written after `return` inside the function does not run.

js

```jsx
function square(n) {  return n * n;}const result = square(4); // 16
```

## 6. What happens if a function doesn't have a `return` statement?

- The function returns `undefined` by default.
- The same happens if `return` is used without a value.

js

```jsx
function sayHi() {  console.log("Hi");}console.log(sayHi()); // Hi, then undefined
```

## 7. What is a function declaration?

- It is a function defined with the `function` keyword and a required name.
- It is **hoisted**, so it can be called before it appears in the code.

js

```jsx
function multiply(a, b) {  return a * b;}
```

## 8. What is a function expression?

- It is a function created and assigned to a variable.
- The function can be named or anonymous.
- It is **not fully hoisted**: the variable exists before the line runs, but its value is not the function yet.

js

```jsx
const multiply = function (a, b) {  return a * b;};
```

## 9. What is the difference between a function declaration and a function expression?

- **Syntax:** a declaration starts with `function name() {}`, while an expression is assigned to a variable (`const name = function() {}`).
- **Hoisting:** declarations can be called before they are defined. Expressions cannot, and calling one early throws an error with `const`/`let`, or a TypeError with `var`.
- **Name:** a declaration must have a name. An expression can be anonymous.
- **Usage:** expressions are handy for callbacks and for storing functions in variables.

js

```jsx
sayHello();                  // Worksfunction sayHello() {}sayBye();                    // Errorconst sayBye = function () {};
```

## 10. What is an arrow function?

- It is a shorter syntax for writing function expressions, introduced in ES6.
- It uses the `=>` symbol.
- With a single expression, `return` and the braces can be omitted (implicit return).
- It does not have its own `this`. It uses `this` from the surrounding scope.
- It cannot be used as a constructor.

js

```jsx
const add = (a, b) => a + b;const double = n => n * 2;
```

## 11. What is an anonymous function?

- It is a function without a name.
- It is commonly used as a callback or assigned to a variable.

js

```jsx
setTimeout(function () {  console.log("Runs after 1 second");}, 1000);const nums = [1, 2, 3].map(n => n * 2); // arrow function, also anonymous
```

## 12. What are default parameters?

- They let a parameter have a fallback value when no argument (or `undefined`) is passed.

js

```jsx
function greet(name = "Guest") {  console.log("Hello, " + name);}greet();          // Hello, Guestgreet("Rahul");   // Hello, Rahul
```

- Defaults apply only for `undefined`, not for `null` or `0`.

## 13. What are rest parameters (`...args`)?

- They collect all remaining arguments into a real **array**.
- They must be the **last** parameter in the list.

js

```jsx
function sum(...numbers) {  return numbers.reduce((total, n) => total + n, 0);}sum(1, 2, 3, 4); // 10
```

## 14. Can a function accept multiple arguments?

- Yes, a function can accept any number of arguments.
- Separate multiple parameters with commas.
- You can also pass more arguments than parameters. The extras are ignored unless you use rest parameters or `arguments`.

js

```jsx
function introduce(name, age, city) {  console.log(`${name},${age},${city}`);}introduce("Rahul", 25, "Delhi");
```

## 15. Can a function return another value or function?

- Yes, a function can return any value: number, string, object, array, or another function.
- A function that returns a function is the basis of **closures** and **higher-order functions**.

js

```jsx
function multiplier(factor) {  return function (n) {    return n * factor;  };}const triple = multiplier(3);triple(5); // 15
```

![1.png](The%20Complete%20Guide%20of%20Function/1.png)

![2.png](The%20Complete%20Guide%20of%20Function/2.png)

![3.png](The%20Complete%20Guide%20of%20Function/3.png)

![4.png](The%20Complete%20Guide%20of%20Function/4.png)

![5.png](The%20Complete%20Guide%20of%20Function/5.png)

![6.png](The%20Complete%20Guide%20of%20Function/6.png)

![7.png](The%20Complete%20Guide%20of%20Function/7.png)

![8.png](The%20Complete%20Guide%20of%20Function/8.png)

![9.png](The%20Complete%20Guide%20of%20Function/9.png)

![10.png](The%20Complete%20Guide%20of%20Function/10.png)

![11.png](The%20Complete%20Guide%20of%20Function/11.png)

![13.png](The%20Complete%20Guide%20of%20Function/13.png)

# **JavaScript  Function  — Intermediate Questions with Answers**

## 1. What are first-class functions in JavaScript?

- It means functions are treated like any other value.
- They can be stored in variables, passed as arguments, and returned from other functions.
- They can also be stored in arrays and objects.

js

```jsx
const greet = function () {  return "Hello";};const list = [greet];console.log(list[0]()); // Hello
```

## 2. What is a callback function?

- It is a function passed as an argument to another function.
- The receiving function calls it later, after some task or event.
- It is used in event handlers, timers, array methods, and async code.

js

```jsx
function fetchData(callback) {  setTimeout(() => {    callback("Data received");  }, 1000);}fetchData(function (result) {  console.log(result); // Data received});
```

## 3. What is a higher-order function?

- It is a function that takes another function as an argument, returns a function, or both.
- Built-in examples are `map`, `filter`, `reduce`, and `forEach`.

js

```jsx
const nums = [1, 2, 3, 4];const evens = nums.filter(n => n % 2 === 0); // [2, 4]
```

## 4. What is the difference between a callback and a higher-order function?

- **Callback:** the function that is *passed in* as an argument.
- **Higher-order function:** the function that *receives or returns* another function.
- They work together: the higher-order function uses the callback.
- One function can be both, but the two terms describe different roles.

js

```jsx
function repeat(times, action) {   // repeat → higher-order function  for (let i = 0; i < times; i++) action(i);}repeat(3, i => console.log(i));    // arrow function → callback
```

## 5. What is function scope?

- Variables declared inside a function are accessible only inside that function.
- They cannot be accessed from outside.
- Each function call creates its own new scope.

js

```jsx
function demo() {  const message = "Inside";  console.log(message); // Inside}demo();console.log(message); // ReferenceError
```

## 6. What is lexical scope in JavaScript?

- Scope is decided by where the code is **written**, not where it is called.
- An inner function can access variables of its outer functions.
- JavaScript looks for a variable in the current scope, then moves outward step by step (the scope chain).

js

```jsx
const name = "Global";function outer() {  const name = "Outer";  function inner() {    console.log(name); // Outer  }  inner();}outer();
```

## 7. What is a closure?

- A closure is a function that remembers the variables from its outer scope, even after the outer function has finished running.
- It is created every time a function is created.
- It is useful for data privacy, counters, and function factories.

js

```jsx
function counter() {  let count = 0;  return function () {    count++;    return count;  };}const next = counter();next(); // 1next(); // 2
```

## 8. How do closures work with private variables?

- JavaScript functions can hide variables inside their scope.
- A closure exposes only specific functions that can read or change those variables.
- Outside code cannot access the variable directly.

js

```jsx
function createAccount(balance) {  return {    deposit(amount) {      balance += amount;      return balance;    },    getBalance() {      return balance;    }  };}const account = createAccount(100);account.deposit(50);      // 150account.balance;          // undefined (private)
```

## 9. What is an IIFE (Immediately Invoked Function Expression)?

- It is a function that runs immediately after it is defined.
- It is wrapped in parentheses, followed by `()` to invoke it.
- It creates a private scope and avoids polluting the global scope.

js

```jsx
(function () {  const secret = "hidden";  console.log("IIFE ran");})();(() => console.log("Arrow IIFE"))();
```

## 10. What is the difference between regular functions and arrow functions?

- **Syntax:** arrow functions are shorter and support implicit return.
- **`this`:** regular functions get their own `this`. Arrow functions use `this` from the surrounding scope.
- **`arguments`:** regular functions have the `arguments` object. Arrow functions do not.
- **Constructor:** regular functions can be used with `new`. Arrow functions cannot.
- **Hoisting:** function declarations are hoisted. Arrow functions are not, since they are expressions.

js

```jsx
function add(a, b) { return a + b; }const addArrow = (a, b) => a + b;
```

## 11. How does `this` behave inside a regular function?

- The value of `this` depends on **how the function is called**.
- **Plain call:** `this` is `window` (or `globalThis`) in non-strict mode, and `undefined` in strict mode.
- **Method call:** `this` is the object before the dot.
- **With `new`:** `this` is the newly created object.
- **With `call`/`apply`/`bind`:** `this` is the value you set.

js

```jsx
const user = {  name: "Rahul",  show() {    console.log(this.name);  }};user.show();          // Rahulconst fn = user.show;fn();                 // undefined (this is lost)
```

## 12. How does `this` behave inside an arrow function?

- Arrow functions do not have their own `this`.
- They take `this` from the scope where they were **defined** (lexical `this`).
- `call`, `apply`, and `bind` cannot change it.
- Avoid arrow functions as object methods when you need `this` to be the object.

js

```jsx
const user = {  name: "Rahul",  showLater() {    setTimeout(() => {      console.log(this.name); // Rahul    }, 1000);  }};user.showLater();
```

## 13. What are `call()`, `apply()`, and `bind()`?

- They are methods to set the value of `this` for a function.
- **`call(thisArg, arg1, arg2)`:** calls the function immediately, with arguments passed one by one.
- **`apply(thisArg, [args])`:** calls the function immediately, with arguments passed as an array.
- **`bind(thisArg, ...args)`:** does not call it, but returns a **new function** with `this` fixed.

js

```jsx
function intro(city, country) {  console.log(`${this.name} from${city},${country}`);}const person = { name: "Rahul" };intro.call(person, "Delhi", "India");intro.apply(person, ["Delhi", "India"]);const boundIntro = intro.bind(person, "Delhi");boundIntro("India");
```

## 14. What is recursion, and when would you use it?

- Recursion is when a function calls itself to solve a smaller version of the same problem.
- Every recursive function needs a **base case** to stop, or it will overflow the call stack.
- **Use it for:** tree or nested structures, factorials, Fibonacci, searching, and divide-and-conquer problems.
- Loops are often simpler and faster when recursion is not needed.

js

```jsx
function factorial(n) {  if (n <= 1) return 1;          // base case  return n * factorial(n - 1);   // recursive case}factorial(5); // 120
```

## 15. What is the difference between pure and impure functions?

- **Pure function:**
    - Same input always gives the same output.
    - Has no side effects (does not change anything outside itself).
    - Easy to test and predict.
- **Impure function:**
    - Can give different output for the same input.
    - Has side effects such as modifying external variables, changing the DOM, API calls, or using `Math.random()` or `Date.now()`.

js

```jsx
// Purefunction add(a, b) {  return a + b;}// Impurelet total = 0;function addToTotal(n) {  total += n;   // modifies outside variable  return total;}
```

# **JavaScript  Function  — Advanced Questions with Answers**

## 1. How does function execution context work in JavaScript?

- An execution context is the environment where JavaScript code runs.
- There are three types: **global**, **function**, and **eval** (rarely used).
- Each context has two phases:
    - **Creation phase:** memory is set up, variables are hoisted, and `this` is determined.
    - **Execution phase:** code runs line by line and values are assigned.
- Each context holds a **variable environment**, a **lexical environment**, and the value of `this`.

js

```jsx
var a = 10;function show() {  console.log(a); // undefined (hoisted, not yet assigned)  var a = 5;}show();
```

## 2. What happens internally when a function is called?

- A new **function execution context** is created.
- It is pushed onto the **call stack**.
- In the creation phase, parameters and local variables are set up, `this` is decided, and a reference to the outer scope is stored.
- In the execution phase, the body runs line by line.
- When the function returns or finishes, its context is **popped** off the stack.

js

```jsx
function add(a, b) {  return a + b;}add(2, 3); // context created → run → popped
```

## 3. How does the call stack work with function calls?

- The call stack is a **LIFO** (Last In, First Out) structure that tracks running functions.
- When a function is called, it is pushed. When it returns, it is popped.
- The function on top of the stack is the one currently running.
- Too many nested calls (like infinite recursion) cause a **stack overflow**.

js

```jsx
function first() { second(); }function second() { third(); }function third() { console.log("Done"); }first();// Stack: global → first → second → third// Then popped in reverse: third → second → first → global
```

## 4. How does closure work internally with lexical environments?

- Every execution context has a **lexical environment** that stores its variables and a reference to its **outer** lexical environment.
- When a function is created, it stores a hidden reference to the environment where it was defined (`[[Environment]]`).
- Even after the outer function finishes, that environment stays in memory as long as the inner function references it.
- This is how closures "remember" variables.

js

```jsx
function outer() {  let count = 0;  return function inner() {    count++;    return count;  };}const counter = outer();counter(); // 1counter(); // 2 (count lives in outer's preserved environment)
```

## 5. How can closures cause memory leaks?

- A closure keeps its outer variables alive as long as the closure itself is reachable.
- Leaks happen when closures hold references to **large data** that is no longer needed.
- **Common causes:**
    - Event listeners that are never removed.
    - Timers (`setInterval`) that are never cleared.
    - Long-lived closures capturing large objects or DOM nodes.
- **Fixes:** remove listeners, clear timers, and set unused references to `null`.

js

```jsx
function attach() {  const bigData = new Array(1000000).fill("x");  document.addEventListener("click", function handler() {    console.log(bigData.length); // keeps bigData alive  });}// Fix: remove the listener when it's no longer needed// document.removeEventListener("click", handler);
```

## 6. How does `this` binding work in different function invocation patterns?

- **Default (plain call):** `this` is `globalThis` in non-strict mode, `undefined` in strict mode.
- **Method call:** `this` is the object before the dot.
- **Constructor call (`new`):** `this` is the newly created object.
- **Explicit (`call`/`apply`/`bind`):** `this` is the value you pass.
- **Arrow function:** no own `this`, uses the surrounding scope's `this`.

js

```jsx
function show() { console.log(this); }show();                 // global / undefinedconst obj = { show };obj.show();             // objnew show();             // new empty objectshow.call({ a: 1 });    // { a: 1 }
```

## 7. What is the difference between implicit, explicit, and lexical `this` binding?

- **Implicit binding:** `this` is set by the calling object (`obj.method()`).
- **Explicit binding:** you set `this` manually using `call`, `apply`, or `bind`.
- **Lexical binding:** arrow functions inherit `this` from where they are defined.
- **Priority order:** `new` > explicit > implicit > default.

js

```jsx
const user = {  name: "Rahul",  implicit() { console.log(this.name); },  lexical: () => console.log(this.name)};user.implicit();                        // Rahul (implicit)user.implicit.call({ name: "Aman" });   // Aman (explicit)user.lexical();                         // undefined (lexical, from outer scope)
```

## 8. How do `call()`, `apply()`, and `bind()` work internally?

- All three set `this` for a function.
- Conceptually, `call` temporarily attaches the function to the object as a method, calls it, then removes it.
- `apply` does the same but takes arguments as an array.
- `bind` returns a **new function** that permanently has `this` fixed.

js

```jsx
// Simple polyfill of callFunction.prototype.myCall = function (context, ...args) {  context = context || globalThis;  const key = Symbol();  context[key] = this;  const result = context[key](...args);  delete context[key];  return result;};// Simple polyfill of bindFunction.prototype.myBind = function (context, ...boundArgs) {  const fn = this;  return function (...args) {    return fn.apply(context, [...boundArgs, ...args]);  };};
```

## 9. What is function currying, and how can you implement it?

- Currying converts a function with multiple arguments into a chain of functions, each taking **one** argument.
- `f(a, b, c)` becomes `f(a)(b)(c)`.
- It helps with reusability and creating specialized functions.

js

```jsx
// Manual curryingconst add = a => b => c => a + b + c;add(1)(2)(3); // 6// Generic curry functionfunction curry(fn) {  return function curried(...args) {    if (args.length >= fn.length) {      return fn(...args);    }    return (...next) => curried(...args, ...next);  };}const sum = curry((a, b, c) => a + b + c);sum(1)(2)(3);   // 6sum(1, 2)(3);   // 6
```

## 10. What is partial application, and how is it different from currying?

- **Partial application:** fix some arguments of a function now and supply the rest later. It returns a function that takes the remaining arguments **all at once**.
- **Currying:** always transforms a function into a chain of **unary** (one-argument) functions.
- Partial application can be done with `bind` or a custom helper.

js

```jsx
function multiply(a, b, c) {  return a * b * c;}// Partial applicationconst double = multiply.bind(null, 2);double(3, 4); // 24 (remaining args passed together)// Curryingconst curriedMultiply = a => b => c => a * b * c;curriedMultiply(2)(3)(4); // 24 (one arg at a time)
```

## 11. What is function composition, and how can you implement it?

- Composition combines multiple functions so the output of one becomes the input of the next.
- `compose` runs functions **right to left**.
- `pipe` runs functions **left to right**.

js

```jsx
const compose = (...fns) => x => fns.reduceRight((acc, fn) => fn(acc), x);const pipe = (...fns) => x => fns.reduce((acc, fn) => fn(acc), x);const addOne = n => n + 1;const double = n => n * 2;compose(double, addOne)(5); // double(addOne(5)) = 12pipe(double, addOne)(5);    // addOne(double(5)) = 11
```

## 12. What is memoization, and how can it improve function performance?

- Memoization caches the result of a function for given inputs.
- If the function is called again with the same inputs, the cached result is returned instead of recomputing.
- It works best with **pure functions** that are expensive to compute.
- The trade-off is extra memory use.

js

```jsx
function memoize(fn) {  const cache = {};  return function (...args) {    const key = JSON.stringify(args);    if (key in cache) return cache[key];    const result = fn(...args);    cache[key] = result;    return result;  };}const slowSquare = n => {  console.log("Calculating...");  return n * n;};const fastSquare = memoize(slowSquare);fastSquare(5); // Calculating... 25fastSquare(5); // 25 (from cache)
```

## 13. How do generator functions work with `yield` and `.next()`?

- A generator is declared with `function*` and can **pause and resume** execution.
- Calling it returns an **iterator** and does not run the body immediately.
- `yield` pauses the function and sends a value out.
- `.next()` resumes it and returns `{ value, done }`.
- `.next(x)` can also send a value **into** the generator, which becomes the result of the paused `yield`.

js

```jsx
function* numbers() {  yield 1;  yield 2;  return 3;}const gen = numbers();gen.next(); // { value: 1, done: false }gen.next(); // { value: 2, done: false }gen.next(); // { value: 3, done: true }// Two-way communicationfunction* chat() {  const name = yield "What is your name?";  console.log("Hello, " + name);}const c = chat();c.next();          // { value: "What is your name?", done: false }c.next("Rahul");   // Hello, Rahul
```

## 14. How do async functions work internally with Promises and the event loop?

- An `async` function always returns a **Promise**.
- `await` pauses the function and waits for a Promise to settle. It does **not** block the main thread.
- When it pauses, the rest of the function is scheduled as a **microtask** to run after the Promise resolves.
- **Event loop order:** call stack → microtask queue (Promises, `await`) → macrotask queue (`setTimeout`, events).
- Internally, async/await is built on Promises and behaves like generators.

js

```jsx
console.log("1");setTimeout(() => console.log("2 - macrotask"), 0);async function run() {  console.log("3");  await Promise.resolve();  console.log("4 - microtask");}run();console.log("5");// Output: 1, 3, 5, 4 - microtask, 2 - macrotask
```

## 15. What is the difference between debouncing and throttling, and how can you implement them using functions?

- **Debouncing:** runs the function only after the user **stops** triggering it for a set delay. Good for search inputs and window resize.
- **Throttling:** runs the function **at most once** in a given time interval. Good for scroll and mouse move events.
- Both use closures to keep track of timers or timestamps.

js

```jsx
// Debouncefunction debounce(fn, delay) {  let timer;  return function (...args) {    clearTimeout(timer);    timer = setTimeout(() => fn.apply(this, args), delay);  };}// Throttlefunction throttle(fn, limit) {  let lastCall = 0;  return function (...args) {    const now = Date.now();    if (now - lastCall >= limit) {      lastCall = now;      fn.apply(this, args);    }  };}const onSearch = debounce(q => console.log("Search:", q), 500);const onScroll = throttle(() => console.log("Scrolled"), 1000);
```

[Claude is AI and can make mistakes. Please do](https://support.anthropic.com/en/articles/8525154-claude-is-providing-incorrect-or-misleading-responses-what-s-going-on)
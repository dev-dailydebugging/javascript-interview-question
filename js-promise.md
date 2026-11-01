# The Complete Guide of Promises

## 1. What is a Promise in JavaScript?

A Promise is an object that represents the eventual completion (or failure) of an asynchronous operation and its resulting value. It lets you handle async work like API calls or timers without deeply nested callbacks.

## 2. What are the three states of a Promise?

1. **Pending**: the initial state, neither fulfilled nor rejected.
2. **Fulfilled**: the operation completed successfully and the Promise has a value.
3. **Rejected**: the operation failed and the Promise has a reason (error).

Once a Promise is fulfilled or rejected, it is *settled* and its state can never change again.

## 3. How do you create a Promise in JavaScript?

Use the `Promise` constructor, which takes an executor function with `resolve` and `reject` parameters.

javascript

```jsx
const myPromise = new Promise((resolve, reject) => {  const success = true;  if (success) {    resolve("Data loaded");  } else {    reject(new Error("Something went wrong"));  }});
```

## 4. What is the difference between resolve() and reject()?

- `resolve(value)` moves the Promise to the **fulfilled** state and passes `value` to `.then()` handlers.
- `reject(reason)` moves the Promise to the **rejected** state and passes `reason` to `.catch()` handlers.

Only the first call counts. Any later calls to `resolve` or `reject` are ignored.

## 5. What is the purpose of the .then() method?

`.then()` registers a callback that runs when the Promise is fulfilled. It can also take a second callback for rejection. It always returns a new Promise, which is what makes chaining possible.

javascript

```jsx
myPromise.then((value) => console.log(value));
```

## 6. What is the purpose of the .catch() method?

`.catch()` handles errors. It runs when the Promise is rejected or when an error is thrown in a previous `.then()`. It is shorthand for `.then(undefined, onRejected)`.

javascript

```jsx
myPromise.catch((error) => console.error(error.message));
```

## 7. What is the use of the .finally() method?

`.finally()` runs a callback after the Promise settles, whether it was fulfilled or rejected. It is used for cleanup work like hiding a loading spinner or closing a connection. The callback receives no arguments, and the original result or error passes through unchanged.

javascript

```jsx
fetchData()  .then(show)  .catch(handleError)  .finally(() => hideLoader());
```

## 8. What is Promise chaining?

Promise chaining is calling multiple `.then()` methods one after another, where each one receives the result of the previous one. It lets you run async steps in sequence without nesting callbacks.

javascript

```jsx
fetchUser()  .then((user) => fetchPosts(user.id))  .then((posts) => console.log(posts))  .catch((err) => console.error(err));
```

A single `.catch()` at the end handles an error from any step in the chain.

## 9. What is Promise.all()?

`Promise.all()` takes an array of Promises and returns a single Promise that:

- **fulfills** with an array of all results (in the original order) when **all** Promises fulfill;
- **rejects** immediately when **any one** Promise rejects.

javascript

```jsx
Promise.all([p1, p2, p3]).then(([r1, r2, r3]) => { /* ... */ });
```

## 10. What is Promise.allSettled()?

`Promise.allSettled()` waits for **all** Promises to settle, whether fulfilled or rejected, and never rejects. It returns an array of result objects:

javascript

```jsx
[  { status: "fulfilled", value: 10 },  { status: "rejected", reason: Error("fail") }]
```

## 11. What is Promise.race()?

`Promise.race()` returns a Promise that settles as soon as **the first** Promise in the array settles, with that Promise's value or error. It is commonly used to implement timeouts.

javascript

```jsx
Promise.race([fetchData(), timeout(5000)]);
```

## 12. What is Promise.any()?

`Promise.any()` returns a Promise that fulfills as soon as **the first Promise fulfills**. It ignores rejections unless **all** Promises reject, in which case it rejects with an `AggregateError`.

javascript

```jsx
Promise.any([p1, p2, p3]).then((firstSuccess) => console.log(firstSuccess));
```

## 13. What is the difference between Promise.all() and Promise.allSettled()?

|  | `Promise.all()` | `Promise.allSettled()` |
| --- | --- | --- |
| On any rejection | Rejects immediately | Keeps waiting for all |
| Result | Array of values | Array of `{status, value/reason}` objects |
| Can it reject? | Yes | No, it always fulfills |
| Use when | All tasks must succeed | You want the outcome of every task |

## 14. What happens when you return a value from a .then() callback?

The returned value is wrapped in a new Promise that fulfills with that value, so the next `.then()` in the chain receives it.

- If you return a **plain value**, the next `.then()` gets it directly.
- If you return a **Promise**, the chain waits for it to settle and passes on its result.
- If you return **nothing**, the next `.then()` receives `undefined`.
- If you **throw an error**, the chain skips to the nearest `.catch()`.

javascript

```jsx
Promise.resolve(2)  .then((x) => x * 2)   // returns 4  .then((x) => console.log(x)); // 4
```

## 15. Are Promises synchronous or asynchronous in JavaScript?

The **executor function** passed to `new Promise()` runs **synchronously**, immediately when the Promise is created. However, the `.then()`, `.catch()`, and `.finally()` callbacks always run **asynchronously**, as microtasks after the current synchronous code finishes.

javascript

```jsx
console.log("1");new Promise((resolve) => {  console.log("2");   // runs synchronously  resolve();}).then(() => console.log("4")); // runs asynchronouslyconsole.log("3");// Output: 1, 2, 3, 4
```

![1.png](The%20Complete%20Guide%20of%20Promises/1.png)

![2.png](The%20Complete%20Guide%20of%20Promises/2.png)

![3.png](The%20Complete%20Guide%20of%20Promises/3.png)

![4.png](The%20Complete%20Guide%20of%20Promises/4.png)

![5.png](The%20Complete%20Guide%20of%20Promises/5.png)

![6.png](The%20Complete%20Guide%20of%20Promises/6.png)

![7.png](The%20Complete%20Guide%20of%20Promises/7.png)

![8.png](The%20Complete%20Guide%20of%20Promises/8.png)

![9.png](The%20Complete%20Guide%20of%20Promises/9.png)

# **JavaScript  Promises  — Intermediate Questions with Answers**

## 1. What is the difference between returning a value and returning a Promise inside `.then()`?

- Returning a **plain value** makes the next `.then()` receive that value immediately (in a microtask).
- Returning a **Promise** makes the chain **wait** for that Promise to settle. The next `.then()` receives its fulfilled value, or the chain moves to `.catch()` if it rejects. The Promise is *flattened*, so you never get a Promise nested inside a Promise.

javascript

```jsx
Promise.resolve(1)  .then((x) => x + 1)                       // returns value 2  .then((x) => new Promise((res) => setTimeout(() => res(x * 10), 1000))) // returns Promise  .then((x) => console.log(x));             // after 1s: 20
```

## 2. What happens if you don't return a value inside a `.then()` callback?

The callback returns `undefined`, so the next `.then()` receives `undefined`. This is a common bug, especially when you start an async operation inside `.then()` but forget to `return` it. The chain then does not wait for that operation.

javascript

```jsx
Promise.resolve(5)  .then((x) => { x * 2; })        // no return  .then((x) => console.log(x));   // undefined
```

## 3. What happens when an error is thrown inside a `.then()` callback?

The Promise returned by that `.then()` becomes **rejected** with the thrown error. The chain skips all following `.then()` success handlers and goes to the nearest `.catch()` (or rejection handler).

javascript

```jsx
Promise.resolve(1)  .then(() => { throw new Error("Oops"); })  .then(() => console.log("skipped"))  .catch((err) => console.log(err.message)); // "Oops"
```

## 4. How does error propagation work in Promise chaining?

A rejection **travels down the chain** until a handler for it is found. Every `.then()` without a rejection handler passes the rejection along untouched. A single `.catch()` at the end can handle errors from **any** earlier step. If nothing handles it, the result is an **unhandled promise rejection**.

javascript

```jsx
step1()  .then(step2)   // error here...  .then(step3)   // ...skipped  .catch(handleError); // ...caught here
```

## 5. What happens if you use `.catch()` in the middle of a Promise chain?

`.catch()` handles the error and returns a **new Promise that is fulfilled** with whatever the catch callback returns. So the chain **recovers** and continues with the following `.then()` calls. If the catch callback itself throws (or you re-throw), the chain stays rejected.

javascript

```jsx
Promise.reject(new Error("fail"))  .catch((err) => "recovered")  .then((value) => console.log(value)); // "recovered"
```

## 6. What is the difference between handling errors using `.catch()` and the second argument of `.then()`?

`.then(onFulfilled, onRejected)` handles rejections of the **previous** Promise only. It does **not** catch errors thrown inside its own `onFulfilled`. `.catch(fn)` placed after `.then()` catches errors from the original Promise **and** from the `.then()` callback.

javascript

```jsx
// Error in onFulfilled is NOT caught by the second argumentPromise.resolve(1).then(  () => { throw new Error("boom"); },  (err) => console.log("not reached")); // unhandled rejection// .catch() catches itPromise.resolve(1)  .then(() => { throw new Error("boom"); })  .catch((err) => console.log("caught:", err.message));
```

`.catch()` is generally preferred because it is clearer and covers more cases.

## 7. What happens when you pass a Promise inside `Promise.resolve()`?

If the value is a **native Promise**, `Promise.resolve()` returns **that same Promise** (the exact same object). If it is a *thenable* (an object with a `.then` method), it is converted into a real Promise that follows it. Any other value is wrapped in a new fulfilled Promise.

javascript

```jsx
const p = Promise.resolve(42);console.log(Promise.resolve(p) === p); // true
```

## 8. What happens when you pass a rejected Promise inside `Promise.resolve()`?

You get back the **same rejected Promise**, so it stays rejected with the same reason. `Promise.resolve()` does not turn a rejection into a fulfillment, and it still needs a `.catch()` handler.

javascript

```jsx
const rejected = Promise.reject(new Error("fail"));Promise.resolve(rejected).catch((e) => console.log(e.message)); // "fail"
```

## 9. How does JavaScript handle multiple `.then()` handlers attached to the same Promise?

All handlers are stored and run **in the order they were attached**, each as its own microtask once the Promise settles. They are **independent branches**, not a chain. Each receives the **same original value**, and the return value of one does not affect the others.

javascript

```jsx
const p = Promise.resolve(10);p.then((v) => console.log("A", v));      // A 10p.then((v) => { console.log("B", v); return 99; }); // B 10p.then((v) => console.log("C", v));      // C 10
```

## 10. What is the difference between `Promise.resolve()` and creating a Promise using `new Promise()`?

|  | `Promise.resolve(value)` | `new Promise(executor)` |
| --- | --- | --- |
| Purpose | Shortcut to get an already-fulfilled Promise | Wrap callback-based or custom async logic |
| Executor | None needed | Required: `(resolve, reject) => {}` |
| Can reject | No (use `Promise.reject()`) | Yes, via `reject()` or throwing |
| Given a Promise | Returns the same Promise | Always creates a new Promise |

javascript

```jsx
const a = Promise.resolve("hi");const b = new Promise((resolve) => setTimeout(() => resolve("hi"), 1000));
```

## 11. How does `Promise.race()` behave when multiple Promises settle at nearly the same time?

`Promise.race()` is settled by whichever Promise's settlement is **processed first** by the microtask queue, and that result (fulfilled or rejected) wins. If several are already settled when `race()` is called, the **first one in the array order** wins. The remaining Promises are not cancelled and keep running, but their results are ignored.

javascript

```jsx
Promise.race([  Promise.resolve("first"),  Promise.resolve("second"),]).then(console.log); // "first"
```

## 12. What happens when one Promise rejects inside `Promise.all()`? Do the other Promises stop executing?

`Promise.all()` **rejects immediately** with the first rejection reason. The other Promises **do not stop**. Promises cannot be cancelled, so they keep running in the background and their results are simply ignored by `Promise.all()`. Their side effects (network requests, writes, and so on) still happen.

javascript

```jsx
Promise.all([  new Promise((_, rej) => setTimeout(() => rej("fail"), 100)),  new Promise((res) => setTimeout(() => { console.log("still ran"); res(); }, 500)),]).catch((e) => console.log(e)); // "fail", then later "still ran"
```

## 13. What is the difference between sequential and parallel execution of Promises?

- **Sequential**: each task starts only **after the previous one finishes**. Total time is the **sum** of all tasks.
- **Parallel**: all tasks start **at the same time**. Total time is roughly the **longest** single task.

javascript

```jsx
// Sequential: ~3sawait task(1000);await task(1000);await task(1000);// Parallel: ~1sawait Promise.all([task(1000), task(1000), task(1000)]);
```

Use sequential when tasks depend on each other, and parallel when they are independent.

## 14. How can you execute multiple asynchronous tasks sequentially using Promises?

**Option 1: Promise chaining**

javascript

```jsx
task1()  .then(() => task2())  .then(() => task3());
```

**Option 2: `reduce()` for a dynamic list**

javascript

```jsx
const tasks = [task1, task2, task3];tasks.reduce((chain, task) => chain.then(() => task()), Promise.resolve());
```

**Option 3: `async/await` in a loop (the cleanest)**

javascript

```jsx
async function runSequentially(tasks) {  const results = [];  for (const task of tasks) {    results.push(await task());  }  return results;}
```

Pass **functions that return Promises**, not already-created Promises. A Promise starts running the moment it is created, so creating them all upfront makes them run in parallel.

## 15. What is the difference between a Promise that is pending and a Promise that is fulfilled with `undefined`?

- A **pending** Promise has **not finished yet**. It has no result, and `.then()` callbacks are waiting.
- A Promise **fulfilled with `undefined`** has **already completed successfully**. Its result just happens to be `undefined`, and `.then()` callbacks will run (asynchronously) with `undefined`.

javascript

```jsx
const pending = new Promise(() => {});          // never settlesconst fulfilled = Promise.resolve(undefined);   // settled, value is undefinedfulfilled.then((v) => console.log("done", v)); // "done undefined"pending.then(() => console.log("never runs"));
```

A Promise that is fulfilled with `undefined` is **settled**, and a pending one is not.

# **JavaScript  Promised  — Advanced Questions with Answers**

## 1. How does Promise resolution work when a Promise resolves to another Promise?

When you call `resolve(otherPromise)`, the outer Promise does **not** fulfill with the inner Promise as its value. Instead it **locks in** to the inner Promise and adopts its eventual state. If the inner Promise fulfills with `v`, the outer fulfills with `v`. If the inner rejects, the outer rejects with the same reason. This is why you never see `Promise<Promise<T>>` in JavaScript.

javascript

```jsx
const inner = new Promise((res) => setTimeout(() => res("done"), 1000));const outer = new Promise((res) => res(inner));outer.then((v) => console.log(v)); // after 1s: "done" (not a Promise)
```

Adopting an inner Promise costs extra microtask ticks, so the outer Promise settles a couple of ticks later than it would with a plain value.

## 2. What is a Promise Resolution Procedure, and how does it handle thenables?

The **Promise Resolution Procedure** is the internal algorithm (written `[[Resolve]](promise, x)` in the Promises/A+ spec) that runs whenever a Promise is resolved with a value `x`. Its rules, simplified:

1. If `x` is the **same object** as the promise, reject with a `TypeError`.
2. If `x` is an **object or function**, read `x.then`. If reading it throws, reject with that error.
3. If `x.then` is a **function** (x is a *thenable*), call it with `x` as `this`, passing a `resolvePromise` and a `rejectPromise` callback. The procedure recursively resolves with whatever the thenable provides. Only the **first** call counts, and later calls are ignored.
4. If `x.then` is not a function, or `x` is not an object, **fulfill** with `x`.

javascript

```jsx
const thenable = {  then(resolve) { resolve("from thenable"); }};Promise.resolve(thenable).then(console.log); // "from thenable"
```

This is what allows different Promise libraries, and objects that only look like Promises, to interoperate.

## 3. What happens if a Promise resolves to itself?

It rejects with a **`TypeError`** (a "chaining cycle detected"). Otherwise the Promise would wait forever for itself to settle. The most common way to hit this is returning the same Promise from its own `.then()` callback.

javascript

```jsx
const p = Promise.resolve().then(() => p);p.catch((err) => console.log(err instanceof TypeError)); // true
```

## 4. How does the JavaScript event loop schedule Promise callbacks and microtasks?

The event loop runs one cycle at a time:

1. Run the current **macrotask** (for example the main script, a timer callback, or an I/O callback) until the call stack is empty.
2. Run **all microtasks** in the microtask queue. This includes microtasks added while draining, so the queue runs until it is completely empty.
3. Render (in browsers), if needed.
4. Pick the next macrotask and repeat.

When a Promise settles, its `.then()`, `.catch()` and `.finally()` callbacks are not run immediately. They are placed in the **microtask queue**. `await` continuations and `queueMicrotask()` use the same queue.

javascript

```jsx
console.log("1 sync");setTimeout(() => console.log("4 macrotask"), 0);Promise.resolve().then(() => console.log("3 microtask"));console.log("2 sync");// 1 sync, 2 sync, 3 microtask, 4 macrotask
```

## 5. What is the difference between microtasks and macrotasks when working with Promises?

|  | Microtasks | Macrotasks |
| --- | --- | --- |
| Examples | Promise callbacks, `await`, `queueMicrotask()`, `MutationObserver` | `setTimeout`, `setInterval`, I/O, UI events |
| When they run | Right after the current task, before anything else | One per event loop iteration |
| Queue draining | Entire queue is emptied each time | Only one task is taken at a time |
| Priority | Higher | Lower |

Because the whole microtask queue is drained before the next macrotask, a Promise chain that keeps scheduling new microtasks can **starve** timers, rendering and user events.

javascript

```jsx
setTimeout(() => console.log("timeout"), 0);Promise.resolve().then(() => console.log("promise"));// promise, timeout
```

## 6. What happens when you attach multiple `.then()` handlers to a Promise in different parts of your code?

Each `.then()` call registers an **independent reaction** on the same Promise. When it settles, the handlers are queued as microtasks in **the order they were attached**, and each receives the **same value**. This holds even for handlers attached from different modules or files.

If you attach a handler **after** the Promise has already settled, it is still called, asynchronously, in a new microtask. A Promise remembers its result forever.

javascript

```jsx
const p = Promise.resolve("data");p.then((v) => console.log("module A:", v));setTimeout(() => {  p.then((v) => console.log("module B (late):", v)); // still runs}, 1000);
```

An error in one handler does not affect the others, but it rejects only the Promise returned by that particular `.then()`.

## 7. How can you implement a custom version of `Promise.all()`?

javascript

```jsx
function promiseAll(promises) {  return new Promise((resolve, reject) => {    const items = Array.from(promises);    const results = new Array(items.length);    let completed = 0;    if (items.length === 0) return resolve([]);    items.forEach((item, index) => {      Promise.resolve(item)          // handles plain values and thenables        .then((value) => {          results[index] = value;    // keep original order          completed++;          if (completed === items.length) resolve(results);        })        .catch(reject);              // first rejection wins    });  });}
```

Key details: results are stored **by index** to preserve order, `Promise.resolve()` normalizes non-Promise values, an empty input resolves immediately, and calling `reject` more than once is harmless.

## 8. How would you implement a custom version of `Promise.race()`?

javascript

```jsx
function promiseRace(promises) {  return new Promise((resolve, reject) => {    for (const item of promises) {      Promise.resolve(item).then(resolve, reject);    }  });}
```

The first Promise to settle calls `resolve` or `reject`, and every later call is ignored because a Promise can only settle once. An empty array gives a Promise that stays **pending forever**, which matches the native behavior.

## 9. How can you limit the number of Promises executing concurrently?

Use a **concurrency limiter**: keep only `limit` tasks running, and start the next one each time one finishes. Tasks must be passed as **functions**, so they do not start early.

javascript

```jsx
async function runWithLimit(tasks, limit) {  const results = new Array(tasks.length);  let next = 0;  async function worker() {    while (next < tasks.length) {      const index = next++;      results[index] = await tasks[index]();    }  }  const workers = Array.from({ length: Math.min(limit, tasks.length) }, worker);  await Promise.all(workers);  return results;}// Usage: at most 3 at a timerunWithLimit(urls.map((u) => () => fetch(u)), 3);
```

`next++` is safe because JavaScript is single-threaded, so there is no race between workers.

## 10. How would you implement a Promise pool to process a large number of asynchronous tasks?

A pool is a reusable version of the limiter above. It adds results handling, error collection and a clean API.

javascript

```jsx
class PromisePool {  constructor(concurrency) {    this.concurrency = concurrency;  }  async run(items, handler) {    const results = new Array(items.length);    const errors = [];    let index = 0;    const worker = async () => {      while (index < items.length) {        const i = index++;        try {          results[i] = await handler(items[i], i);        } catch (err) {          errors.push({ index: i, error: err });        }      }    };    await Promise.all(      Array.from({ length: Math.min(this.concurrency, items.length) }, worker)    );    return { results, errors };  }}// Usage: process 1000 IDs, 5 at a timeconst pool = new PromisePool(5);const { results, errors } = await pool.run(ids, (id) => fetchUser(id));
```

Because each worker catches its own errors, one failure does not stop the rest, and the pool never has more than `concurrency` tasks in flight. For production use, consider adding retries, a progress callback, and an abort signal.

## 11. How can you cancel an asynchronous operation associated with a Promise?

A native Promise **cannot be cancelled**. Once started, the work continues. What you can do:

- **Use `AbortController`** for APIs that support it, such as `fetch`. This actually stops the underlying work.
- **Ignore the result** with a flag, so the outcome is discarded.
- **Race against a cancel Promise** so your code stops waiting.

javascript

```jsx
const controller = new AbortController();fetch("/api/data", { signal: controller.signal })  .then((res) => res.json())  .catch((err) => {    if (err.name === "AbortError") console.log("Cancelled");  });controller.abort(); // cancels the request
```

## 12. What is the difference between Promise cancellation and using `AbortController`?

**Promise cancellation** (as a concept) would mean a Promise itself has a third "cancelled" state. JavaScript does not have it. A proposal for it was withdrawn.

**`AbortController`** is a separate API for signalling cancellation. It does not touch the Promise. It sends an abort signal to the **operation**, and the operation then rejects its Promise (usually with an `AbortError`).

|  | Promise "cancellation" | `AbortController` |
| --- | --- | --- |
| Exists in JavaScript | No | Yes |
| What it stops | The Promise itself | The underlying operation |
| Result | A third state (not available) | Operation rejects with `AbortError` |
| Support needed | Not applicable | The API or your code must listen to `signal` |

You can also use it in your own code:

javascript

```jsx
function delay(ms, signal) {  return new Promise((resolve, reject) => {    const id = setTimeout(resolve, ms);    signal?.addEventListener("abort", () => {      clearTimeout(id);      reject(new DOMException("Aborted", "AbortError"));    });  });}
```

## 13. How would you implement a timeout for a Promise without modifying the original asynchronous operation?

Race the original Promise against a timer Promise that rejects, and clear the timer when the race finishes.

javascript

```jsx
function withTimeout(promise, ms) {  let timerId;  const timeout = new Promise((_, reject) => {    timerId = setTimeout(() => reject(new Error(`Timed out after${ms}ms`)), ms);  });  return Promise.race([promise, timeout]).finally(() => clearTimeout(timerId));}// UsagewithTimeout(fetch("/api/slow"), 3000)  .then((res) => console.log("ok"))  .catch((err) => console.error(err.message));
```

The original operation is **not stopped**. It keeps running and its result is ignored. To really stop it, combine this with an `AbortController` and call `controller.abort()` in the timeout. Modern runtimes also offer `AbortSignal.timeout(ms)` for this.

## 14. What happens when a Promise rejection is not handled? How does JavaScript report unhandled rejections?

If a Promise is rejected and no handler is attached by the time the microtask queue is drained, the engine treats it as an **unhandled rejection**.

- **Browsers** fire an `unhandledrejection` event on `window` and log an error to the console. A later `rejectionhandled` event fires if a handler is attached afterwards.
- **Node.js** emits an `unhandledRejection` event on `process`. Since Node 15, if nothing handles it, the process **crashes** with a non-zero exit code by default.

javascript

```jsx
// Browserwindow.addEventListener("unhandledrejection", (event) => {  console.error("Unhandled:", event.reason);  event.preventDefault(); // suppress default console error});// Node.jsprocess.on("unhandledRejection", (reason, promise) => {  console.error("Unhandled:", reason);});Promise.reject(new Error("nobody caught me"));
```

Always end chains with `.catch()` or wrap `await` in `try/catch`. Global handlers are for logging and last-resort reporting, not normal error handling.

## 15. How would you prevent a Promise chain from becoming deeply nested while preserving error handling and execution order?

The problem is "Promise hell": starting a new `.then()` chain **inside** a `.then()` callback.

javascript

```jsx
// Bad: nestedgetUser().then((user) => {  getPosts(user.id).then((posts) => {    getComments(posts[0].id).then((comments) => {      console.log(comments);    });  });});
```

**Fix 1: return the Promise and keep the chain flat.** Order and error handling are preserved, and one `.catch()` covers everything.

javascript

```jsx
getUser()  .then((user) => getPosts(user.id))  .then((posts) => getComments(posts[0].id))  .then((comments) => console.log(comments))  .catch((err) => console.error(err));
```

**Fix 2: `async/await` (the cleanest).** It reads top to bottom, and `try/catch` handles errors.

javascript

```jsx
async function load() {  try {    const user = await getUser();    const posts = await getPosts(user.id);    const comments = await getComments(posts[0].id);    console.log(comments);  } catch (err) {    console.error(err);  }}
```

If a later step needs values from earlier steps, `async/await` makes that easy because everything stays in one scope. In a flat `.then()` chain you would need to pass an object along or store values in outer variables.

# 🚀 **Follow @daily.debugging for complete frontend resources and interview preparation.**
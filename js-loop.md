# The Complete Guide of Event Loop

## 1. What is the Event Loop in JavaScript?

JavaScript is **single-threaded**, so it can run only one thing at a time. The Event Loop is the mechanism that lets it handle asynchronous work (timers, network requests, user events) without freezing.

It constantly checks one thing: **is the Call Stack empty?** If it is, the Event Loop picks the next waiting callback from the queues and pushes it onto the stack to run.

Without the Event Loop, a slow task such as a network request would block the whole page.

## 2. What is the Call Stack?

The Call Stack is a **LIFO** (Last In, First Out) structure that tracks which function is currently running.

js

```jsx
function a() { b(); }function b() { c(); }function c() { console.log("Hello"); }a();
```

Stack flow: `a` is pushed, then `b`, then `c`. After `c` finishes, it is popped, then `b`, then `a`.

If functions keep calling each other without stopping (infinite recursion), the stack fills up and you get a **Stack Overflow** error.

## 3. What are Web APIs in JavaScript?

Web APIs are features provided by the **browser**, not by the JavaScript engine itself. They run outside the Call Stack, so they don't block it.

Common examples:

- `setTimeout()` / `setInterval()`
- DOM events (`click`, `scroll`)
- `fetch()` / `XMLHttpRequest`
- `localStorage`, Geolocation

When you call one of these, JavaScript hands the work to the browser, continues running other code, and gets the result back later through a queue. (In Node.js, similar work is handled by its own system APIs instead of browser Web APIs.)

## 4. What is the Task Queue (Macrotask Queue)?

The Task Queue is a **FIFO** (First In, First Out) waiting line for callbacks that are ready to run.

It holds callbacks from:

- `setTimeout` / `setInterval`
- DOM events (click, keypress)
- I/O operations

The Event Loop takes **one task at a time** from this queue, and only when the Call Stack is empty.

## 5. What is the Microtask Queue?

The Microtask Queue is a second queue with **higher priority** than the Task Queue.

It holds:

- `.then()`, `.catch()`, `.finally()` callbacks of Promises
- Code after `await` in `async/await` functions
- `queueMicrotask()` callbacks
- `MutationObserver` callbacks

## 6. What is the difference between synchronous and asynchronous code?

| Synchronous | Asynchronous |
| --- | --- |
| Runs line by line, in order | Doesn't wait; the result comes later |
| Each line must finish before the next starts | The program continues while the task runs elsewhere |
| Can block the program | Non-blocking |

js

```jsx
console.log("A");setTimeout(() => console.log("B"), 1000);console.log("C");// Output: A C B
```

`B` is asynchronous, so the program doesn't wait for it.

## 7. How does the Event Loop work?

Step by step:

1. Synchronous code runs on the **Call Stack**.
2. Async operations (timers, fetch) are handed to the **Web APIs**.
3. When they finish, their callbacks go into the **Task Queue** (or the **Microtask Queue** for Promises).
4. When the Call Stack becomes **empty**, the Event Loop:
    - First runs **all** microtasks until the Microtask Queue is empty.
    - Then takes **one** task from the Task Queue and runs it.
5. Repeat forever.

## 8. What is the difference between the Task Queue and Microtask Queue?

|  | Task Queue | Microtask Queue |
| --- | --- | --- |
| Also called | Macrotask queue | Job queue |
| Contains | `setTimeout`, `setInterval`, events | Promise callbacks, `await`, `queueMicrotask` |
| Priority | Lower | **Higher** |
| How it's processed | One task per loop iteration | **All** microtasks are drained before the next task |

## 9. What is the role of `setTimeout()` in the Event Loop?

`setTimeout()` doesn't run the callback after the delay. It **schedules** it:

1. The timer is handed to the Web API.
2. The browser counts down the delay.
3. When it expires, the callback is placed in the **Task Queue**.
4. The Event Loop pushes it onto the Call Stack when the stack is empty.

So the delay is a **minimum** wait time, not a guarantee. If the stack is busy, the callback runs later.

## 10. Why does `setTimeout(fn, 0)` not execute immediately?

Even with `0` delay, the callback still has to:

1. Go through the Web API.
2. Wait in the Task Queue.
3. Wait for the Call Stack to be empty.
4. Wait for all microtasks to finish.

js

```jsx
console.log("Start");setTimeout(() => console.log("Timeout"), 0);console.log("End");// Start, End, Timeout
```

Browsers may also enforce a small minimum delay for timers, especially nested ones.

## 11. What happens when a function is added to the Call Stack?

1. An **execution context** is created for the function (its variables, scope, and `this`).
2. The function is **pushed** on top of the stack.
3. Its code runs line by line.
4. If it calls another function, that function is pushed on top and runs first.
5. When a function returns, it is **popped** off, and control returns to the one below it.

## 12. Which executes first: a Promise callback or a `setTimeout()` callback?

The **Promise callback** runs first, even if the timeout is `0`, because microtasks have priority over tasks.

js

```jsx
setTimeout(() => console.log("setTimeout"), 0);Promise.resolve().then(() => console.log("Promise"));// Output: Promise, setTimeout
```

## 13. What happens when the Call Stack is empty?

The Event Loop steps in:

1. It checks the **Microtask Queue** and runs every microtask in it (including new ones added while draining).
2. Then it takes the **next task** from the Task Queue and pushes it to the stack.
3. In browsers, the page may re-render between tasks.
4. The cycle repeats.

If both queues are empty, the loop simply waits for new work.

## 14. How does `fetch()` work with Promises and the Event Loop?

1. Calling `fetch(url)` hands the network request to the **browser (Web API)**. JavaScript gets back a **pending Promise** immediately and keeps running.
2. The network request happens outside the Call Stack.
3. When the response arrives, the Promise resolves.
4. Its `.then()` callback goes into the **Microtask Queue**.
5. When the stack is empty, the Event Loop runs that callback.

js

```jsx
console.log("1");fetch("https://api.example.com/data")  .then(res => res.json())  .then(data => console.log("3", data));console.log("2");// 1, 2, then 3 (later, when the response arrives)
```

Note that `fetch` only rejects on network failure. An HTTP error like 404 still resolves, so check `res.ok`.

## 15. What is the execution order of synchronous code, microtasks, and tasks?

The order is:

**1. Synchronous code → 2. Microtasks → 3. Tasks (macrotasks)**

js

```jsx
console.log("1");                                   // syncsetTimeout(() => console.log("2"), 0);              // taskPromise.resolve().then(() => console.log("3"));     // microtaskconsole.log("4");                                   // sync// Output: 1, 4, 3, 2
```

Why this order:

- `1` and `4` are synchronous, so they run first on the Call Stack.
- `3` is a microtask, so it runs as soon as the stack is empty.
- `2` is a task, so it runs last.

**Quick memory trick:** Sync code first, then **all** microtasks, then **one** task, then repeat.

 

![1.png](The%20Complete%20Guide%20of%20Event%20Loop/1.png)

![2.png](The%20Complete%20Guide%20of%20Event%20Loop/2.png)

![3.png](The%20Complete%20Guide%20of%20Event%20Loop/3.png)

![4.png](The%20Complete%20Guide%20of%20Event%20Loop/4.png)

![5.png](The%20Complete%20Guide%20of%20Event%20Loop/5.png)

![6.png](The%20Complete%20Guide%20of%20Event%20Loop/6.png)

![7.png](The%20Complete%20Guide%20of%20Event%20Loop/7.png)

![8.png](The%20Complete%20Guide%20of%20Event%20Loop/8.png)

![9.png](The%20Complete%20Guide%20of%20Event%20Loop/9.png)

![10.png](The%20Complete%20Guide%20of%20Event%20Loop/10.png)

![11.png](The%20Complete%20Guide%20of%20Event%20Loop/11.png)

![12.png](The%20Complete%20Guide%20of%20Event%20Loop/12.png)

# **JavaScript  Event Loop — Intermediate Questions with Answers**

## 1. What is the Event Loop, and why is it important in JavaScript?

The Event Loop is the mechanism that watches the **Call Stack** and the **callback queues**. When the stack is empty, it moves the next waiting callback onto the stack to run.

**Why it matters:** JavaScript has only one thread, so without the Event Loop, any slow operation (a timer, a network request) would freeze the entire page. The Event Loop makes non-blocking, asynchronous behavior possible.

## 2. How does JavaScript handle asynchronous operations despite being single-threaded?

JavaScript itself runs one thing at a time, but the **environment around it** (the browser or Node.js) can do work in the background.

1. JavaScript hands slow work (timers, network, events) to the **Web APIs**.
2. The browser performs that work outside the Call Stack.
3. When it finishes, the callback is placed in a **queue**.
4. The **Event Loop** moves it to the Call Stack when the stack is free.

So the JavaScript engine is single-threaded, but the runtime is not.

## 3. What is the difference between the Call Stack, Web APIs, and Task Queue?

| Part | Role | Who provides it |
| --- | --- | --- |
| **Call Stack** | Runs functions one at a time (LIFO) | JavaScript engine |
| **Web APIs** | Handle async work in the background (timers, fetch, DOM events) | Browser |
| **Task Queue** | Holds finished callbacks waiting for their turn (FIFO) | Browser/runtime |

In short: the stack **executes**, Web APIs **wait and work**, and the queue **holds** callbacks until the stack is free.

## 4. Explain the complete execution flow of `setTimeout()` using the Event Loop.

js

```jsx
console.log("Start");setTimeout(() => console.log("Timer"), 1000);console.log("End");
```

1. `console.log("Start")` is pushed on the Call Stack, runs, and is popped.
2. `setTimeout` is pushed on the stack. It registers the timer with the **Web API** and is popped immediately.
3. `console.log("End")` runs.
4. The Call Stack is now empty, and the browser keeps counting down the 1000 ms.
5. When the timer expires, the callback moves into the **Task Queue**.
6. The Event Loop sees the stack is empty, checks the microtasks (none), and pushes the callback onto the stack.
7. `"Timer"` is printed.

Output: `Start`, `End`, `Timer`

## 5. What is the difference between the Microtask Queue and the Macrotask Queue?

|  | Microtask Queue | Macrotask (Task) Queue |
| --- | --- | --- |
| Contains | Promise `.then/.catch/.finally`, `await` continuations, `queueMicrotask`, `MutationObserver` | `setTimeout`, `setInterval`, DOM events, I/O |
| Priority | **Higher** | Lower |
| Processing | **All** microtasks are drained before moving on | **One** task per loop iteration |
| Runs | Right after the current code finishes | Only after microtasks are empty |

## 6. Why do Promise callbacks execute before `setTimeout()` callbacks?

Because of how the Event Loop prioritizes queues:

- Promise callbacks go into the **Microtask Queue**.
- `setTimeout` callbacks go into the **Task Queue**.
- After the Call Stack empties, the Event Loop **always drains the Microtask Queue first**, and only then picks a task.

js

```jsx
setTimeout(() => console.log("timeout"), 0);Promise.resolve().then(() => console.log("promise"));// promise, timeout
```

This holds even if the timeout is `0`.

## 7. What happens when the Call Stack is busy and a callback is waiting in the Task Queue?

The callback **waits**. The Event Loop only moves a callback to the stack when the stack is completely empty, so a busy stack delays it, no matter how long ago its timer expired.

js

```jsx
setTimeout(() => console.log("Timer"), 100);const start = Date.now();while (Date.now() - start < 2000) {} // blocks for 2 seconds// "Timer" prints only after about 2 seconds, not 100 ms
```

This is why `setTimeout` delay is a **minimum**, not an exact time.

## 8. Does `setTimeout(callback, 0)` execute immediately? Why or why not?

**No.** Even with `0`, the callback must:

1. Pass through the Web API.
2. Go into the Task Queue.
3. Wait until the Call Stack is empty.
4. Wait until all microtasks are finished.

js

```jsx
setTimeout(() => console.log("B"), 0);console.log("A");// A, B
```

So `0` means "run as soon as possible after the current code and microtasks", not "run now".

## 9. How does `fetch()` interact with Web APIs, Promises, and the Microtask Queue?

1. `fetch(url)` is a **Web API**. The browser performs the network request outside the Call Stack.
2. It immediately returns a **pending Promise** to JavaScript.
3. JavaScript continues running other code.
4. When the response arrives, the Promise is **resolved**.
5. The `.then()` callback is placed in the **Microtask Queue**.
6. When the stack is empty, the Event Loop runs it.

js

```jsx
console.log("1");fetch(url).then(res => console.log("3"));console.log("2");// 1, 2, 3
```

The network work uses the Web API, but the callbacks use the Promise and the Microtask Queue.

## 10. What is the difference between a task and a microtask in JavaScript?

- A **task** (macrotask) is a larger unit of scheduled work, such as a timer callback, an event handler, or running a script. The Event Loop runs **one task** per iteration.
- A **microtask** is a small, short follow-up job, mostly from Promises. The Event Loop runs **all microtasks** after the current task finishes, before the next task starts.

Think of it as: a task is the main job, and microtasks are the quick follow-ups that must finish before the next main job begins.

## 11. What happens if a microtask creates another microtask? When will the new microtask execute?

The new microtask is added to the **end of the Microtask Queue** and runs **in the same drain cycle**, before any task from the Task Queue.

js

```jsx
setTimeout(() => console.log("timeout"), 0);Promise.resolve().then(() => {  console.log("micro 1");  Promise.resolve().then(() => console.log("micro 2"));});// micro 1, micro 2, timeout
```

**Danger:** if microtasks keep creating new microtasks forever, the queue never empties. The Task Queue and page rendering are **starved**, and the page freezes.

## 12. How does the Event Loop coordinate the Call Stack and callback queues?

It runs a continuous loop:

1. Run the current script on the **Call Stack** (synchronous code).
2. When the stack is empty, **drain the Microtask Queue** completely.
3. (In browsers) the page may **re-render**.
4. Take **one task** from the Task Queue and run it on the stack.
5. After that task, drain microtasks again.
6. Repeat.

The Event Loop never runs callbacks while the stack is busy. It only acts as the coordinator that decides **what runs next**.

## 13. What is the output of the following code, and why?

js

```jsx
console.log("A");setTimeout(() => console.log("B"), 0);Promise.resolve().then(() => console.log("C"));console.log("D");
```

**Output:** `A`, `D`, `C`, `B`

**Why:**

1. `console.log("A")` is synchronous, so it prints `A`.
2. `setTimeout` sends its callback to the Web API, which then queues it in the **Task Queue**.
3. `Promise.resolve().then(...)` queues its callback in the **Microtask Queue**.
4. `console.log("D")` is synchronous, so it prints `D`.
5. The stack is empty, so microtasks run first and print `C`.
6. Then the task runs and prints `B`.

## 14. What happens if an infinite loop blocks the Call Stack? Can the Event Loop execute callbacks during that time?

**No.** The Event Loop can only move callbacks when the Call Stack is empty. An infinite loop means the stack is never empty, so:

- No callbacks (timers, events, Promises) can run.
- The page **freezes**: clicks, scrolling, and rendering stop.
- The browser may eventually show an "unresponsive page" warning.

js

```jsx
setTimeout(() => console.log("Never runs"), 1000);while (true) {} // blocks forever
```

The timer in the Web API may finish, and the callback may wait in the queue, but it never reaches the stack.

**Fix:** break heavy work into smaller chunks, or move it to a **Web Worker**.

## 15. What is the difference between `queueMicrotask()`, `Promise.then()`, and `setTimeout()` in terms of execution order?

- `queueMicrotask()` and `Promise.then()` both schedule **microtasks**, so they run **before** `setTimeout`.
- Between those two, order depends on **when they were queued** (first queued, first run).
- `setTimeout()` schedules a **task**, so it runs last.

js

```jsx
setTimeout(() => console.log("setTimeout"), 0);Promise.resolve().then(() => console.log("Promise.then"));queueMicrotask(() => console.log("queueMicrotask"));console.log("sync");
```

**Output:** `sync`, `Promise.then`, `queueMicrotask`, `setTimeout`

| Method | Queue | Runs |
| --- | --- | --- |
| `Promise.then()` | Microtask | After sync code, in queued order |
| `queueMicrotask()` | Microtask | After sync code, in queued order |
| `setTimeout()` | Task | After all microtasks |

# **JavaScript  Event Loop — Advanced Questions with Answers**

## 1. Explain how the Event Loop handles execution when multiple microtasks and macrotasks are scheduled simultaneously.

The rule is: **run one task, then drain all microtasks, then (maybe) render, then pick the next task.**

js

```jsx
setTimeout(() => console.log("T1"), 0);setTimeout(() => console.log("T2"), 0);Promise.resolve().then(() => console.log("M1"));queueMicrotask(() => console.log("M2"));console.log("Sync");
```

Output: `Sync`, `M1`, `M2`, `T1`, `T2`

1. The script itself is the first task. It prints `Sync`.
2. When the stack empties, all microtasks run (`M1`, `M2`).
3. The next task (`T1`) runs. After it finishes, microtasks are drained again (none here).
4. `T2` runs.

Within each queue, order is **first in, first out**.

## 2. What will be the output of the following code, and why?

js

```jsx
console.log("A");setTimeout(() => console.log("B"), 0);Promise.resolve()  .then(() => {    console.log("C");    return Promise.resolve();  })  .then(() => console.log("D"));queueMicrotask(() => console.log("E"));console.log("F");
```

**Output:** `A`, `F`, `C`, `E`, `D`, `B`

**Why:**

1. Sync code prints `A` and `F`.
2. Microtask queue at this point: `[first .then callback, E]`.
3. The first `.then` runs and prints `C`. It **returns a Promise**, which is the key detail.
4. Returning a promise (not a plain value) makes the Promise machinery add **extra microtask steps** before the next `.then` can run. The engine must adopt the returned promise's state, which takes about 2 additional microtask ticks.
5. Meanwhile `E` (already waiting in the queue) runs and prints `E`.
6. After those extra internal steps finish, the second `.then` runs and prints `D`.
7. Finally the task `setTimeout` runs and prints `B`.

If the first `.then` had returned a plain value (or nothing), the output would be `A F C D E B`.

## 3. What happens when a microtask continuously schedules new microtasks? How can this affect macrotask execution and rendering?

The Microtask Queue is drained **until it is empty**, including microtasks added while draining. If every microtask schedules another, the queue never empties, so:

- **Macrotasks never run** (timers, click handlers, network callbacks).
- **Rendering never happens**, so the page freezes.
- The tab becomes unresponsive, even though the Call Stack technically keeps going empty and refilling.

js

```jsx
function loop() {  Promise.resolve().then(loop);}loop(); // starves everything else
```

Compare this with `setTimeout(loop, 0)`, which schedules a **task**. That lets rendering and other tasks run in between, so the page stays responsive.

## 4. How does `async/await` interact with the Call Stack, Promises, and Microtask Queue?

- An `async` function **always returns a Promise**.
- It runs **synchronously** on the Call Stack until the first `await`.
- At `await`, the function is **paused**, the rest of it becomes a continuation, and control returns to the caller (the function is popped from the stack).
- When the awaited promise settles, the continuation is placed in the **Microtask Queue**.
- The Event Loop resumes it when the stack is empty.

js

```jsx
async function foo() {  console.log(1);  await null;  console.log(2);}console.log(0);foo();console.log(3);// 0, 1, 3, 2
```

`await` is essentially syntax sugar over `.then()`: the code after `await` behaves like a `.then()` callback.

## 5. What is the difference between a task checkpoint and a task in the HTML Event Loop model?

The term in the HTML specification is actually the **microtask checkpoint** (there is no standard "task checkpoint").

- A **task** is a unit of work taken from a task queue: running a script, an event callback, a timer callback, and so on.
- A **microtask checkpoint** is a point where the browser **drains the Microtask Queue**. It happens after a task finishes, and also whenever the JavaScript Call Stack becomes empty after a callback (for example, after each event listener is invoked by the browser).

So a task is **what runs**, and a microtask checkpoint is **when the microtasks get to run**.

## 6. Can two different task sources have different scheduling priorities? How does the browser decide which task to execute next?

**Yes.** The HTML spec defines multiple task queues, grouped by **task source** (DOM manipulation, user interaction, networking, timers, and so on). It guarantees only that:

- Tasks from the **same** task source run in **order** (FIFO).
- Which queue the browser picks next is **implementation-defined**.

In practice, browsers give **user interaction** (clicks, typing) higher priority than things like timers, so the page feels responsive. Modern browsers use internal schedulers with priority levels, and the web exposes this partly through the Scheduler API (`scheduler.postTask()`).

## 7. How does the Event Loop behave differently in browsers and Node.js?

|  | Browser | Node.js |
| --- | --- | --- |
| Implementation | HTML spec, per-source task queues | **libuv**, with fixed phases |
| Rendering | Has a rendering step (style, layout, paint, `requestAnimationFrame`) | No rendering |
| Structure | Task → microtasks → render opportunity | Timers → pending callbacks → idle/prepare → **poll** (I/O) → **check** (`setImmediate`) → close callbacks |
| Special queues | Microtask queue | `process.nextTick` queue **and** Promise microtask queue |

In modern Node.js (since v11), microtasks are drained **between individual callbacks**, which brings it closer to browser behavior.

## 8. Explain the difference between `process.nextTick()`, `setImmediate()`, `setTimeout()`, and Promise callbacks in Node.js.

| API | When it runs |
| --- | --- |
| `process.nextTick()` | Right after the current operation, **before** other microtasks. It has its own queue with the highest priority. |
| Promise `.then()` | Microtask queue, after the `nextTick` queue is drained |
| `setTimeout(fn, 0)` | **Timers phase** of the next loop iteration |
| `setImmediate()` | **Check phase**, right after the poll (I/O) phase |

js

```jsx
setTimeout(() => console.log("timeout"), 0);setImmediate(() => console.log("immediate"));Promise.resolve().then(() => console.log("promise"));process.nextTick(() => console.log("nextTick"));console.log("sync");// sync, nextTick, promise, then timeout/immediate
```

Notes:

- From the **main module**, the order of `timeout` and `immediate` is **not guaranteed**.
- Inside an **I/O callback**, `setImmediate` always runs **before** `setTimeout(..., 0)`.
- Overusing `process.nextTick` recursively can starve I/O, just like recursive microtasks.

## 9. Why might a `setTimeout()` callback execute later than its specified delay, even when the timer has already expired?

The delay is only the **minimum** time before the callback is *eligible* to run. It can be late because:

1. **The Call Stack is busy** with long synchronous code.
2. **Other tasks are ahead** in the queue.
3. **Microtasks** are still being drained.
4. **Timer clamping**: browsers enforce a minimum delay (about 4 ms) for deeply nested timers.
5. **Background tab throttling**: inactive tabs may run timers only about once per second or less.
6. The browser or device is busy (CPU load, rendering work).

## 10. What is the role of rendering opportunities in the browser Event Loop? Why might a browser delay painting while JavaScript is executing?

A **rendering opportunity** is a moment, typically about once per display refresh (every ~16.7 ms at 60 Hz), when the browser may update the screen. During it, the browser runs:

1. `requestAnimationFrame` callbacks
2. Style calculation
3. Layout
4. Paint

This happens **between tasks**, after microtasks have been drained.

JavaScript and rendering share the **same main thread**. While a script runs, the browser **cannot paint**, so a long task delays the next frame. That is why heavy synchronous code makes the page look frozen or janky. Browsers may also skip a rendering opportunity if nothing visual has changed.

## 11. What will happen if a Promise callback throws an error? How does Promise rejection propagate across chained `.then()` handlers?

If a `.then()` callback throws, the promise returned by that `.then()` becomes **rejected** with that error. The rejection then travels down the chain, **skipping** `.then()` success handlers until it reaches a `.catch()` (or a `.then()` with a second argument).

js

```jsx
Promise.resolve()  .then(() => { throw new Error("Oops"); })  .then(() => console.log("Skipped"))  .catch(err => { console.log("Caught:", err.message); return "recovered"; })  .then(value => console.log("Continues:", value));// Caught: Oops// Continues: recovered
```

Key points:

- After `.catch()` handles the error and returns normally, the chain continues in the **fulfilled** state.
- An **unhandled rejection** triggers the `unhandledrejection` event in browsers. In Node.js (v15+) it crashes the process by default.
- The same applies to `async/await`: a thrown error becomes a rejected promise, which you catch with `try/catch`.

## 12. How does `MutationObserver` interact with the Microtask Queue, and what makes it different from a normal DOM event callback?

- `MutationObserver` callbacks are delivered as **microtasks**. They run after the current script or task finishes, before rendering.
- Multiple DOM changes are **batched** into one callback that receives an array of mutation records.

|  | `MutationObserver` | Normal DOM event (e.g. `click`) |
| --- | --- | --- |
| Queue | Microtask | Task (macrotask) |
| Timing | Right after the current code, before rendering | Whenever its task is scheduled |
| Batching | Yes, one callback for many changes | One callback per event |

This is also why it replaced the old **Mutation Events**, which fired synchronously on every change and were slow.

## 13. Consider the following code. Explain the execution order and the role of Promise resolution in the result.

js

```jsx
Promise.resolve()  .then(() => {    console.log("A");    queueMicrotask(() => console.log("B"));  })  .then(() => console.log("C"));queueMicrotask(() => console.log("D"));console.log("E");
```

**Output:** `E`, `A`, `D`, `B`, `C`

**Why:**

1. Sync code runs: `E` is printed. Before that, the queue was set up as `[first .then callback, D]`.
2. The first `.then` callback runs: prints `A` and queues `B` at the **end** of the queue, so the queue is now `[D, B]`.
3. When that callback finishes (returning `undefined`), its promise resolves, which schedules the **second `.then`** (the `C` callback) at the end: `[D, B, C]`.
4. They run in order: `D`, `B`, `C`.

The key idea is that a chained `.then()` callback is queued only **after** the previous one finishes, so `C` lands behind microtasks that were already queued.

## 14. How can long-running synchronous JavaScript block user interactions, timers, and rendering? What strategies can help prevent this?

All of these need the **main thread**, which can only do one thing at a time. While a long synchronous task occupies the Call Stack:

- Click handlers and other events can't run.
- Timers can't fire (their callbacks wait in the queue).
- The browser can't paint or update the screen.

**Strategies:**

- **Break the work into chunks** and yield between them (`setTimeout`, `scheduler.yield()`, `requestIdleCallback`).
- Move heavy computation to a **Web Worker**.
- Use **asynchronous APIs** instead of synchronous ones.
- **Debounce/throttle** frequent events.
- Use `requestAnimationFrame` for visual updates.
- Reduce the work itself (better algorithms, pagination, list virtualization).

js

```jsx
function processInChunks(items) {  let i = 0;  function chunk() {    const end = Math.min(i + 1000, items.length);    for (; i < end; i++) { /* work on items[i] */ }    if (i < items.length) setTimeout(chunk, 0); // lets the browser breathe  }  chunk();}
```

## 15. Is the statement "all microtasks always execute before every macrotask" completely accurate? Explain the limitations of this simplified rule in browser and Node.js environments.

It's a **good rule of thumb**, but it is a simplification. The limitations:

1. **Microtasks only run when the Call Stack is empty.** Microtasks queued during a running task wait until that task's synchronous code finishes. They aren't run "between lines" of code.
2. **Programmatic events behave differently.** If a script calls `button.click()`, the listeners run inside the same call stack, so microtasks **don't** run between listeners. When a **real user click** triggers the listeners, microtasks run **between** each listener.
3. **Starvation.** If microtasks keep scheduling microtasks, the "before every macrotask" part holds, but macrotasks may never run at all.
4. **Node.js has an extra queue.** `process.nextTick` callbacks run **before** Promise microtasks, and Node's phases (timers, poll, check) add ordering rules that the simple model doesn't describe.
5. **Node module type matters.** In ES modules, top-level code runs inside a Promise context, which can change the relative order of `nextTick` and Promise callbacks compared to CommonJS.
6. **Rendering sits between tasks.** In browsers, the render step happens after microtasks but before the next task, which the simple rule doesn't show.
7. **Separate event loops.** Web Workers and other contexts each have their own event loop, so the rule applies **per event loop**, not globally.

A more accurate version: *after each task (and whenever the Call Stack empties), the microtask queue is drained completely before the next task begins.*

# 🚀 **Follow @daily.debugging for complete frontend resources and interview preparation.**
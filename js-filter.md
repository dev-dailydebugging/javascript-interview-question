# The Complete Guide of filter() js

## JavaScript `filter()`

### 1. What is `filter()`?

`filter()` is a built-in **array method**. It goes through every element of an array, tests each one with a function you give it, and returns a **new array** containing only the elements that passed the test.

Think of it as a sieve: everything goes in, only the matching items come out.

### 2. Syntax

js

```jsx
const result = array.filter(function (element, index, array) {  return condition;}, thisArg);
```

| Part | Meaning |
| --- | --- |
| `element` | The current item being checked (required) |
| `index` | Position of that item (optional) |
| `array` | The original array (optional) |
| `thisArg` | Value to use as `this` inside the callback (rarely used) |

**Returns:** a new array with the passing elements. If nothing passes, it returns `[]`.

### 3. How it works, step by step

js

```jsx
const nums = [10, 15, 20, 25];const result = nums.filter(n => n > 12);
```

1. `10 > 12` is false, so 10 is skipped.
2. `15 > 12` is true, so 15 is kept.
3. `20 > 12` is true, so 20 is kept.
4. `25 > 12` is true, so 25 is kept.

`result` is `[15, 20, 25]`.

### 4. Basic examples

**Numbers**

js

```jsx
const nums = [1, 2, 3, 4, 5, 6];nums.filter(n => n % 2 === 0);   // [2, 4, 6]
```

**Strings**

js

```jsx
const words = ["apple", "banana", "kiwi", "mango"];words.filter(w => w.length > 4); // ["apple", "banana", "mango"]
```

**Array of objects** (the most common real-world use)

js

```jsx
const products = [  { name: "Pen", price: 10, inStock: true },  { name: "Book", price: 250, inStock: false },  { name: "Bag", price: 800, inStock: true }];products.filter(p => p.inStock);// [{Pen}, {Bag}]products.filter(p => p.price < 500 && p.inStock);// [{Pen}]
```

### 5. Using `index` and `array`

js

```jsx
const letters = ["a", "b", "c", "d"];// Keep only items at even positionsletters.filter((item, index) => index % 2 === 0);  // ["a", "c"]
```

**Removing duplicates**

js

```jsx
const arr = [1, 2, 2, 3, 3, 3];arr.filter((item, index, array) => array.indexOf(item) === index);// [1, 2, 3]
```

This works because `indexOf` returns the *first* position of a value. A duplicate's own index won't match it, so the duplicate is dropped.

### 6. Truthy and falsy: how the callback is judged

The callback doesn't have to return `true` or `false`. Any **truthy** value keeps the item, and any **falsy** value drops it.

Falsy values: `false`, `0`, `""`, `null`, `undefined`, `NaN`.

**Removing falsy values from an array**

js

```jsx
const mixed = [0, "hello", "", null, 42, undefined, false, "JS"];mixed.filter(Boolean);   // ["hello", 42, "JS"]
```

`filter(Boolean)` is a popular shortcut: `Boolean` is itself a function that converts a value to true or false.

### 7. `filter()` does NOT modify the original array

js

```jsx
const original = [1, 2, 3, 4];const filtered = original.filter(n => n > 2);console.log(original); // [1, 2, 3, 4]console.log(filtered); // [3, 4]
```

This is called **immutability**. It's the reason `filter()` is used so much in React: state should never be changed directly.

### 8. Chaining with other methods

Because `filter()` returns an array, you can chain more array methods right after it.

js

```jsx
const users = [  { name: "Asha", age: 17 },  { name: "Ravi", age: 25 },  { name: "Meera", age: 30 }];const adultNames = users  .filter(u => u.age >= 18)   // keep adults  .map(u => u.name);          // take only namesconsole.log(adultNames);      // ["Ravi", "Meera"]
```

Common combos: `filter().map()`, `filter().length` (to count matches), `filter().reduce()`.

### 9. `filter()` in React (useful for your debugging topics too)

**Delete an item from state**

jsx

```jsx
const handleDelete = (id) => {  setTodos(todos.filter(todo => todo.id !== id));};
```

**Search or filter a list**

jsx

```jsx
const visible = products.filter(p =>  p.name.toLowerCase().includes(searchText.toLowerCase()));return visible.map(p => <li key={p.id}>{p.name}</li>);
```

### 10. `filter()` vs `find()` vs `map()`

| Method | Returns | Use when |
| --- | --- | --- |
| `filter()` | New array of **all** matches | You want every item that matches |
| `find()` | The **first** matching item (or `undefined`) | You want just one item |
| `map()` | New array of the **same length**, with transformed items | You want to change every item |
| `some()` | `true`/`false` | You only need to know if at least one matches |

js

```jsx
const nums = [5, 12, 8, 20];nums.filter(n => n > 10);  // [12, 20]nums.find(n => n > 10);    // 12nums.some(n => n > 10);    // true
```

### 11. Common mistakes

**1. Forgetting `return` with curly braces**

js

```jsx
nums.filter(n => { n > 5 });        // wrong: returns undefined, so result is []nums.filter(n => { return n > 5 }); // correctnums.filter(n => n > 5);            // correct (implicit return)
```

**2. Using `filter()` to find a single item**

js

```jsx
users.filter(u => u.id === 3)[0];   // works, but wastefulusers.find(u => u.id === 3);        // better
```

**3. Expecting the original array to change**

js

```jsx
nums.filter(n => n > 5);            // result thrown away!nums = nums.filter(n => n > 5);     // store the result
```

**4. Returning the wrong thing from a transform**

`filter()` only decides keep or drop. It never changes the items. To transform them, use `map()`.

**5. Not handling an empty result**

js

```jsx
const matches = list.filter(...);if (matches.length === 0) { /* show "No results" */ }
```

### 12. Edge cases

- It works on **empty arrays** and returns `[]`.
- It skips **empty slots** in sparse arrays (e.g. `[1, , 3]`).
- The callback is **not** called for elements added after `filter()` starts.
- It does not mutate the array, but it keeps the **same object references**. Objects in the new array are the same objects, not copies:

js

```jsx
const a = [{ x: 1 }];const b = a.filter(() => true);b[0].x = 99;console.log(a[0].x);  // 99 (same object!)
```

### 13. Quick summary

- `filter()` returns a new array of elements that pass your test.
- The callback returns truthy to keep an item and falsy to drop it.
- The original array is untouched.
- It's chainable, and very common in React for search, delete, and conditional lists.
- Use `find()` for one item, `map()` to transform, and `filter()` to select.

### 14. Practice problems

1. From `[3, 8, 12, 5, 20]`, get numbers greater than 10.
2. From an array of names, keep only those starting with "A".
3. From an array of products, keep those with `price < 100` and `inStock === true`.
4. Remove all falsy values from `[0, 1, "", "a", null, 2]`.
5. Remove duplicates from `[1, 1, 2, 3, 3]` using `filter()`.
6. Given a todo list in React state, write a function that deletes a todo by `id`.

# **JavaScript  filter() — Basic Interview Questions with Answers**

## 1. What is the purpose of `filter()` in JavaScript?

`filter()` creates a **new array** containing only the elements that pass a test. You give it a callback function. If the callback returns a **truthy** value for an element, that element is kept. If it returns a **falsy** value, the element is left out.

js

```jsx
const nums = [1, 2, 3, 4, 5];const evens = nums.filter(n => n % 2 === 0);console.log(evens); // [2, 4]
```

Use it whenever you need "only the items that match some condition".

---

## 2. Does `filter()` modify the original array?

**No.** `filter()` is **non-mutating**. It leaves the original array unchanged and returns a new array.

js

```jsx
const nums = [1, 2, 3, 4];const result = nums.filter(n => n > 2);console.log(result); // [3, 4]console.log(nums);   // [1, 2, 3, 4]  (unchanged)
```

Note that the new array is a *shallow* copy. If the elements are objects, the new array holds the **same object references**, so changing an object's property affects both arrays.

---

## 3. What does `filter()` return if no elements satisfy the condition?

It returns an **empty array** `[]`. It never returns `null`, `undefined` or an error.

js

```jsx
const result = [1, 2, 3].filter(n => n > 10);console.log(result); // []
```

This makes it safe to chain further array methods or check `result.length`.

---

## 4. What is the difference between `filter()` and `map()`?

|  | `filter()` | `map()` |
| --- | --- | --- |
| Purpose | **Select** some elements | **Transform** every element |
| Callback returns | A boolean (truthy/falsy) | The new value for each element |
| Length of result | Same or **shorter** than the original | **Always the same** as the original |
| Element values | Unchanged | Changed |
| Mutates original? | No | No |

js

```jsx
const nums = [1, 2, 3, 4];nums.filter(n => n > 2);  // [3, 4]       (fewer items, same values)nums.map(n => n * 2);     // [2, 4, 6, 8] (same count, new values)
```

They are often combined:

js

```jsx
nums.filter(n => n % 2 === 0).map(n => n * 10); // [20, 40]
```

---

## 5. What arguments are passed to the `filter()` callback function?

The callback receives **three arguments**:

1. **`element`**: the current item being processed.
2. **`index`**: the index of the current item.
3. **`array`**: the original array `filter()` was called on.

js

```jsx
const arr = ["a", "b", "c"];arr.filter((element, index, array) => {  console.log(element, index, array);  return true;});// a 0 ["a","b","c"]// b 1 ["a","b","c"]// c 2 ["a","b","c"]
```

`filter()` also accepts an optional second argument, `thisArg`, which sets the value of `this` inside a regular (non-arrow) callback. It is rarely needed.

---

## 6. What is the output?

js

```jsx
const nums = [1, 2, 3, 4, 5];const result = nums.filter(num => num > 3);console.log(result);
```

**Output:**

```
[4, 5]
```

Only 4 and 5 are greater than 3.

---

## 7. What is the output?

js

```jsx
const nums = [10, 15, 20, 25];const result = nums.filter(num => num % 5 === 0);console.log(result);
```

**Output:**

```
[10, 15, 20, 25]
```

Every number is divisible by 5 (remainder 0), so all of them pass.

---

## 8. What is the output?

js

```jsx
const users = [  { name: "A", age: 20 },  { name: "B", age: 15 },  { name: "C", age: 25 }];const result = users.filter(user => user.age >= 18);console.log(result);
```

**Output:**

```
[
  { name: "A", age: 20 },
  { name: "C", age: 25 }
]
```

User B (age 15) fails `age >= 18`, so B is removed. The objects are the **same references** as in the original array, not copies.

---

## 9. What happens here?

js

```jsx
const nums = [1, 2, 3];const result = nums.filter(() => false);console.log(result);
```

**Output:**

```
[]
```

The callback always returns `false`, so no element passes and the result is an empty array.

---

## 10. What happens here?

js

```jsx
const nums = [1, 2, 3];const result = nums.filter(() => true);console.log(result);
```

**Output:**

```
[1, 2, 3]
```

Every element passes. The result has the same values as the original, but it is a **new array**, so `result === nums` is `false`. This is a common way to make a shallow copy.

---

## 11. How would you remove duplicate values from an array using `filter()`?

Keep an element only if its **current index equals the index of its first occurrence** (found by `indexOf`).

js

```jsx
const arr = [1, 2, 2, 3, 4, 4, 5];const unique = arr.filter((value, index, array) => array.indexOf(value) === index);console.log(unique); // [1, 2, 3, 4, 5]
```

How it works: for the second `2` (index 2), `indexOf(2)` returns 1, which is not equal to 2, so it is filtered out.

Notes:

- This is O(n²) because `indexOf` scans the array each time. It is fine for small arrays.
- For large arrays, `Set` is faster and shorter: `[...new Set(arr)]`.
- `indexOf` cannot find `NaN`, so `[NaN, NaN].filter((v, i, a) => a.indexOf(v) === i)` returns an empty array. A `Set` handles `NaN` correctly.
- For arrays of objects, de-duplicate by a key, for example: `arr.filter((o, i, a) => a.findIndex(x => x.id === o.id) === i)`.

---

## 12. How would you filter users whose role is `"admin"`?

js

```jsx
const users = [  { name: "A", role: "admin" },  { name: "B", role: "user" },  { name: "C", role: "admin" }];const admins = users.filter(user => user.role === "admin");console.log(admins);// [{ name: "A", role: "admin" }, { name: "C", role: "admin" }]
```

Use strict equality (`===`) so that only the exact string `"admin"` matches. For several roles, use `includes`:

js

```jsx
const privileged = users.filter(u => ["admin", "moderator"].includes(u.role));
```

---

## 13. How would you filter products that are currently in stock?

Assume each product has an `inStock` boolean (or a `stock` number).

js

```jsx
const products = [  { name: "Laptop", inStock: true },  { name: "Phone", inStock: false },  { name: "Tablet", inStock: true }];const available = products.filter(product => product.inStock);console.log(available);// [{ name: "Laptop", inStock: true }, { name: "Tablet", inStock: true }]
```

If stock is stored as a quantity:

js

```jsx
const available = products.filter(p => p.stock > 0);
```

In React, this is commonly written inside the component before rendering:

jsx

```jsx
{products.filter(p => p.inStock).map(p => <li key={p.id}>{p.name}</li>)}
```

---

## 14. Can `filter()` be used on strings directly? If not, how can you filter characters from a string?

**No.** `filter()` is an **array method**, and strings don't have it. `"hello".filter(...)` throws `TypeError: "hello".filter is not a function`.

Convert the string to an array first, filter, then join back:

js

```jsx
const str = "hello world";// remove spacesconst noSpaces = str.split("").filter(ch => ch !== " ").join("");console.log(noSpaces); // "helloworld"// keep only vowelsconst vowels = [...str].filter(ch => "aeiou".includes(ch)).join("");console.log(vowels); // "eoo"
```

- `str.split("")` and `[...str]` both turn the string into an array of characters.
- The spread version `[...str]` handles emoji and other Unicode characters better, because `split("")` can break characters made of two code units.
- `join("")` turns the array back into a string.

---

## 15. What is the difference between these two?

js

```jsx
const result = arr.filter(x => x > 10);
```

js

```jsx
const result = arr.filter(x => {  x > 10;});
```

**The first works. The second does not.**

- **First version:** an arrow function **without braces** has an **implicit return**. `x > 10` is returned, so `filter` receives `true` or `false`.
- **Second version:** with **curly braces `{ }`**, the arrow function has a block body, and you must write `return` yourself. The expression `x > 10;` is evaluated and thrown away, so the function returns `undefined`. `undefined` is falsy, so **every element is filtered out**.

js

```jsx
const arr = [5, 12, 20];arr.filter(x => x > 10);         // [12, 20]arr.filter(x => { x > 10; });    // []   (always undefined → falsy)
```

**Fix for the second version:**

js

```jsx
const result = arr.filter(x => {  return x > 10;});
```

Rule: use braces and `return` together, or leave out both.

![1.png](The%20Complete%20Guide%20of%20filter()%20js/1.png)

![2.png](The%20Complete%20Guide%20of%20filter()%20js/2.png)

![3.png](The%20Complete%20Guide%20of%20filter()%20js/3.png)

![4.png](The%20Complete%20Guide%20of%20filter()%20js/4.png)

![5.png](The%20Complete%20Guide%20of%20filter()%20js/5.png)

![6.png](The%20Complete%20Guide%20of%20filter()%20js/6.png)

![7.png](The%20Complete%20Guide%20of%20filter()%20js/7.png)

![8.png](The%20Complete%20Guide%20of%20filter()%20js/8.png)

![9.png](The%20Complete%20Guide%20of%20filter()%20js/9.png)

![10.png](The%20Complete%20Guide%20of%20filter()%20js/10.png)

![11.png](The%20Complete%20Guide%20of%20filter()%20js/11.png)

![final.png](The%20Complete%20Guide%20of%20filter()%20js/final.png)

# **JavaScript  filter() — Intermediate Interview Questions with Answers**

## 1. How does `filter()` work internally, and what does its callback return determine?

Internally, `filter()` does roughly this:

1. Creates a new empty array.
2. Loops over the original array from index `0` up to the **original length** (read once at the start).
3. For each index that actually exists, calls your callback with `(element, index, array)`.
4. Converts the callback's return value to a boolean (truthy or falsy).
5. If truthy, **pushes the element** into the new array. If falsy, skips it.
6. Returns the new array.

So the callback's return value decides **only whether the element is kept**. It cannot change the element itself.

js

```jsx
[0, 1, "", "hi", null].filter(x => x);// [1, "hi"]  (the callback returns the element, which is used as truthy/falsy)
```

Falsy values are `false`, `0`, `""`, `null`, `undefined`, `NaN`. Everything else is truthy, so the callback doesn't have to return a strict boolean.

---

## 2. What happens if the `filter()` callback doesn't explicitly return anything?

js

```jsx
const result = [1, 2, 3].filter(num => {  num > 1;});
```

**Output:**

```
[]
```

The arrow function uses **curly braces**, so it has a block body and no implicit return. `num > 1;` is evaluated and discarded, and the function returns `undefined`. `undefined` is falsy, so **every element is rejected**.

**Fix:** either return explicitly or remove the braces.

js

```jsx
[1, 2, 3].filter(num => { return num > 1; }); // [2, 3][1, 2, 3].filter(num => num > 1);             // [2, 3]
```

---

## 3. What is the output?

js

```jsx
const nums = [1, 2, 3, 4, 5];const result = nums.filter((num, index) => {  return num > index;});console.log(result);
```

**Output:**

```
[1, 2, 3, 4, 5]
```

Each element compared with its index:

| num | index | `num > index` | Kept? |
| --- | --- | --- | --- |
| 1 | 0 | true | ✅ |
| 2 | 1 | true | ✅ |
| 3 | 2 | true | ✅ |
| 4 | 3 | true | ✅ |
| 5 | 4 | true | ✅ |

Each value is exactly one more than its index, so every element passes.

---

## 4. How can you filter an array of objects based on multiple conditions?

Combine the conditions inside the callback with logical operators: `&&` (AND), `||` (OR).

js

```jsx
const users = [  { name: "A", age: 25, active: true },  { name: "B", age: 17, active: true },  { name: "C", age: 30, active: false }];// AND: adults who are activeconst result = users.filter(user => user.age >= 18 && user.active);console.log(result);// [{ name: "A", age: 25, active: true }]// OR: under 18 OR inactiveconst result2 = users.filter(user => user.age < 18 || !user.active);// B and C
```

For many conditions, keep the code readable by destructuring or using a named function:

js

```jsx
const isEligible = ({ age, active }) => age >= 18 && active;const eligible = users.filter(isEligible);
```

---

## 5. How would you filter users who have both `admin` and `active` status?

The sample data has no `role` field, so assume each user has `role` and `active`:

js

```jsx
const users = [  { name: "A", role: "admin", active: true },  { name: "B", role: "user", active: true },  { name: "C", role: "admin", active: false }];const activeAdmins = users.filter(user => user.role === "admin" && user.active);console.log(activeAdmins);// [{ name: "A", role: "admin", active: true }]
```

If a user can have **multiple roles** stored in an array:

js

```jsx
const activeAdmins = users.filter(u => u.roles.includes("admin") && u.active);
```

---

## 6. How can you filter an array using another array?

Keep only the items that **exist in the other array**, using `includes()`.

js

```jsx
const users = ["A", "B", "C", "D"];const allowedUsers = ["A", "C"];const result = users.filter(user => allowedUsers.includes(user));console.log(result); // ["A", "C"]
```

To **exclude** instead, negate the condition:

js

```jsx
const blocked = users.filter(user => !allowedUsers.includes(user));// ["B", "D"]
```

For large arrays, convert the lookup array to a `Set`. `Set.has()` is O(1), while `includes()` scans the whole array each time:

js

```jsx
const allowedSet = new Set(allowedUsers);const result = users.filter(user => allowedSet.has(user));
```

---

## 7. How would you remove duplicate objects from an array using `filter()`?

Objects are compared by **reference**, so two objects with identical content are still different. You need to decide what makes two objects "the same", usually a unique key like `id`.

**Option A: `findIndex` (keep the first occurrence)**

js

```jsx
const users = [  { id: 1, name: "A" },  { id: 2, name: "B" },  { id: 1, name: "A" }];const unique = users.filter(  (user, index, arr) => arr.findIndex(u => u.id === user.id) === index);console.log(unique);// [{ id: 1, name: "A" }, { id: 2, name: "B" }]
```

**Option B: a `Set` of seen keys (faster, O(n))**

js

```jsx
const seen = new Set();const unique = users.filter(user => {  if (seen.has(user.id)) return false;  seen.add(user.id);  return true;});
```

**Option C: compare entire objects with `JSON.stringify`**

js

```jsx
const unique = users.filter(  (user, i, arr) => arr.findIndex(u => JSON.stringify(u) === JSON.stringify(user)) === i);
```

Option C is simple, but it depends on **key order** (`{a:1,b:2}` and `{b:2,a:1}` look different) and fails with functions, `undefined` and circular references. Prefer a unique key when you have one.

---

## 8. What is the difference between using `filter()` with `indexOf()` and using a `Set` to remove duplicates?

js

```jsx
const arr = [1, 2, 2, 3, NaN, NaN];// filter + indexOfconst a = arr.filter((v, i, array) => array.indexOf(v) === i);// [1, 2, 3]            ← NaN lost!// Setconst b = [...new Set(arr)];// [1, 2, 3, NaN]       ← NaN kept once
```

|  | `filter()` + `indexOf()` | `Set` |
| --- | --- | --- |
| Time complexity | **O(n²)** (`indexOf` scans for each element) | **O(n)** |
| Speed on large arrays | Slow | Fast |
| `NaN` handling | **Fails**: `indexOf(NaN)` always returns `-1`, so `NaN` is dropped | Works: a `Set` treats `NaN` as equal to `NaN` |
| Code length | Longer | Shorter |
| Works on objects by key | Yes, via `findIndex` | Needs extra code (a `Map` or a `seen` Set) |
| Flexibility | Can add custom conditions in the same pass | Pure de-duplication only |

Use `Set` for primitives. Use `filter` with `findIndex` or a `seen` Set when you need custom logic, such as de-duplicating objects by a key.

---

## 9. What happens when you modify the original array inside a `filter()` callback?

You can modify it, but the results can be surprising and it is **bad practice**. The rules, as defined by the language:

- The **range** of indexes to visit is fixed **before the loop starts** (the original length).
- Elements **appended** during filtering are **not visited**.
- Elements **removed** before being reached are **skipped**.
- Elements **changed** before being reached are visited with their **new value**.

js

```jsx
const arr = [1, 2, 3];const result = arr.filter((num, i, array) => {  array.push(99);          // appended elements are NOT visited  return true;});console.log(result); // [1, 2, 3]console.log(arr);    // [1, 2, 3, 99, 99, 99]
```

js

```jsx
const arr = [1, 2, 3, 4];const result = arr.filter((num, i, array) => {  if (i === 0) array[1] = 100;   // changed before it is reached  return true;});console.log(result); // [1, 100, 3, 4]
```

Because `filter()` is designed to be a pure, non-mutating operation, avoid side effects inside the callback. If you need to change the original array, do it separately after filtering.

---

## 10. Does `filter()` work with sparse arrays? Which elements are actually processed?

Yes, it works, but it **skips empty slots (holes)**. The callback is called only for indexes that actually **exist** in the array. The result is a **dense** array with the holes gone.

js

```jsx
const sparse = [1, , 3, , 5];     // two holes at index 1 and 3const visited = [];const result = sparse.filter((x, i) => {  visited.push(i);  return true;});console.log(visited); // [0, 2, 4]   (holes never visited)console.log(result);  // [1, 3, 5]
```

An **explicit `undefined`** is not a hole. It is a real element, so it **is** processed:

js

```jsx
[1, undefined, 3].filter(() => true); // [1, undefined, 3][1, , 3].filter(() => true);          // [1, 3]
```

Methods like `forEach`, `map`, `some` and `every` also skip holes. If you need to process holes, use a `for` loop or `Array.from(sparse)`, which turns holes into `undefined`.

---

## 11. What is the difference between `filter()` and `find()`? When would you use each?

|  | `filter()` | `find()` |
| --- | --- | --- |
| Returns | A **new array** of **all** matches | The **first** matching element |
| If nothing matches | `[]` | `undefined` |
| Stops early? | No, checks every element | **Yes**, stops at the first match |
| Result type | Array | Single element |

js

```jsx
const users = [  { id: 1, role: "admin" },  { id: 2, role: "user" },  { id: 3, role: "admin" }];users.filter(u => u.role === "admin"); // [{id:1,...}, {id:3,...}]users.find(u => u.role === "admin");   // {id:1, role:"admin"}
```

**Use `filter()`** when you need **all** matching items (a list of results, a search).

**Use `find()`** when you need **one** item, usually looked up by a unique value like `id`. It is also faster because it stops early.

Related: `findIndex()` returns the index of the first match, and `some()` returns just `true` or `false`.

---

## 12. What is the difference between `filter()` and `some()`?

|  | `filter()` | `some()` |
| --- | --- | --- |
| Returns | New array of matches | **Boolean**: does **at least one** element match? |
| Stops early? | No | **Yes**, stops at the first match |
| Use for | Getting the matching items | Just checking whether a match exists |

js

```jsx
const nums = [1, 3, 5, 8];nums.filter(n => n % 2 === 0);        // [8]nums.some(n => n % 2 === 0);          // true
```

A common mistake is using `filter` just to check existence:

js

```jsx
// Wasteful: builds an array only to check its lengthif (nums.filter(n => n > 5).length > 0) { ... }// Better: stops at the first match and returns a booleanif (nums.some(n => n > 5)) { ... }
```

Use `filter()` when you need the items, and `some()` when you only need a yes/no answer. (`every()` is the opposite check: do **all** elements match?)

---

## 13. How would you filter nested data?

**Get users who know React** (the `skills` array is nested inside each user):

js

```jsx
const users = [  { name: "A", skills: ["React", "JS"] },  { name: "B", skills: ["Python", "Java"] },  { name: "C", skills: ["React", "Node"] }];const reactUsers = users.filter(user => user.skills.includes("React"));console.log(reactUsers);// [//   { name: "A", skills: ["React", "JS"] },//   { name: "C", skills: ["React", "Node"] }// ]
```

`includes()` checks the nested array, and its boolean result tells `filter()` whether to keep the user.

**Variations:**

js

```jsx
// Know React OR Pythonusers.filter(u => u.skills.some(s => ["React", "Python"].includes(s)));// Know BOTH React and Nodeusers.filter(u => ["React", "Node"].every(s => u.skills.includes(s)));// Nested objects: skills = [{ name: "React", level: 5 }]users.filter(u => u.skills.some(s => s.name === "React" && s.level >= 4));
```

**Filtering at both levels** (keep only matching users and also trim their inner arrays) needs `filter` plus `map`:

js

```jsx
const result = users  .map(u => ({ ...u, skills: u.skills.filter(s => s !== "JS") }))  .filter(u => u.skills.length > 0);
```

---

## 14. What is the output and why?

js

```jsx
const nums = [1, 2, 3, 4];const result = nums.filter((num, index, arr) => {  arr.pop();  return num % 2 === 0;});console.log(result);
```

**Output:**

```
[2]
```

**Why:** `filter()` fixes the range at the original length (4), but before calling the callback for each index it checks whether that index **still exists** in the array. The callback removes the last element on every call.

| Step | Index | Array before callback | Value | `pop()` removes | `num % 2 === 0` | Kept? |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | 0 | `[1,2,3,4]` | 1 | 4 | false | ❌ |
| 2 | 1 | `[1,2,3]` | 2 | 3 | true | ✅ |
| 3 | 2 | `[1,2]` | index 2 no longer exists, **skipped** |  |  |  |
| 4 | 3 | `[1,2]` | index 3 no longer exists, **skipped** |  |  |  |

Only the value `2` passes. This is the rule from question 9: the length is read once, and removed elements are never visited. After the call, `nums` is `[1, 2]`.

---

## 15. How would you implement your own `filter()` method without using the built-in `filter()`?

**Simple version (a standalone function):**

js

```jsx
function myFilter(array, callback) {  const result = [];  for (let i = 0; i < array.length; i++) {    if (callback(array[i], i, array)) {      result.push(array[i]);    }  }  return result;}console.log(myFilter([1, 2, 3, 4], n => n > 2)); // [3, 4]
```

**As a method on `Array.prototype`, closer to the real behavior:**

js

```jsx
Array.prototype.myFilter = function (callback, thisArg) {  if (typeof callback !== "function") {    throw new TypeError(callback + " is not a function");  }  const result = [];  const length = this.length;               // fixed once, like the built-in  for (let i = 0; i < length; i++) {    if (i in this) {                        // skip holes in sparse arrays      const value = this[i];      if (callback.call(thisArg, value, i, this)) {        result.push(value);      }    }  }  return result;};console.log([1, 2, 3, 4].myFilter(n => n % 2 === 0)); // [2, 4]console.log([1, , 3].myFilter(() => true));            // [1, 3]
```

What the improved version does:

- **Validates** that the callback is a function.
- **Reads the length once**, so appended elements aren't visited.
- **Uses `i in this`** to skip empty slots in sparse arrays.
- **Passes `(value, index, array)`** to the callback.
- **Supports `thisArg`** through `callback.call(thisArg, ...)`.
- **Returns a new array** and leaves the original untouched.

A shorter version with `reduce`, which is a common interview alternative:

js

```jsx
const myFilter = (arr, cb) =>  arr.reduce((acc, val, i) => (cb(val, i, arr) ? [...acc, val] : acc), []);
```

This one is less efficient because spreading creates a new array on every step, so the `for` loop version is preferred.

# **JavaScript  filter() — Advanced Interview Questions with Answers**

## 1. Callback Return Behavior: what happens when the callback returns `true`, `false`, `undefined`, `null`, an object, or a non-zero number?

`filter()` converts whatever the callback returns into a boolean (truthy or falsy). It does not need a strict `true` or `false`.

| Callback returns | Truthy / falsy | Element kept? |
| --- | --- | --- |
| `true` | truthy | ✅ Yes |
| `false` | falsy | ❌ No |
| `undefined` | falsy | ❌ No |
| `null` | falsy | ❌ No |
| an object (even `{}` or `[]`) | **truthy** | ✅ Yes |
| a non-zero number (even `-5`) | **truthy** | ✅ Yes |

Other falsy values are `0`, `""`, `NaN` (and `0n`). Everything else is truthy.

js

```jsx
const result = [1, 2, 3, 4].filter(x => x);console.log(result); // [1, 2, 3, 4]
```

Here the callback returns the element itself, and every number from 1 to 4 is a non-zero number, so all of them are truthy and kept. With `[0, 1, 2]` the `0` would be removed.

---

## 2. Mutation During `filter()`: what will be the output and why?

js

```jsx
const arr = [1, 2, 3, 4, 5];const result = arr.filter((value, index, array) => {  array[index] = value * 2;  return value > 2;});console.log(result);console.log(arr);
```

**Output:**

```
[3, 4, 5]
[2, 4, 6, 8, 10]
```

**Why:**

- `filter()` reads each element **before** calling the callback and passes it in as `value`. That `value` is a local copy of the original element.
- The callback overwrites `array[index]`, but only **after** `value` was already read. It changes the original array, not the `value` variable.
- The return check uses the original values: `1 > 2` ❌, `2 > 2` ❌, `3 > 2` ✅, `4 > 2` ✅, `5 > 2` ✅.
- When an element passes, `filter()` adds the **originally read value** to the result. That is why you get `3, 4, 5` and not the doubled `6, 8, 10`.
- Each index is changed only at the moment it is visited, so the original array ends up fully doubled.

The lesson is that mutating inside `filter()` creates confusing side effects. Do it in a separate step.

---

## 3. Adding Elements During Iteration: what happens when you add elements while `filter()` is running?

js

```jsx
const arr = [1, 2, 3];const result = arr.filter((value, index, array) => {  array.push(value + 10);  return value > 1;});console.log(result);console.log(arr);
```

**Output:**

```
[2, 3]
[1, 2, 3, 11, 12, 13]
```

**Why:**

- `filter()` reads `length` **once**, before it starts (here 3), so it only visits indexes 0, 1 and 2.
- The pushed elements (`11`, `12`, `13`) land at indexes 3, 4 and 5, which are **beyond the fixed range**, so they are never visited.
- Visited values: `1 > 1` ❌, `2 > 1` ✅, `3 > 1` ✅, so the result is `[2, 3]`.
- The original array did grow by three elements, because `push` really mutates it.

This also protects you from infinite loops. If `filter()` re-checked the length each time, pushing inside the callback would never end.

---

## 4. Sparse Arrays: what is the output, and why aren't the empty slots processed?

js

```jsx
const arr = [1, , 3, , 5];const result = arr.filter((value, index) => {  console.log(index);  return true;});console.log(result);
```

**Output:**

```
0
2
4
[1, 3, 5]
```

**Why the empty slots are skipped:** `[1, , 3]` has a **hole** at index 1, meaning no property exists at that index at all. Before calling the callback, `filter()` checks whether the index exists in the array (like `index in arr`). For a hole that check is false, so the callback is not called.

- A hole is different from an explicit `undefined`. In `[1, undefined, 3]` the index exists, so the callback **is** called.
- The result is always a **dense array**: the holes disappear.

Methods like `forEach`, `map`, `some` and `every` skip holes the same way.

---

## 5. `filter()` + `thisArg`: explain the purpose of the second argument of `filter()`

The second argument, `thisArg`, sets the value of **`this` inside the callback**.

js

```jsx
const obj = { min: 10 };const numbers = [5, 10, 15, 20];const result = numbers.filter(function (num) {  return num >= this.min;}, obj);console.log(result); // [10, 15, 20]
```

**How it works:** `filter()` calls the callback with `this` set to `obj`, so `this.min` is `10`. Then `5 >= 10` ❌, and 10, 15 and 20 pass.

Important points:

- It only works with **regular `function` callbacks**. **Arrow functions** ignore `thisArg`, because they take `this` from where they were written (lexical `this`).
- If you don't pass it, `this` inside a regular callback is `undefined` in strict mode (or the global object otherwise).
- It is rarely needed today. A closure does the same thing more clearly:

js

```jsx
const min = 10;numbers.filter(num => num >= min);
```

---

## 6. `filter()` with Async Callback: what will this return, and why doesn't `filter()` wait for the Promise?

js

```jsx
const numbers = [1, 2, 3];const result = numbers.filter(async num => {  return num > 1;});console.log(result);
```

**Output:**

```
[1, 2, 3]
```

**Why:**

- An `async` function **always returns a Promise**, even when it returns `false`.
- A Promise is an **object**, and objects are **truthy**. So the callback always returns something truthy and **every element is kept**.
- `filter()` is **synchronous**. It never calls `await` or `.then()` on what the callback returns. It only checks truthiness at that moment.
- The Promises are created and then thrown away. The result contains the original numbers, not Promises.

Even `async num => false` would keep every element. This is a classic bug, so never pass an `async` function directly to `filter()`.

---

## 7. Async Filtering: how would you correctly filter an array based on an asynchronous condition?

js

```jsx
const users = [1, 2, 3, 4];// checkUser(id) returns a Promise<boolean>
```

**Option A: in parallel (fast, order preserved)**

js

```jsx
async function filterAsync(array, predicate) {  const flags = await Promise.all(array.map(item => predicate(item)));  return array.filter((_, index) => flags[index]);}const validUsers = await filterAsync(users, checkUser);
```

Steps:

1. `map` starts all checks at once and returns an array of Promises.
2. `Promise.all` waits for all of them and gives an array of booleans.
3. A normal `filter` uses the boolean at the same index to keep or drop each user.

**Option B: sequentially (one at a time)**

js

```jsx
const validUsers = [];for (const id of users) {  if (await checkUser(id)) {    validUsers.push(id);  }}
```

**Which to choose:**

- Parallel is faster, but it fires **all requests at once**, which can hit rate limits. For big arrays, limit concurrency (for example in batches).
- Sequential is slower but gentle on the server and keeps side effects ordered.
- `Promise.all` **rejects if any check fails**. Use `Promise.allSettled` if you want to tolerate individual failures.
- `await` must be inside an `async` function (or at the top level of a module).

---

## 8. `filter()` + `map()` vs `reduce()`: get the names of users who are 18+

js

```jsx
const users = [  { name: "A", age: 25 },  { name: "B", age: 16 },  { name: "C", age: 30 }];
```

**Using `filter()` + `map()`:**

js

```jsx
const names = users  .filter(user => user.age >= 18)  .map(user => user.name);console.log(names); // ["A", "C"]
```

**Using `reduce()`:**

js

```jsx
const names = users.reduce((acc, user) => {  if (user.age >= 18) acc.push(user.name);  return acc;}, []);console.log(names); // ["A", "C"]
```

**Comparison:**

|  | `filter()` + `map()` | `reduce()` |
| --- | --- | --- |
| Readability | ✅ Very clear: "select, then transform" | Less obvious at a glance |
| Passes over the data | Two | One |
| Intermediate array | Yes | No |
| Best for | Most everyday code | Hot paths or complex accumulation |

Another single-pass option is `flatMap`: `users.flatMap(u => u.age >= 18 ? [u.name] : [])`. In most apps, prefer `filter().map()` for readability. The speed difference only matters for very large arrays.

---

## 9. Multiple `filter()` Calls: which performs fewer iterations and why?

js

```jsx
// A: chainedconst result = users  .filter(user => user.active)  .filter(user => user.age >= 18);// B: singleconst result = users.filter(user => user.active && user.age >= 18);
```

**B (single `filter`) performs fewer iterations.**

- **A:** the first `filter` visits all **n** users. The second `filter` visits only the **m** users who passed the first. Total callback calls: **n + m**, plus an extra intermediate array.
- **B:** visits each user **once**: **n** calls. The `&&` also **short-circuits**, so `age` is only checked for active users.

Example: 1000 users, 600 active. Chained does 1000 + 600 = **1600** calls. Single does **1000**.

Both are still **O(n)**, so in practice the difference is tiny. Chaining can be more readable (one rule per line), and it is a reasonable choice unless the array is huge or the code runs in a hot path. If you do chain, put the **cheapest or most selective** filter first so the second one sees fewer elements.

---

## 10. Time Complexity: what is the complexity of this, and what if the callback is `O(n)`?

js

```jsx
const result = arr.filter(x => x > 10);
```

- **Time: O(n).** Each of the `n` elements is visited once, and the comparison is O(1).
- **Space: O(k)** for the new array, where `k` is the number of matches (up to `n`).

**If the callback itself does an O(n) operation**, the total becomes **O(n × n) = O(n²)**.

js

```jsx
// O(n²): includes() scans another array of size n for every elementconst result = arr.filter(x => other.includes(x));
```

The usual fix is to precompute a faster lookup, so the inner step becomes O(1):

js

```jsx
const set = new Set(other);const result = arr.filter(x => set.has(x));   // O(n) overall
```

---

## 11. Removing Duplicates: explain the time complexity, and how would you improve it for a large dataset?

js

```jsx
const unique = arr.filter((value, index) => arr.indexOf(value) === index);
```

**Time complexity: O(n²).**

- `filter()` visits `n` elements.
- For each element, `indexOf` scans from the start until it finds the first occurrence, which is up to `n` steps.
- That gives roughly n × n comparisons in the worst case. With 100,000 items, that is billions of operations.

**Improvements:**

js

```jsx
// 1. Set: O(n) time, O(n) spaceconst unique = [...new Set(arr)];// 2. filter + a "seen" Set (when you need extra logic)const seen = new Set();const unique = arr.filter(value => {  if (seen.has(value)) return false;  seen.add(value);  return true;});
```

`Set` lookups and inserts are O(1) on average, so the whole job is **O(n)**. A `Set` also treats `NaN` correctly, which `indexOf` cannot.

---

## 12. Objects and Reference Equality: why doesn't this remove duplicate objects, and how do you remove duplicates by `id`?

js

```jsx
const users = [{ id: 1 }, { id: 1 }, { id: 2 }];const unique = users.filter(  (user, index) => users.indexOf(user) === index);
```

**Why it fails:**

- `indexOf` uses **strict equality (`===`)**, and objects are compared by **reference** (memory location), not by content.
- `{ id: 1 }` and `{ id: 1 }` are two separate objects, so they are **not equal**.
- Therefore `users.indexOf(user)` always finds that exact object at its own index, `=== index` is always true, and **nothing is removed**.
- The result is all three objects.

**Remove duplicates by `id`:**

js

```jsx
// A: seen Set (keeps the first occurrence, O(n))const seen = new Set();const unique = users.filter(user => {  if (seen.has(user.id)) return false;  seen.add(user.id);  return true;});// [{ id: 1 }, { id: 2 }]// B: findIndex (simple, but O(n²))const unique2 = users.filter(  (user, index) => users.findIndex(u => u.id === user.id) === index);// C: Map (keeps the last occurrence for each id)const unique3 = [...new Map(users.map(u => [u.id, u])).values()];
```

---

## 13. `filter()` on Array-Like Objects: can `filter()` be used directly on this object?

js

```jsx
const data = {  0: "React",  1: "JavaScript",  2: "Node",  length: 3};
```

**No.** `data` is a plain object, not an array, so it has no `filter` method:

js

```jsx
data.filter(x => x); // TypeError: data.filter is not a function
```

**Ways to use `filter()` with it:**

js

```jsx
// 1. Borrow the method with call()const result = Array.prototype.filter.call(data, item => item.length > 4);console.log(result); // ["React", "JavaScript"]// 2. Convert to a real array firstconst result2 = Array.from(data).filter(item => item.length > 4);// ["React", "JavaScript"]
```

Notes:

- Spread, `[...data]`, **does not work** here, because the object isn't iterable (it has no `Symbol.iterator`). It would throw a `TypeError`.
- Real-world array-likes are `arguments`, `NodeList` (from `querySelectorAll`) and `HTMLCollection`. Some of those are iterable, so spread works for them.

---

## 14. Prototype / Generic Behavior: why does this work, and what does it tell you about how `filter()` works?

js

```jsx
const result = Array.prototype.filter.call(  { 0: 10, 1: 20, 2: 30, length: 3 },  num => num > 10);console.log(result); // [20, 30]
```

**Why it works:** `call()` runs `filter` with `this` set to our plain object. The `filter` algorithm doesn't require `this` to be a real array. It only needs:

1. a **`length`** property (it reads this once, so the iteration range is fixed),
2. **numeric-indexed properties** (`0`, `1`, `2`), which it reads and checks with an "does this index exist" test.

The object has both, so it is processed like an array: 10 fails, 20 and 30 pass.

**What it tells you:**

- `filter()` is a **generic method**. It works on any **array-like** object, not just arrays.
- It never changes `this`.
- It **always returns a real array**, even when the input was not one.
- Many other array methods (`map`, `forEach`, `slice`, `some`, `every`, `reduce`) are generic in the same way.

---

## 15. Implement Advanced `filter()`: write your own version of `Array.prototype.filter()`

js

```jsx
Object.defineProperty(Array.prototype, "myFilter", {  value: function (callback, thisArg) {// 1. `this` must not be null/undefined    if (this == null) {      throw new TypeError("Array.prototype.myFilter called on null or undefined");    }// 2. callback must be a function    if (typeof callback !== "function") {      throw new TypeError(String(callback) + " is not a function");    }// 3. Work on an object and fix the length once    const O = Object(this);    const len = O.length >>> 0;          // convert to an unsigned integer    const result = [];    for (let i = 0; i < len; i++) {// 4. Skip holes in sparse arrays      if (i in O) {        const value = O[i];// 5. Call with thisArg, passing (value, index, array)        if (callback.call(thisArg, value, i, O)) {          result.push(value);        }      }    }// 6. New array; the original is untouched    return result;  },  writable: true,  configurable: true,  enumerable: false      // keeps it out of for...in loops});
```

**Test it:**

js

```jsx
const numbers = [1, 2, 3, 4];const result = numbers.myFilter((value, index, array) => value % 2 === 0);console.log(result); // [2, 4]// sparse arrays: holes skipped[1, , 3].myFilter(() => true);                        // [1, 3]// thisArg[5, 10, 15].myFilter(function (n) { return n >= this.min; }, { min: 10 }); // [10, 15]// array-like objects (generic behavior)Array.prototype.myFilter.call({ 0: 10, 1: 20, length: 2 }, n => n > 10);   // [20]// validation[1, 2].myFilter("nope");  // TypeError: nope is not a function
```

**How it matches the built-in behavior:**

| Requirement | How it's handled |
| --- | --- |
| Callback gets `(value, index, array)` | `callback.call(thisArg, value, i, O)` |
| Returns a new array, doesn't mutate | Pushes into a separate `result` array |
| Length is fixed at the start | `len` is read once, so pushed elements aren't visited |
| Removed elements are skipped | `i in O` is checked on each iteration |
| Skips holes | Same `i in O` check |
| Supports `thisArg` | `.call(thisArg, ...)` |
| Truthy/falsy check | Plain `if (...)` on the return value |
| Works on array-likes | `Object(this)` + `length` + index access |

The built-in version has a few extra details that this one leaves out, such as converting `length` with the spec's exact `ToLength` rules and creating the result through the array "species" constructor. For interviews and learning, this version covers everything that matters.

# 🚀 **Follow @daily.debugging for complete frontend resources and interview preparation.**
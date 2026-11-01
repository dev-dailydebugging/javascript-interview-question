# The Complete Guide of Array

## 1. What is an array in JavaScript?

An array is a special object used to store multiple values in a single variable, in an ordered list. Each value is called an element, and each element has a numeric position called an index. Arrays can hold any type of data (numbers, strings, objects, even other arrays).

## 2. How do you create an array in JavaScript?

The most common way is with square brackets (array literal):

javascript

```jsx
const fruits = ["Apple", "Banana", "Mango"];
```

You can also use the `Array` constructor: `const fruits = new Array("Apple", "Banana", "Mango");`

## 3. What is the index of the first element in an array?

The index of the first element is **0**. JavaScript arrays are zero-indexed.

## 4. What will be the output?

javascript

```jsx
const fruits = ["Apple", "Banana", "Mango"];console.log(fruits[1]);
```

**Output:** `Banana`

Index 0 is "Apple", index 1 is "Banana", index 2 is "Mango".

## 5. How do you access the last element of an array?

Use `array.length - 1` as the index:

javascript

```jsx
const numbers = [10, 20, 30, 40];console.log(numbers[numbers.length - 1]); // 40
```

You can also use the modern `at()` method: `numbers.at(-1)`, which also returns `40`.

## 6. What does the `length` property return?

It returns the total number of elements in the array.

javascript

```jsx
const numbers = [10, 20, 30, 40];console.log(numbers.length);
```

**Output:** `4`

## 7. How do you change an existing value in an array?

Assign a new value to the element's index:

javascript

```jsx
const fruits = ["Apple", "Banana", "Mango"];// Change Banana to Orangefruits[1] = "Orange";console.log(fruits); // ["Apple", "Orange", "Mango"]
```

Even though `fruits` is declared with `const`, you can modify its elements. You just can't reassign the variable itself.

## 8. What does `push()` do?

`push()` adds one or more elements to the **end** of an array and returns the new length.

javascript

```jsx
const numbers = [1, 2, 3];numbers.push(4);console.log(numbers);
```

**Output:** `[1, 2, 3, 4]`

## 9. What does `pop()` do?

`pop()` removes the **last** element from an array and returns that removed element.

javascript

```jsx
const numbers = [1, 2, 3];numbers.pop();console.log(numbers);
```

**Output:** `[1, 2]`

## 10. What is the difference between `push()` and `unshift()`?

- `push()` adds elements to the **end** of the array.
- `unshift()` adds elements to the **beginning** of the array.

javascript

```jsx
const arr = [2, 3];arr.push(4);     // [2, 3, 4]arr.unshift(1);  // [1, 2, 3, 4]
```

Both return the new length of the array.

## 11. What is the difference between `pop()` and `shift()`?

- `pop()` removes the **last** element.
- `shift()` removes the **first** element.

javascript

```jsx
const arr = [1, 2, 3];arr.pop();    // removes 3 → [1, 2]arr.shift();  // removes 1 → [2]
```

Both return the removed element.

## 12. What will be the output?

javascript

```jsx
const numbers = [10, 20, 30, 40];console.log(numbers.slice(1, 3));
```

**Output:** `[20, 30]`

`slice(start, end)` returns elements from index 1 up to, but not including, index 3.

## 13. What is the difference between `slice()` and `splice()`?

| Feature | `slice()` | `splice()` |
| --- | --- | --- |
| Purpose | Copies a portion of an array | Adds, removes, or replaces elements |
| Modifies original array? | **No** | **Yes** |
| Returns | A new array with the selected elements | An array of the removed elements |
| Syntax | `slice(start, end)` | `splice(start, deleteCount, ...items)` |

javascript

```jsx
const arr = [1, 2, 3, 4, 5];arr.slice(1, 3);   // [2, 3], arr is still [1, 2, 3, 4, 5]arr.splice(1, 2);  // [2, 3], arr is now [1, 4, 5]
```

## 14. What will be the output?

javascript

```jsx
const fruits = ["Apple", "Banana", "Mango"];console.log(fruits.includes("Banana"));console.log(fruits.indexOf("Mango"));
```

**Output:**

```
true
2
```

- `includes("Banana")` returns `true` because "Banana" exists in the array.
- `indexOf("Mango")` returns `2`, the index where "Mango" is found (it returns `1` if not found).

![2.png](The%20Complete%20Guide%20of%20Array/2.png)

![3.png](The%20Complete%20Guide%20of%20Array/3.png)

![4.png](The%20Complete%20Guide%20of%20Array/4.png)

![5.png](The%20Complete%20Guide%20of%20Array/5.png)

![6.png](The%20Complete%20Guide%20of%20Array/6.png)

![7.png](The%20Complete%20Guide%20of%20Array/7.png)

![8.png](The%20Complete%20Guide%20of%20Array/8.png)

![9.png](The%20Complete%20Guide%20of%20Array/9.png)

![10.png](The%20Complete%20Guide%20of%20Array/10.png)

![11.png](The%20Complete%20Guide%20of%20Array/11.png)

![12.png](The%20Complete%20Guide%20of%20Array/12.png)

![13.png](The%20Complete%20Guide%20of%20Array/13.png)

![14.png](The%20Complete%20Guide%20of%20Array/14.png)

![final.png](The%20Complete%20Guide%20of%20Array/final.png)

# **JavaScript  Array — Intermediate Questions with Answers**

## 1. What is the output?

javascript

```jsx
const arr = [1, 2, 3];arr[5] = 6;console.log(arr);console.log(arr.length);
```

**Output:**

```
[1, 2, 3, <2 empty items>, 6]
6
```

Assigning to index 5 creates a "hole" at indexes 3 and 4 (sparse array). The length becomes the highest index + 1, which is 6.

## 2. What is the output?

javascript

```jsx
const arr = [10, 20, 30];const copy = arr;copy.push(40);console.log(arr);
```

**Output:** `[10, 20, 30, 40]`

`copy = arr` does not create a new array. Both variables point to the **same array in memory**, so changing one changes the other.

## 3. What is the difference between these two?

javascript

```jsx
const a = [1, 2, 3];const b = a;
```

vs.

javascript

```jsx
const a = [1, 2, 3];const b = [...a];
```

- `const b = a;` copies the **reference**. `a` and `b` point to the same array, so changes through one are visible in the other.
- `const b = [...a];` creates a **new array** (shallow copy) with the same elements. `a` and `b` are independent, so changes to one don't affect the other.

## 4. What is the output?

javascript

```jsx
const arr = [1, 2, 3];const copy = [...arr];copy.push(4);console.log(arr);console.log(copy);
```

**Output:**

```
[1, 2, 3]
[1, 2, 3, 4]
```

The spread operator made a separate array, so pushing to `copy` does not affect `arr`.

## 5. What is the output?

javascript

```jsx
const arr = [1, 2, 3, 4, 5];arr.splice(2, 1);console.log(arr);
```

**Output:** `[1, 2, 4, 5]`

`splice(2, 1)` removes 1 element starting at index 2 (the value `3`). It modifies the original array.

## 6. What is the output?

javascript

```jsx
const arr = [1, 2, 3, 4];const result = arr.slice(1, 3);console.log(result);console.log(arr);
```

**Output:**

```
[2, 3]
[1, 2, 3, 4]
```

`slice(1, 3)` returns elements at index 1 and 2 (end index is excluded). The original array is unchanged.

## 7. What is the output?

javascript

```jsx
const arr = [1, 2, 3];console.log(arr.slice(-1));console.log(arr.slice(-2));
```

**Output:**

```
[3]
[2, 3]
```

Negative indexes count from the end. `slice(-1)` gives the last element, `slice(-2)` gives the last two.

## 8. What happens here?

javascript

```jsx
const arr = [1, 2, 3];arr.length = 0;console.log(arr);
```

**Output:** `[]`

Setting `length` to `0` empties the array. This is a common trick to clear an array (and it works even with `const`, since the array itself is being modified, not reassigned).

## 9. What is the output?

javascript

```jsx
const arr = [1, 2, 3];arr.length = 5;console.log(arr);
```

**Output:** `[1, 2, 3, <2 empty items>]`

Increasing `length` extends the array with empty slots (not `undefined` values, but truly empty holes).

## 10. What is the output?

javascript

```jsx
const arr = [1, 2, 3];console.log(2 in arr);console.log(5 in arr);
```

**Output:**

```
true
false
```

The `in` operator checks whether an **index (key)** exists, not a value. Index `2` exists (value `3`), but index `5` does not.

## 11. What is the output?

javascript

```jsx
const arr = [1, 2, 3];console.log(arr.includes(2));console.log(arr.includes("2"));
```

**Output:**

```
true
false
```

`includes()` uses strict equality (`===`), so the number `2` matches but the string `"2"` does not.

## 12. What is the output?

javascript

```jsx
const arr = [1, 2, 3];const [first, , third] = arr;console.log(first);console.log(third);
```

**Output:**

```
1
3
```

Array destructuring assigns by position. The empty slot between the commas skips the second element (`2`).

## 13. What is the output?

javascript

```jsx
const arr = [1, 2];const result = [0, ...arr, 3];console.log(result);
```

**Output:** `[0, 1, 2, 3]`

The spread operator expands `arr` in place, so its elements are inserted between `0` and `3`.

## 14. What is the output?

javascript

```jsx
const arr = [[1, 2], [3, 4]];const copy = [...arr];copy[0].push(5);console.log(arr);
```

**Output:** `[[1, 2, 5], [3, 4]]`

Spread makes only a **shallow copy**. The outer array is new, but the inner arrays are still shared references. So pushing to `copy[0]` also changes `arr[0]`. To avoid this, use a deep copy such as `structuredClone(arr)`.

## 15. Interview Challenge 🔥 What is the output?

javascript

```jsx
const arr = [1, 2, 3];const a = arr;const b = [...arr];a.push(4);b.push(5);console.log(arr);console.log(a);console.log(b);
```

**Output:**

```
[1, 2, 3, 4]
[1, 2, 3, 4]
[1, 2, 3, 5]
```

- `a` is a reference to `arr`, so `a.push(4)` changes both `arr` and `a`.
- `b` is an independent copy made *before* the push, so it starts as `[1, 2, 3]`, and `b.push(5)` only affects `b`.

# **JavaScript  Array — Advanced Questions with Answers**

## 1. What is the output?

javascript

```jsx
const arr = [1, 2, 3];delete arr[1];console.log(arr);console.log(arr.length);
```

**Output:**

```
[1, <1 empty item>, 3]
3
```

`delete` removes the element but leaves a hole. It does not shift the other elements or change `length`.

## 2. What is the output?

javascript

```jsx
const arr = [1, 2, 3];delete arr[1];console.log(1 in arr);console.log(arr[1]);
```

**Output:**

```
false
undefined
```

The index `1` no longer exists as a property, so `1 in arr` is `false`. Reading a missing index gives `undefined`.

## 3. What is the output?

javascript

```jsx
const arr = [];arr[3] = "Hello";console.log(arr);console.log(arr.length);
```

**Output:**

```
[<3 empty items>, 'Hello']
4
```

Indexes 0 to 2 are empty holes, and `length` becomes highest index + 1 = 4.

## 4. What is the difference between these two arrays?

javascript

```jsx
const a = new Array(3);const b = [undefined, undefined, undefined];console.log(a.length);console.log(b.length);
```

**Output:**

```
3
3
```

Both have length 3, but internally they differ:

- `a` is a **sparse array**: it has `length` 3 but no actual index properties (`0 in a` is `false`). Printed as `[<3 empty items>]`.
- `b` is a **dense array**: indexes 0, 1, 2 really exist and hold the value `undefined` (`0 in b` is `true`).

This matters because methods like `map()`, `forEach()`, and `filter()` skip holes but visit real `undefined` values. So `a.map(x => 1)` still gives empty slots, while `b.map(x => 1)` gives `[1, 1, 1]`.

## 5. What is the output?

javascript

```jsx
const arr = [1, 2, 3];const result = arr.splice(1, 0, 10, 20);console.log(arr);console.log(result);
```

**Output:**

```
[1, 10, 20, 2, 3]
[]
```

`splice(1, 0, 10, 20)` deletes 0 elements at index 1 and inserts `10, 20` there. Nothing was removed, so the returned array is empty.

## 6. What is the output?

javascript

```jsx
const arr = [1, 2, 3, 4];const result = arr.splice(-2, 1);console.log(arr);console.log(result);
```

**Output:**

```
[1, 2, 4]
[3]
```

- `2` means 2 from the end (index 2, value `3`). One element is removed, and it is returned in `result`.

## 7. What is the output?

javascript

```jsx
const arr = [10, 2, 30, 4];arr.sort();console.log(arr);
```

**Output:** `[10, 2, 30, 4]`

Default `sort()` converts elements to **strings** and compares them by UTF-16 code units, so it sorts alphabetically. The strings are `"10"`, `"2"`, `"30"`, `"4"`. Comparing character by character, `"10"` < `"2"` < `"30"` < `"4"`, which happens to be the same order the array already had.

## 8. How would you correctly sort numbers in ascending order?

javascript

```jsx
const numbers = [10, 2, 30, 4];numbers.sort((a, b) => a - b);console.log(numbers); // [2, 4, 10, 30]
```

The compare function returns a negative number if `a` should come first, positive if `b` should, and 0 if equal. `a - b` gives ascending order; use `b - a` for descending.

## 9. What is the output?

javascript

```jsx
const arr = [1, 2, 3];Object.freeze(arr);arr.push(4);console.log(arr);
```

**Result:** It throws a `TypeError: Cannot add property 3, object is not extensible`, and the `console.log` never runs.

`push()` always throws on a frozen array, even in non-strict mode, because the array method itself checks and fails.

## 10. What is the output?

javascript

```jsx
const arr = [1, 2, 3];Object.freeze(arr);arr[0] = 100;console.log(arr);
```

**Output:** `[1, 2, 3]`

Direct assignment to a frozen array is **silently ignored** in non-strict mode (in strict mode or modules, it throws a `TypeError`).

Yes, `Object.freeze()` prevents the array from being modified: no adding, removing, or changing elements. But it is **shallow**, so objects or arrays nested inside can still be changed.

## 11. What is the output?

javascript

```jsx
const arr = [[1, 2], [3, 4]];const copy = structuredClone(arr);copy[0].push(5);console.log(arr);console.log(copy);
```

**Output:**

```
[[1, 2], [3, 4]]
[[1, 2, 5], [3, 4]]
```

`structuredClone()` makes a **deep copy**, so the inner arrays are cloned too. With `[...arr]` (a shallow copy), the inner arrays are shared, so `copy[0].push(5)` would also change `arr` and print `[[1, 2, 5], [3, 4]]` for both.

## 12. What is the output?

javascript

```jsx
const arr = [1, 2, 3];const copy = arr.slice();console.log(arr === copy);console.log(arr[0] === copy[0]);
```

**Output:**

```
false
true
```

- `arr === copy` compares **references**. `slice()` creates a new array, so they are different objects in memory.
- `arr[0] === copy[0]` compares **primitive values** (`1 === 1`), which are equal.

## 13. Interview Trap 🔥

javascript

```jsx
const arr = [1, 2, 3];console.log(arr == "1,2,3");console.log(arr === "1,2,3");
```

**Output:**

```
true
false
```

- `==` allows type coercion. The array is converted to a primitive via `toString()`, giving `"1,2,3"`, which equals the string.
- `===` does no coercion. An array (object) and a string are different types, so it is `false`.

## 14. Advanced Nested Array Challenge 🔥

javascript

```jsx
const arr = Array(3).fill([]);arr[0].push(1);console.log(arr);
```

**Output:** `[[1], [1], [1]]`

`fill([])` evaluates `[]` **once** and puts the **same reference** in all three slots. So `arr[0]`, `arr[1]`, and `arr[2]` are the same array, and pushing through one shows up in all.

To create independent inner arrays, use:

javascript

```jsx
const arr = Array.from({ length: 3 }, () => []);// orconst arr2 = Array(3).fill().map(() => []);arr[0].push(1);console.log(arr); // [[1], [], []]
```

# 🚀 **Follow @daily.debugging for complete frontend resources and interview preparation.**
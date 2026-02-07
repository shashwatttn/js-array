# JavaScript Array Methods Cheat Sheet

## 1. Iteration (Non-mutating – usually preferred)

| Method            | Returns                  | Mutates? | Purpose / How it works                                      | Common Example                                      |
|-------------------|--------------------------|----------|-------------------------------------------------------------|-----------------------------------------------------|
| `forEach()`       | `undefined`              | No       | Execute function for each element (side effects)            | `arr.forEach(x => console.log(x))`                  |
| `map()`           | **new array**            | No       | Transform each element → new array                          | `arr.map(x => x * 2)`                               |
| `filter()`        | **new array**            | No       | Keep only elements that pass test                           | `arr.filter(x => x > 0)`                            |
| `reduce()`        | single value             | No       | Fold array into single value (left → right)                 | `arr.reduce((sum, x) => sum + x, 0)`                |
| `reduceRight()`   | single value             | No       | Same as reduce but right → left                             | Rarely used                                         |
| `some()`          | `boolean`                | No       | Is at least one element true? (short-circuits)              | `arr.some(x => x < 0)`                              |
| `every()`         | `boolean`                | No       | Are all elements true? (short-circuits)                     | `arr.every(x => Number.isInteger(x))`               |
| `find()`          | element or `undefined`   | No       | First element that matches (or undefined)                   | `arr.find(x => x.id === 42)`                        |
| `findIndex()`     | index or `-1`            | No       | Index of first matching element                             | `arr.findIndex(x => x.name === "start")`            |
| `findLast()`      | element or `undefined`   | No       | Last element that matches (ES2022+)                         | `arr.findLast(x => x > 100)`                        |
| `findLastIndex()` | index or `-1`            | No       | Index of last matching element (ES2022+)                    | `scores.findLastIndex(s => s === maxScore)`         |

## 2. Mutation Methods (change original array)

| Method         | Returns                        | Mutates? | What it does                                              | Example                                                |
|----------------|--------------------------------|----------|-----------------------------------------------------------|--------------------------------------------------------|
| `push(...items)` | new length                   | Yes      | Add items to **end**                                      | `arr.push(4, 5)`                                       |
| `pop()`        | removed element                | Yes      | Remove & return last element                              | `const last = arr.pop()`                               |
| `unshift(...items)` | new length                | Yes      | Add items to **beginning**                                | `arr.unshift(0, -1)`                                   |
| `shift()`      | removed element                | Yes      | Remove & return first element                             | `const first = arr.shift()`                            |
| `splice(start, deleteCount?, ...items)` | removed items array | Yes      | Remove/replace/insert at index                            | `arr.splice(2, 1, "new")`                              |
| `reverse()`    | the array itself               | Yes      | Reverse order in place                                    | `arr.reverse()`                                        |
| `sort(compareFn?)` | the array itself           | Yes      | Sort in place (default: string conversion)                | `arr.sort((a,b) => a - b)`                             |
| `fill(value, start?, end?)` | the array itself      | Yes      | Fill range with static value                              | `new Array(5).fill(0)`                                 |
| `copyWithin(target, start, end?)` | the array itself | Yes      | Copy part of array to another position (overlap safe)     | `arr.copyWithin(0, -3)`                                |

## 3. Safe Access / Combination / Conversion (Non-mutating)

| Method              | Returns             | Mutates? | Purpose                                                    | Example                                                |
|---------------------|---------------------|----------|------------------------------------------------------------|--------------------------------------------------------|
| `slice(start?, end?)` | **new array**       | No       | Shallow copy of portion                                    | `arr.slice(1, 4)` or `arr.slice()` (copy)              |
| `concat(...values)` | **new array**       | No       | Merge arrays / values                                      | `arr.concat([4,5], 6)`                                 |
| `join(separator?)`  | string              | No       | Join elements into string                                  | `arr.join(" → ")`                                      |
| `toString()`        | string              | No       | `join(",")` basically                                      | Rarely used directly                                   |
| `indexOf(item, from?)` | index or -1      | No       | First position of value (strict ===)                       | `arr.indexOf(10)`                                      |
| `lastIndexOf(item, from?)` | index or -1  | No       | Last position of value                                     | `arr.lastIndexOf(NaN)`                                 |
| `includes(item, from?)` | boolean         | No       | Does array contain value? (strict)                         | `arr.includes("admin")`                                |
| `flat(depth?)`      | **new array**       | No       | Flatten nested arrays (default depth = 1)                  | `arr.flat(Infinity)`                                   |
| `flatMap(callback)` | **new array**       | No       | map() + flat(1) in one step                                | `arr.flatMap(x => [x, x*2])`                           |
| `at(index)`         | element or undefined| No       | Get element (supports negative indices) – ES2022+          | `arr.at(-1)` → last item                               |

## 4. Iterator-returning methods

| Method       | Returns                        | Use case example                                |
|--------------|--------------------------------|-------------------------------------------------|
| `keys()`     | Iterator of indices            | `for (const i of arr.keys()) …`                 |
| `values()`   | Iterator of values             | `for (const v of arr.values()) …`               |
| `entries()`  | Iterator of [index, value]     | `for (const [i, v] of arr.entries()) …`         |

## Quick Reference Table – Mutating vs Non-mutating

| Goal                          | Mutating method     | Preferred non-mutating way                     |
|-------------------------------|---------------------|------------------------------------------------|
| Add to end                    | `push()`            | `[...arr, value]`                              |
| Remove from end               | `pop()`             | `arr.slice(0, -1)`                             |
| Add to start                  | `unshift()`         | `[value, ...arr]`                              |
| Remove from start             | `shift()`           | `arr.slice(1)`                                 |
| Reverse                       | `reverse()`         | `[...arr].reverse()`                           |
| Sort                          | `sort()`            | `[...arr].sort((a,b) => a - b)`                |
| Delete / insert in middle     | `splice()`          | `[...arr.slice(0,i), newVal, ...arr.slice(i)]` |

## Tips

- Chain methods: `arr.filter(...).map(...).sort(...)`
- Use `at(-1)` instead of `arr[arr.length-1]`
- Use `find` / `findLast` instead of manual loops when you need first/last match
- `flatMap` is great for 1→many transformations
- Avoid `forEach` when you can use `map`/`filter`/`for...of`

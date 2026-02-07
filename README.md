# JavaScript Array Methods Cheat Sheet (2025–2026)

Most important array methods in modern JavaScript (ES6+).  
Each entry shows: **syntax**, **return value**, **mutates original?**, **time complexity**, **purpose**, **example**, and **output**.

## 1. Iteration (Non-mutating – usually preferred)

| Method            | Returns                  | Mutates? | Time Complexity | Purpose / How it works                                      | Common Example                                      | Output                                              |
|-------------------|--------------------------|----------|-----------------|-------------------------------------------------------------|-----------------------------------------------------|-----------------------------------------------------|
| `forEach()`       | `undefined`              | No       | O(n)            | Execute function for each element (side effects)            | `let arr = [1,2,3]; arr.forEach(x => console.log(x))` | Logs: 1 2 3 (returns undefined)                     |
| `map()`           | **new array**            | No       | O(n)            | Transform each element → new array                          | Simple: `let arr = [1,2,3]; arr.map(x => x * 2)`<br>Complex: `let users = [{name:'A'}, {name:'B'}]; users.map(u => u.name.toUpperCase())` | Simple: [2,4,6]<br>Complex: ['A','B']               |
| `filter()`        | **new array**            | No       | O(n)            | Keep only elements that pass test                           | Simple: `let arr = [1,2,3,4]; arr.filter(x => x > 2)`<br>Complex: `let items = [{price:10}, {price:20}, {price:5}]; items.filter(i => i.price > 10)` | Simple: [3,4]<br>Complex: [{price:20}]              |
| `reduce()`        | single value             | No       | O(n)            | Fold array into single value (left → right)                 | Simple: `let arr = [1,2,3]; arr.reduce((sum, x) => sum + x, 0)`<br>Complex: `let arr = [[1,2],[3,4]]; arr.reduce((acc, sub) => acc.concat(sub), [])` | Simple: 6<br>Complex: [1,2,3,4]                     |
| `reduceRight()`   | single value             | No       | O(n)            | Same as reduce but right → left                             | Simple: `let arr = [1,2,3]; arr.reduceRight((sum, x) => sum + x, 0)`<br>Complex: `let words = ['world','hello']; words.reduceRight((acc, w) => acc + ' ' + w, '')` | Simple: 6<br>Complex: 'hello world'                 |
| `some()`          | `boolean`                | No       | O(n) worst      | Is at least one element true? (short-circuits)              | `let arr = [1,3,5]; arr.some(x => x % 2 === 0)`    | false                                               |
| `every()`         | `boolean`                | No       | O(n) worst      | Are all elements true? (short-circuits)                     | `let arr = [2,4,6]; arr.every(x => x % 2 === 0)`   | true                                                |
| `find()`          | element or `undefined`   | No       | O(n) worst      | First element that matches (or undefined)                   | `let arr = [{id:1}, {id:2}]; arr.find(x => x.id === 2)` | {id:2}                                              |
| `findIndex()`     | index or `-1`            | No       | O(n) worst      | Index of first matching element                             | `let arr = ['apple','banana']; arr.findIndex(x => x === 'banana')` | 1                                                   |
| `findLast()`      | element or `undefined`   | No       | O(n) worst      | Last element that matches (ES2022+)                         | `let arr = [1,2,3,2]; arr.findLast(x => x === 2)`  | 2                                                   |
| `findLastIndex()` | index or `-1`            | No       | O(n) worst      | Index of last matching element (ES2022+)                    | `let arr = [1,2,3,2]; arr.findLastIndex(x => x === 2)` | 3                                                   |

## 2. Mutation Methods (change original array)

| Method         | Returns                        | Mutates? | Time Complexity | What it does                                              | Example                                                | Output                                              |
|----------------|--------------------------------|----------|-----------------|-----------------------------------------------------------|--------------------------------------------------------|-----------------------------------------------------|
| `push(...items)` | new length                   | Yes      | O(1) amortized  | Add items to **end**                                      | `let arr = [1,2]; arr.push(3,4)`                      | 4 (arr becomes [1,2,3,4])                           |
| `pop()`        | removed element                | Yes      | O(1)            | Remove & return last element                              | `let arr = [1,2,3]; arr.pop()`                         | 3 (arr becomes [1,2])                               |
| `unshift(...items)` | new length                | Yes      | O(n)            | Add items to **beginning**                                | `let arr = [2,3]; arr.unshift(0,1)`                   | 4 (arr becomes [0,1,2,3])                           |
| `shift()`      | removed element                | Yes      | O(n)            | Remove & return first element                             | `let arr = [1,2,3]; arr.shift()`                       | 1 (arr becomes [2,3])                               |
| `splice(start, deleteCount?, ...items)` | removed items array | Yes      | O(n)            | Remove/replace/insert at index                            | Simple: `let arr = [1,2,3,4]; arr.splice(1,2)`<br>Complex: `let arr = [1,2,3]; arr.splice(1,1,'a','b')` | Simple: [2,3] (arr: [1,4])<br>Complex: [2] (arr: [1,'a','b',3]) |
| `reverse()`    | the array itself               | Yes      | O(n)            | Reverse order in place                                    | `let arr = [1,2,3]; arr.reverse()`                     | [3,2,1] (arr modified)                              |
| `sort(compareFn?)` | the array itself           | Yes      | O(n log n)      | Sort in place (default: string conversion)                | Simple: `let arr = [3,1,2]; arr.sort()`<br>Complex: `let arr = [{age:30},{age:20}]; arr.sort((a,b) => a.age - b.age)` | Simple: [1,2,3] (arr modified)<br>Complex: [{age:20},{age:30}] |
| `fill(value, start?, end?)` | the array itself      | Yes      | O(n)            | Fill range with static value                              | `let arr = [1,2,3]; arr.fill(0,1)`                    | [1,0,0] (arr modified)                              |
| `copyWithin(target, start, end?)` | the array itself | Yes      | O(n)            | Copy part of array to another position (overlap safe)     | `let arr = [1,2,3,4,5]; arr.copyWithin(0,3)`          | [4,5,3,4,5] (arr modified)                          |

## 3. Safe Access / Combination / Conversion (Non-mutating)

| Method              | Returns             | Mutates? | Time Complexity | Purpose                                                    | Example                                                | Output                                              |
|---------------------|---------------------|----------|-----------------|------------------------------------------------------------|--------------------------------------------------------|-----------------------------------------------------|
| `slice(start?, end?)` | **new array**       | No       | O(n)            | Shallow copy of portion                                    | `let arr = [1,2,3,4]; arr.slice(1,3)`                 | [2,3]                                               |
| `concat(...values)` | **new array**       | No       | O(n)            | Merge arrays / values                                      | Simple: `let arr = [1,2]; arr.concat([3])`<br>Complex: `let arr = [1]; arr.concat([2,3],4,[5])` | Simple: [1,2,3]<br>Complex: [1,2,3,4,5]             |
| `join(separator?)`  | string              | No       | O(n)            | Join elements into string                                  | `let arr = ['a','b','c']; arr.join('-')`              | 'a-b-c'                                             |
| `toString()`        | string              | No       | O(n)            | `join(",")` basically                                      | `let arr = [1,2,3]; arr.toString()`                   | '1,2,3'                                             |
| `indexOf(item, from?)` | index or -1      | No       | O(n)            | First position of value (strict ===)                       | `let arr = [1,2,1]; arr.indexOf(1)`                   | 0                                                   |
| `lastIndexOf(item, from?)` | index or -1  | No       | O(n)            | Last position of value                                     | `let arr = [1,2,1]; arr.lastIndexOf(1)`               | 2                                                   |
| `includes(item, from?)` | boolean         | No       | O(n)            | Does array contain value? (strict)                         | `let arr = [1,2,3]; arr.includes(2)`                  | true                                                |
| `flat(depth?)`      | **new array**       | No       | O(n)            | Flatten nested arrays (default depth = 1)                  | Simple: `let arr = [1,[2]]; arr.flat()`<br>Complex: `let arr = [1,[2,[3]]]; arr.flat(Infinity)` | Simple: [1,2]<br>Complex: [1,2,3]                   |
| `flatMap(callback)` | **new array**       | No       | O(n)            | map() + flat(1) in one step                                | `let arr = [1,2]; arr.flatMap(x => [x, x*2])`         | [1,2,2,4]                                           |
| `at(index)`         | element or undefined| No       | O(1)            | Get element (supports negative indices) – ES2022+          | `let arr = [1,2,3]; arr.at(-1)`                       | 3                                                   |

## 4. Iterator-returning methods

| Method       | Returns                        | Time Complexity | Use case example                                | Output Example                                      |
|--------------|--------------------------------|-----------------|-------------------------------------------------|-----------------------------------------------------|
| `keys()`     | Iterator of indices            | O(1) setup      | `let arr = ['a','b']; for (const i of arr.keys()) console.log(i)` | Logs: 0 1                                           |
| `values()`   | Iterator of values             | O(1) setup      | `let arr = ['a','b']; for (const v of arr.values()) console.log(v)` | Logs: 'a' 'b'                                       |
| `entries()`  | Iterator of [index, value]     | O(1) setup      | `let arr = ['a','b']; for (const [i, v] of arr.entries()) console.log(i, v)` | Logs: 0 'a' 1 'b'                                   |

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

## Best Practices (2025+)

- Prefer immutability → use `map`, `filter`, `slice`, spread, `flatMap`
- Chain methods: `arr.filter(...).map(...).sort(...)`
- Use `at(-1)` instead of `arr[arr.length-1]`
- Use `find` / `findLast` instead of manual loops when you need first/last match
- `flatMap` is great for 1→many transformations
- Avoid `forEach` when you can use `map`/`filter`/`for...of`
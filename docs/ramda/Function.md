## __

柯里化函数的参数占位符。允许部分应用于任何位置的参数。

假设 `g` 代表柯里化的三元函数，`_` 代表 `R.__`，则下面几种写法是等价的：

- `g(1, 2, 3)`
- `g(_, 2, 3)(1)`
- `g(_, _, 3)(1)(2)`
- `g(_, _, 3)(1, 2)`
- `g(_, 2, _)(1, 3)`
- `g(_, 2)(1)(3)`
- `g(_, 2)(1, 3)`
- `g(_, 2)(_, 3)(1)`

### 例子

```js
const greet = R.replace('{name}', R.__, 'Hello, {name}!');
greet('Alice'); //=> 'Hello, Alice!'
```

### 参考
- [https://ramdajs.com/docs/#__](https://ramdajs.com/docs/#__)

## addIndex
通过向列表迭代函数的回调函数添加两个新的参数：当前索引、整个列表，创建新的列表迭代函数。

例如，`addIndex` 可以将 `R.map` 转换为类似于 `Array.prototype.map` 的函数。注意，`addIndex` 只适用于迭代回调函数是首个参数、列表是最后一个参数的函数。（如果列表参数没有用到，后一个条件可以忽略）。

### 参数

```
((a … → b) … → [a] → *) → ((a …, Int, [a] → b) … → [a] → *)
```

- `fn`: 列表迭代函数，不将索引或列表传递给其回调。
- 返回函数更改后的列表迭代函数，将其 `(item, index, list)` 传递给其回调。

### 例子

```js
const mapIndexed = R.addIndex(R.map);
mapIndexed((val, idx) => idx + '-' + val, ['f', 'o', 'o', 'b', 'a', 'r']);
//=> ['0-f', '1-o', '2-o', '3-b', '4-a', '5-r']
```

### 参考
- [https://ramdajs.com/docs/#addIndex](https://ramdajs.com/docs/#addIndex)

## always
返回一个返回恒定值的函数。注意，对于非原始值，返回的值是对原始值的引用。

此函数在其他语言或库中也被称作：`const`、`constant`、或 `K` (K combinator 中)。

### 参数

```js
a → (* → a)
```

- `val`：包装在函数中的值。
- 返回一个返回恒定值的函数。

### 例子

```js
const t = R.always('Tee');
t(); //=> 'Tee'
```

### 参考
- [https://ramdajs.com/docs/#always](https://ramdajs.com/docs/#always)

## andThen
将 `onSuccess` 函数应用于一个 `fulfilled Promise` 的内部值，并将计算结果放入新的 `Promise` 中返回。这对于处理函数组合内的  `promises` 很有用。

### 参数

```
(a → b) → (Promise e a) → (Promise e b)
(a → (Promise e b)) → (Promise e a) → (Promise e b)
```

- `onSuccess`：要应用的函数。可以返回值或值的 `Promise`。
- `p`。
- 返回 Promise 调用 `p.then（onSuccess）`的结果。

### 例子

```js
var makeQuery = (email) => ({ query: { email } });

//getMemberName :: String -> Promise ({firstName, lastName})
var getMemberName = R.pipe(
    makeQuery,
    fetchMember,
    R.andThen(R.pick(['firstName', 'lastName']))
);
```

### 参考
- [https://ramdajs.com/docs/#andThen](https://ramdajs.com/docs/#andThen)

## ap

`ap` 将函数列表作用于值列表上。

若第二个参数自身存在 `ap` 方法，则调用自身的 `ap` 方法。柯里化函数也可以作为 applicative。

### 参数

```js
[a → b] → [a] → [b]
Apply f => f (a → b) → f a → f b
(r → a → b) → (r → a) → (r → b)
```

- `applyF`。
- `applyX`。
- 返回 `*`。

### 例子

```js
R.ap([R.multiply(2), R.add(3)], [1, 2, 3]); //=> [2, 4, 6, 4, 5, 6]
R.ap([R.concat('tasty '), R.toUpper], ['pizza', 'salad']); //=> ["tasty pizza", "tasty salad", "PIZZA", "SALAD"]

// R.ap can also be used as S combinator
// when only two functions are passed
R.ap(R.concat, R.toUpper)('Ramda') //=> 'RamdaRAMDA'
```

### 参考
- [https://ramdajs.com/docs/#ap](https://ramdajs.com/docs/#ap)

## apply
将函数 `fn` 作用于参数列表 `args`。`apply` 可以将变参函数转换为为定参函数。如果上下文很重要，则 `fn` 应该绑定其上下文。

### 参数

```
(*… → a) → [*] → a
```

- `fn`: 将用 `args` 调用的函数。
- `args`：用 `fn` 调用的参数。
- 返回 `*`，结果相当于 `fn(...args)`。

### 例子

```js
const nums = [1, 2, 3, -99, 42, 6, 7];
R.apply(Math.max, nums); //=> 42
```

### 参考
- [https://ramdajs.com/docs/#apply](https://ramdajs.com/docs/#apply)

## applySpec
接受一个属性值为函数的对象，返回一个能生成相同结构对象的函数。返回的函数使用传入的参数调用对象的每个属性位对应的函数，来生成相应属性的值。

### 参数

```
{k: ((a, b, …, m) → v)} → ((a, b, …, m) → {k: v})
```

- `spec`：对象将属性递归地映射到用于为这些属性生成值的函数。
- 返回 `function`：返回一个与 `spec` 具有相同结构的对象的函数，每个属性都设置为通过使用提供的参数调用其关联函数而返回的值。

### 例子

```js
const getMetrics = R.applySpec({
    sum: R.add,
    nested: { mul: R.multiply }
});
getMetrics(2, 4); // => { sum: 6, nested: { mul: 8 } }
```

### 参考
- [https://ramdajs.com/docs/#applySpec](https://ramdajs.com/docs/#applySpec)

## applyTo
接受一个值，并将一个函数作用于其上。

该函数又被称为 thrush combinator。

### 参数

```js
a → (a → b) → b
```

- `x`：值。
- `f`：要应用的函数。
- 返回 `*`：将 `f` 应用于 `x` 的结果。

### 例子

```js
const t42 = R.applyTo(42);
t42(R.identity); //=> 42
t42(R.add(1)); //=> 43
```

### 参考
- [https://ramdajs.com/docs/#applyTo](https://ramdajs.com/docs/#applyTo)

## ascend
由返回值可与 `<` 和 `>` 比较的函数，创建一个升序比较函数。

### 参数

```
Ord b => (a → b) → a → a → Number
```

- `fn`：一个返回值是可以比较的值的函数。
- `a`：要比较的第一项。
- `b`：要比较的第二项。
- 返回 `Number`：如果 `fn(a) < fn(b)` 返回 `-1`，`fn(b) < fn(a)` 返回 `1`，否则返回 `0`。

### 例子

```js
const byAge = R.ascend(R.prop('age'));
const people = [
    { name: 'Emma', age: 70 },
    { name: 'Peter', age: 78 },
    { name: 'Mikhail', age: 62 },
];
const peopleByYoungestFirst = R.sort(byAge, people);
//=> [{ name: 'Mikhail', age: 62 },{ name: 'Emma', age: 70 }, { name: 'Peter', age: 78 }]
```

### 参考
- [https://ramdajs.com/docs/#ascend](https://ramdajs.com/docs/#ascend)


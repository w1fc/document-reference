## chunk

```js
_.chunk(array, [size=1])
```

将 `array` 拆分成多个 `size` 长度的区块，并将这些区块组成一个新数组。如果 `array` 无法被分割成全部等长的区块，那么最后剩余的元素将组成一个区块。

### 参数
- `array (Array)`: 需要处理的数组。
- `[size=1] (number)`: 每个数组区块的长度。

### 返回
- `(Array)`: 返回一个包含拆分区块的新数组。

### 例子

```js
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]
 
_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

### 参考
- [https://lodash.com/docs/4.17.15#chunk](https://lodash.com/docs/4.17.15#chunk)

## compact

```js
_.compact(array)
```

创建一个新数组，包含原数组中所有的非假值元素。例如 `false`, `null`, `0`, `""`, `undefined`, 和 `NaN` 都是被认为是“假值”。

### 参数
- `array (Array)`: 待处理的数组。

### 返回
- `(Array)`: 返回过滤掉假值的新数组。

### 例子

```js
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

### 参考
- [https://lodash.com/docs/4.17.15#compact](https://lodash.com/docs/4.17.15#compact)

## concat

```js
_.concat(array, [values])
```

创建一个新数组，将 `array` 与任何**数组或值**连接在一起。

### 参数
- `array (Array)`: 被连接的数组。
- `[values] (...*)`: 连接的值。

### 返回
- `(Array)`: 返回连接后的新数组。

### 例子

```js
var array = [1];
var other = _.concat(array, 2, [3], [[4]]);

console.log(other);
// => [1, 2, 3, [4]]

console.log(array);
// => [1]
```

### 参考
- [https://lodash.com/docs/4.17.15#concat](https://lodash.com/docs/4.17.15#concat)

## difference

```js
_.difference(array, [values])
```

创建一个具有唯一 `array` 值的数组，每个值不包含在其他给定的数组中。该方法使用 `SameValueZero` 做相等比较。结果值的顺序和参考由第一个数组确定。

注意: 不同于 `_.pullAll`，这个方法会返回一个新数组。

### 参数
- `array (Array)`: 要检查的数组。
- `[values] (...Array)`: 排除的值。

### 返回
- `(Array)`: 返回一个过滤值后的新数组。

### 例子

```js
_.difference([3, 2, 1], [4, 2]);
// => [3, 1]
```

### 参考
- [https://lodash.com/docs/4.17.15#difference](https://lodash.com/docs/4.17.15#difference)

## differenceBy

```js
_.differenceBy(array, [values], [iteratee=_.identity])
```

此方法类似于 `_.difference`，不同之处在于它接受为 `array` 和 `values` 的每个元素调用的 `iteratee`，以生成比较它们的条件。结果值的顺序和参考由第一个数组确定。`iteratee` 调用一个参数：`(value)`。

注意: 不同于 `_.pullAllBy`，这个方法会返回一个新数组。

### 参数
- `array (Array)`: 要检查的数组。
- `[values] (...Array)`: 要排除的值。
- `[iteratee=_.identity] (Array|Function|Object|string)`: `iteratee` 调用每个元素。

### 返回
- `(Array)`: 返回一个过滤值后的新数组。

### 例子

```js
_.differenceBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// => [1.2]
 
// The `_.property` iteratee shorthand.
_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
// => [{ 'x': 2 }]
```

### 参考
- [https://lodash.com/docs/4.17.15#differenceBy](https://lodash.com/docs/4.17.15#differenceBy)

## differenceWith

```js
_.differenceWith(array, [values], [comparator])
```

此方法类似于 `_.difference`，不同之处在于它接受 `comparator`，该比较器被调用以将 `array` 的元素与 `values` 进行比较。结果值的顺序和参考由第一个数组确定。比较器调用两个参数：`(arrVal，othVal)` 。

注意: 不像 `_.pullAllWith`, 这个方法会返回一个新数组。

### 参数
- `array (Array)`: 要检查的数组。
- `[values] (...Array)`: 要排除的值。
- `[comparator] (Function)`: `comparator` 调用每个元素。

### 返回
- `(Array)`: 返回一个过滤值后的新数组。

### 例子

```js
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
 
_.differenceWith(objects, [{ 'x': 1, 'y': 2 }], _.isEqual);
// => [{ 'x': 2, 'y': 1 }]
```

### 参考
- [https://lodash.com/docs/4.17.15#differenceWith](https://lodash.com/docs/4.17.15#differenceWith)

## drop

```js
_.drop(array, [n=1])
```

创建一个切片数组，去除 `array` 前面的 `n` 个元素。（ `n` 默认值为 `1` 。）

### 参数
- `array (Array)`: 要查询的数组。
- `[n=1] (number)`: 要去除的元素个数。

### 返回
- `(Array)`: 返回 `array` 剩余切片。

### 例子

```js
_.drop([1, 2, 3]);
// => [2, 3]

_.drop([1, 2, 3], 2);
// => [3]

_.drop([1, 2, 3], 5);
// => []

_.drop([1, 2, 3], 0);
// => [1, 2, 3]
```

### 参考
- [https://lodash.com/docs/4.17.15#drop](https://lodash.com/docs/4.17.15#drop)

## dropRight

```js
_.dropRight(array, [n=1])
```

创建一个切片数组，去除 `array` 尾部的 `n` 个元素。（ `n` 默认值为 `1` 。）

### 参数
- `array (Array)`: 要查询的数组。
- `[n=1] (number)`: 要去除的元素个数。

### 返回
- `(Array)`: 返回 `array` 剩余切片。

### 例子

```js
_.dropRight([1, 2, 3]);
// => [1, 2]
 
_.dropRight([1, 2, 3], 2);
// => [1]
 
_.dropRight([1, 2, 3], 5);
// => []
 
_.dropRight([1, 2, 3], 0);
// => [1, 2, 3]
```

### 参考
- [https://lodash.com/docs/4.17.15#dropRight](https://lodash.com/docs/4.17.15#dropRight)

## dropRightWhile

```js
_.dropRightWhile(array, [predicate=_.identity])
```

创建一个切片数组，去除 `array` 中从 `predicate` 返回假值开始到尾部的部分。`predicate` 会传入 3 个参数：`(value, index, array)`。

### 参数
- `array (Array)`: 要查询的数组。
- `[predicate=_.identity] (Function)`: 这个函数会在每一次迭代调用。

### 返回
- `(Array)`: 返回 `array` 剩余切片。

### 例子

```js
var users = [
    { 'user': 'barney', 'active': true },
    { 'user': 'fred', 'active': false },
    { 'user': 'pebbles', 'active': false }
];

_.dropRightWhile(users, function (o) { return !o.active; });
// => objects for ['barney']

// The `_.matches` iteratee shorthand.
_.dropRightWhile(users, { 'user': 'pebbles', 'active': false });
// => objects for ['barney', 'fred']

// The `_.matchesProperty` iteratee shorthand.
_.dropRightWhile(users, ['active', false]);
// => objects for ['barney']

// The `_.property` iteratee shorthand.
_.dropRightWhile(users, 'active');
// => objects for ['barney', 'fred', 'pebbles']
```

### 参考
- [https://lodash.com/docs/4.17.15#dropRightWhile](https://lodash.com/docs/4.17.15#dropRightWhile)

## dropWhile

```js
_.dropWhile(array, [predicate=_.identity])
```

创建一个切片数组，去除 `array` 中从起点开始到 `predicate` 返回假值结束部分。`predicate` 会传入 3 个参数：`(value, index, array)`。

### 参数
- `array (Array)`: 要查询的数组。
- `[predicate=_.identity] (Function)`: 这个函数会在每一次迭代调用。

### 返回
- `(Array)`: 返回 `array` 剩余切片。

### 例子

```js
var users = [
    { 'user': 'barney', 'active': false },
    { 'user': 'fred', 'active': false },
    { 'user': 'pebbles', 'active': true }
];

_.dropWhile(users, function (o) { return !o.active; });
// => objects for ['pebbles']

// The `_.matches` iteratee shorthand.
_.dropWhile(users, { 'user': 'barney', 'active': false });
// => objects for ['fred', 'pebbles']

// The `_.matchesProperty` iteratee shorthand.
_.dropWhile(users, ['active', false]);
// => objects for ['pebbles']

// The `_.property` iteratee shorthand.
_.dropWhile(users, 'active');
// => objects for ['barney', 'fred', 'pebbles']
```

### 参考
- [https://lodash.com/docs/4.17.15#dropWhile](https://lodash.com/docs/4.17.15#dropWhile)

## fill

```js
_.fill(array, value, [start=0], [end=array.length])
```

使用从 `start` 到 `end`（但不包括 `end`）的 `value` 填充 `array`。

注意：这个方法会改变 `array`。

### 参数
- `array (Array)`: 要填充改变的数组。
- `value (*)`: 填充给 `array` 的值。
- `[start=0] (number)`: 开始位置（默认 `0` ）。
- `[end=array.length] (number)`: 结束位置（默认 `array.length` ）。

### 返回
- `(Array)`: 返回 `array`。

### 例子

```js
var array = [1, 2, 3];

_.fill(array, 'a');
console.log(array);
// => ['a', 'a', 'a']

_.fill(Array(3), 2);
// => [2, 2, 2]

_.fill([4, 6, 8, 10], '*', 1, 3);
// => [4, '*', '*', 10]
```

### 参考
- [https://lodash.com/docs/4.17.15#fill](https://lodash.com/docs/4.17.15#fill)

## findIndex

```js
_.findIndex(array, [predicate=_.identity], [fromIndex=0])
```

该方法类似 `_.find`，区别是该方法返回第一个通过 `predicate` 判断为真值的元素的索引值（`index`），而不是元素本身。

### 参数
- `array (Array)`: 要搜索的数组。
- `[predicate=_.identity] (Array|Function|Object|string)`: 这个函数会在每一次迭代调用。
- `[fromIndex=0] (number)`: 开始搜索的索引.

### 返回
- `(number)`: 返回找到元素的索引值（ `index` ），否则返回 `-1`。

### 例子

```js
var users = [
    { 'user': 'barney', 'active': false },
    { 'user': 'fred', 'active': false },
    { 'user': 'pebbles', 'active': true }
];

_.findIndex(users, function (o) { return o.user == 'barney'; });
// => 0

// The `_.matches` iteratee shorthand.
_.findIndex(users, { 'user': 'fred', 'active': false });
// => 1

// The `_.matchesProperty` iteratee shorthand.
_.findIndex(users, ['active', false]);
// => 0

// The `_.property` iteratee shorthand.
_.findIndex(users, 'active');
// => 2
```

### 参考
- [https://lodash.com/docs/4.17.15#findIndex](https://lodash.com/docs/4.17.15#findIndex)

## findLastIndex
这个方式类似 `_.findIndex`，区别是它是从右到左的迭代集合 `array` 中的元素。

### 参数
- `array (Array)`: 要搜索的数组。
- `[predicate=_.identity] (Array|Function|Object|string)`: 这个函数会在每一次迭代调用。
- `[fromIndex=array.length-1] (number)`: 开始搜索的索引。

### 返回
- `(number)`: 返回找到元素的索引值（ `index` ），否则返回 `-1`。

### 例子

```js
var users = [
    { 'user': 'barney', 'active': true },
    { 'user': 'fred', 'active': false },
    { 'user': 'pebbles', 'active': false }
];

_.findLastIndex(users, function (o) { return o.user == 'pebbles'; });
// => 2

// The `_.matches` iteratee shorthand.
_.findLastIndex(users, { 'user': 'barney', 'active': true });
// => 0

// The `_.matchesProperty` iteratee shorthand.
_.findLastIndex(users, ['active', false]);
// => 2

// The `_.property` iteratee shorthand.
_.findLastIndex(users, 'active');
// => 0
```

### 参考
- [https://lodash.com/docs/4.17.15#findLastIndex](https://lodash.com/docs/4.17.15#findLastIndex)

## first / head
获取数组 `array` 的第一个元素。

### 参数
- `array (Array)`: 要查询的数组。

### 返回
- `(*)`: 返回数组 `array` 的第一个元素。

### 例子

```js
_.head([1, 2, 3]);
// => 1
 
_.head([]);
// => undefined
```

### 参考
- [https://lodash.com/docs/4.17.15#head](https://lodash.com/docs/4.17.15#head)

## flatten

```js
_.flatten(array)
```

减少一级 `array` 嵌套深度。

### 参数
- `array (Array)`: 需要减少嵌套层级的数组。

### 返回
- `(Array)`: 返回减少嵌套层级后的新数组。

### 例子

```js
_.flatten([1, [2, [3, [4]], 5]]);
// => [1, 2, [3, [4]], 5]
```

### 参考
- [https://lodash.com/docs/4.17.15#flatten](https://lodash.com/docs/4.17.15#flatten)

## flattenDeep

```js
_.flattenDeep(array)
```

将 `array` 递归为一维数组。

### 参数
- `array (Array)`: 需要处理的数组。

### 返回
- `(Array)`: 返回一个的新一维数组。

### 例子

```js
_.flattenDeep([1, [2, [3, [4]], 5]]);
// => [1, 2, 3, 4, 5]
```

### 参考
- [https://lodash.com/docs/4.17.15#flattenDeep](https://lodash.com/docs/4.17.15#flattenDeep)

## flattenDepth

```js
_.flattenDepth(array, [depth=1])
```

根据 `depth` 递归减少 `array` 的嵌套层级。

### 参数
- `array (Array)`: 需要减少嵌套层级的数组。
- `[depth=1] (number)`:最多减少的嵌套层级数。

### 返回
- `(Array)`: 返回减少嵌套层级后的新数组。

### 例子

```js
var array = [1, [2, [3, [4]], 5]];

_.flattenDepth(array, 1);
// => [1, 2, [3, [4]], 5]

_.flattenDepth(array, 2);
// => [1, 2, 3, [4], 5]
```

### 参考
- [https://lodash.com/docs/4.17.15#flattenDepth](https://lodash.com/docs/4.17.15#flattenDepth)

## fromPairs

```js
_.fromPairs(pairs)
```

与 `_.toPairs` 正好相反；这个方法返回一个由键值对 `pairs` 构成的对象。

### 参数
- `pairs (Array)`: 键值对 `pairs`。

### 返回
- `(Object)`: 返回一个新对象。

### 例子

```js
_.fromPairs([['fred', 30], ['barney', 40]]);
// => { 'fred': 30, 'barney': 40 }
```

### 参考
- [https://lodash.com/docs/4.17.15#fromPairs](https://lodash.com/docs/4.17.15#fromPairs)

## indexOf

```js
_.indexOf(array, value, [fromIndex=0])
```

使用 `SameValueZero` 等值比较，返回首次 `value` 在数组 `array` 中被找到的索引值，如果 `fromIndex` 为负值，将从数组 `array` 尾端索引进行匹配。

### 参数
- `array (Array)`: 需要查找的数组。
- `value (*)`: 需要查找的值。
- `[fromIndex=0] (number)`: 开始查询的位置。

### 返回
- `(number)`: 返回值 `value` 在数组中的索引位置, 没有找到为返回 `-1`。

### 例子

```js
_.indexOf([1, 2, 1, 2], 2);
// => 1

// Search from the `fromIndex`.
_.indexOf([1, 2, 1, 2], 2, 2);
// => 3
```

### 参考
- [https://lodash.com/docs/4.17.15#indexOf](https://lodash.com/docs/4.17.15#indexOf)

## initial

```js
_.initial(array)
```

获取数组 `array` 中除了最后一个元素之外的所有元素。

### 参数
- `array (Array)`: 要查询的数组。

### 返回
- `(Array)`: 返回截取后的数组 `array`。

### 例子

```js
_.initial([1, 2, 3]);
// => [1, 2]
```

### 参考
- [https://lodash.com/docs/4.17.15#initial](https://lodash.com/docs/4.17.15#initial)

## intersection

```js
_.intersection([arrays])
```

创建唯一值的数组，这个数组包含所有给定数组都包含的元素，使用 `SameValueZero` 进行相等性比较。（注：可以理解为给定数组的交集）

### 参数
- `[arrays] (...Array)`: 待检查的数组。

### 返回
- `(Array)`: 返回一个包含所有传入数组交集元素的新数组。

### 例子

```js
_.intersection([2, 1], [4, 2], [1, 2]);
// => [2]
```

### 参考
- [https://lodash.com/docs/4.17.15#intersection](https://lodash.com/docs/4.17.15#intersection)

## intersectionBy

```js
_.intersectionBy([arrays], [iteratee=_.identity])
```

这个方法类似 `_.intersection`，区别是它接受一个 `iteratee` 调用每一个 `arrays` 的每个值以产生一个值，通过产生的值进行比较。结果值是从第一数组中选择。`iteratee` 会传入一个参数：`(value)`。

### 参数
- `[arrays] (...Array)`: 待检查的数组。
- `[iteratee=_.identity] (Array|Function|Object|string)`: `iteratee`（迭代器）调用每个元素。

### 返回
- `(Array)`: 返回一个包含所有传入数组交集元素的新数组。

### 例子

```js
_.intersectionBy([2.1, 1.2], [4.3, 2.4], Math.floor);
// => [2.1]

// The `_.property` iteratee shorthand.
_.intersectionBy([{ 'x': 1 }], [{ 'x': 2 }, { 'x': 1 }], 'x');
// => [{ 'x': 1 }]
```

### 参考
- [https://lodash.com/docs/4.17.15#intersectionBy](https://lodash.com/docs/4.17.15#intersectionBy)

## intersectionWith

```js
_.intersectionWith([arrays], [comparator])
```

这个方法类似 `_.intersection`，区别是它接受一个 `comparator` 调用比较 `arrays` 中的元素。结果值是从第一个数组中选择。`comparator` 会传入两个参数：`(arrVal, othVal)`。

### 参数
- `[arrays] (...Array)`: 待检查的数组。
- `[comparator] (Function)`: `comparator`（比较器）调用每个元素。

### 返回
- `(Array)`: 返回一个包含所有传入数组交集元素的新数组。

### 例子

```js
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }];
 
_.intersectionWith(objects, others, _.isEqual);
// => [{ 'x': 1, 'y': 2 }]
```

### 参考
- [https://lodash.com/docs/4.17.15#intersectionWith](https://lodash.com/docs/4.17.15#intersectionWith)

## join

```js
_.join(array, [separator=','])
```

将 `array` 中的所有元素转换为由 `separator` 分隔的字符串。

### 参数
- `array (Array)`: 要转换的数组。
- `[separator=','] (string)`: 分隔元素。

### 返回
- `(string)`: 返回连接字符串。

### 例子

```js
_.join(['a', 'b', 'c'], '~');
// => 'a~b~c'
```

### 参考
- [https://lodash.com/docs/4.17.15#join](https://lodash.com/docs/4.17.15#join)

## last

```js
_.last(array)
```

获取 `array` 中的最后一个元素。

### 参数
- `array (Array)`: 要检索的数组。

### 返回
- `(*)`: 返回 `array` 中的最后一个元素

### 例子

```js
_.last([1, 2, 3]);
// => 3
```

### 参考
- [https://lodash.com/docs/4.17.15#last](https://lodash.com/docs/4.17.15#last)

## lastIndexOf

```js
_.lastIndexOf(array, value, [fromIndex=array.length-1])
```

这个方法类似 `_.indexOf`，区别是它是从右到左遍历 `array` 的元素。

### 参数
- `array (Array)`: 要搜索的数组。
- `value (*)`: 要搜索的值。
- `[fromIndex=array.length-1] (number)`: 开始搜索的索引值。

### 返回
- `(number)`: 返回匹配值的索引值，否则返回 `-1`。

### 例子

```js
_.lastIndexOf([1, 2, 1, 2], 2);
// => 3

// Search from the `fromIndex`.
_.lastIndexOf([1, 2, 1, 2], 2, 2);
// => 1
```

### 参考
- [https://lodash.com/docs/4.17.15#lastIndexOf](https://lodash.com/docs/4.17.15#lastIndexOf)

## nth

```js
_.nth(array, [n=0])
```

获取 `array` 数组的第 `n` 个元素。如果 `n` 为负数，则返回从数组结尾开始的第 `n` 个元素。

### 参数
- `array (Array)`: 要查询的数组。
- `[n=0] (number)`: 要返回元素的索引值。

### 返回
- `(*)`: 获取 `array` 数组的第 `n` 个元素。

### 例子

```js
var array = ['a', 'b', 'c', 'd'];
 
_.nth(array, 1);
// => 'b'
 
_.nth(array, -2);
// => 'c';
```

### 参考
- [https://lodash.com/docs/4.17.15#nth](https://lodash.com/docs/4.17.15#nth)

## pull

```js
_.pull(array, [values])
```

移除数组 `array` 中所有和给定值相等的元素，使用 `SameValueZero` 进行全等比较。

注意：和 `_.without` 方法不同，这个方法会改变数组。使用 `_.remove` 从一个数组中移除元素。

### 参数
- `array (Array)`: 要修改的数组。
- `[values] (...*)`: 要删除的值。

### 返回
- `(Array)`: 返回 `array`。

### 例子

```js
var array = [1, 2, 3, 1, 2, 3];

_.pull(array, 2, 3);
console.log(array);
// => [1, 1]
```

### 参考
- [https://lodash.com/docs/4.17.15#pull](https://lodash.com/docs/4.17.15#pull)

## pullAll

```js
_.pullAll(array, values)
```

这个方法类似 `_.pull`，区别是这个方法接收一个要移除值的数组。

注意：不同于 `_.difference`, 这个方法会改变数组 `array`。

### 参数
- `array (Array)`: 要修改的数组。
- `values (Array)`: 要移除值的数组。

### 返回
- `(Array)`: 返回 `array`。

### 例子

```js
var array = [1, 2, 3, 1, 2, 3];

_.pullAll(array, [2, 3]);
console.log(array);
// => [1, 1]
```

### 参考
- [https://lodash.com/docs/4.17.15#pullAll](https://lodash.com/docs/4.17.15#pullAll)

## pullAllBy

```js
_.pullAllBy(array, values, [iteratee=_.identity])
```

这个方法类似于 `_.pullAll`，区别是这个方法接受一个 `iteratee` 调用 `array` 和 `values` 的每个值以产生一个值，通过产生的值进行了比较。`iteratee` 会传入一个参数：`(value)`。

注意：不同于 `_.differenceBy`, 这个方法会改变数组 `array`。

### 参数
- `array (Array)`: 要修改的数组。
- `values (Array)`: 要移除值的数组。
- `[iteratee=_.identity] (Array|Function|Object|string)`: `iteratee` 调用每个元素。

### 返回
- `(Array)`: 返回 `array`。

### 例子

```js
var array = [{ 'x': 1 }, { 'x': 2 }, { 'x': 3 }, { 'x': 1 }];

_.pullAllBy(array, [{ 'x': 1 }, { 'x': 3 }], 'x');
console.log(array);
// => [{ 'x': 2 }]
```

### 参考
- [https://lodash.com/docs/4.17.15#pullAllBy](https://lodash.com/docs/4.17.15#pullAllBy)

## pullAllWith

```js
_.pullAllWith(array, values, [comparator])
```

这个方法类似于 `_.pullAll`，区别是这个方法接受 `comparator` 调用 `array` 中的元素和 `values` 比较。`comparator` 会传入两个参数：`(arrVal, othVal)`。

注意: 和 `_.differenceWith` 不同, 这个方法会改变数组 `array`。

### 参数
- `array (Array)`: 要修改的数组。
- `values (Array)`: 要移除值的数组。
- `[comparator] (Function)`: `comparator` 调用每个元素。

### 返回
- `(Array)`: 返回 `array`。

### 例子

```js
var array = [{ 'x': 1, 'y': 2 }, { 'x': 3, 'y': 4 }, { 'x': 5, 'y': 6 }];

_.pullAllWith(array, [{ 'x': 3, 'y': 4 }], _.isEqual);
console.log(array);
// => [{ 'x': 1, 'y': 2 }, { 'x': 5, 'y': 6 }]
```

### 参考
- [https://lodash.com/docs/4.17.15#pullAllWith](https://lodash.com/docs/4.17.15#pullAllWith)

## pullAt

```js
_.pullAt(array, [indexes])
```

根据索引 `indexes`，移除 `array` 中对应的元素，并返回被移除元素的数组。

注意: 和 `_.at` 不同, 这个方法会改变数组 `array`。

### 参数
- `array (Array)`: 要修改的数组。
- `[indexes] (...(number|number[]))`: 要移除元素的索引。

### 返回
- `(Array)`: 返回移除元素组成的新数组。

### 例子

```js
var array = [5, 10, 15, 20];
var evens = _.pullAt(array, 1, 3);

console.log(array);
// => [5, 15]

console.log(evens);
// => [10, 20]
```

### 参考
- [https://lodash.com/docs/4.17.15#pullAt](https://lodash.com/docs/4.17.15#pullAt)

## remove

```js
_.remove(array, [predicate=_.identity])
```

移除数组中 `predicate` 返回为真值的所有元素，并返回移除元素组成的数组。`predicate` 会传入 3 个参数：`(value, index, array)`。

注意: 和 `_.filter` 不同, 这个方法会改变数组 `array`。使用 `_.pull` 来根据提供的 `value` 值从数组中移除元素。

### 参数
- `array (Array)`: 要修改的数组。
- `[predicate=_.identity] (Array|Function|Object|string)`: 每次迭代调用的函数。

### 返回
- `(Array)`: 返回移除元素组成的新数组。

### 例子

```js
var array = [1, 2, 3, 4];
var evens = _.remove(array, function (n) {
    return n % 2 == 0;
});

console.log(array);
// => [1, 3]

console.log(evens);
// => [2, 4]
```

### 参考
- [https://lodash.com/docs/4.17.15#remove](https://lodash.com/docs/4.17.15#remove)

## reverse

```js
_.reverse(array)
```

反转 `array`，使得第一个元素变为最后一个元素，第二个元素变为倒数第二个元素，依次类推。

注意: 这个方法会改变原数组 `array`，基于 [Array#reverse](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)。

### 参数
- `array (Array)`: 要修改的数组。

### 返回
- `(Array)`: 返回 `array`。

### 例子

```js
var array = [1, 2, 3];

_.reverse(array);
// => [3, 2, 1]

console.log(array);
// => [3, 2, 1]
```

### 参考
- [https://lodash.com/docs/4.17.15#reverse](https://lodash.com/docs/4.17.15#reverse)

## slice

```js
_.slice(array, [start=0], [end=array.length])
```

裁剪数组 `array`，从 `start` 位置开始到 `end` 结束，但不包括 `end` 本身的位置。

注意: 这个方法用于代替 [Array#slice](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) 来确保数组正确返回。

### 参数
- `array (Array)`: 要裁剪数组。
- `[start=0] (number)`: 开始位置。
- `[end=array.length] (number)`: 结束位置。

### 返回
- `(Array)`: 返回数组 `array` 裁剪部分的新数组。

### 例子

### 参考
- [https://lodash.com/docs/4.17.15#slice](https://lodash.com/docs/4.17.15#slice)

## sortedIndex

```js
_.sortedIndex(array, value)
```

使用二分检索来决定 `value` 值应该插入到数组中尽可能小的索引位置，以保证 `array` 的排序。

### 参数
- `array (Array)`: 要检查的排序数组。
- `value (*)`: 要评估的值。

### 返回
- `(number)`: 返回 `value` 值应该在数组 `array` 中插入的索引位置 `index`。

### 例子

```js
_.sortedIndex([30, 50], 40);
// => 1
```

### 参考
- [https://lodash.com/docs/4.17.15#sortedIndex](https://lodash.com/docs/4.17.15#sortedIndex)

## sortedIndexBy

```js
_.sortedIndexBy(array, value, [iteratee=_.identity])
```

这个方法类似 `_.sortedIndex` ，不同之处在于它接受一个 `iteratee` ，调用每一个数组的元素，返回结果和 `value` 比较来计算排序。`iteratee` 会传入一个参数：`(value)`。

### 参数
- `array (Array)`: 要检查的排序数组。
- `value (*)`: 要评估的值。
- `[iteratee=_.identity] (Array|Function|Object|string)`: 迭代函数，调用每个元素。

### 返回
- `(number)`: 返回 `value` 值应该在数组 `array` 中插入的索引位置 `index`。

### 例子

```js
var objects = [{ 'x': 4 }, { 'x': 5 }];

_.sortedIndexBy(objects, { 'x': 4 }, function (o) { return o.x; });
// => 0

// The `_.property` iteratee shorthand.
_.sortedIndexBy(objects, { 'x': 4 }, 'x');
// => 0
```

### 参考
- [https://lodash.com/docs/4.17.15#sortedIndexBy](https://lodash.com/docs/4.17.15#sortedIndexBy)

## sortedIndexOf

```js
_.sortedIndexOf(array, value)
```

这个方法类似 `_.indexOf`，不同之处在于它是在已经排序的数组 `array` 上执行二分检索。

### 参数
- `array (Array)`: 要搜索的数组。
- `value (*)`: 搜索的值。

### 返回
- `(number)`: 返回匹配值的索引位置，否则返回 `-1`。

### 例子

```js
_.sortedIndexOf([4, 5, 5, 5, 6], 5);
// => 1
```

### 参考
- [https://lodash.com/docs/4.17.15#sortedIndexOf](https://lodash.com/docs/4.17.15#sortedIndexOf)

## sortedLastIndex

```js
_.sortedLastIndex(array, value)
```

此方法类似于 `_.sortedIndex`，不同之处在于它返回 `value` 值在 `array` 数组中尽可能大的索引位置 `index`。

### 参数
- `array (Array)`: 要检查的排序数组。
- `value (*)`: 要评估的值。

### 返回
- `(number)`: 返回 `value` 值应该在数组 `array` 中插入的索引位置 `index`。

### 例子

```js
_.sortedLastIndex([4, 5, 5, 5, 6], 5);
// => 4
```

### 参考
- [https://lodash.com/docs/4.17.15#sortedLastIndex](https://lodash.com/docs/4.17.15#sortedLastIndex)

## sortedLastIndexBy

```js
_.sortedLastIndexBy(array, value, [iteratee=_.identity])
```

这个方法类似 `_.sortedLastIndex` ，不同之处在于它接受一个迭代函数 `iteratee` ，调用每一个数组 `array` 元素，返回结果和 `value` 值比较来计算排序。`iteratee` 会传入一个参数：`(value)`。

### 参数
- `array (Array)`: 要检查的排序数组。
- `value (*)`: 要评估的值。
- `[iteratee=_.identity] (Array|Function|Object|string)`: 迭代函数，调用每个元素。

### 返回
- `(number)`: 返回 `value` 值应该在数组 `array` 中插入的索引位置 `index`。

### 例子

```js
var objects = [{ 'x': 4 }, { 'x': 5 }];

_.sortedLastIndexBy(objects, { 'x': 4 }, function (o) { return o.x; });
// => 1

// The `_.property` iteratee shorthand.
_.sortedLastIndexBy(objects, { 'x': 4 }, 'x');
// => 1
```

### 参考
- [https://lodash.com/docs/4.17.15#sortedLastIndexBy](https://lodash.com/docs/4.17.15#sortedLastIndexBy)

## sortedLastIndexOf

```js
_.sortedLastIndexOf(array, value)
```

这个方法类似 `_.lastIndexOf`，不同之处在于它是在已经排序的数组 `array` 上执行二分检索。

### 参数
- `array (Array)`: 要搜索的数组。
- `value (*)`: 搜索的值。

### 返回
- `(number)`: 返回匹配值的索引位置，否则返回 `-1`。

### 例子

```js
_.sortedLastIndexOf([4, 5, 5, 5, 6], 5);
// => 3
```

### 参考
- [https://lodash.com/docs/4.17.15#sortedLastIndexOf](https://lodash.com/docs/4.17.15#sortedLastIndexOf)

## sortedUniq

```js
_.sortedUniq(array)
```

这个方法类似 `_.uniq`，不同之处在于它会优化排序数组。

### 参数
- `array (Array)`: 要检查的数组。

### 返回
- `(Array)`: 返回一个新的不重复的数组。

### 例子

```js
_.sortedUniq([1, 1, 2]);
// => [1, 2]
```

### 参考
- [https://lodash.com/docs/4.17.15#sortedUniq](https://lodash.com/docs/4.17.15#sortedUniq)

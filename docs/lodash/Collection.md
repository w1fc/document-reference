## countBy

```js
_.countBy(collection, [iteratee=_.identity])
```

创建一个组成对象，键 `key` 是经过迭代函数 `iteratee` 执行处理 `collection` 中每个元素后返回的结果，每个键 `key` 对应的值是迭代函数 `iteratee` 返回该键 `key` 的迭代次数。`iteratee` 调用一个参数：`(value)`。

### 参数
- `collection (Array|Object)`: 一个用来迭代的集合。
- `[iteratee=_.identity] (Array|Function|Object|string)`: 一个迭代函数，用来转换键 `key`。

### 返回
- `(Object)`: 返回一个组成集合对象。

### 例子

```js
_.countBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': 1, '6': 2 }

// The `_.property` iteratee shorthand.
_.countBy(['one', 'two', 'three'], 'length');
// => { '3': 2, '5': 1 }
```

### 参考
- [https://lodash.com/docs/4.17.15#countBy](https://lodash.com/docs/4.17.15#countBy)

## each / forEach

```js
_.forEach(collection, [iteratee=_.identity])
```

调用 `iteratee` 遍历集合 `collection` 中的每个元素，`iteratee` 调用 3 个参数：`(value, index|key, collection)`。如果迭代函数 `iteratee` 显式的返回 `false` ，迭代会提前退出。

注意: 与其他"集合"方法一样，类似于数组，对象的 `"length"` 属性也会被遍历。想避免这种情况，可以用 `_.forIn` 或者 `_.forOwn` 代替。

### 参数
- `collection (Array|Object)`: 一个用来迭代的集合。
- `[iteratee=_.identity] (Function)`: 每次迭代调用的函数。

### 返回
- `(*)`: 返回集合 `collection`。

### 例子

```js
_([1, 2]).forEach(function (value) {
    console.log(value);
});
// => Logs `1` then `2`.

_.forEach({ 'a': 1, 'b': 2 }, function (value, key) {
    console.log(key);
});
// => Logs 'a' then 'b' (iteration order is not guaranteed).
```

### 参考
- [https://lodash.com/docs/4.17.15#forEach](https://lodash.com/docs/4.17.15#forEach)

## eachRight / forEachRight

```js
_.forEachRight(collection, [iteratee=_.identity])
```

这个方法类似 `_.forEach`，不同之处在于，`_.forEachRight` 是从右到左遍历集合中每一个元素的。

### 参数
- `collection (Array|Object)`: 一个用来迭代的集合。
- `[iteratee=_.identity] (Function)`: 每次迭代调用的函数。

### 返回
- `(*)`: 返回集合 `collection`。

### 例子

```js
_.forEachRight([1, 2], function (value) {
    console.log(value);
});
// => Logs `2` then `1`.
```

### 参考
- [https://lodash.com/docs/4.17.15#forEachRight](https://lodash.com/docs/4.17.15#forEachRight)

## every

```js
_.every(collection, [predicate=_.identity])
```

通过断言函数 `predicate` 检查集合 `collection` 中的所有元素是否都返回真值。一旦断言函数 `predicate` 返回假值，迭代就马上停止。断言函数 `predicate` 调用三个参数：`(value, index|key, collection)`。

注意: 这个方法对于对于空集合返回 `true`，因为空集合的任何元素都是 `true` 。

### 参数
- `collection (Array|Object)`: 一个用来迭代的集合。
- `[predicate=_.identity] (Array|Function|Object|string)`: 每次迭代调用的函数。

### 返回
- `(boolean)`: 如果所有元素经断言函数 `predicate` 检查后都都返回真值，那么就返回 `true`，否则返回 `false` 。

### 例子

```js
_.every([true, 1, null, 'yes'], Boolean);
// => false

var users = [
    { 'user': 'barney', 'age': 36, 'active': false },
    { 'user': 'fred', 'age': 40, 'active': false }
];

// The `_.matches` iteratee shorthand.
_.every(users, { 'user': 'barney', 'active': false });
// => false

// The `_.matchesProperty` iteratee shorthand.
_.every(users, ['active', false]);
// => true

// The `_.property` iteratee shorthand.
_.every(users, 'active');
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#every](https://lodash.com/docs/4.17.15#every)

## filter

```js
_.filter(collection, [predicate=_.identity])
```

遍历集合 `collection` 元素，返回断言函数 `predicate` 返回真值的所有元素的数组。断言函数 `predicate` 调用三个参数：`(value, index|key, collection)`。

注意：与 `_.remove` 不同，此方法返回一个新数组。

### 参数
- `collection (Array|Object)`: 一个用来迭代的集合。
- `[predicate=_.identity] (Array|Function|Object|string)`: 每次迭代调用的函数。

### 返回
- `(Array)`: 返回一个新的过滤后的数组。

### 例子

```js
var users = [
    { 'user': 'barney', 'age': 36, 'active': true },
    { 'user': 'fred', 'age': 40, 'active': false }
];

_.filter(users, function (o) { return !o.active; });
// => objects for ['fred']

// The `_.matches` iteratee shorthand.
_.filter(users, { 'age': 36, 'active': true });
// => objects for ['barney']

// The `_.matchesProperty` iteratee shorthand.
_.filter(users, ['active', false]);
// => objects for ['fred']

// The `_.property` iteratee shorthand.
_.filter(users, 'active');
// => objects for ['barney']
```

### 参考
- [https://lodash.com/docs/4.17.15#filter](https://lodash.com/docs/4.17.15#filter)

## find

```js
_.find(collection, [predicate=_.identity], [fromIndex=0])
```

遍历集合 `collection` 元素，返回断言函数 `predicate` 第一个返回真值的第一个元素。断言函数 `predicate` 调用 3 个参数：`(value, index|key, collection)`。

### 参数
- `collection (Array|Object)`: 一个用来迭代的集合。
- `[predicate=_.identity] (Array|Function|Object|string)`: 每次迭代调用的函数。
- `[fromIndex=0] (number)`: 开始搜索的索引位置。

### 返回
- `(*)`: 返回匹配元素，否则返回 `undefined`。

### 例子

```js
var users = [
    { 'user': 'barney', 'age': 36, 'active': true },
    { 'user': 'fred', 'age': 40, 'active': false },
    { 'user': 'pebbles', 'age': 1, 'active': true }
];

_.find(users, function (o) { return o.age < 40; });
// => object for 'barney'

// The `_.matches` iteratee shorthand.
_.find(users, { 'age': 1, 'active': true });
// => object for 'pebbles'

// The `_.matchesProperty` iteratee shorthand.
_.find(users, ['active', false]);
// => object for 'fred'

// The `_.property` iteratee shorthand.
_.find(users, 'active');
// => object for 'barney'
```

### 参考
- [https://lodash.com/docs/4.17.15#find](https://lodash.com/docs/4.17.15#find)

## findLast

```js
_.findLast(collection, [predicate=_.identity], [fromIndex=collection.length-1])
```

这个方法类似 `_.find` ，不同之处在于 `_.findLast` 是从右至左遍历集合 `collection` 元素的。

### 参数
- `collection (Array|Object)`: 一个用来迭代的集合。
- `[predicate=_.identity] (Array|Function|Object|string)`: 每次迭代调用的函数。
- `[fromIndex=collection.length-1] (number)`: 开始搜索的索引位置。

### 返回
- `(*)`: 返回匹配元素，否则返回 `undefined`。

### 例子

```js
_.findLast([1, 2, 3, 4], function (n) {
    return n % 2 == 1;
});
// => 3
```

### 参考
- [https://lodash.com/docs/4.17.15#findLast](https://lodash.com/docs/4.17.15#findLast)

## flatMap

```js
_.flatMap(collection, [iteratee=_.identity])
```

创建一个扁平化的数组，这个数组的值来自集合 `collection` 中的每一个值经过迭代函数 `iteratee` 处理后返回的结果，并且扁平化合并。`iteratee` 调用三个参数：`(value, index|key, collection)`。

### 参数
- `collection (Array|Object)`: 一个用来迭代遍历的集合。
- `[iteratee=_.identity] (Array|Function|Object|string)`: 每次迭代调用的函数。

### 返回
- `(Array)`: 返回新扁平化数组。

### 例子

```js
function duplicate(n) {
    return [n, n];
}

_.flatMap([1, 2], duplicate);
// => [1, 1, 2, 2]
```

### 参考
- [https://lodash.com/docs/4.17.15#flatMap](https://lodash.com/docs/4.17.15#flatMap)

## flatMapDeep

```js
_.flatMapDeep(collection, [iteratee=_.identity])
```

这个方法类似 `_.flatMap`，不同之处在于 `_.flatMapDeep` 会继续扁平化递归映射的结果。

### 参数
- `collection (Array|Object)`: 一个用来迭代的集合。
- `[iteratee=_.identity] (Array|Function|Object|string)`: 每次迭代调用的函数。

### 返回
- `(Array)`: 返回新扁平化数组。

### 例子

```js
function duplicate(n) {
    return [[[n, n]]];
}

_.flatMapDeep([1, 2], duplicate);
// => [1, 1, 2, 2]
```

### 参考
- [https://lodash.com/docs/4.17.15#flatMapDeep](https://lodash.com/docs/4.17.15#flatMapDeep)

## flatMapDepth

```js
_.flatMapDepth(collection, [iteratee=_.identity], [depth=1])
```

该方法类似 `_.flatMap`，不同之处在于 `_.flatMapDepth` 会根据指定的递归深度 `depth` 继续扁平化递归映射结果。

### 参数
- `collection (Array|Object)`: 一个用来迭代的集合。
- `[iteratee=_.identity] (Array|Function|Object|string)`: 每次迭代调用的函数。
- `[depth=1] (number)`: 最大递归深度。

### 返回
- `(Array)`: 返回新扁平化数组。

### 例子

```js
function duplicate(n) {
    return [[[n, n]]];
}

_.flatMapDepth([1, 2], duplicate, 2);
// => [[1, 1], [2, 2]]
```

### 参考
- [https://lodash.com/docs/4.17.15#flatMapDepth](https://lodash.com/docs/4.17.15#flatMapDepth)

## groupBy

```js
_.groupBy(collection, [iteratee=_.identity])
```

创建一个对象，`key` 是 `iteratee` 遍历集合 `collection` 中的每个元素返回的结果。分组值的顺序是由他们出现在集合 `collection` 中的顺序确定的。每个键对应的值负责生成 `key` 的元素组成的数组。`iteratee` 调用 1 个参数：`(value)`。

### 参数
- `collection (Array|Object)`: 一个用来迭代的集合。
- `[iteratee=_.identity] (Array|Function|Object|string)`: 这个迭代函数用来转换 `key`。

### 返回
- `(Object)`: 返回一个组成聚合的对象。

### 例子

```js
_.groupBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': [4.2], '6': [6.1, 6.3] }

// The `_.property` iteratee shorthand.
_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

### 参考
- [https://lodash.com/docs/4.17.15#groupBy](https://lodash.com/docs/4.17.15#groupBy)

## includes

```js
_.includes(collection, value, [fromIndex=0])
```

检查值 `value` 是否在集合 `collection` 中。如果集合 `collection` 是一个字符串，那么检查值 `value` 是否在字符串中，否则使用 `SameValueZero` 做等值比较。如果指定 `fromIndex` 是负数，那么从集合 `collection` 的结尾开始检索。

### 参数
- `collection (Array|Object|string)`: 要检索的集合。
- `value (*)`: 要检索的值。
- `[fromIndex=0] (number)`: 要检索的索引位置。

### 返回
- `(boolean)`: 如果找到 `value` 返回 `true`，否则返回 `false`。

### 例子

```js
_.includes([1, 2, 3], 1);
// => true

_.includes([1, 2, 3], 1, 2);
// => false

_.includes({ 'user': 'fred', 'age': 40 }, 'fred');
// => true

_.includes('pebbles', 'eb');
// => true
```

### 参考
- [https://lodash.com/docs/4.17.15#includes](https://lodash.com/docs/4.17.15#includes)

## invokeMap

```js
_.invokeMap(collection, path, [args])
```

调用路径 `path` 上的方法处理集合 `collection` 中的每个元素，返回一个数组，包含每次调用方法得到的结果。任何附加的参数提供给每个被调用的方法。如果方法名 `methodName` 是一个函数，每次调用函数时，内部的 `this` 指向集合中的每个元素。

### 参数
- `collection (Array|Object)`: 用来迭代的集合。
- `path (Array|Function|string)`: 用来调用方法的路径或者每次迭代调用的函数。
- `[args] (...*)`: 调用每个方法的参数。

### 返回
- `(Array)`: 返回的结果数组。

### 例子

```js
_.invokeMap([[5, 1, 7], [3, 2, 1]], 'sort');
// => [[1, 5, 7], [1, 2, 3]]

_.invokeMap([123, 456], String.prototype.split, '');
// => [['1', '2', '3'], ['4', '5', '6']]
```

### 参考
- [https://lodash.com/docs/4.17.15#invokeMap](https://lodash.com/docs/4.17.15#invokeMap)

## keyBy

```js
_.keyBy(collection, [iteratee=_.identity])
```

创建一个由键组成的对象，键 `key` 是集合 `collection` 中的每个元素经过迭代函数 `iteratee` 处理后返回的结果。每个键 `key` 对应的值是生成键 `key` 的最后一个元素。迭代函数 `iteratee` 调用 1 个参数：`(value)`。

### 参数
- `collection (Array|Object)`: 用来迭代的集合。
- `[iteratee=_.identity] (Array|Function|Object|string)`: 这个迭代函数用来转换 `key`。

### 返回
- `(Object)`: 返回一个由键组成的对象。

### 例子

```js
var array = [
    { 'dir': 'left', 'code': 97 },
    { 'dir': 'right', 'code': 100 }
];

_.keyBy(array, function (o) {
    return String.fromCharCode(o.code);
});
// => { 'a': { 'dir': 'left', 'code': 97 }, 'd': { 'dir': 'right', 'code': 100 } }

_.keyBy(array, 'dir');
// => { 'left': { 'dir': 'left', 'code': 97 }, 'right': { 'dir': 'right', 'code': 100 } }
```

### 参考
- [https://lodash.com/docs/4.17.15#keyBy](https://lodash.com/docs/4.17.15#keyBy)

## map

```js
_.map(collection, [iteratee=_.identity])
```

创建一个数组，值 `value` 是迭代函数 `iteratee` 遍历集合 `collection` 中的每个元素后返回的结果。迭代函数 `iteratee` 调用 3 个参数：`(value, index|key, collection)`。

lodash 中有许多方法不能作为其他方法的迭代函数（注：即不能作为 `iteratee` 参数传递给其他方法），例如： `_.every`， `_.filter`，` _.map`，`_.mapValues`， `_.reject`，`_.some`。

受保护的方法有（注：即这些方法不能使用 `_.every`, `_.filter`, `_.map`, `_.mapValues`, `_.reject`, ` _.some` 作为 `iteratee` 迭代函数参数）：`ary`, `chunk`, `curry`, `curryRight`, `drop`, `dropRight`, `every`, `fill`, `invert`, `parseInt`, `random`, `range`, `rangeRight`, `repeat`, `sampleSize`, `slice`, `some`, `sortBy`, `split`, `take`, `takeRight`, `template`, `trim`, `trimEnd`, `trimStart`, `words`。

### 参数
- `collection (Array|Object)`: 用来迭代的集合。
- `[iteratee=_.identity] (Array|Function|Object|string)`: 每次迭代调用的函数。

### 返回
- `(Array)`: 返回新的映射后数组。

### 例子

```js
function square(n) {
    return n * n;
}

_.map([4, 8], square);
// => [16, 64]

_.map({ 'a': 4, 'b': 8 }, square);
// => [16, 64] (iteration order is not guaranteed)

var users = [
    { 'user': 'barney' },
    { 'user': 'fred' }
];

// The `_.property` iteratee shorthand.
_.map(users, 'user');
// => ['barney', 'fred']
```

### 参考
- [https://lodash.com/docs/4.17.15#map](https://lodash.com/docs/4.17.15#map)

## orderBy

```js
_.orderBy(collection, [iteratees=[_.identity]], [orders])
```

此方法类似于 `_.sortBy`，不同之处在于它允许指定迭代函数 `iteratee` 结果如何排序。如果没指定排序 `orders` ，所有值以升序排序。否则，指定为 `"desc"` 降序，或者指定为 `"asc"` 升序，排序对应值。

### 参数
- `collection (Array|Object)`: 用来迭代的集合。
- `[iteratees=[_.identity]] (Array[]|Function[]|Object[]|string[])`: 排序的迭代函数。
- `[orders] (string[])`: `iteratees` 迭代函数的排序顺序。

### 返回
- `(Array)`: 排序后的新数组。

### 例子

```js
var users = [
    { 'user': 'fred', 'age': 48 },
    { 'user': 'barney', 'age': 34 },
    { 'user': 'fred', 'age': 40 },
    { 'user': 'barney', 'age': 36 }
];

// Sort by `user` in ascending order and by `age` in descending order.
_.orderBy(users, ['user', 'age'], ['asc', 'desc']);
// => objects for [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 40]]
```

### 参考
- [https://lodash.com/docs/4.17.15#orderBy](https://lodash.com/docs/4.17.15#orderBy)

## partition
创建一个分成两组的元素数组，第一组包含断言函数 `predicate` 返回为真值 `truthy` 的元素，第二组包含断言函数 `predicate` 返回为假值 `falsey` 的元素。`predicate` 调用 1 个参数：`(value)`。

### 参数
- `collection (Array|Object)`: 用来迭代的集合。
- `[predicate=_.identity] (Array|Function|Object|string)`: 每次迭代调用的函数。

### 返回
- `(Array)`: 返回元素分组后的数组。

### 例子

```js
var users = [
    { 'user': 'barney', 'age': 36, 'active': false },
    { 'user': 'fred', 'age': 40, 'active': true },
    { 'user': 'pebbles', 'age': 1, 'active': false }
];

_.partition(users, function (o) { return o.active; });
// => objects for [['fred'], ['barney', 'pebbles']]

// The `_.matches` iteratee shorthand.
_.partition(users, { 'age': 1, 'active': false });
// => objects for [['pebbles'], ['barney', 'fred']]

// The `_.matchesProperty` iteratee shorthand.
_.partition(users, ['active', false]);
// => objects for [['barney', 'pebbles'], ['fred']]

// The `_.property` iteratee shorthand.
_.partition(users, 'active');
// => objects for [['fred'], ['barney', 'pebbles']]
```

### 参考
- [https://lodash.com/docs/4.17.15#partition](https://lodash.com/docs/4.17.15#partition)

## reduce

```js
_.reduce(collection, [iteratee=_.identity], [accumulator])
```

压缩集合 `collection` 为一个值，通过迭代函数 `iteratee` 遍历集合 `collection` 中的每个元素，每次返回的值会作为下一次迭代使用(注：作为迭代函数 `iteratee` 的第一个参数使用)。如果没有提供 `accumulator`，则集合 `collection` 中的第一个元素作为初始值(注：`accumulator` 参数在第一次迭代的时候作为迭代函数 `iteratee` 第一个参数使用)。`iteratee` 调用 4 个参数：`(accumulator, value, index|key, collection)`。

lodash 中有许多方法不能作为其他方法的迭代函数（注：即不能作为 `iteratee` 参数传递给其他方法），例如：`_.reduce`, `_.reduceRight`, 和 `_.transform` 。

受保护的方法有（注：即这些方法不能使用 `_.reduce`, `_.reduceRight`, `_.transform` 作为 `iteratee` 迭代函数参数）：
`assign`, `defaults`, `defaultsDeep`, `includes`, `merge`, `orderBy`, `sortBy`。

### 参数
- `collection (Array|Object)`: 用来迭代的集合。
- `[iteratee=_.identity] (Function)`: 每次迭代调用的函数。
- `[accumulator] (*)`: 初始值。

### 返回
- `(*)`: 返回累加后的值。

### 例子

```js
_.reduce([1, 2], function (sum, n) {
    return sum + n;
}, 0);
// => 3

_.reduce({ 'a': 1, 'b': 2, 'c': 1 }, function (result, value, key) {
    (result[value] || (result[value] = [])).push(key);
    return result;
}, {});
// => { '1': ['a', 'c'], '2': ['b'] } (iteration order is not guaranteed)
```

### 参考
- [https://lodash.com/docs/4.17.15#reduce](https://lodash.com/docs/4.17.15#reduce)

## reduceRight

```js
_.reduceRight(collection, [iteratee=_.identity], [accumulator])
```

这个方法类似 `_.reduce` ，不同之处在于它是从右到左遍历集合 `collection` 中的元素的。

### 参数
- `collection (Array|Object)`: 用来迭代的集合。
- `[iteratee=_.identity] (Function)`: 每次迭代调用的函数。
- `[accumulator] (*)`: 初始值。

### 返回
- `(*)`: 返回累加后的值。

### 例子

```js
var array = [[0, 1], [2, 3], [4, 5]];

_.reduceRight(array, function (flattened, other) {
    return flattened.concat(other);
}, []);
// => [4, 5, 2, 3, 0, 1]
```

### 参考
- [https://lodash.com/docs/4.17.15#reduceRight](https://lodash.com/docs/4.17.15#reduceRight)

## reject

```js
_.reject(collection, [predicate=_.identity])
```

`_.filter` 的反向方法；此方法返回断言函数 `predicate` 不返回真值 `truthy` 的集合 `collection` 元素。

### 参数
- `collection (Array|Object)`: 用来迭代的集合。
- `[predicate=_.identity] (Array|Function|Object|string)`: 每次迭代调用的函数。

### 返回
- `(Array)`: 返回过滤后的新数组。

### 例子

```js
var users = [
    { 'user': 'barney', 'age': 36, 'active': false },
    { 'user': 'fred', 'age': 40, 'active': true }
];

_.reject(users, function (o) { return !o.active; });
// => objects for ['fred']

// The `_.matches` iteratee shorthand.
_.reject(users, { 'age': 40, 'active': true });
// => objects for ['barney']

// The `_.matchesProperty` iteratee shorthand.
_.reject(users, ['active', false]);
// => objects for ['fred']

// The `_.property` iteratee shorthand.
_.reject(users, 'active');
// => objects for ['barney']
```

### 参考
- [https://lodash.com/docs/4.17.15#reject](https://lodash.com/docs/4.17.15#reject)

## sample

```js
_.sample(collection)
```

从集合 `collection` 中获得一个随机元素。

### 参数
- `collection (Array|Object)`: 要取样的集合。

### 返回
- `(*)`: 返回随机元素。

### 例子

```js
_.sample([1, 2, 3, 4]);
// => 2
```

### 参考
- [https://lodash.com/docs/4.17.15#sample](https://lodash.com/docs/4.17.15#sample)

## sampleSize

```js
_.sampleSize(collection, [n=1])
```

从集合 `collection` 中获得 `n` 个随机元素。

### 参数
- `collection (Array|Object)`: 要取样的集合。
- `[n=1] (number)`: 取样的元素个数。

### 返回
- `(Array)`: 返回随机元素。

### 例子

```js
_.sampleSize([1, 2, 3], 2);
// => [3, 1]
 
_.sampleSize([1, 2, 3], 4);
// => [2, 3, 1]
```

### 参考
- [https://lodash.com/docs/4.17.15#sampleSize](https://lodash.com/docs/4.17.15#sampleSize)

## shuffle

```js
_.shuffle(collection)
```

创建一个被打乱值的集合。使用 [Fisher-Yates shuffle](https://en.wikipedia.org/wiki/Fisher-Yates_shuffle) 版本。

### 参数
- `collection (Array|Object)`: 要打乱的集合。

### 返回
- `(Array)`: 返回打乱的新数组。

### 例子

```js
_.shuffle([1, 2, 3, 4]);
// => [4, 1, 3, 2]
```

### 参考
- [https://lodash.com/docs/4.17.15#shuffle](https://lodash.com/docs/4.17.15#shuffle)

## size

```js
_.size(collection)
```

返回集合 `collection` 的长度，如果集合是类数组或字符串，返回其 `length` ；如果集合是对象，返回其可枚举属性的个数。

### 参数
- `collection (Array|Object)`: 要检查的集合。

### 返回
- `(number)`: 返回集合的长度。

### 例子

```js
_.size([1, 2, 3]);
// => 3

_.size({ 'a': 1, 'b': 2 });
// => 2

_.size('pebbles');
// => 7
```

### 参考
- [https://lodash.com/docs/4.17.15#size](https://lodash.com/docs/4.17.15#size)

## some

```js
_.some(collection, [predicate=_.identity])
```

通过断言函数 `predicate` 检查集合 `collection` 中的元素是否存在任意真值 `truthy` 的元素，一旦断言函数 `predicate` 返回真值 `truthy`，遍历就停止。`predicate` 调用 3 个参数：`(value, index|key, collection)`。

### 参数
- `collection (Array|Object)`: 用来迭代的集合。
- `[predicate=_.identity] (Array|Function|Object|string)`: 每次迭代调用的函数。

### 返回
- `(boolean)`: 如果任意元素经 `predicate` 检查都为真值 `truthy` ，返回 `true` ，否则返回 `false` 。

### 例子

```js
_.some([null, 0, 'yes', false], Boolean);
// => true

var users = [
    { 'user': 'barney', 'active': true },
    { 'user': 'fred', 'active': false }
];

// The `_.matches` iteratee shorthand.
_.some(users, { 'user': 'barney', 'active': false });
// => false

// The `_.matchesProperty` iteratee shorthand.
_.some(users, ['active', false]);
// => true

// The `_.property` iteratee shorthand.
_.some(users, 'active');
// => true
```

### 参考
- [https://lodash.com/docs/4.17.15#some](https://lodash.com/docs/4.17.15#some)

## sortBy

```js
_.sortBy(collection, [iteratees=[_.identity]])
```

创建一个元素数组。以 `iteratee` 处理的结果升序排序。这个方法执行稳定排序，也就是说相同元素会保持原始排序。`iteratees` 调用 1 个参数：`(value)`。

### 参数
- `collection (Array|Object)`: 用来迭代的集合。
- `[iteratees=[_.identity]] (...(Array|Array[]|Function|Function[]|Object|Object[]|string|string[]))`: 这个函数决定排序。

### 返回
- `(Array)`: 返回排序后的数组。

### 例子

```js
var users = [
    { 'user': 'fred', 'age': 48 },
    { 'user': 'barney', 'age': 36 },
    { 'user': 'fred', 'age': 40 },
    { 'user': 'barney', 'age': 34 }
];

_.sortBy(users, function (o) { return o.user; });
// => objects for [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 40]]

_.sortBy(users, ['user', 'age']);
// => objects for [['barney', 34], ['barney', 36], ['fred', 40], ['fred', 48]]

_.sortBy(users, 'user', function (o) {
    return Math.floor(o.age / 10);
});
// => objects for [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 40]]
```

### 参考
- [https://lodash.com/docs/4.17.15#sortBy](https://lodash.com/docs/4.17.15#sortBy)


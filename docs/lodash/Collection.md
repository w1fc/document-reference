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


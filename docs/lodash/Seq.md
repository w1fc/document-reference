## _

```js
_(value)
```

创建一个 `lodash` 对象，包装 `value` 后的对象启用隐式方法链。返回的数组、集合、方法相互之间能够链式调用。检索唯一值或返回原始值会自动解除链条并返回计算后的值，否则需要调用 `_#value` 方法解除链。

显式链式调用，在任何情况下需要先用 `_#value` 解除链后，才能使用 `_.chain` 开启。

链式方法是惰性计算的，直到隐式或者显式调用了 `_#value` 才会执行计算。

惰性计算接受几种支持 *shortcut fusion* 的方法，*shortcut fusion* 是一种通过合并链式 `iteratee` 调用从而大大降低迭代的次数以提高执行性能的方式。部分链有资格 *shortcut fusion*，如果它至少有超过 200 个元素的数组和任何只接受一个参数的 `iteratees`。触发的方式是任何一个 *shortcut fusion* 有了变化。

链式方法支持定制版本，只要 `_#value` 包含或者间接包含在版本中。

除了 lodash 的自身方法，包装后的对象还支持 `Array` 和 `String` 的方法。

支持 `Array` 的方法: `concat`, `join`, `pop`, `push`, `shift`, `sort`, `splice`, `unshift` 。

支持 `String` 的方法: `replace` 和 `split` 。

支持 *shortcut fusion* 的方法: `at`, `compact`, `drop`, `dropRight`, `dropWhile`, `filter`, `find`, `findLast`, `head`, `initial`, `last`, `map`, `reject`, `reverse`, `slice`, `tail`, `take`, `takeRight`, `takeRightWhile`, `takeWhile`, 和 `toArray` 。

支持链式调用的方法: after, ary, assign, assignIn, assignInWith, assignWith, at, before, bind, bindAll, bindKey, castArray, chain, chunk, commit, compact, concat, conforms, constant, countBy, create, curry, debounce, defaults, defaultsDeep, defer, delay, difference, differenceBy, differenceWith, drop, dropRight, dropRightWhile, dropWhile, extend, extendWith, fill, filter, flatMap, flatMapDeep, flatMapDepth, flatten, flattenDeep, flattenDepth, flip, flow, flowRight, fromPairs, functions, functionsIn, groupBy, initial, intersection, intersectionBy, intersectionWith, invert, invertBy, invokeMap, iteratee, keyBy, keys, keysIn, map, mapKeys, mapValues, matches, matchesProperty, memoize, merge, mergeWith, method, methodOf, mixin, negate, nthArg, omit, omitBy, once, orderBy, over, overArgs, overEvery, overSome, partial, partialRight, partition, pick, pickBy, plant, property, propertyOf, pull, pullAll, pullAllBy, pullAllWith, pullAt, push, range, rangeRight, rearg, reject, remove, rest, reverse, sampleSize, set, setWith, shuffle, slice, sort, sortBy, splice, spread, tail, take, takeRight, takeRightWhile, takeWhile, tap, throttle, thru, toArray, toPairs, toPairsIn, toPath, toPlainObject, transform, unary, union, unionBy, unionWith, uniq, uniqBy, uniqWith, unset, unshift, unzip, unzipWith, update, updateWith, values, valuesIn, without, wrap, xor, xorBy, xorWith, zip, zipObject, zipObjectDeep, zipWith 。

默认不支持链式调用的方法: add, attempt, camelCase, capitalize, ceil, clamp, clone, cloneDeep, cloneDeepWith, cloneWith, conformsTo, deburr, defaultTo, divide, each, eachRight, endsWith, eq, escape, escapeRegExp, every, find, findIndex, findKey, findLast, findLastIndex, findLastKey, first, floor, forEach, forEachRight, forIn, forInRight, forOwn, forOwnRight, get, gt, gte, has, hasIn, head, identity, includes, indexOf, inRange, invoke, isArguments, isArray, isArrayBuffer, isArrayLike, isArrayLikeObject, isBoolean, isBuffer, isDate, isElement, isEmpty, isEqual, isEqualWith, isError, isFinite, isFunction, isInteger, isLength, isMap, isMatch, isMatchWith, isNaN, isNative, isNil, isNull, isNumber, isObject, isObjectLike, isPlainObject, isRegExp, isSafeInteger, isSet, isString, isUndefined, isTypedArray, isWeakMap, isWeakSet, join, kebabCase, last, lastIndexOf, lowerCase, lowerFirst, lt, lte, max, maxBy, mean, meanBy, min, minBy, multiply, noConflict, noop, now, nth, pad, padEnd, padStart, parseInt, pop, random, reduce, reduceRight, repeat, result, round, runInContext, sample, shift, size, snakeCase, some, sortedIndex, sortedIndexBy, sortedLastIndex, sortedLastIndexBy, startCase, startsWith, stubArray, stubFalse, stubObject, stubString, stubTrue, subtract, sum, sumBy, template, times, toFinite, toInteger, toJSON, toLength, toLower, toNumber, toSafeInteger, toString, toUpper, trim, trimEnd, trimStart, truncate, unescape, uniqueId, upperCase, upperFirst, value, words 。

### 参数
- `value (*)`: 需要被包装为 lodash 实例的值。

### 返回
- `(Object)`: 返回 lodash 包装后的实例。

### 例子

```js
function square(n) {
    return n * n;
}

var wrapped = _([1, 2, 3]);

// Returns an unwrapped value.
wrapped.reduce(_.add);
// => 6

// Returns a wrapped value.
var squares = wrapped.map(square);

_.isArray(squares);
// => false

_.isArray(squares.value());
// => true
```

### 参考
- [https://lodash.com/docs/4.17.15#lodash](https://lodash.com/docs/4.17.15#lodash)

## chain

```js
_.chain(value)
```

创建一个 lodash 包装实例，包装 `value` 以启用显式链模式。要解除链必须使用 `_#value` 方法。

### 参数
- `value (*)`: 要包装的值。

### 返回
- `(Object)`: 返回 lodash 包装的实例。

### 例子

```js
var users = [
    { 'user': 'barney', 'age': 36 },
    { 'user': 'fred', 'age': 40 },
    { 'user': 'pebbles', 'age': 1 }
];

var youngest = _
    .chain(users)
    .sortBy('age')
    .map(function (o) {
        return o.user + ' is ' + o.age;
    })
    .head()
    .value();
// => 'pebbles is 1'
```

### 参考
- [https://lodash.com/docs/4.17.15#chain](https://lodash.com/docs/4.17.15#chain)

## tap

```js
_.tap(value, interceptor)
```

这个方法调用一个 `interceptor` 并返回 `value`。`interceptor` 调用 1 个参数：`(value)`。该方法的目的是进入方法链序列以便修改中间结果。

### 参数
- `value (*)`: 提供给 `interceptor` 的值。
- `interceptor (Function)`: 用来调用的函数。

### 返回
- `(*)`: 返回 `value`。

### 例子

```js
_([1, 2, 3])
    .tap(function (array) {
        // Mutate input array.
        array.pop();
    })
    .reverse()
    .value();
// => [2, 1]
```

### 参考
- [https://lodash.com/docs/4.17.15#tap](https://lodash.com/docs/4.17.15#tap)

## thru

```js
_.thru(value, interceptor)
```

这个方法类似 `_.tap`，不同之处在于它返回 `interceptor` 的返回结果。该方法的目的是"传递"值到一个方法链序列以取代中间结果。

### 参数
- `value (*)`: 提供给 `interceptor` 的值。
- `interceptor (Function)`: 用来调用的函数。

### 返回
- `(*)`: 返回 `interceptor` 的返回结果。

### 例子

```js
_('  abc  ')
    .chain()
    .trim()
    .thru(function (value) {
        return [value];
    })
    .value();
// => ['abc']
```

### 参考
- [https://lodash.com/docs/4.17.15#thru](https://lodash.com/docs/4.17.15#thru)

## prototype[Symbol.iterator]

启用包装对象为 `iterable`。

### 返回
- `(Object)`: 返回包装对象。

### 例子

```js
var wrapped = _([1, 2]);

wrapped[Symbol.iterator]() === wrapped;
// => true

Array.from(wrapped);
// => [1, 2]
```

### 参考
- [https://lodash.com/docs/4.17.15#prototype-Symbol-iterator](https://lodash.com/docs/4.17.15#prototype-Symbol-iterator)

## prototype.at

这个方法是 `_.at` 的包装版本 。

### 参数
- `[paths] (...(string|string[]))`: 要选择元素的属性路径。

### 返回
- `(Object)`: 返回 lodash 的包装实例。

### 例子

```js
var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };

_(object).at(['a[0].b.c', 'a[1]']).value();
// => [3, 4]
```

### 参考
- [https://lodash.com/docs/4.17.15#prototype-at](https://lodash.com/docs/4.17.15#prototype-at)

## prototype.chain

创建一个 lodash 包装实例，启用显式链模式。

### 返回
- `(Object)`: 返回 lodash 的包装实例。

### 例子

```js
var users = [
    { 'user': 'barney', 'age': 36 },
    { 'user': 'fred', 'age': 40 }
];

// A sequence without explicit chaining.
_(users).head();
// => { 'user': 'barney', 'age': 36 }

// A sequence with explicit chaining.
_(users)
    .chain()
    .head()
    .pick('user')
    .value();
// => { 'user': 'barney' }
```

### 参考
- [https://lodash.com/docs/4.17.15#prototype-chain](https://lodash.com/docs/4.17.15#prototype-chain)

## prototype.commit

执行链式队列并返回结果。

### 返回
- `(Object)`: 返回 lodash 的包装实例。

### 例子

```js
var array = [1, 2];
var wrapped = _(array).push(3);

console.log(array);
// => [1, 2]

wrapped = wrapped.commit();
console.log(array);
// => [1, 2, 3]

wrapped.last();
// => 3

console.log(array);
// => [1, 2, 3]
```

### 参考
- [https://lodash.com/docs/4.17.15#prototype-commit](https://lodash.com/docs/4.17.15#prototype-commit)

## prototype.next

获得包装对象的下一个值，遵循 [iterator protocol](https://mdn.io/iteration_protocols#iterator) 。

### 返回
- `(Object)`: 返回下一个 `iterator` 值。

### 例子

```js
var wrapped = _([1, 2]);

wrapped.next();
// => { 'done': false, 'value': 1 }

wrapped.next();
// => { 'done': false, 'value': 2 }

wrapped.next();
// => { 'done': true, 'value': undefined }
```

### 参考
- [https://lodash.com/docs/4.17.15#prototype-next](https://lodash.com/docs/4.17.15#prototype-next)

## prototype.plant

创建一个链式队列的拷贝，传入的 `value` 作为链式队列的值。

### 参数
- `value (*)`: 替换原值的值。

### 返回
- `(Object)`: 返回 lodash 的包装实例。

### 例子

```js
function square(n) {
    return n * n;
}

var wrapped = _([1, 2]).map(square);
var other = wrapped.plant([3, 4]);

other.value();
// => [9, 16]

wrapped.value();
// => [1, 4]
```

### 参考
- [https://lodash.com/docs/4.17.15#prototype-plant](https://lodash.com/docs/4.17.15#prototype-plant)

## prototype.reverse

这个方法是 `_.reverse` 的包装版本。

注意: 这种方法会改变包装数组。

### 返回
- `(Object)`: 返回新的 lodash 包装实例。

### 例子

```js
var array = [1, 2, 3];

_(array).reverse().value()
// => [3, 2, 1]

console.log(array);
// => [3, 2, 1]
```

### 参考
- [https://lodash.com/docs/4.17.15#prototype-reverse](https://lodash.com/docs/4.17.15#prototype-reverse)

## prototype.value / prototype.toJSON / prototype.valueOf

执行链式队列并提取解链后的值。

### 返回
- `(*)`: 返回解链后的值。

### 例子

```js
_([1, 2, 3]).value();
// => [1, 2, 3]
```

### 参考
- [https://lodash.com/docs/4.17.15#prototype-value](https://lodash.com/docs/4.17.15#prototype-value)

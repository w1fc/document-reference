## attempt

```js
_.attempt(func, [args])
```

尝试调用 `func`，返回结果或者捕捉错误对象。任何附加的参数都会在调用时传给 `func`。

### 参数
- `func (Function)`: 要尝试调用的函数。
- `[args] (...*)`: 调用 `func` 时，传递的参数。

### 返回
- `(*)`: 返回 `func` 结果或者错误对象。

### 例子

```js
// Avoid throwing errors for invalid selectors.
var elements = _.attempt(function (selector) {
    return document.querySelectorAll(selector);
}, '>_>');

if (_.isError(elements)) {
    elements = [];
}
```

### 参考
- [https://lodash.com/docs/4.17.15#attempt](https://lodash.com/docs/4.17.15#attempt)

## bindAll

```js
_.bindAll(object, methodNames)
```

绑定一个对象的方法到对象本身，覆盖现有的方法。

注意: 这个方法不会设置绑定函数的 `"length"` 属性。

### 参数
- `object (Object)`: 用来绑定和分配绑定方法的对象。
- `methodNames (...(string|string[]))`: 对象绑定方法的名称。

### 返回
- `(Object)`: 返回 `object`。

### 例子

```js
var view = {
    'label': 'docs',
    'click': function () {
        console.log('clicked ' + this.label);
    }
};

_.bindAll(view, ['click']);
jQuery(element).on('click', view.click);
// => Logs 'clicked docs' when clicked.
```

### 参考
- [https://lodash.com/docs/4.17.15#bindAll](https://lodash.com/docs/4.17.15#bindAll)

## cond

```js
_.cond(pairs)
```

创建一个函数，这个函数会迭代 `pairs`，并调用最先返回真值对应的函数。该断言函数对绑定 `this` 及传入创建函数的参数。

### 参数
- `pairs (Array)`: 断言函数对。

### 返回
- `(Function)`: 返回新的复合函数。

### 例子

```js
var func = _.cond([
    [_.matches({ 'a': 1 }), _.constant('matches A')],
    [_.conforms({ 'b': _.isNumber }), _.constant('matches B')],
    [_.stubTrue, _.constant('no match')]
]);

func({ 'a': 1, 'b': 2 });
// => 'matches A'

func({ 'a': 0, 'b': 1 });
// => 'matches B'

func({ 'a': '1', 'b': '2' });
// => 'no match'
```

### 参考
- [https://lodash.com/docs/4.17.15#cond](https://lodash.com/docs/4.17.15#cond)

## conforms

```js
_.conforms(source)
```

创建一个函数。这个函数会调用 `source` 的属性名对应的 `predicate` 与传入对象相对应属性名的值进行断言处理。如果都符合返回 `true` ，否则返回 `false` 。

注意: 当 `source` 为偏应用时，这种方法等价于 `_.conformsTo` 。

### 参数
- `source (Object)`: 包含断言属性值的对象。

### 返回
- `(Function)`: 返回新的函数。

### 例子

```js
var objects = [
    { 'a': 2, 'b': 1 },
    { 'a': 1, 'b': 2 }
];

_.filter(objects, _.conforms({ 'b': function (n) { return n > 1; } }));
// => [{ 'a': 1, 'b': 2 }]
```

### 参考
- [https://lodash.com/docs/4.17.15#conforms](https://lodash.com/docs/4.17.15#conforms)

## constant

```js
_.constant(value)
```

创建一个返回 `value` 的函数。

### 参数
- `value (*)`: 要新函数返回的值。

### 返回
- `(Function)`: 返回新的常量函数。

### 例子

```js
var objects = _.times(2, _.constant({ 'a': 1 }));

console.log(objects);
// => [{ 'a': 1 }, { 'a': 1 }]

console.log(objects[0] === objects[1]);
// => true
```

### 参考
- [https://lodash.com/docs/4.17.15#constant](https://lodash.com/docs/4.17.15#constant)

## defaultTo

```js
_.defaultTo(value, defaultValue)
```

检查 `value`，以确定一个默认值是否应被返回。如果 `value` 为 `NaN`, `null`, `undefined`，那么返回 `defaultValue` 默认值。

### 参数
- `value (*)`: 要检查的值。
- `defaultValue (*)`: 默认值。

### 返回
- `(*)`: 返回 `resolved` 值。

### 例子

```js
_.defaultTo(1, 10);
// => 1

_.defaultTo(undefined, 10);
// => 10
```

### 参考
- [https://lodash.com/docs/4.17.15#defaultTo](https://lodash.com/docs/4.17.15#defaultTo)

## flow

```js
_.flow([funcs])
```

创建一个函数。 返回的结果是调用提供函数的结果，`this` 会绑定到创建函数。每一个连续调用，传入的参数都是前一个函数返回的结果。

### 参数
- `[funcs] (...(Function|Function[]))`: 要调用的函数。

### 返回
- `(Function)`: 返回新的函数。

### 例子

```js
function square(n) {
    return n * n;
}

var addSquare = _.flow([_.add, square]);
addSquare(1, 2);
// => 9
```

### 参考
- [https://lodash.com/docs/4.17.15#flow](https://lodash.com/docs/4.17.15#flow)

## flowRight

```js
_.flowRight([funcs])
```

这个方法类似 `_.flow`，除了它调用函数的顺序是从右往左的。

### 参数
- `[funcs] (...(Function|Function[]))`: 要调用的函数。

### 返回
- `(Function)`: 返回新的函数。

### 例子

```js
function square(n) {
    return n * n;
}

var addSquare = _.flowRight([square, _.add]);
addSquare(1, 2);
// => 9
```

### 参考
- [https://lodash.com/docs/4.17.15#flowRight](https://lodash.com/docs/4.17.15#flowRight)

## identity

```js
_.identity(value)
```

这个方法返回首个提供的参数。

### 参数
- `value (*)`: 任何值。

### 返回
- `(*)`: 返回 `value`。

### 例子

```js
var object = { 'a': 1 };

console.log(_.identity(object) === object);
// => true
```

### 参考
- [https://lodash.com/docs/4.17.15#identity](https://lodash.com/docs/4.17.15#identity)

## iteratee

```js
_.iteratee([func=_.identity])
```

创建一个函数，通过创建函数的参数调用 `func` 函数。如果 `func` 是一个属性名，传入包含这个属性名的对象，回调返回对应属性名的值。如果 `func` 是一个对象，传入的元素有相同的对象属性，回调返回 `true` 。 其他情况返回 `false` 。

### 参数
- `[func=_.identity] (*)`: 转换成 `callback` 的值。

### 返回
- `(Function)`: 返回回调函数 `callback`。

### 例子

```js
var users = [
    { 'user': 'barney', 'age': 36, 'active': true },
    { 'user': 'fred', 'age': 40, 'active': false }
];

// The `_.matches` iteratee shorthand.
_.filter(users, _.iteratee({ 'user': 'barney', 'active': true }));
// => [{ 'user': 'barney', 'age': 36, 'active': true }]

// The `_.matchesProperty` iteratee shorthand.
_.filter(users, _.iteratee(['user', 'fred']));
// => [{ 'user': 'fred', 'age': 40 }]

// The `_.property` iteratee shorthand.
_.map(users, _.iteratee('user'));
// => ['barney', 'fred']

// Create custom iteratee shorthands.
_.iteratee = _.wrap(_.iteratee, function (iteratee, func) {
    return !_.isRegExp(func) ? iteratee(func) : function (string) {
        return func.test(string);
    };
});

_.filter(['abc', 'def'], /ef/);
// => ['def']
```

### 参考
- [https://lodash.com/docs/4.17.15#iteratee](https://lodash.com/docs/4.17.15#iteratee)

## matches

```js
_.matches(source)
```

创建一个深比较的方法来比较给定的对象和 `source` 对象。如果给定的对象拥有相同的属性值返回 `true`，否则返回 `false`。

注意: 创建的函数相当于 `_.isMatch` 应用 `source` 。

部分比较匹配空数组和空对象源值，分别针对任何数组或对象的值。见 `_.isEqual` 支持的价值比较的列表。

### 参数
- `source (Object)`: 要匹配属性值的源对象。

### 返回
- `(Function)`: 返回新的函数。

### 例子

```js
var objects = [
    { 'a': 1, 'b': 2, 'c': 3 },
    { 'a': 4, 'b': 5, 'c': 6 }
];

_.filter(objects, _.matches({ 'a': 4, 'c': 6 }));
// => [{ 'a': 4, 'b': 5, 'c': 6 }]
```

### 参考
- [https://lodash.com/docs/4.17.15#matches](https://lodash.com/docs/4.17.15#matches)

## matchesProperty

```js
_.matchesProperty(path, srcValue)
```

创建一个深比较的方法来比较给定对象的 `path` 的值是否是 `srcValue` 。如果是返回 `true` ，否则返回 `false` 。

注意: 这个方法支持以 `_.isEqual` 的方式比较相同的值。

### 参数
- `path (Array|string)`: 给定对象的属性路径名。
- `srcValue (*)`: 要匹配的值。

### 返回
- `(Function)`: 返回新的函数。

### 例子

```js
var objects = [
    { 'a': 1, 'b': 2, 'c': 3 },
    { 'a': 4, 'b': 5, 'c': 6 }
];

_.find(objects, _.matchesProperty('a', 4));
// => { 'a': 4, 'b': 5, 'c': 6 }
```

### 参考
- [https://lodash.com/docs/4.17.15#matchesProperty](https://lodash.com/docs/4.17.15#matchesProperty)

## method

```js
_.method(path, [args])
```

创建一个调用给定对象 `path` 上的函数。任何附加的参数都会传入这个调用函数中。

### 参数
- `path (Array|string)`: 调用函数所在对象的路径。
- `[args] (...*)`: 传递给调用函数的参数。

### 返回
- `(Function)`: 返回新的调用函数。

### 例子

```js
var objects = [
    { 'a': { 'b': _.constant(2) } },
    { 'a': { 'b': _.constant(1) } }
];

_.map(objects, _.method('a.b'));
// => [2, 1]

_.map(objects, _.method(['a', 'b']));
// => [2, 1]
```

### 参考
- [https://lodash.com/docs/4.17.15#method](https://lodash.com/docs/4.17.15#method)

## methodOf

```js
_.methodOf(object, [args])
```

`_.method` 的反向版。这个创建一个函数调用给定 `object` 的 `path` 上的方法，任何附加的参数都会传入这个调用函数中。

### 参数
- `object (Object)`: 要检索的对象。
- `[args] (...*)`: 传递给调用函数的参数。

### 返回
- `(Function)`: 返回新的调用函数。

### 例子

```js
var array = _.times(3, _.constant),
    object = { 'a': array, 'b': array, 'c': array };

_.map(['a[2]', 'c[0]'], _.methodOf(object));
// => [2, 0]

_.map([['a', '2'], ['c', '0']], _.methodOf(object));
// => [2, 0]
```

### 参考
- [https://lodash.com/docs/4.17.15#methodOf](https://lodash.com/docs/4.17.15#methodOf)

## mixin

```js
_.mixin([object=lodash], source, [options={}])
```

添加来源对象自身的所有可枚举函数属性到目标对象。如果 `object` 是个函数，那么函数方法将被添加到原型链上。

注意: 使用 `_.runInContext` 来创建原始的 lodash 函数来避免修改造成的冲突。

### 参数
- `[object=lodash] (Function|Object)`: 目标对象。
- `source (Object)`: 来源对象。
- `[options={}] (Object)`: 选项对象。
- `[options.chain=true] (boolean)`: 是否开启链式操作。

### 返回
- `(*)`: 返回 `object`。

### 例子

```js
function vowels(string) {
    return _.filter(string, function (v) {
        return /[aeiou]/i.test(v);
    });
}

_.mixin({ 'vowels': vowels });
_.vowels('fred');
// => ['e']

_('fred').vowels().value();
// => ['e']

_.mixin({ 'vowels': vowels }, { 'chain': false });
_('fred').vowels();
// => ['e']
```

### 参考
- [https://lodash.com/docs/4.17.15#mixin](https://lodash.com/docs/4.17.15#mixin)

## noConflict

```js
_.runInContext([context=root])
```

创建一个给定 `context` 上下文对象的原始的 lodash 函数。

### 参数
- `[context=root] (Object)`: 上下文对象。

### 返回
- `(Function)`: 返回新的 lodash 对象

### 例子

```js
var lodash = _.noConflict();
```

### 参考
- [https://lodash.com/docs/4.17.15#noConflict](https://lodash.com/docs/4.17.15#noConflict)

## noop

```js
_.noop()
```

这个方法返回 `undefined`。

### 例子

```js
_.times(2, _.noop);
// => [undefined, undefined]
```

### 参考
- [https://lodash.com/docs/4.17.15#noop](https://lodash.com/docs/4.17.15#noop)

## nthArg

```js
_.nthArg([n=0])
```

创建一个函数，这个函数返回第 `n` 个参数。如果 `n` 为负数，则返回从结尾开始的第 `n` 个参数。

### 参数
- `[n=0] (number)`: 要返回参数的索引值。

### 返回
- `(Function)`: 返回新的函数。

### 例子

```js
var func = _.nthArg(1);
func('a', 'b', 'c', 'd');
// => 'b'

var func = _.nthArg(-2);
func('a', 'b', 'c', 'd');
// => 'c'
```

### 参考
- [https://lodash.com/docs/4.17.15#nthArg](https://lodash.com/docs/4.17.15#nthArg)

## over

```js
_.over([iteratees=[_.identity]])
```

创建一个函数，传入提供的参数的函数并调用 `iteratees` 返回结果。

### 参数
- `[iteratees=[_.identity]] (...(Function|Function[]))`: 要调用的 `iteratees`。

### 返回
- `(Function)`: 返回新的函数。

### 例子

```js
var func = _.over([Math.max, Math.min]);

func(1, 2, 3, 4);
// => [4, 1]
```

### 参考
- [https://lodash.com/docs/4.17.15#over](https://lodash.com/docs/4.17.15#over)

## overEvery

```js
_.overEvery([predicates=[_.identity]])
```

建一个函数，传入提供的参数的函数并调用 `predicates` 判断是否全部都为真值。

### 参数
- `[predicates=[_.identity]] (...(Function|Function[]))`: 要调用的 `predicates`。

### 返回
- `(Function)`: 返回新的函数。

### 例子

```js
var func = _.overEvery([Boolean, isFinite]);

func('1');
// => true

func(null);
// => false

func(NaN);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#overEvery](https://lodash.com/docs/4.17.15#overEvery)

## overSome

```js
_.overSome([predicates=[_.identity]])
```

创建一个函数，传入提供的参数的函数并调用 `predicates` 判断是否存在有真值。

### 参数
- `[predicates=[_.identity]] (...(Function|Function[]))`: 要调用的 `predicates`。

### 返回
- `(Function)`: 返回新的函数。

### 例子

```js
var func = _.overSome([Boolean, isFinite]);

func('1');
// => true

func(null);
// => true

func(NaN);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#overSome](https://lodash.com/docs/4.17.15#overSome)

## property

```js
_.property(path)
```

创建一个返回给定对象的 `path` 的值的函数。

### 参数
- `path (Array|string)`: 要得到值的属性路径。

### 返回
- `(Function)`: 返回新的函数。

### 例子

```js
var objects = [
    { 'a': { 'b': 2 } },
    { 'a': { 'b': 1 } }
];

_.map(objects, _.property('a.b'));
// => [2, 1]

_.map(_.sortBy(objects, _.property(['a', 'b'])), 'a.b');
// => [1, 2]
```

### 参考
- [https://lodash.com/docs/4.17.15#property](https://lodash.com/docs/4.17.15#property)

## propertyOf

```js
_.propertyOf(object)
```

`_.property` 的反相版本。这个方法创建的函数返回给定 `path` 在 `object` 上的值。

### 参数
- `object (Object)`: 要检索的对象。

### 返回
- `(Function)`: 返回新的函数。

### 例子

```js
var array = [0, 1, 2],
    object = { 'a': array, 'b': array, 'c': array };

_.map(['a[2]', 'c[0]'], _.propertyOf(object));
// => [2, 0]

_.map([['a', '2'], ['c', '0']], _.propertyOf(object));
// => [2, 0]
```

### 参考
- [https://lodash.com/docs/4.17.15#propertyOf](https://lodash.com/docs/4.17.15#propertyOf)

## range

```js
_.range([start=0], end, [step=1])
```

创建一个包含从 `start` 到 `end`，但不包含 `end` 本身范围数字的数组。如果 `start` 是负数，而 `end` 或 `step` 没有指定，那么 `step` 从 `-1` 为开始。如果 `end` 没有指定，`start` 设置为 `0`。如果 `end` 小于 `start` ，会创建一个空数组，除非指定了 `step`。

注意： JavaScript 遵循 IEEE-754 标准处理无法预料的浮点数结果。

### 参数
- `[start=0] (number)`: 开始的范围。
- `end (number)`: 结束的范围。
- `[step=1] (number)`: 范围的增量或者减量。

### 返回
- `(Array)`: 返回范围内数字组成的新数组。

### 例子

```js
_.range(4);
// => [0, 1, 2, 3]

_.range(-4);
// => [0, -1, -2, -3]

_.range(1, 5);
// => [1, 2, 3, 4]

_.range(0, 20, 5);
// => [0, 5, 10, 15]

_.range(0, -4, -1);
// => [0, -1, -2, -3]

_.range(1, 4, 0);
// => [1, 1, 1]

_.range(0);
// => []
```

### 参考
- [https://lodash.com/docs/4.17.15#range](https://lodash.com/docs/4.17.15#range)

## rangeRight

```js
_.rangeRight([start=0], end, [step=1])
```

这个方法类似 `_.range` ，不同之处在于它是降序生成值的。

### 参数
- `[start=0] (number)`: 开始的范围。
- `end (number)`: 结束的范围。
- `[step=1] (number)`: 范围的增量或者减量。

### 返回
- `(Array)`: 返回范围内数字组成的新数组。

### 例子

```js
_.rangeRight(4);
// => [3, 2, 1, 0]

_.rangeRight(-4);
// => [-3, -2, -1, 0]

_.rangeRight(1, 5);
// => [4, 3, 2, 1]

_.rangeRight(0, 20, 5);
// => [15, 10, 5, 0]

_.rangeRight(0, -4, -1);
// => [-3, -2, -1, 0]

_.rangeRight(1, 4, 0);
// => [1, 1, 1]

_.rangeRight(0);
// => []
```

### 参考
- [https://lodash.com/docs/4.17.15#rangeRight](https://lodash.com/docs/4.17.15#rangeRight)

## runInContext

```js
_.runInContext([context=root])
```

创建一个给定 `context` 上下文对象的原始的 lodash 函数。

### 参数
- `[context=root] (Object)`: 上下文对象。

### 返回
- `(Function)`: 返回新的 lodash 对象

### 例子

```js
_.mixin({ 'foo': _.constant('foo') });

var lodash = _.runInContext();
lodash.mixin({ 'bar': lodash.constant('bar') });

_.isFunction(_.foo);
// => true
_.isFunction(_.bar);
// => false

lodash.isFunction(lodash.foo);
// => false
lodash.isFunction(lodash.bar);
// => true

// Create a suped-up `defer` in Node.js.
var defer = _.runInContext({ 'setTimeout': setImmediate }).defer;
```

### 参考
- [https://lodash.com/docs/4.17.15#runInContext](https://lodash.com/docs/4.17.15#runInContext)

## stubArray

```js
_.stubArray()
```

这个方法返回一个新的空数组。

### 返回
- `(Array)`: 返回新的空数组。

### 例子

```js
var arrays = _.times(2, _.stubArray);

console.log(arrays);
// => [[], []]

console.log(arrays[0] === arrays[1]);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#stubArray](https://lodash.com/docs/4.17.15#stubArray)

## stubFalse

```js
_.stubFalse()
```

这个方法返回 `false`。

### 返回
- `(boolean)`: 返回 `false`。

### 例子

```js
_.times(2, _.stubFalse);
// => [false, false]
```

### 参考
- [https://lodash.com/docs/4.17.15#stubFalse](https://lodash.com/docs/4.17.15#stubFalse)

## stubObject

```js
_.stubObject()
```

这个方法返回一个空对象。

### 返回
- `(Object)`: 返回新的空对象。

### 例子

```js
var objects = _.times(2, _.stubObject);

console.log(objects);
// => [{}, {}]

console.log(objects[0] === objects[1]);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#stubObject](https://lodash.com/docs/4.17.15#stubObject)

## stubString

```js
_.stubString()
```

这个方法返回一个空字符串。

### 返回
- `(string)`: 返回新的空字符串。

### 例子

```js
_.times(2, _.stubString);
// => ['', '']
```

### 参考
- [https://lodash.com/docs/4.17.15#stubString](https://lodash.com/docs/4.17.15#stubString)

## stubTrue

```js
_.stubTrue()
```

这个方法返回 `true`。

### 返回
- `(boolean)`: 返回 `true`。

### 例子

```js
_.times(2, _.stubTrue);
// => [true, true]
```

### 参考
- [https://lodash.com/docs/4.17.15#stubTrue](https://lodash.com/docs/4.17.15#stubTrue)

## times

```js
_.times(n, [iteratee=_.identity])
```

调用 `n` 次 `iteratee` ，每次调用返回的结果存入到数组中。`iteratee` 调用 1 个参数：`(index)`。

### 参数
- `n (number)`: 调用 `iteratee` 的次数。
- `[iteratee=_.identity] (Function)`: 每次迭代调用的函数。

### 返回
- `(Array)`: 返回调用结果的数组。

### 例子

```js
_.times(3, String);
// => ['0', '1', '2']

_.times(4, _.constant(0));
// => [0, 0, 0, 0]
```

### 参考
- [https://lodash.com/docs/4.17.15#times](https://lodash.com/docs/4.17.15#times)

## toPath

```js
_.toPath(value)
```

转化 `value` 为属性路径的数组。

### 参数
- `value (*)`: 要转换的值。

### 返回
- `(Array)`: 返回包含属性路径的数组。

### 例子

```js
_.toPath('a.b.c');
// => ['a', 'b', 'c']

_.toPath('a[0].b.c');
// => ['a', '0', 'b', 'c']
```

### 参考
- [https://lodash.com/docs/4.17.15#toPath](https://lodash.com/docs/4.17.15#toPath)

## uniqueId

```js
_.uniqueId([prefix=''])
```

生成唯一 ID。如果提供了 `prefix`，会被添加到 ID 前缀上。

### 参数
- `[prefix=''] (string)`: 要添加到ID前缀的值。

### 返回
- `(string)`: 返回唯一 ID。

### 例子

```js
_.uniqueId('contact_');
// => 'contact_104'

_.uniqueId();
// => '105'
```

### 参考
- [https://lodash.com/docs/4.17.15#uniqueId](https://lodash.com/docs/4.17.15#uniqueId)

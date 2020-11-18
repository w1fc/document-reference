## assign

```js
_.assign(object, [sources])
```

分配来源对象的可枚举属性到目标对象上。 来源对象的应用规则是从左到右，随后的下一个对象的属性会覆盖上一个对象的属性。

注意: 这方法会改变 `object`，参考自 [Object.assign](https://mdn.io/Object/assign)。

### 参数
- `object (Object)`: 目标对象。
- `[sources] (...Object)`: 来源对象。

### 返回
- `(Object)`: 返回 `object`。

### 例子

```js
function Foo() {
    this.a = 1;
}

function Bar() {
    this.c = 3;
}

Foo.prototype.b = 2;
Bar.prototype.d = 4;

_.assign({ 'a': 0 }, new Foo, new Bar);
// => { 'a': 1, 'c': 3 }
```

### 参考
- [https://lodash.com/docs/4.17.15#assign](https://lodash.com/docs/4.17.15#assign)

## assignIn / extend

```js
_.assignIn(object, [sources])
```

这个方法类似 `_.assign`，不同之处在于它会遍历并继承来源对象的属性。

注意：这方法会改变 `object`。

### 参数
- `object (Object)`: 目标对象。
- `[sources] (...Object)`: 来源对象。

### 返回
- `(Object)`: 返回 `object`。

### 例子

```js
function Foo() {
    this.a = 1;
}

function Bar() {
    this.c = 3;
}

Foo.prototype.b = 2;
Bar.prototype.d = 4;

_.assignIn({ 'a': 0 }, new Foo, new Bar);
// => { 'a': 1, 'b': 2, 'c': 3, 'd': 4 }
```

### 参考
- [https://lodash.com/docs/4.17.15#assignIn](https://lodash.com/docs/4.17.15#assignIn)

## assignInWith / extendWith

```js
_.assignInWith(object, sources, [customizer])
```

这个方法类似 `_.assignIn`，不同之处在于它接受一个 `customizer` ，被调用以产生所分配的值。如果 `customizer` 返回 `undefined` 将会由分配处理方法代替。`customizer` 会传入 5 个参数：`(objValue, srcValue, key, object, source)`。

注意：这方法会改变 `object`。

### 参数
- `object (Object)`: 目标对象。
- `sources (...Object)`: 来源对象。
- `[customizer] (Function)`: 这个函数用来自定义分配的值。

### 返回
- `(Object)`: 返回 `object`。

### 例子

```js
function customizer(objValue, srcValue) {
    return _.isUndefined(objValue) ? srcValue : objValue;
}

var defaults = _.partialRight(_.assignInWith, customizer);

defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

### 参考
- [https://lodash.com/docs/4.17.15#assignInWith](https://lodash.com/docs/4.17.15#assignInWith)

## assignWith

```js
_.assignWith(object, sources, [customizer])
```

这个方法类似 `_.assign` ，不同之处在于它接受一个 `customizer` 决定如何分配值。如果 `customizer` 返回 `undefined` 将会由分配处理方法代替。`customizer` 会传入 5 个参数：`(objValue, srcValue, key, object, source)`。

注意：这方法会改变 `object`。

### 参数
- `object (Object)`: 目标对象。
- `sources (...Object)`: 来源对象。
- `[customizer] (Function)`: 这个函数用来自定义分配的值。

### 返回
- `(Object)`: 返回 `object`。

### 例子

```js
function customizer(objValue, srcValue) {
    return _.isUndefined(objValue) ? srcValue : objValue;
}

var defaults = _.partialRight(_.assignWith, customizer);

defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

### 参考
- [https://lodash.com/docs/4.17.15#assignWith](https://lodash.com/docs/4.17.15#assignWith)

## at

```js
_.at(object, [paths])
```

创建一个数组，值来自 `object` 的 `paths` 路径相应的值。


### 参数
- `object (Object)`: 要迭代的对象。
- [paths] (...(string|string[]))`: 要获取的对象的元素路径，单独指定或者指定在数组中。

### 返回
- `(Array)`: 返回选中值的数组。

### 例子

```js
var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };

_.at(object, ['a[0].b.c', 'a[1]']);
// => [3, 4]
```

### 参考
- [https://lodash.com/docs/4.17.15#at](https://lodash.com/docs/4.17.15#at)

## create

```js
_.create(prototype, [properties])
```

创建一个继承 `prototype` 的对象。如果提供了 `prototype`，它的可枚举属性会被分配到创建的对象上。

### 参数
- `prototype (Object)`: 要继承的对象。
- `[properties] (Object)`: 待分配的属性。

### 返回
- `(Object)`: 返回新对象。

### 例子

```js
function Shape() {
    this.x = 0;
    this.y = 0;
}

function Circle() {
    Shape.call(this);
}

Circle.prototype = _.create(Shape.prototype, {
    'constructor': Circle
});

var circle = new Circle;
circle instanceof Circle;
// => true

circle instanceof Shape;
// => true
```

### 参考
- [https://lodash.com/docs/4.17.15#create](https://lodash.com/docs/4.17.15#create)

## defaults

```js
_.defaults(object, [sources])
```

分配来源对象的可枚举属性到目标对象所有解析为 `undefined` 的属性上。来源对象从左到右应用。一旦设置了相同属性的值，后续的将被忽略掉。

注意: 这方法会改变 `object`。

### 参数
- `object (Object)`: 目标对象。
- `[sources] (...Object)`: 来源对象。

### 返回
- `(Object)`: 返回 `object`。

### 例子

```js
_.defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

### 参考
- [https://lodash.com/docs/4.17.15#defaults](https://lodash.com/docs/4.17.15#defaults)

## defaultsDeep

```js
_.defaultsDeep(object, [sources])
```

这个方法类似 `_.defaults`，不同之处在于它会递归分配默认属性。

注意: 这方法会改变 `object`。

### 参数
- `object (Object)`: 目标对象。
- `[sources] (...Object)`: 来源对象。

### 返回
- `(Object)`: 返回 `object`。

### 例子

```js
_.defaultsDeep({ 'a': { 'b': 2 } }, { 'a': { 'b': 1, 'c': 3 } });
// => { 'a': { 'b': 2, 'c': 3 } }
```

### 参考
- [https://lodash.com/docs/4.17.15#defaultsDeep](https://lodash.com/docs/4.17.15#defaultsDeep)

## entries / toPairs

```js
_.toPairs(object)
```

创建一个 `object` 对象自身可枚举属性的键值对数组。这个数组可以通过 `_.fromPairs` 撤回。如果 `object` 是 `map` 或 `set`，返回其条目。

### 参数
- `object (Object)`: 要检索的对象。

### 返回
- `(Array)`: 返回键值对的数组。

### 例子

```js
function Foo() {
    this.a = 1;
    this.b = 2;
}

Foo.prototype.c = 3;

_.toPairs(new Foo);
// => [['a', 1], ['b', 2]] (iteration order is not guaranteed)
```

### 参考
- [https://lodash.com/docs/4.17.15#toPairs](https://lodash.com/docs/4.17.15#toPairs)

## entriesIn / toPairsIn

```js
_.toPairsIn(object)
```

创建一个 `object` 对象自身和继承的可枚举属性的键值对数组。这个数组可以通过 `_.fromPairs` 撤回。如果 `object` 是 `map` 或 `set`，返回其条目。

### 参数
- `object (Object)`: 要检索的对象。

### 返回
- `(Array)`: 返回键值对的数组。

### 例子

```js
function Foo() {
    this.a = 1;
    this.b = 2;
}

Foo.prototype.c = 3;

_.toPairsIn(new Foo);
// => [['a', 1], ['b', 2], ['c', 3]] (iteration order is not guaranteed)
```

### 参考
- [https://lodash.com/docs/4.17.15#toPairs](https://lodash.com/docs/4.17.15#toPairs)

## findKey

```js
_.findKey(object, [predicate=_.identity])
```

这个方法类似 `_.find` 。不同之处在于它返回最先被 `predicate` 判断为真值的元素 `key`，而不是元素本身。

### 参数
- `object (Object)`: 需要检索的对象。
- `[predicate=_.identity] (Function)`: 每次迭代时调用的函数。

### 返回
- `(*)`: 返回匹配的 `key`，否则返回 `undefined`。

### 例子

```js
var users = {
    'barney': { 'age': 36, 'active': true },
    'fred': { 'age': 40, 'active': false },
    'pebbles': { 'age': 1, 'active': true }
};

_.findKey(users, function (o) { return o.age < 40; });
// => 'barney' (iteration order is not guaranteed)

// The `_.matches` iteratee shorthand.
_.findKey(users, { 'age': 1, 'active': true });
// => 'pebbles'

// The `_.matchesProperty` iteratee shorthand.
_.findKey(users, ['active', false]);
// => 'fred'

// The `_.property` iteratee shorthand.
_.findKey(users, 'active');
// => 'barney'
```

### 参考
- [https://lodash.com/docs/4.17.15#findKey](https://lodash.com/docs/4.17.15#findKey)

## findLastKey

```js
_.findLastKey(object, [predicate=_.identity])
```

这个方法类似 `_.findKey` 。不过它是反方向开始遍历的。

### 参数
- `object (Object)`: 需要检索的对象。
- `[predicate=_.identity] (Function)`: 每次迭代时调用的函数。

### 返回
- `(*)`: 返回匹配的 `key`，否则返回 `undefined`。

### 例子

```js
var users = {
    'barney': { 'age': 36, 'active': true },
    'fred': { 'age': 40, 'active': false },
    'pebbles': { 'age': 1, 'active': true }
};

_.findLastKey(users, function (o) { return o.age < 40; });
// => returns 'pebbles' assuming `_.findKey` returns 'barney'

// The `_.matches` iteratee shorthand.
_.findLastKey(users, { 'age': 36, 'active': true });
// => 'barney'

// The `_.matchesProperty` iteratee shorthand.
_.findLastKey(users, ['active', false]);
// => 'fred'

// The `_.property` iteratee shorthand.
_.findLastKey(users, 'active');
// => 'pebbles'
```

### 参考
- [https://lodash.com/docs/4.17.15#findLastKey](https://lodash.com/docs/4.17.15#findLastKey)

## forIn

```js
_.forIn(object, [iteratee=_.identity])
```

使用 `iteratee` 遍历对象的自身和继承的可枚举属性。`iteratee` 会传入 3 个参数：`(value, key, object)`。如果返回 `false`，`iteratee` 会提前退出遍历。

### 参数
- `object (Object)`: 要遍历的对象。
- `[iteratee=_.identity] (Function)`: 每次迭代时调用的函数。

### 返回
- `(Object)`: 返回 `object`。

### 例子

```js
function Foo() {
    this.a = 1;
    this.b = 2;
}

Foo.prototype.c = 3;

_.forIn(new Foo, function (value, key) {
    console.log(key);
});
// => Logs 'a', 'b', then 'c' (iteration order is not guaranteed).
```

### 参考
- [https://lodash.com/docs/4.17.15#forIn](https://lodash.com/docs/4.17.15#forIn)

## forInRight

```js
_.forInRight(object, [iteratee=_.identity])
```

这个方法类似 `_.forIn`。不同之处在于它是反方向开始遍历 `object` 的。

### 参数
- `object (Object)`: 要遍历的对象。
- `[iteratee=_.identity] (Function)`: 每次迭代时调用的函数。

### 返回
- `(Object)`: 返回 `object`。

### 例子

```js
function Foo() {
    this.a = 1;
    this.b = 2;
}

Foo.prototype.c = 3;

_.forInRight(new Foo, function (value, key) {
    console.log(key);
});
// => Logs 'c', 'b', then 'a' assuming `_.forIn` logs 'a', 'b', then 'c'.
```

### 参考
- [https://lodash.com/docs/4.17.15#forInRight](https://lodash.com/docs/4.17.15#forInRight)

## forOwn

```js
_.forOwn(object, [iteratee=_.identity])
```

使用 `iteratee` 遍历自身的可枚举属性。`iteratee` 会传入 3 个参数：`(value, key, object)`。如果返回 `false`，`iteratee` 会提前退出遍历。

### 参数
- `object (Object)`: 要遍历的对象。
- `[iteratee=_.identity] (Function)`: 每次迭代时调用的函数。

### 返回
- `(Object)`: 返回 `object`。

### 例子

```js
function Foo() {
    this.a = 1;
    this.b = 2;
}

Foo.prototype.c = 3;

_.forOwn(new Foo, function (value, key) {
    console.log(key);
});
// => Logs 'a' then 'b' (iteration order is not guaranteed).
```

### 参考
- [https://lodash.com/docs/4.17.15#forOwn](https://lodash.com/docs/4.17.15#forOwn)

## forOwnRight

```js
_.forOwnRight(object, [iteratee=_.identity])
```

这个方法类似 `_.forOwn`。除了它是反方向开始遍历 `object` 的。

### 参数
- `object (Object)`: 要遍历的对象。
- `[iteratee=_.identity] (Function)`: 每次迭代时调用的函数。

### 返回
- `(Object)`: 返回 `object`。

### 例子

```js
function Foo() {
    this.a = 1;
    this.b = 2;
}

Foo.prototype.c = 3;

_.forOwnRight(new Foo, function (value, key) {
    console.log(key);
});
// => Logs 'b' then 'a' assuming `_.forOwn` logs 'a' then 'b'.
```

### 参考
- [https://lodash.com/docs/4.17.15#forOwnRight](https://lodash.com/docs/4.17.15#forOwnRight)

## functions

```js
_.functions(object)
```

创建一个函数属性名称的数组，函数属性名称来自 `object` 对象自身可枚举属性。

### 参数
- `object (Object)`: 要检查的对象。

### 返回
- `object (Object)`: 要检查的对象。

### 例子

```js
function Foo() {
    this.a = _.constant('a');
    this.b = _.constant('b');
}

Foo.prototype.c = _.constant('c');

_.functions(new Foo);
// => ['a', 'b']
```

### 参考
- [https://lodash.com/docs/4.17.15#functions](https://lodash.com/docs/4.17.15#functions)

## functionsIn

```js
_.functionsIn(object)
```

创建一个函数属性名称的数组，函数属性名称来自 `object` 对象自身和继承的可枚举属性。

### 参数
- `object (Object)`: 要检查的对象。

### 返回
- `(Array)`: 返回函数名。

### 例子

```js
function Foo() {
    this.a = _.constant('a');
    this.b = _.constant('b');
}

Foo.prototype.c = _.constant('c');

_.functionsIn(new Foo);
// => ['a', 'b', 'c']
```

### 参考
- [https://lodash.com/docs/4.17.15#functionsIn](https://lodash.com/docs/4.17.15#functionsIn)

## get

```js
_.get(object, path, [defaultValue])
```

根据 `object` 对象的 `path` 路径获取值。如果解析 `value` 是 `undefined` 会以 `defaultValue` 取代。

### 参数
- `object (Object)`: 要检索的对象。
- `path (Array|string)`: 要获取属性的路径。
- `[defaultValue] (*)`: 解析值是 `undefined` 时，返回的值。

### 返回
- `(*)`: 返回解析的值。

### 例子

```js
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.get(object, 'a[0].b.c');
// => 3

_.get(object, ['a', '0', 'b', 'c']);
// => 3

_.get(object, 'a.b.c', 'default');
// => 'default'
```

### 参考
- [https://lodash.com/docs/4.17.15#get](https://lodash.com/docs/4.17.15#get)

## has

```js
_.has(object, path)
```

检查 `path` 是否是 `object` 对象的直接属性。

### 参数
- `object (Object)`: 要检索的对象。
- `path (Array|string)`: 要检查的路径 `path`。

### 返回
- `(boolean)`: 如果 `path` 存在，那么返回 `true`，否则返回 `false` 。

### 例子

```js
var object = { 'a': { 'b': 2 } };
var other = _.create({ 'a': _.create({ 'b': 2 }) });

_.has(object, 'a');
// => true

_.has(object, 'a.b');
// => true

_.has(object, ['a', 'b']);
// => true

_.has(other, 'a');
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#has](https://lodash.com/docs/4.17.15#has)

## hasIn

```js
_.hasIn(object, path)
```

检查 `path` 是否是 `object` 对象的直接或继承属性。

### 参数
- `object (Object)`: 要检索的对象。
- `path (Array|string)`: 要检查的路径 `path`。

### 返回
- `(boolean)`: 如果 `path` 存在，那么返回 `true`，否则返回 `false`。


### 例子

```js
var object = _.create({ 'a': _.create({ 'b': 2 }) });

_.hasIn(object, 'a');
// => true

_.hasIn(object, 'a.b');
// => true

_.hasIn(object, ['a', 'b']);
// => true

_.hasIn(object, 'b');
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#hasIn](https://lodash.com/docs/4.17.15#hasIn)

## invert

```js
_.invert(object)
```

创建一个 `object` 键值倒置后的对象。如果 `object` 有重复的值，后面的值会覆盖前面的值。

### 参数
- `object (Object)`: 要键值倒置对象。

### 返回
- `(Object)`: 返回新的键值倒置后的对象。

### 例子
```js
var object = { 'a': 1, 'b': 2, 'c': 1 };

_.invert(object);
// => { '1': 'c', '2': 'b' }
```
### 参考
- [https://lodash.com/docs/4.17.15#invert](https://lodash.com/docs/4.17.15#invert)

## invertBy

```js
_.invertBy(object, [iteratee=_.identity])
```

这个方法类似 `_.invert`，除了倒置对象是集合 `collection` 中的每个元素经过迭代函数 `iteratee` 处理后返回的结果。每个反转键相应反转的值是一个负责生成反转值 `key` 的数组。`iteratee` 会传入 1 个参数：`(value)`。

### 参数
- `object (Object)`: 要键值倒置对象。
- `[iteratee=_.identity] (Function)`: 每次迭代时调用的函数。

### 返回
- `(Object)`: 返回新的键值倒置后的对象。

### 例子

```js
var object = { 'a': 1, 'b': 2, 'c': 1 };

_.invertBy(object);
// => { '1': ['a', 'c'], '2': ['b'] }

_.invertBy(object, function (value) {
    return 'group' + value;
});
// => { 'group1': ['a', 'c'], 'group2': ['b'] }
```

### 参考
- [https://lodash.com/docs/4.17.15#invertBy](https://lodash.com/docs/4.17.15#invertBy)

## invoke

```js
_.invoke(object, path, [args])
```

调用 `object` 对象 `path` 上的方法。

### 参数
- `object (Object)`: 要检索的对象。
- `path (Array|string)`: 用来调用的方法路径。
- `[args] (...*)`: 调用的方法的参数。

### 返回
- `(*)`: 返回调用方法的结果。

### 例子

```js
var object = { 'a': [{ 'b': { 'c': [1, 2, 3, 4] } }] };

_.invoke(object, 'a[0].b.c.slice', 1, 3);
// => [2, 3]
```

### 参考
- [https://lodash.com/docs/4.17.15#invoke](https://lodash.com/docs/4.17.15#invoke)

## keys

```js
_.keys(object)
```

创建一个 `object` 的自身可枚举属性名为数组。

注意：非对象的值会被强制转换为对象，查看 [ES spec](http://ecma-international.org/ecma-262/6.0/#sec-object.keys) 了解详情。

### 参数
- `object (Object)`: 要检索的对象。

### 返回
- `(Array)`: 返回包含属性名的数组。

### 例子

```js
function Foo() {
    this.a = 1;
    this.b = 2;
}

Foo.prototype.c = 3;

_.keys(new Foo);
// => ['a', 'b'] (iteration order is not guaranteed)

_.keys('hi');
// => ['0', '1']
```

### 参考
- [https://lodash.com/docs/4.17.15#invoke](https://lodash.com/docs/4.17.15#invoke)

## keysIn

```js
_.keysIn(object)
```

创建一个 `object` 自身和继承的可枚举属性名为数组。

注意: 非对象的值会被强制转换为对象。

### 参数
- `object (Object)`: 要检索的对象。

### 返回
- `(Array)`: 返回包含属性名的数组。

### 例子

```js
function Foo() {
    this.a = 1;
    this.b = 2;
}

Foo.prototype.c = 3;

_.keysIn(new Foo);
// => ['a', 'b', 'c'] (iteration order is not guaranteed)
```

### 参考
- [https://lodash.com/docs/4.17.15#keysIn](https://lodash.com/docs/4.17.15#keysIn)

## mapKeys

```js
_.mapKeys(object, [iteratee=_.identity])
```

反向版 `_.mapValues`。这个方法创建一个对象，对象的值与 `object` 相同，并且 `key` 是通过 `iteratee` 运行 `object` 中每个自身可枚举属性名字符串产生的。`iteratee` 调用 3 个参数：`(value, key, object)`。

### 参数
- `object (Object)`: 要遍历的对象。
- `[iteratee=_.identity] (Function)`: 每次迭代时调用的函数。

### 返回
- `(Object)`: 返回映射后的新对象。

### 例子

```js
function Foo() {
    this.a = 1;
    this.b = 2;
}

Foo.prototype.c = 3;

_.keysIn(new Foo);
// => ['a', 'b', 'c'] (iteration order is not guaranteed)
```

### 参考
- [https://lodash.com/docs/4.17.15#mapKeys](https://lodash.com/docs/4.17.15#mapKeys)

## mapValues

```js
_.mapValues(object, [iteratee=_.identity])
```

创建一个对象，这个对象的 `key` 与 `object` 对象相同，值是通过 `iteratee` 运行 `object` 中每个自身可枚举属性名字符串产生的。 `iteratee` 调用 3 个参数：`(value, key, object)`。

### 参数
- `object (Object)`: 要遍历的对象。
- `[iteratee=_.identity] (Function)`: 每次迭代时调用的函数。

### 返回
- `(Object)`: 返回映射后的新对象。

### 例子

```js
var users = {
    'fred': { 'user': 'fred', 'age': 40 },
    'pebbles': { 'user': 'pebbles', 'age': 1 }
};

_.mapValues(users, function (o) { return o.age; });
// => { 'fred': 40, 'pebbles': 1 } (iteration order is not guaranteed)

// The `_.property` iteratee shorthand.
_.mapValues(users, 'age');
// => { 'fred': 40, 'pebbles': 1 } (iteration order is not guaranteed)
```

### 参考
- [https://lodash.com/docs/4.17.15#mapValues](https://lodash.com/docs/4.17.15#mapValues)

## merge

```js
_.merge(object, [sources])
```

该方法类似 `_.assign`，不同之处在于它递归合并 `sources` 来源对象自身和继承的可枚举属性到 `object` 目标对象。如果目标值存在，被解析为 `undefined` 的 `sources` 来源对象属性将被跳过。数组和普通对象会递归合并，其他对象和值会被直接分配覆盖。源对象从从左到右分配。后续的来源对象属性会覆盖之前分配的属性。

注意：这方法会改变对象 `object`。

### 参数
- `object (Object)`: 目标对象。
- `[sources] (...Object)`: 来源对象。

### 返回
- `(Object)`: 返回 `object`。

### 例子

```js
var object = {
    'a': [{ 'b': 2 }, { 'd': 4 }]
};

var other = {
    'a': [{ 'c': 3 }, { 'e': 5 }]
};

_.merge(object, other);
// => { 'a': [{ 'b': 2, 'c': 3 }, { 'd': 4, 'e': 5 }] }
```

### 参考
- [https://lodash.com/docs/4.17.15#merge](https://lodash.com/docs/4.17.15#merge)

## mergeWith

```js
_.mergeWith(object, sources, customizer)
```

该方法类似 `_.merge`，不同之处在于它接受一个 `customizer`，调用以产生目标对象和来源对象属性的合并值。如果 `customizer` 返回 `undefined`，将会由合并处理方法代替。`customizer` 调用 7 个参数：`(objValue, srcValue, key, object, source, stack)`。

注意：这方法会改变对象 `object`。

### 参数
- `object (Object)`: 目标对象。
- `[sources] (...Object)`: 来源对象。
- `customizer (Function)`: 这个函数定制合并值。

### 返回
- `(Object)`: 返回 `object`。

### 例子

```js
function customizer(objValue, srcValue) {
    if (_.isArray(objValue)) {
        return objValue.concat(srcValue);
    }
}

var object = { 'a': [1], 'b': [2] };
var other = { 'a': [3], 'b': [4] };

_.mergeWith(object, other, customizer);
// => { 'a': [1, 3], 'b': [2, 4] }
```

### 参考
- [https://lodash.com/docs/4.17.15#mergeWith](https://lodash.com/docs/4.17.15#mergeWith)

## omit

```js
_.omit(object, [props])
```

反向版 `_.pick`；这个方法创建一个对象，这个对象由忽略属性之外的 `object` 自身和继承的可枚举属性组成（注：可以理解为删除 `object` 对象的属性）。

### 参数
- `object (Object)`: 来源对象。
- `[props] (...(string|string[]))`: 要被忽略的属性。

### 返回
- `(Object)`: 返回新对象。

### 例子

```js
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.omit(object, ['a', 'c']);
// => { 'b': '2' }
```

### 参考
- [https://lodash.com/docs/4.17.15#omit](https://lodash.com/docs/4.17.15#omit)

## omitBy

```js
_.omitBy(object, [predicate=_.identity])
```

反向版 `_.pickBy`；这个方法创建一个对象，这个对象忽略断言函数 `predicate` 判断不是真值的属性后，`object` 自身和继承的可枚举属性组成。`predicate` 调用 2 个参数：`(value, key)`。

### 参数
- `object (Object)`: 来源对象。
- `[predicate=_.identity] (Function)`: 调用每一个属性的函数。

### 返回
- `(Object)`: 返回新对象。

### 例子

```js
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.omitBy(object, _.isNumber);
// => { 'b': '2' }
```

### 参考
- [https://lodash.com/docs/4.17.15#omitBy](https://lodash.com/docs/4.17.15#omitBy)

## pick

```js
_.pick(object, [props])
```

创建一个从 `object` 中选中的属性的对象。

### 参数
- `object (Object)`: 来源对象。
- `[props] (...(string|string[]))`: 要被忽略的属性。

### 返回
- `(Object)`: 返回新对象。

### 例子

```js
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.pick(object, ['a', 'c']);
// => { 'a': 1, 'c': 3 }
```

### 参考
- [https://lodash.com/docs/4.17.15#pick](https://lodash.com/docs/4.17.15#pick)

## pickBy

```js
_.pickBy(object, [predicate=_.identity])
```

创建一个对象，这个对象组成为从 `object` 中经 `predicate` 判断为真值的属性。`predicate` 调用 2 个参数：`(value, key)`。

### 参数
- `object (Object)`: 来源对象。
- `[predicate=_.identity] (Function)`: 调用每一个属性的函数。

### 返回
- `(Object)`: 返回新对象。

### 例子

```js
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.pickBy(object, _.isNumber);
// => { 'a': 1, 'c': 3 }
```

### 参考
- [https://lodash.com/docs/4.17.15#pickBy](https://lodash.com/docs/4.17.15#pickBy)

## result

```js
_.result(object, path, [defaultValue])
```

这个方法类似 `_.get`，不同之处在于如果解析到的值是一个函数的话，就绑定 `this` 到这个函数并返回执行后的结果。

### 参数
- `object (Object)`: 要检索的对象。
- `path (Array|string)`: 要解析的属性路径。
- `[defaultValue] (*)`: 如果值解析为 `undefined`，返回这个值。

### 返回
- `(*)`: 返回解析后的值。

### 例子

```js
var object = { 'a': [{ 'b': { 'c1': 3, 'c2': _.constant(4) } }] };

_.result(object, 'a[0].b.c1');
// => 3

_.result(object, 'a[0].b.c2');
// => 4

_.result(object, 'a[0].b.c3', 'default');
// => 'default'

_.result(object, 'a[0].b.c3', _.constant('default'));
// => 'default'
```

### 参考
- [https://lodash.com/docs/4.17.15#result](https://lodash.com/docs/4.17.15#result)

## set

```js
_.set(object, path, value)
```

设置 `object` 对象中对应 `path` 属性路径上的值，如果 `path` 不存在，则创建。缺少的索引属性会创建为数组，而缺少的属性会创建为对象。使用 `_.setWith` 定制 `path` 创建。

注意：这个方法会改变 `object`。

### 参数
- `object (Object)`: 要修改的对象。
- `path (Array|string)`: 要设置的对象路径。
- `value (*)`: 要设置的值。

### 返回
- `(Object)`: 返回 `object`。

### 例子

```js
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.set(object, 'a[0].b.c', 4);
console.log(object.a[0].b.c);
// => 4

_.set(object, ['x', '0', 'y', 'z'], 5);
console.log(object.x[0].y.z);
// => 5
```

### 参考
- [https://lodash.com/docs/4.17.15#set](https://lodash.com/docs/4.17.15#set)

## setWith

```js
_.setWith(object, path, value, [customizer])
```

这个方法类似 `_.set`，除了它接受一个 `customizer`，调用生成对象的 `path`。如果 `customizer` 返回 `undefined` 将会有它的处理方法代替。`customizer` 调用 3 个参数：`(nsValue, key, nsObject)`。

注意: 这个方法会改变 `object` 。

### 参数
- `object (Object)`: 要修改的对象。
- `path (Array|string)`: 要设置的对象路径。
- `value (*)`: 要设置的值。
- `[customizer] (Function)`: 这个函数用来定制分配的值。

### 返回
- `(Object)`: 返回 `object`。

### 例子

```js
var object = {};

_.setWith(object, '[0][1]', 'a', Object);
// => { '0': { '1': 'a' } }
```

### 参考
- [https://lodash.com/docs/4.17.15#setWith](https://lodash.com/docs/4.17.15#setWith)

## transform

```js
_.transform(object, [iteratee=_.identity], [accumulator])
```

`_.reduce` 的替代方法；此方法将转换 `object` 对象为一个新的 `accumulator` 对象，结果来自 `iteratee` 处理自身可枚举的属性。每次调用可能会改变 `accumulator` 对象。如果不提供 `accumulator`，将使用与 `[[Prototype]]` 相同的新对象。`iteratee` 调用 4 个参数：`(accumulator, value, key, object)`。如果返回 `false`，`iteratee` 会提前退出。

### 参数
- `object (Object)`: 要遍历的对象
- `[iteratee=_.identity] (Function)`: 每次迭代时调用的函数。
- `[accumulator] (*)`: 定制叠加的值。

### 返回
- `(*)`: 返回叠加后的值。

### 例子

```js
_.transform([2, 3, 4], function (result, n) {
    result.push(n *= n);
    return n % 2 == 0;
}, []);
// => [4, 9]

_.transform({ 'a': 1, 'b': 2, 'c': 1 }, function (result, value, key) {
    (result[value] || (result[value] = [])).push(key);
}, {});
// => { '1': ['a', 'c'], '2': ['b'] }
```

### 参考
- [https://lodash.com/docs/4.17.15#transform](https://lodash.com/docs/4.17.15#transform)

## unset

```js
_.unset(object, path)
```

移除 `object` 对象 `path` 路径上的属性。

注意：这个方法会改变源对象 `object`。

### 参数
- `object (Object)`: 要修改的对象。
- `path (Array|string)`: 要移除的对象路径。

### 返回
- `(boolean)`: 如果移除成功，那么返回 `true`，否则返回 `false`。

### 例子

```js
var object = { 'a': [{ 'b': { 'c': 7 } }] };
_.unset(object, 'a[0].b.c');
// => true

console.log(object);
// => { 'a': [{ 'b': {} }] };

_.unset(object, ['a', '0', 'b', 'c']);
// => true

console.log(object);
// => { 'a': [{ 'b': {} }] };
```

### 参考
- [https://lodash.com/docs/4.17.15#unset](https://lodash.com/docs/4.17.15#unset)

## update

```js
_.update(object, path, updater)
```

该方法类似 `_.set`，除了接受 `updater` 以生成要设置的值。使用 `_.updateWith` 来自定义生成的新 `path`。`updater` 调用 1 个参数：`(value)`。

注意：这个方法会改变 `object`。

### 参数
- `object (Object)`: 要修改的对象。
- `path (Array|string)`: 要设置属性的路径。
- `updater (Function)`: 用来生成设置值的函数。

### 返回
- `(Object)`: 返回 `object` 。

### 例子

```js
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.update(object, 'a[0].b.c', function (n) { return n * n; });
console.log(object.a[0].b.c);
// => 9

_.update(object, 'x[0].y.z', function (n) { return n ? n + 1 : 0; });
console.log(object.x[0].y.z);
// => 0
```

### 参考
- [https://lodash.com/docs/4.17.15#update](https://lodash.com/docs/4.17.15#update)

## updateWith

```js
_.updateWith(object, path, updater, [customizer])
```

该方法类似 `_.update`，不同之处在于它接受 `customizer`，调用来生成新的对象的 `path`。如果 `customizer` 返回 `undefined`，路径创建由该方法代替。`customizer` 调用有 3 个参数：`(nsValue, key, nsObject)` 。

注意：这个方法会改变 `object`。

### 参数
- `object (Object)`: 要修改的对象。
- `path (Array|string)`: 要设置属性的路径。
- `updater (Function)`: 用来生成设置值的函数。
- `[customizer] (Function)`: 用来自定义分配值的函数。

### 返回
- `(Object)`: 返回 `object`。

### 例子

```js
var object = {};

_.updateWith(object, '[0][1]', _.constant('a'), Object);
// => { '0': { '1': 'a' } }
```

### 参考
- [https://lodash.com/docs/4.17.15#updateWith](https://lodash.com/docs/4.17.15#updateWith)

## values

```js
_.values(object)
```

创建 `object` 自身可枚举属性的值为数组。

注意：非对象的值会强制转换为对象。

### 参数
- `object (Object)`: 要检索的对象。

### 返回
- `(Array)`: 返回对象属性的值的数组。

### 例子

```js
function Foo() {
    this.a = 1;
    this.b = 2;
}

Foo.prototype.c = 3;

_.values(new Foo);
// => [1, 2] (iteration order is not guaranteed)

_.values('hi');
// => ['h', 'i']
```

### 参考
- [https://lodash.com/docs/4.17.15#values](https://lodash.com/docs/4.17.15#values)

## valuesIn

```js
_.valuesIn(object)
```

创建 `object` 自身和继承的可枚举属性的值为数组。

注意：非对象的值会强制转换为对象。

### 参数
- `object (Object)`: 要检索的对象。

### 返回
- `(Array)`: 返回对象属性的值的数组。

### 例子

```js
function Foo() {
    this.a = 1;
    this.b = 2;
}

Foo.prototype.c = 3;

_.valuesIn(new Foo);
// => [1, 2, 3] (iteration order is not guaranteed)
```

### 参考
- [https://lodash.com/docs/4.17.15#valuesIn](https://lodash.com/docs/4.17.15#valuesIn)

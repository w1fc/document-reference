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


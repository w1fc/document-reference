## castArray

```js
_.castArray(value)
```

如果 `value` 不是数组, 那么强制转为数组。

### 参数
- `value (*)`: 要处理的值。

### 返回
- `(Array)`: 返回转换后的数组。

### 例子

```js
_.castArray(1);
// => [1]

_.castArray({ 'a': 1 });
// => [{ 'a': 1 }]

_.castArray('abc');
// => ['abc']

_.castArray(null);
// => [null]

_.castArray(undefined);
// => [undefined]

_.castArray();
// => []

var array = [1, 2, 3];
console.log(_.castArray(array) === array);
// => true
```

### 参考
- [https://lodash.com/docs/4.17.15#castArray](https://lodash.com/docs/4.17.15#castArray)

## clone

```js
_.clone(value)
```

创建一个 `value` 的浅拷贝。

注意：这个方法参考自 [structured clone algorithm](https://mdn.io/Structured_clone_algorithm) 以及支持 `arrays`、`array buffers`、`booleans`、`date objects`、`maps`、`numbers`，`Object` 对象、 `regexes`, `sets`, `strings`, `symbols`, 以及 `typed arrays`。`arguments` 对象的可枚举属性会拷贝为普通对象。一些不可拷贝的对象，例如 `error objects`、`functions`, `DOM nodes`, 以及 `WeakMaps` 会返回空对象。

### 参数
- `value (*)`: 要拷贝的值。

### 返回
- `(*)`: 返回拷贝后的值。

### 例子

```js
var objects = [{ 'a': 1 }, { 'b': 2 }];

var shallow = _.clone(objects);
console.log(shallow[0] === objects[0]);
// => true
```

### 参考
- [https://lodash.com/docs/4.17.15#clone](https://lodash.com/docs/4.17.15#clone)

## cloneDeep

```js
_.cloneDeep(value)
```

这个方法类似 `_.clone`，不同之处在于它会递归拷贝 `value`（注：也叫深拷贝）。

### 参数
- `value (*)`: 要深拷贝的值。

### 返回
- `(*)`: 返回拷贝后的值。

### 例子

```js
var objects = [{ 'a': 1 }, { 'b': 2 }];

var deep = _.cloneDeep(objects);
console.log(deep[0] === objects[0]);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#cloneDeep](https://lodash.com/docs/4.17.15#cloneDeep)

## cloneDeepWith

```js
_.cloneDeepWith(value, [customizer])
```

这个方法类似 `_.cloneWith`，不同之处在于它会递归克隆 `value`。

### 参数
- `value (*)`: 用来递归克隆的值。
- `[customizer] (Function)`: 用来自定义克隆的函数。

### 返回
- `(*)`: 返回深度克隆后的值。

### 例子

```js
function customizer(value) {
    if (_.isElement(value)) {
        return value.cloneNode(true);
    }
}

var el = _.cloneDeepWith(document.body, customizer);

console.log(el === document.body);
// => false
console.log(el.nodeName);
// => 'BODY'
console.log(el.childNodes.length);
// => 20
```

### 参考
- [https://lodash.com/docs/4.17.15#cloneDeepWith](https://lodash.com/docs/4.17.15#cloneDeepWith)

## cloneWith
```js
_.cloneWith(value, [customizer])
```

这个方法类似 `_.clone`，不同之处在于它接受一个 `customizer` 定制返回的克隆值。如果 `customizer` 返回 `undefined` 将会使用拷贝方法代替处理。`customizer` 调用 4 个参数：`(value [, index|key, object, stack])`。

### 参数
- `value (*)`: 要克隆的值。
- `[customizer] (Function)`: 用来自定义克隆的函数。

### 返回
- `(*)`: 返回克隆值。

### 例子

```js
function customizer(value) {
    if (_.isElement(value)) {
        return value.cloneNode(false);
    }
}

var el = _.cloneWith(document.body, customizer);

console.log(el === document.body);
// => false
console.log(el.nodeName);
// => 'BODY'
console.log(el.childNodes.length);
// => 0
```

### 参考
- [https://lodash.com/docs/4.17.15#cloneWith](https://lodash.com/docs/4.17.15#cloneWith)

## conformsTo

```js
_.conformsTo(object, source)
```

通过调用断言 `source` 的属性与 `object` 的相应属性值，检查 `object` 是否符合 `source`。当 `source` 是偏应用时，这种方法和 `_.conforms` 函数是等价的。

注意: 当 `source` 为偏应用时，这种方法等价于 `_.conforms` 。

### 参数
- `object (Object)`: 要检查的对象。
- `source (Object)`: 要断言属性是否符合的对象。

### 返回
- `(boolean)`: 如果 `object` 符合，返回 `true`，否则 `false`。

### 例子

```js
var object = { 'a': 1, 'b': 2 };

_.conformsTo(object, { 'b': function (n) { return n > 1; } });
// => true

_.conformsTo(object, { 'b': function (n) { return n > 2; } });
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#conformsTo](https://lodash.com/docs/4.17.15#conformsTo)

## eq

```js
_.eq(value, other)
```

执行 `SameValueZero` 比较两者的值，来确定它们是否相等。

### 参数
- `value (*)`: 要比较的值。
- `other (*)`: 另一个要比较的值。

### 返回
- `(boolean)`: 如果两个值相等返回 `true` ，否则返回 `false` 。

### 例子

```js
var object = { 'a': 1 };
var other = { 'a': 1 };

_.eq(object, object);
// => true

_.eq(object, other);
// => false

_.eq('a', 'a');
// => true

_.eq('a', Object('a'));
// => false

_.eq(NaN, NaN);
// => true
```

### 参考
- [https://lodash.com/docs/4.17.15#eq](https://lodash.com/docs/4.17.15#eq)

## gt

```js
_.gt(value, other)
```

检查 `value` 是否大于 `other`。

### 参数
- `value (*)`: 要比较的值。
- `other (*)`: 另一个要比较的值。

### 返回
- `(boolean)`: 如果 `value` 大于 `other` 返回 `true`，否则返回 `false`。

### 例子

```js
_.gt(3, 1);
// => true

_.gt(3, 3);
// => false

_.gt(1, 3);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#gt](https://lodash.com/docs/4.17.15#gt)

## gte

```js
_.gte(value, other)
```

检查 `value` 是否大于或者等于 `other`。

### 参数
- `value (*)`: 要比较的值。
- `other (*)`: 另一个要比较的值。

### 返回
- `(boolean)`: 如果 `value` 大于或者等于 `other` 返回 `true`，否则返回 `false`。

### 例子

```js
_.gte(3, 1);
// => true

_.gte(3, 3);
// => true

_.gte(1, 3);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#gte](https://lodash.com/docs/4.17.15#gte)

## isArguments

```js
_.isArguments(value)
```

检查 `value` 是否是一个类 `arguments` 对象。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是一个 `arguments` 对象返回 `true`，否则返回 `false`。

### 例子

```js
_.isArguments(function () { return arguments; }());
// => true

_.isArguments([1, 2, 3]);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isArguments](https://lodash.com/docs/4.17.15#isArguments)

## isArray

```js
_.isArray(value)
```

检查 `value` 是否是 `Array` 类对象。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是一个数组返回 `true`，否则返回 `false`。

### 例子

```js
_.isArray([1, 2, 3]);
// => true

_.isArray(document.body.children);
// => false

_.isArray('abc');
// => false

_.isArray(_.noop);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isArray](https://lodash.com/docs/4.17.15#isArray)

## isArrayBuffer

```js
_.isArrayBuffer(value)
```

检查 `value` 是否是 `ArrayBuffer` 对象。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是一个 `ArrayBuffer` 返回 `true`，否则返回 `false`。

### 例子

```js
_.isArrayBuffer(new ArrayBuffer(2));
// => true

_.isArrayBuffer(new Array(2));
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isArrayBuffer](https://lodash.com/docs/4.17.15#isArrayBuffer)

## isArrayLike

```js
_.isArrayLike(value)

```

检查 `value` 是否是类数组。如果一个值被认为是类数组，那么它不是一个函数，并且 `value.length` 是个整数，大于等于 `0`，小于或等于 `Number.MAX_SAFE_INTEGER`。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是一个类数组，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isArrayLike([1, 2, 3]);
// => true

_.isArrayLike(document.body.children);
// => true

_.isArrayLike('abc');
// => true

_.isArrayLike(_.noop);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isArrayLike](https://lodash.com/docs/4.17.15#isArrayLike)

## isArrayLikeObject

```js
_.isArrayLikeObject(value)
```
这个方法类似 `_.isArrayLike`。不同之处在于它还检查 `value` 是否是个对象。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是一个类数组对象，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isArrayLikeObject([1, 2, 3]);
// => true

_.isArrayLikeObject(document.body.children);
// => true

_.isArrayLikeObject('abc');
// => false

_.isArrayLikeObject(_.noop);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isArrayLikeObject](https://lodash.com/docs/4.17.15#isArrayLikeObject)

## isBoolean

```js
_.isBoolean(value)
```

检查 `value` 是否是原始 `boolean` 类型或者对象。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是一个布尔值，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isBoolean(false);
// => true

_.isBoolean(null);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isBoolean](https://lodash.com/docs/4.17.15#isBoolean)

## isBuffer

```js
_.isBuffer(value)
```

检查 `value` 是否是个 `buffer`。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是一个 `buffer`，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isBuffer(new Buffer(2));
// => true

_.isBuffer(new Uint8Array(2));
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isBuffer](https://lodash.com/docs/4.17.15#isBuffer)

## isDate

```js
_.isDate(value)
```

检查 `value` 是否是 `Date` 对象。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是一个日期对象，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isDate(new Date);
// => true

_.isDate('Mon April 23 2012');
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isDate](https://lodash.com/docs/4.17.15#isDate)

## isElement

```js
_.isElement(value)
```

检查 `value` 是否是可能是 DOM 元素。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是一个 DOM 元素，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isElement(document.body);
// => true

_.isElement('');
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isElement](https://lodash.com/docs/4.17.15#isElement)

## isEmpty

```js
_.isEmpty(value)
```

检查 `value` 是否为一个空对象，集合，映射或者 `set`。判断的依据是除非是有枚举属性的对象，`length` 大于 `0` 的 `arguments` `object`, `array`, `string` 或类 jQuery 选择器。

对象如果被认为为空，那么他们没有自己的可枚举属性的对象。

类数组值，比如 `arguments` 对象，`array`，`buffer`，`string` 或者类 jQuery 集合的 `length` 为 `0`，被认为是空。类似的，`map` 和 `set` 的 `size` 为 `0`，被认为是空。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 为空，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isEmpty(null);
// => true

_.isEmpty(true);
// => true

_.isEmpty(1);
// => true

_.isEmpty([1, 2, 3]);
// => false

_.isEmpty({ 'a': 1 });
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isEmpty](https://lodash.com/docs/4.17.15#isEmpty)

## isEqual

```js
_.isEqual(value, other)

```

执行深比较来确定两者的值是否相等。

**注意:** 这个方法支持比较 `arrays`, `array buffers`, `booleans`, `date objects`, `error objects`, `maps`, `numbers`, `Object objects`, `regexes`, `sets`, `strings`, `symbols`, 以及 `typed arrays`。 `Object` 对象值比较自身的属性，不包括继承的和可枚举的属性。 不支持函数和 DOM 节点比较。

### 参数
- `value (*)`: 用来比较的值。
- `other (*)`: 另一个用来比较的值。

### 返回
- `(boolean)`: 如果两个值完全相同，那么返回 `true`，否则返回 `false`。

### 例子

```js
var object = { 'a': 1 };
var other = { 'a': 1 };

_.isEqual(object, other);
// => true

object === other;
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isEqual](https://lodash.com/docs/4.17.15#isEqual)

## isEqualWith
```js
_.isEqualWith(value, other, [customizer])

```

这个方法类似 `_.isEqual`。不同之处在于它接受一个 `customizer` 用来定制比较值。如果 `customizer` 返回 `undefined` 将会比较处理方法代替。`customizer` 会传入 6 个参数：`(objValue, othValue [, index|key, object, other, stack])`

### 参数
- `value (*)`: 用来比较的值。
- `other (*)`: 另一个用来比较的值。
- `[customizer] (Function)`: 用来定制比较值的函数。

### 返回
- `(boolean)`: 如果两个值完全相同，那么返回 `true`，否则返回 `false`。

### 例子

```js
function isGreeting(value) {
    return /^h(?:i|ello)$/.test(value);
}

function customizer(objValue, othValue) {
    if (isGreeting(objValue) && isGreeting(othValue)) {
        return true;
    }
}

var array = ['hello', 'goodbye'];
var other = ['hi', 'goodbye'];

_.isEqualWith(array, other, customizer);
// => true
```

### 参考
- [https://lodash.com/docs/4.17.15#isEqualWith](https://lodash.com/docs/4.17.15#isEqualWith)

## isError

```js
_.isError(value)
```

检查 `value` 是否是 `Error`, `EvalError`, `RangeError`, `ReferenceError`, `SyntaxError`, `TypeError`, 或者 `URIError` 对象。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是一个 `Error` 对象，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isError(new Error);
// => true

_.isError(Error);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isError](https://lodash.com/docs/4.17.15#isError)

## isFinite

```js
_.isFinite(value)

```

检查 `value` 是否是原始有限数值。

注意：这个方法基于 [Number.isFinite](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/isFinite) 。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是一个有限数值，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isFinite(3);
// => true

_.isFinite(Number.MIN_VALUE);
// => true

_.isFinite(Infinity);
// => false

_.isFinite('3');
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isFinite](https://lodash.com/docs/4.17.15#isFinite)

## isFunction

```js
_.isFunction(value)
```

检查 `value` 是否是 `Function` 对象。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是一个函数，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isFunction(_);
// => true

_.isFunction(/abc/);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isFunction](https://lodash.com/docs/4.17.15#isFunction)

## isInteger

```js
_.isInteger(value)

```

检查 `value` 是否为一个整数。

注意: 这个方法基于 [Number.isInteger](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/isInteger)。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是一个整数，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isInteger(3);
// => true

_.isInteger(Number.MIN_VALUE);
// => false

_.isInteger(Infinity);
// => false

_.isInteger('3');
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isInteger](https://lodash.com/docs/4.17.15#isInteger)

## isLength

```js
_.isLength(value)
```

检查 `value` 是否为有效的类数组长度。

注意: 这个函数基于 [ToLength](http://ecma-international.org/ecma-262/6.0/#sec-tolength) 。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是一个有效长度，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isLength(3);
// => true

_.isLength(Number.MIN_VALUE);
// => false

_.isLength(Infinity);
// => false

_.isLength('3');
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isLength](https://lodash.com/docs/4.17.15#isLength)

## isMap

```js
_.isMap(value)
```

检查 `value` 是否为一个 `Map` 对象。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是一个 `Map` 对象，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isMap(new Map);
// => true

_.isMap(new WeakMap);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isMap](https://lodash.com/docs/4.17.15#isMap)

## isMatch

```js
_.isMatch(object, source)
```

执行一个深度比较，来确定 `object` 是否含有和 `source` 完全相等的属性值。

注意: 当 `source` 为偏应用时，这种方法等价于 `_.matches` 。

偏应用比较匹配空数组和空对象 `source` 值分别针对任何数组或对象的值。在 `_.isEqual` 中查看支持的值比较列表。

### 参数
- `object (Object)`: 要检查的对象。
- `source (Object)`: 属性值相匹配的对象。

### 返回
- `(boolean)`: 如果 `object` 匹配，那么返回 `true`，否则返回 `false`。

### 例子

```js
var object = { 'a': 1, 'b': 2 };

_.isMatch(object, { 'b': 2 });
// => true

_.isMatch(object, { 'b': 1 });
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isMatch](https://lodash.com/docs/4.17.15#isMatch)

## isMatchWith

```js
_.isMatchWith(object, source, [customizer])
```

这个方法类似 `_.isMatch`。不同之处在于它接受一个 `customizer` 定制比较的值。如果 `customizer` 返回 `undefined` 将会比较处理方法代替。`customizer` 会传入 5 个参数：`(objValue, srcValue, index|key, object, source)`。

### 参数
- `object (Object)`: 要检查的对象。
- `source (Object)`: 属性值相匹配的对象。
- `[customizer] (Function)`: 这个函数用来定制比较。

### 返回
- `(boolean)`: 如果 `object` 匹配，那么返回 `true`，否则返回 `false`。

### 例子

```js
function isGreeting(value) {
    return /^h(?:i|ello)$/.test(value);
}

function customizer(objValue, srcValue) {
    if (isGreeting(objValue) && isGreeting(srcValue)) {
        return true;
    }
}

var object = { 'greeting': 'hello' };
var source = { 'greeting': 'hi' };

_.isMatchWith(object, source, customizer);
// => true
```

### 参考
- [https://lodash.com/docs/4.17.15#isMatchWith](https://lodash.com/docs/4.17.15#isMatchWith)

## isNaN

```js
_.isNaN(value)
```

检查 `value` 是否是 `NaN`。

注意: 这个方法基于 `Number.isNaN`，和全局的 `isNaN` 不同之处在于，全局的 `isNaN` 对于 `undefined` 和其他非数字的值返回 `true` 。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是一个 `NaN`，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isNaN(NaN);
// => true

_.isNaN(new Number(NaN));
// => true

isNaN(undefined);
// => true

_.isNaN(undefined);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isNaN](https://lodash.com/docs/4.17.15#isNaN)

## isNative

```js
_.isNative(value)
```

检查 `value` 是否是一个原生函数。

注意：这种方法不能可靠地检测在 core-js 包中存在的本地函数，因为 core-js 规避这种检测。尽管有多个请求，core-js 维护者已经明确表态：任何试图修复检测将受阻。这样一来，我们别无选择，只能抛出一个错误。不幸的是，这也影响其他的包，比如依赖于 core-js的 [babel-polyfill](https://www.npmjs.com/package/babel-polyfill)。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是一个原生函数，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isNative(Array.prototype.push);
// => true

_.isNative(_);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isNative](https://lodash.com/docs/4.17.15#isNative)

## isNil

```js
_.isNil(value)
```

检查 `value` 是否是 `null` 或者 `undefined`。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 为 `null` 或 `undefined`，那么返回 `true`，否则返回 `false`。

### 例子
```js
_.isNil(null);
// => true

_.isNil(void 0);
// => true

_.isNil(NaN);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isNil](https://lodash.com/docs/4.17.15#isNil)

## isNull

```js
_.isNull(value)
```

检查 `value` 是否是 `null`。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 为 `null`，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isNull(null);
// => true

_.isNull(void 0);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isNull](https://lodash.com/docs/4.17.15#isNull)

## isNumber

```js
_.isNumber(value)
```

检查 `value` 是否是原始 `Number` 数值型或者对象。

注意: 要排除 `Infinity`, `-Infinity`, 以及 `NaN` 数值类型，用 [_.isFinite](https://www.lodashjs.com/docs/lodash.isNumber#isFinite) 方法。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 为一个数值，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isNumber(3);
// => true

_.isNumber(Number.MIN_VALUE);
// => true

_.isNumber(Infinity);
// => true

_.isNumber('3');
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isNumber](https://lodash.com/docs/4.17.15#isNumber)

## isObject

```js
_.isObject(value)
```

检查 `value` 是否为 `Object` 的 [language type](http://www.ecma-international.org/ecma-262/6.0/#sec-ecmascript-language-types)。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 为一个对象，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isObject({});
// => true

_.isObject([1, 2, 3]);
// => true

_.isObject(_.noop);
// => true

_.isObject(null);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isObject](https://lodash.com/docs/4.17.15#isObject)

## isObjectLike

```js
_.isObjectLike(value)
```

检查 `value` 是否是类对象。如果一个值是类对象，那么它不应该是 `null`，而且 `typeof` 后的结果是 `"object"`。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 为一个类对象，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isObjectLike({});
// => true

_.isObjectLike([1, 2, 3]);
// => true

_.isObjectLike(_.noop);
// => false

_.isObjectLike(null);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isObjectLike](https://lodash.com/docs/4.17.15#isObjectLike)

## isPlainObject

```js
_.isPlainObject(value)
```

检查 `value` 是否是普通对象。也就是说该对象由 `Object` 构造函数创建，或者 `[[Prototype]]` 为 `null` 。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 为一个普通对象，那么返回 `true`，否则返回 `false`。

### 例子

```js
function Foo() {
    this.a = 1;
}

_.isPlainObject(new Foo);
// => false

_.isPlainObject([1, 2, 3]);
// => false

_.isPlainObject({ 'x': 0, 'y': 0 });
// => true

_.isPlainObject(Object.create(null));
// => true
```

### 参考
- [https://lodash.com/docs/4.17.15#isPlainObject](https://lodash.com/docs/4.17.15#isPlainObject)

## isRegExp

```js
_.isRegExp(value)
```

检查 `value` 是否为 `RegExp` 对象。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 为一个正则表达式，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isRegExp(/abc/);
// => true

_.isRegExp('/abc/');
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isRegExp](https://lodash.com/docs/4.17.15#isRegExp)

## isSafeInteger
```js
_.isSafeInteger(value)
```

检查 `value` 是否是一个安全整数。 一个安全整数应该是符合 IEEE-754 标准的非双精度浮点数。

注意: 这个方法基于 [Number.isSafeInteger](https://mdn.io/Number/isSafeInteger)。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 为一个安全整数，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isSafeInteger(3);
// => true

_.isSafeInteger(Number.MIN_VALUE);
// => false

_.isSafeInteger(Infinity);
// => false

_.isSafeInteger('3');
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isSafeInteger](https://lodash.com/docs/4.17.15#isSafeInteger)

## isSet

```js
_.isSet(value)
```

检查 `value` 是否是一个 `Set` 对象。

### 参数
value (*): 要检查的值。
### 返回
(boolean): 如果 value 为一个 set 对象，那么返回 true，否则返回 false。

### 例子

```js
_.isSet(new Set);
// => true

_.isSet(new WeakSet);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isSet](https://lodash.com/docs/4.17.15#isSet)

## isString

```js
_.isString(value)
```

检查 `value` 是否是原始字符串 `String` 或者对象。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 为一个字符串，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isString('abc');
// => true

_.isString(1);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isString](https://lodash.com/docs/4.17.15#isString)

## isSymbol

```js
_.isSymbol(value)
```

检查 `value` 是否是原始 `Symbol` 或者对象。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 为一个 `symbol`，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isSymbol(Symbol.iterator);
// => true

_.isSymbol('abc');
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isSymbol](https://lodash.com/docs/4.17.15#isSymbol)

## isTypedArray

```js
_.isTypedArray(value)
```

检查 `value` 是否是 `TypedArray`。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 为一个 `TypedArray` ，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isTypedArray(new Uint8Array);
// => true

_.isTypedArray([]);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isTypedArray](https://lodash.com/docs/4.17.15#isTypedArray)

## isUndefined

```js
_.isUndefined(value)
```

检查 `value` 是否是 `undefined` 。


### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 是 `undefined`，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isUndefined(void 0);
// => true

_.isUndefined(null);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isUndefined](https://lodash.com/docs/4.17.15#isUndefined)

## isWeakMap

```js
_.isWeakMap(value)
```

检查 `value` 是否是 `WeakMap` 对象。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 为一个 `WeakMap` 对象 ，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isWeakMap(new WeakMap);
// => true

_.isWeakMap(new Map);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isWeakMap](https://lodash.com/docs/4.17.15#isWeakMap)

## isWeakSet

```js
_.isWeakSet(value)
```

检查 `value` 是否是 `WeakSet` 对象。

### 参数
- `value (*)`: 要检查的值。

### 返回
- `(boolean)`: 如果 `value` 为一个 `WeakSet` 对象 ，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.isWeakSet(new WeakSet);
// => true

_.isWeakSet(new Set);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#isWeakSet](https://lodash.com/docs/4.17.15#isWeakSet)

## lt

```js
_.lt(value, other)
```

检查 `value` 是否小于 `other`。

### 参数
- `value (*)`: 用来比较的值。
- `other (*)`: 另一个用来比较的值。

### 返回
- `(boolean)`: 如果 `value` 小于 `other` 返回 `true`，否则返回 `false`。

### 例子

```js
_.lt(1, 3);
// => true

_.lt(3, 3);
// => false

_.lt(3, 1);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#lt](https://lodash.com/docs/4.17.15#lt)

## lte

```js
_.lte(value, other)
```

检查 `value` 是否小于等于 `other`。

### 参数
- `value (*)`: 用来比较的值。
- `other (*)`: 另一个用来比较的值。

### 返回
- `(boolean)`: 如果 `value` 小于等于 `other` 返回 `true`，否则返回 `false`。

### 例子

```js
_.lte(1, 3);
// => true

_.lte(3, 3);
// => true

_.lte(3, 1);
// => false
```

### 参考
- [https://lodash.com/docs/4.17.15#lte](https://lodash.com/docs/4.17.15#lte)

## toArray

```js
_.toArray(value)
```

转换 `value` 为一个数组。

### 参数
- `value (*)`: 要转换的值。

### 返回
- `(Array)`: 返回转换后的数组。

### 例子

```js
_.toArray({ 'a': 1, 'b': 2 });
// => [1, 2]

_.toArray('abc');
// => ['a', 'b', 'c']

_.toArray(1);
// => []

_.toArray(null);
// => []
```

### 参考
- [https://lodash.com/docs/4.17.15#toArray](https://lodash.com/docs/4.17.15#toArray)

## toFinite

```js
_.toFinite(value)
```

转换 `value` 为一个有限数字。

### 参数
- `value (*)`: 要转换的值。

### 返回
- `(number)`: 返回转换后的数字。

### 例子

```js
_.toFinite(3.2);
// => 3.2

_.toFinite(Number.MIN_VALUE);
// => 5e-324

_.toFinite(Infinity);
// => 1.7976931348623157e+308

_.toFinite('3.2');
// => 3.2
```

### 参考
- [https://lodash.com/docs/4.17.15#toFinite](https://lodash.com/docs/4.17.15#toFinite)

## toInteger

```js
_.toInteger(value)
```

转换 `value` 为一个整数。

注意: 这个方法基于 [ToInteger](http://www.ecma-international.org/ecma-262/6.0/#sec-tointeger)。

### 参数
- `value (*)`: 要转换的值。

### 返回
- `(number)`: 返回转换后的整数。

### 例子

```js
_.toInteger(3.2);
// => 3

_.toInteger(Number.MIN_VALUE);
// => 0

_.toInteger(Infinity);
// => 1.7976931348623157e+308

_.toInteger('3.2');
// => 3
```

### 参考
- [https://lodash.com/docs/4.17.15#toInteger](https://lodash.com/docs/4.17.15#toInteger)

## toLength

```js
_.toLength(value)
```

转换 `value` 为用作类数组对象的长度整数。

注意: 这个方法基于 [ToLength](http://ecma-international.org/ecma-262/6.0/#sec-tolength)。

### 参数
- `value (*)`: 要转换的值。

### 返回
- `(number)`: 返回转换后的整数。

### 例子

```js
_.toLength(3.2);
// => 3

_.toLength(Number.MIN_VALUE);
// => 0

_.toLength(Infinity);
// => 4294967295

_.toLength('3.2');
// => 3
```

### 参考
- [https://lodash.com/docs/4.17.15#toLength](https://lodash.com/docs/4.17.15#toLength)

## toNumber

```js
_.toNumber(value)
```

转换 `value` 为一个数字。

### 参数
- `value (*)`: 要处理的值。

### 返回
- `(number)`: 返回数字。

### 例子
```js
_.toNumber(3.2);
// => 3.2

_.toNumber(Number.MIN_VALUE);
// => 5e-324

_.toNumber(Infinity);
// => Infinity

_.toNumber('3.2');
// => 3.2
```

### 参考
- [https://lodash.com/docs/4.17.15#toNumber](https://lodash.com/docs/4.17.15#toNumber)

## toPlainObject

```js
_.toPlainObject(value)
```

转换 `value` 为普通对象。包括继承的可枚举属性。

### 参数
- `value (*)`: 要转换的值。

### 返回
- `(Object)`: 返回转换后的普通对象。

### 例子

```js
function Foo() {
    this.b = 2;
}

Foo.prototype.c = 3;

_.assign({ 'a': 1 }, new Foo);
// => { 'a': 1, 'b': 2 }

_.assign({ 'a': 1 }, _.toPlainObject(new Foo));
// => { 'a': 1, 'b': 2, 'c': 3 }
```

### 参考
- [https://lodash.com/docs/4.17.15#toPlainObject](https://lodash.com/docs/4.17.15#toPlainObject)

## toSafeInteger

```js
_.toSafeInteger(value)
```

转换 `value` 为安全整数。 安全整数可以用于比较和准确的表示。

### 参数
- `value (*)`: 要转换的值。

### 返回
- `(number)`: 返回转换后的整数。

### 例子

```js
_.toSafeInteger(3.2);
// => 3

_.toSafeInteger(Number.MIN_VALUE);
// => 0

_.toSafeInteger(Infinity);
// => 9007199254740991

_.toSafeInteger('3.2');
// => 3
```

### 参考
- [https://lodash.com/docs/4.17.15#toSafeInteger](https://lodash.com/docs/4.17.15#toSafeInteger)

## toString

```js
_.toString(value)
```

转换 `value` 为字符串。`null` 和 `undefined` 将返回空字符串。`-0` 将被转换为字符串 `"-0"`。

### 参数
- `value (*)`: 要处理的值。

### 返回
- `(string)`: 返回字符串。

### 例子

```js
_.toString(null);
// => ''

_.toString(-0);
// => '-0'

_.toString([1, 2, 3]);
// => '1,2,3'
```

### 参考
- [https://lodash.com/docs/4.17.15#toString](https://lodash.com/docs/4.17.15#toString)

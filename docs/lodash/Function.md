## after

```js
_.after(n, func)
```

`_.before` 的反向函数；此方法创建一个函数，当他被调用 `n` 或更多次之后将马上触发 `func` 。

### 参数
- `n (number)`: `func` 方法应该在调用多少次后才执行。
- `func (Function)`: 用来限定的函数。

### 返回
- `(Function)`: 返回新的限定函数。

### 例子

```js
var saves = ['profile', 'settings'];

var done = _.after(saves.length, function () {
    console.log('done saving!');
});

_.forEach(saves, function (type) {
    asyncSave({ 'type': type, 'complete': done });
});
// => Logs 'done saving!' after the two async saves have completed.
```

### 参考
- [https://lodash.com/docs/4.17.15#after](https://lodash.com/docs/4.17.15#after)

## ary

```js
_.ary(func, [n=func.length])
```

创建一个调用 `func` 的函数。调用 `func` 时最多接受 `n` 个参数，忽略多出的参数。

### 参数
- `func (Function)`: 需要被限制参数个数的函数。
- `[n=func.length] (number)`: 限制的参数数量。

### 返回
- `(Function)`: 返回新的覆盖函数。

### 例子

```js
_.map(['6', '8', '10'], _.ary(parseInt, 1));
// => [6, 8, 10]
```

### 参考
- [https://lodash.com/docs/4.17.15#ary](https://lodash.com/docs/4.17.15#ary)

## before

```js
_.before(n, func)
```

创建一个调用 `func` 的函数，通过 `this` 绑定和创建函数的参数调用 `func`，调用次数不超过 `n` 次。之后再调用这个函数，将返回一次最后调用 `func` 的结果。

### 参数
- `n (number)`: 超过多少次不再调用 `func` 。
- `func (Function)`: 限制执行的函数。

### 返回
- `(Function)`: 返回新的限定函数。

### 例子

```js
jQuery(element).on('click', _.before(5, addContactToList));
// => Allows adding up to 4 contacts to the list.
```

### 参考
- [https://lodash.com/docs/4.17.15#before](https://lodash.com/docs/4.17.15#before)

## bind

```js
_.bind(func, thisArg, [partials])
```

创建一个调用 `func` 的函数，`thisArg` 绑定 `func` 函数中的 `this` ，并且 `func` 函数会接收 `partials` 附加参数。

`_.bind.placeholder` 值，默认是以 `_` 作为附加部分参数的占位符。

注意: 不同于原生的 [Function#bind](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)，这个方法不会设置绑定函数的 `"length"` 属性。

### 参数
- `func (Function)`: 绑定的函数。
- `thisArg (*)`: `func` 绑定的 `this` 对象。
- `[partials] (...*)`: 附加的部分参数。

### 返回
- `(Function)`: 返回新的绑定函数。

### 例子

```js
function greet(greeting, punctuation) {
    return greeting + ' ' + this.user + punctuation;
}

var object = { 'user': 'fred' };

var bound = _.bind(greet, object, 'hi');
bound('!');
// => 'hi fred!'

// Bound with placeholders.
var bound = _.bind(greet, object, _, '!');
bound('hi');
// => 'hi fred!'
```

### 参考
- [https://lodash.com/docs/4.17.15#bind](https://lodash.com/docs/4.17.15#bind)

## bindKey

```js
_.bindKey(object, key, [partials])
```

创建一个函数，在 `object[key]` 上通过接收 `partials` 附加参数，调用这个方法。

这个方法与 `_.bind` 的不同之处在于允许重新定义绑定函数即使它还不存在。浏览 [Peter Michaux's article](http://peter.michaux.ca/articles/lazy-function-definition-pattern) 了解更多详情。

`_.bind.placeholder` 值，默认是以 `_` 作为附加部分参数的占位符。

### 参数
- `object (Object)`: 需要绑定函数的对象。
- `key (string)`: 需要绑定函数对象的键。
- `[partials] (...*)`: 附加的部分参数。

### 返回
- `(Function)`: 返回新的绑定函数。

### 例子

```js
var object = {
    'user': 'fred',
    'greet': function (greeting, punctuation) {
        return greeting + ' ' + this.user + punctuation;
    }
};

var bound = _.bindKey(object, 'greet', 'hi');
bound('!');
// => 'hi fred!'

object.greet = function (greeting, punctuation) {
    return greeting + 'ya ' + this.user + punctuation;
};

bound('!');
// => 'hiya fred!'

// Bound with placeholders.
var bound = _.bindKey(object, 'greet', _, '!');
bound('hi');
// => 'hiya fred!'
```

### 参考
- [https://lodash.com/docs/4.17.15#bindKey](https://lodash.com/docs/4.17.15#bindKey)

## curry

```js
_.curry(func, [arity=func.length])
```

创建一个函数，该函数接收 `func` 的参数，要么调用 `func` 返回的结果，如果 `func` 所需参数已经提供，则直接返回 `func` 所执行的结果。或返回一个函数，接受余下的 `func` 参数的函数，可以使用 `func.length` 强制需要累积的参数个数。

`_.curry.placeholder` 值，默认是以 `_` 作为附加部分参数的占位符。

注意：这个方法不会设置 `curried` 函数的 `"length"` 属性。

### 参数
- `func (Function)`: 用来柯里化（curry）的函数。
- `[arity=func.length] (number)`: 需要提供给 `func` 的参数数量。

### 返回
- `(Function)`: 返回新的柯里化（curry）函数。

### 例子

```js
var abc = function (a, b, c) {
    return [a, b, c];
};

var curried = _.curry(abc);

curried(1)(2)(3);
// => [1, 2, 3]

curried(1, 2)(3);
// => [1, 2, 3]

curried(1, 2, 3);
// => [1, 2, 3]

// Curried with placeholders.
curried(1)(_, 3)(2);
// => [1, 2, 3]
```

### 参考
- [https://lodash.com/docs/4.17.15#curry](https://lodash.com/docs/4.17.15#curry)

## curryRight

```js
_.curryRight(func, [arity=func.length])
```

这个方法类似 `_.curry`。不同之处在于它接受参数的方式用 `_.partialRight` 代替了 `_.partial`。

`_.curryRight.placeholder` 值，默认是以 `_` 作为附加部分参数的占位符。

注意：这个方法不会设置 `curried` 函数的 `"length"` 属性。

### 参数
- `func (Function)`: 用来柯里化（curry）的函数。
- `[arity=func.length] (number)`: 需要提供给 `func` 的参数数量。

### 返回
- `(Function)`: 返回新的柯里化（curry）函数。

### 例子

```js
var abc = function (a, b, c) {
    return [a, b, c];
};

var curried = _.curryRight(abc);

curried(3)(2)(1);
// => [1, 2, 3]

curried(2, 3)(1);
// => [1, 2, 3]

curried(1, 2, 3);
// => [1, 2, 3]

// Curried with placeholders.
curried(3)(1, _)(2);
// => [1, 2, 3]
```

### 参考
- [https://lodash.com/docs/4.17.15#curryRight](https://lodash.com/docs/4.17.15#curryRight)

## debounce

```js
_.debounce(func, [wait=0], [options={}])
```

创建一个防抖动 `debounced` 函数，该函数会从上一次被调用后，延迟 `wait` 毫秒后调用 `func` 方法。防抖动 `debounced` 函数提供一个 `cancel` 方法取消延迟的函数调用以及 `flush` 方法立即调用。可以提供一个选项 `options` 对象决定如何调用 `func` 方法，`options.leading` 与/或 `options.trailing` 决定延迟前后如何触发（注：是先调用后等待还是先等待后调用）。 `func` 调用时会传入最后一次提供给防抖动 `debounced` 函数的参数。后续调用的防抖动 `debounced` 函数返回是最后一次 `func` 调用的结果。

注意: 如果 `leading` 和 `trailing` 选项为 `true`, 则 `func` 允许 `trailing` 方式调用的条件为: 在 `wait` 期间多次调用防抖方法。

如果 `wait` 为 `0` 并且 `leading` 为 `false`, `func` 调用将被推迟到下一个点，类似 `setTimeout` 为 `0` 的超时。

有关 `_.debounce` 和 `_.throttle` 之间差异的详细信息，请参见 [David Corbacho 的文章](https://css-tricks.com/debouncing-throttling-explained-examples/)。

### 参数
- `func (Function)`: 要防抖动的函数。
- `[wait=0] (number)`: 需要延迟的毫秒数。
- `[options={}] (Object)`: 选项对象。
- `[options.leading=false] (boolean)`: 指定在延迟开始前调用。
- `[options.maxWait] (number)`: 设置 `func` 允许被延迟的最大值。
- `[options.trailing=true] (boolean)`: 指定在延迟结束后调用。

### 返回
- `(Function)`: 返回新的防抖动 `debounced` 函数。

### 例子

```js
// Avoid costly calculations while the window size is in flux.
jQuery(window).on('resize', _.debounce(calculateLayout, 150));

// Invoke `sendMail` when clicked, debouncing subsequent calls.
jQuery(element).on('click', _.debounce(sendMail, 300, {
    'leading': true,
    'trailing': false
}));

// Ensure `batchLog` is invoked once after 1 second of debounced calls.
var debounced = _.debounce(batchLog, 250, { 'maxWait': 1000 });
var source = new EventSource('/stream');
jQuery(source).on('message', debounced);

// Cancel the trailing debounced invocation.
jQuery(window).on('popstate', debounced.cancel);
```

### 参考
- [https://lodash.com/docs/4.17.15#debounce](https://lodash.com/docs/4.17.15#debounce)

## defer

```js
_.defer(func, [args])
```

推迟调用 `func`，直到当前堆栈清理完毕。调用时，任何附加的参数会传给 `func`。

### 参数
- `func (Function)`: 要延迟的函数。
- `[args] (...*)`: 会在调用时传给 `func` 的参数。

### 返回
- `(number)`: 返回计时器 `id`。

### 例子

```js
_.defer(function(text) {
  console.log(text);
}, 'deferred');
// => Logs 'deferred' after one millisecond.
```

### 参考
- [https://lodash.com/docs/4.17.15#defer](https://lodash.com/docs/4.17.15#defer)

## delay

```js
_.delay(func, wait, [args])
```

延迟 `wait` 毫秒后调用 `func`。调用时，任何附加的参数会传给 `func`。

### 参数
- `func (Function)`: 要延迟的函数。
- `wait (number)`: 要延迟的毫秒数。
- `[args] (...*)`: 会在调用时传入到 `func` 的参数。

### 返回
- `(number)`: 返回计时器 `id`。

### 例子

```js
_.delay(function(text) {
  console.log(text);
}, 1000, 'later');
// => Logs 'later' after one second.
```

### 参考
- [https://lodash.com/docs/4.17.15#delay](https://lodash.com/docs/4.17.15#delay)

## flip

```js
_.flip(func)
```

创建一个函数，调用 `func` 时候接收翻转的参数。

### 参数
- `func (Function)`: 要翻转参数的函数。

### 返回
- `(Function)`: 返回新的函数。

### 例子

```js
var flipped = _.flip(function () {
    return _.toArray(arguments);
});

flipped('a', 'b', 'c', 'd');
// => ['d', 'c', 'b', 'a']
```

### 参考
- [https://lodash.com/docs/4.17.15#flip](https://lodash.com/docs/4.17.15#flip)

## memoize

```js
_.memoize(func, [resolver])
```

创建一个会缓存 `func` 结果的函数。如果提供了 `resolver` ，就用 `resolver` 的返回值作为 `key` 缓存函数的结果。默认情况下用第一个参数作为缓存的 `key`。`func` 在调用时 `this` 会绑定在缓存函数上。

注意: 缓存会暴露在缓存函数的 `cache` 上。它是可以定制的，只要替换了 `_.memoize.Cache` 构造函数，或实现了 `Map` 的 `delete`, `get`, `has`, 和 `set` 方法。

### 参数
- `func (Function)`: 需要缓存化的函数.
- `[resolver] (Function)`: 这个函数的返回值作为缓存的 `key`。

### 返回
- `(Function)`: 返回缓存化后的函数。

### 例子

```js
var object = { 'a': 1, 'b': 2 };
var other = { 'c': 3, 'd': 4 };

var values = _.memoize(_.values);
values(object);
// => [1, 2]

values(other);
// => [3, 4]

object.a = 2;
values(object);
// => [1, 2]

// Modify the result cache.
values.cache.set(object, ['a', 'b']);
values(object);
// => ['a', 'b']

// Replace `_.memoize.Cache`.
_.memoize.Cache = WeakMap;
```

### 参考
- [https://lodash.com/docs/4.17.15#memoize](https://lodash.com/docs/4.17.15#memoize)

## negate

```js
_.negate(predicate)
```

创建一个针对断言函数 `func` 结果取反的函数。`func` 断言函数被调用的时候，`this` 绑定到创建的函数，并传入对应参数。

### 参数
- `predicate (Function)`: 需要对结果取反的函数。

### 返回
- `(Function)`: 返回一个新的取反函数。

### 例子

```js
function isEven(n) {
    return n % 2 == 0;
}

_.filter([1, 2, 3, 4, 5, 6], _.negate(isEven));
// => [1, 3, 5]
```

### 参考
- [https://lodash.com/docs/4.17.15#negate](https://lodash.com/docs/4.17.15#negate)

## once

```js
_.once(func)
```

创建一个只能调用 `func` 一次的函数。重复调用返回第一次调用的结果。`func` 调用时，`this` 绑定到创建的函数，并传入对应参数。

### 参数
- `func (Function)`: 指定的触发的函数。

### 返回
- `(Function)`: 返回新的受限函数。

### 例子

```js
var initialize = _.once(createApplication);
initialize();
initialize();
// => `createApplication` is invoked onceF
```

### 参考
- [https://lodash.com/docs/4.17.15#once](https://lodash.com/docs/4.17.15#once)

## overArgs

```js
_.overArgs(func, [transforms=[_.identity]])
```

创建一个函数，调用 `func` 时参数为相对应的 `transforms` 的返回值。

### 参数
- `func (Function)`: 要包裹的函数。

### 返回
- `(Function)`: 返回新函数。

### 例子

```js
function doubled(n) {
    return n * 2;
}

function square(n) {
    return n * n;
}

var func = _.overArgs(function (x, y) {
    return [x, y];
}, [square, doubled]);

func(9, 3);
// => [81, 6]

func(10, 5);
// => [100, 10]
```

### 参考
- [https://lodash.com/docs/4.17.15#overArgs](https://lodash.com/docs/4.17.15#overArgs)

## partial

```js
_.partial(func, [partials])
```

创建一个函数。该函数调用 `func`，并传入预设的 `partials` 参数。这个方法类似 `_.bind`，不同之处在于它不会绑定 `this`。

这个 `_.partial.placeholder` 的值，默认是以 `_` 作为附加部分参数的占位符。

注意：这个方法不会设置 `"length"` 到函数上。

### 参数
- `func (Function)`: 需要预设的函数。
- `[partials] (...*)`: 预设的参数。

### 返回
- `(Function)`: 返回预设参数的函数。

### 例子

```js
function greet(greeting, name) {
    return greeting + ' ' + name;
}

var sayHelloTo = _.partial(greet, 'hello');
sayHelloTo('fred');
// => 'hello fred'

// Partially applied with placeholders.
var greetFred = _.partial(greet, _, 'fred');
greetFred('hi');
// => 'hi fred'
```

### 参考
- [https://lodash.com/docs/4.17.15#partial](https://lodash.com/docs/4.17.15#partial)

## partialRight

```js
_.partialRight(func, [partials])
```

这个函数类似 `_.partial`，不同之处在于预设参数被附加到接受参数的后面。

这个 `_.partialRight.placeholder` 的值，默认是以 `_` 作为附加部分参数的占位符。

注意：这个方法不会设置 `"length"` 到函数上。

### 参数
- `func (Function)`: 需要预设的函数。
- `[partials] (...*)`: 预设的参数。

### 返回
- `(Function)`: 返回预设参数的函数。

### 例子

```js
function greet(greeting, name) {
    return greeting + ' ' + name;
}

var greetFred = _.partialRight(greet, 'fred');
greetFred('hi');
// => 'hi fred'

// Partially applied with placeholders.
var sayHelloTo = _.partialRight(greet, 'hello', _);
sayHelloTo('fred');
// => 'hello fred'
```

### 参考
- [https://lodash.com/docs/4.17.15#partialRight](https://lodash.com/docs/4.17.15#partialRight)

## rearg

```js
_.rearg(func, indexes)
```

创建一个函数，调用 `func` 时，根据指定的 `indexes` 调整对应位置参数。其中第一个索引值是对应第一个参数，第二个索引值是作为第二个参数，依此类推。

### 参数
- `func (Function)`: 待调用的函数。
- `indexes (...(number|number[]))`: 排列参数的位置。

### 返回
- `(Function)`: 返回新的函数。

### 例子

```js
var rearged = _.rearg(function (a, b, c) {
    return [a, b, c];
}, [2, 0, 1]);

rearged('b', 'c', 'a')
// => ['a', 'b', 'c']
```

### 参考
- [https://lodash.com/docs/4.17.15#rearg](https://lodash.com/docs/4.17.15#rearg)

## rest

```js
_.rest(func, [start=func.length-1])
```

创建一个函数，调用 `func` 时，`this` 绑定到创建的新函数，并且 `start` 之后的参数作为数组传入。

注意：这个方法基于 [rest parameter](https://mdn.io/rest_parameters)。

### 参数
- `func (Function)`: 要应用的函数。
- `[start=func.length-1] (number)`: `rest` 参数的开始位置。

### 返回
- `(Function)`: 返回新的函数。

### 例子

```js
var say = _.rest(function (what, names) {
    return what + ' ' + _.initial(names).join(', ') +
        (_.size(names) > 1 ? ', & ' : '') + _.last(names);
});

say('hello', 'fred', 'barney', 'pebbles');
// => 'hello fred, barney, & pebbles'
```

### 参考
- [https://lodash.com/docs/4.17.15#rest](https://lodash.com/docs/4.17.15#rest)

## spread

```js
_.spread(func, [start=0])
```

创建一个函数，调用 `func` 时，`this` 绑定到创建的新函数，把参数作为数组传入，类似于 [Function#apply](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) 。

注意：这个方法基于 [spread operator](https://mdn.io/spread_operator) 。

### 参数
- `func (Function)`: 要应用传播参数的函数。
- `[start=0] (number)`: `spread` 参数的开始位置。

### 返回
- `(Function)`: 返回新的函数。

### 例子

```js
var say = _.spread(function (who, what) {
    return who + ' says ' + what;
});

say(['fred', 'hello']);
// => 'fred says hello'

var numbers = Promise.all([
    Promise.resolve(40),
    Promise.resolve(36)
]);

numbers.then(_.spread(function (x, y) {
    return x + y;
}));
// => a Promise of 76
```

### 参考
- [https://lodash.com/docs/4.17.15#spread](https://lodash.com/docs/4.17.15#spread)

## throttle

```js
_.throttle(func, [wait=0], [options={}])
```

创建一个节流函数，在 `wait` 秒内最多执行 `func` 一次的函数。该函数提供一个 `cancel` 方法取消延迟的函数调用以及 `flush` 方法立即调用。可以提供一个 `options` 对象决定如何调用 `func` 方法，`options.leading` 与/或 `options.trailing` 决定 `wait` 前后如何触发。`func` 会传入最后一次传入的参数给这个函数。随后调用的函数返回是最后一次 `func` 调用的结果。

注意: 如果 `leading` 和 `trailing` 都设定为 `true` 则 `func` 允许 `trailing` 方式调用的条件为: 在 `wait` 期间多次调用。

如果 `wait` 为 `0` 并且 `leading` 为 `false`， `func` 调用将被推迟到下一个点，类似 `setTimeout` 为 `0` 的超时。

查看 [David Corbacho's article](https://css-tricks.com/debouncing-throttling-explained-examples/) 了解 `_.throttle` 与 `_.debounce` 的区别。

### 参数
- `func (Function)`: 要节流的函数。
- `[wait=0] (number)`: 需要节流的毫秒。
- `[options={}] (Object)`: 选项对象。
- `[options.leading=true] (boolean)`: 指定调用在节流开始前。
- `[options.trailing=true] (boolean)`: 指定调用在节流结束后。

### 返回
- `(Function)`: 返回节流的函数。

### 例子

```js
// Avoid excessively updating the position while scrolling.
jQuery(window).on('scroll', _.throttle(updatePosition, 100));

// Invoke `renewToken` when the click event is fired, but not more than once every 5 minutes.
var throttled = _.throttle(renewToken, 300000, { 'trailing': false });
jQuery(element).on('click', throttled);

// Cancel the trailing throttled invocation.
jQuery(window).on('popstate', throttled.cancel);
```

### 参考
- [https://lodash.com/docs/4.17.15#throttle](https://lodash.com/docs/4.17.15#throttle)

## unary

```js
_.unary(func)
```

创建一个最多接受一个参数的函数，忽略多余的参数。

### 参数
- `func (Function)`: 要处理的函数。

### 返回
- `(Function)`: 返回新函数。

### 例子

```js
_.map(['6', '8', '10'], _.unary(parseInt));
// => [6, 8, 10]
```

### 参考
- [https://lodash.com/docs/4.17.15#unary](https://lodash.com/docs/4.17.15#unary)

## wrap

```js
_.wrap(value, [wrapper=identity])
```

创建一个函数。提供的 `value` 包装在 `wrapper` 函数的第一个参数里。任何附加的参数都提供给 `wrapper` 函数。被调用时 `this` 绑定在创建的函数上。

### 参数
- `value (*)`: 要包装的值。
- `[wrapper=identity] (Function)`: 包装函数。

### 返回
- `(Function)`: 返回新的函数。

### 例子

```js
var p = _.wrap(_.escape, function (func, text) {
    return '<p>' + func(text) + '</p>';
});

p('fred, barney, & pebbles');
// => '<p>fred, barney, &amp; pebbles</p>'
```

### 参考
- [https://lodash.com/docs/4.17.15#wrap](https://lodash.com/docs/4.17.15#wrap)

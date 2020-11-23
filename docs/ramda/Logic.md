## allPass
传入包含多个 `predicate` 的列表，返回一个 `predicate`：如果给定的参数满足列表中的所有 `predicate` ，则返回 `true`。

该函数返回一个柯里化的函数，参数个数由列表中参数最多的 `predicate` 决定。

### 参数

```
[(*… → Boolean)] → (*… → Boolean)
```

- `predicates`：一系列要检查的谓词函数。
- `function`：组合谓词函数。

### 例子

```js
const isQueen = R.propEq('rank', 'Q');
const isSpade = R.propEq('suit', '♠︎');
const isQueenOfSpades = R.allPass([isQueen, isSpade]);

isQueenOfSpades({ rank: 'Q', suit: '♣︎' }); //=> false
isQueenOfSpades({ rank: 'Q', suit: '♠︎' }); //=> true
```

### 参考
- [https://ramdajs.com/docs/#allPass](https://ramdajs.com/docs/#allPass)

## and
如果两个参数都是 `true`，则返回 `true`；否则返回 `false`。

### 参数

```
a → b → a | b
```

- `a`。
- `b`。
- 返回 `Any`：如果第一个参数是 `falsy` 则返回它，否则返回第二个参数。

### 例子

```js
R.and(true, true); //=> true
R.and(true, false); //=> false
R.and(false, true); //=> false
R.and(false, false); //=> false
```

### 参考
- [https://ramdajs.com/docs/#and](https://ramdajs.com/docs/#and)

## anyPass
传入包含多个 `predicate` 的列表，返回一个 `predicate`：只要给定的参数满足列表中的一个 `predicate` ，就返回 `true`。

该函数返回一个柯里化的函数，参数个数由列表中参数最多的 `predicate` 决定。

### 参数

```
[(*… → Boolean)] → (*… → Boolean)
```

- `predicates`：一系列要检查的谓词函数。
- `function`：组合谓词函数。

### 例子

```js
const isClub = R.propEq('suit', '♣');
const isSpade = R.propEq('suit', '♠');
const isBlackCard = R.anyPass([isClub, isSpade]);

isBlackCard({ rank: '10', suit: '♣' }); //=> true
isBlackCard({ rank: 'Q', suit: '♠' }); //=> true
isBlackCard({ rank: 'Q', suit: '♦' }); //=> false
```

### 参考
- [https://ramdajs.com/docs/#anyPass](https://ramdajs.com/docs/#anyPass)

## both
该函数调用两个函数，并对两函数返回值进行与操作。若第一个函数结果为 `false-y` 值，则返回该结果，否则返回第二个函数的结果。注意，`both` 为短路操作，即如果第一个函数返回 `false-y` 值，则不会调用第二个函数。

除了函数，`R.both` 还接受任何兼容 `fantasy-land` 的 `applicative functor`。

### 参数

```
(*… → Boolean) → (*… → Boolean) → (*… → Boolean)
```

- `f`：一个谓词函数。
- `g`：另一个谓词函数。
- `function`：一个函数，将其参数应用于 `f` 和 `g` 并对两函数返回值进行 `&&` 操作。

### 例子

```js
const gt10 = R.gt(R.__, 10)
const lt20 = R.lt(R.__, 20)
const f = R.both(gt10, lt20);
f(15); //=> true
f(30); //=> false

R.both(Maybe.Just(false), Maybe.Just(55)); // => Maybe.Just(false)
R.both([false, false, 'a'], [11]); //=> [false, false, 11]
```

### 参考
- [https://ramdajs.com/docs/#both](https://ramdajs.com/docs/#both)

## complement
对函数的返回值取反。接受一个函数 `f`，返回一个新函数 `g`：在输入参数相同的情况下，若 `f` 返回 `true-y` ，则 `g` 返回 `false-y` ，反之亦然。

`R.complement` 可用于任何 `functor`。

### 参数

```
(*… → *) → (*… → Boolean)
```

- `f`。
- 返回 `function`。

### 例子

```js
const isNotNil = R.complement(R.isNil);
isNil(null); //=> true
isNotNil(null); //=> false
isNil(7); //=> false
isNotNil(7); //=> true
```

### 参考
- [https://ramdajs.com/docs/#complement](https://ramdajs.com/docs/#complement)

## cond
返回一个封装了 `if / else，if / else, ...` 逻辑的函数 `fn`。`R.cond` 接受列表元素为 `[predicate，transformer]` 的列表。`fn` 的所有参数顺次作用于每个 `predicate`，直到有一个返回 `truthy` 值，此时相应 `transformer` 对参数处理，并作为 `fn` 的结果返回。如果没有 `predicate` 匹配，则 `fn` 返回 `undefined`。

### 参数

```
[[(*… → Boolean),(*… → *)]] → (*… → *)
```

- `pairs`：`[predicate, transformer]` 列表。
- 返回 `function`。

### 例子

```js
const fn = R.cond([
    [R.equals(0), R.always('water freezes at 0°C')],
    [R.equals(100), R.always('water boils at 100°C')],
    [R.T, temp => 'nothing special happens at ' + temp + '°C']
]);
fn(0); //=> 'water freezes at 0°C'
fn(50); //=> 'nothing special happens at 50°C'
fn(100); //=> 'water boils at 100°C'
```

### 参考
- [https://ramdajs.com/docs/#cond](https://ramdajs.com/docs/#cond)

## defaultTo
如果第二个参数不是 `null`、`undefined` 或 `NaN`，则返回第二个参数，否则返回第一个参数（默认值）。

### 参数

```
a → b → a | b
```

- `default`：默认值。
- `val`：除非 `val` 为 `null`，`undefined` 或 `NaN`，否则将返回 `val` 而不是默认值。
- `*`：第二个值（如果不是 `null`，`undefined` 或 `NaN`），否则为默认值。

### 例子

```js
const defaultTo42 = R.defaultTo(42);

defaultTo42(null);  //=> 42
defaultTo42(undefined);  //=> 42
defaultTo42(false);  //=> false
defaultTo42('Ramda');  //=> 'Ramda'
// parseInt('string') results in NaN
defaultTo42(parseInt('string')); //=> 42
```

### 参考
- [https://ramdajs.com/docs/#defaultTo](https://ramdajs.com/docs/#defaultTo)

## either
返回由 `||` 运算符连接的两个函数的包装函数。如果两个函数中任一函数的执行结果为 `truth-y`，则返回其执行结果。注意，这个是短路表达式，意味着如果第一个函数返回 `truth-y` 值的话，第二个函数将不会执行。

除了函数之外，`R.either` 也接受任何符合 `fantasy-land` 标准的 `applicative functor` 。

### 参数

```
(*… → Boolean) → (*… → Boolean) → (*… → Boolean)
```

- `f`：一个谓词函数。
- `g`：另一个谓词函数。
- `function`：一个函数，将其参数应用于 `f` 和 `g` 并对两函数返回值进行 `||` 操作。

### 例子

```js
const gt10 = x => x > 10;
const even = x => x % 2 === 0;
const f = R.either(gt10, even);
f(101); //=> true
f(8); //=> true

R.either(Maybe.Just(false), Maybe.Just(55)); // => Maybe.Just(55)
R.either([false, false, 'a'], [11]) // => [11, 11, "a"]
```

### 参考
- [https://ramdajs.com/docs/#either](https://ramdajs.com/docs/#either)

## ifElse
根据 `condition` 谓词函数的返回值调用 `onTrue` 或 `onFalse` 函数。

### 参数

```
(*… → Boolean) → (*… → *) → (*… → *) → (*… → *)
```

- `condition`：谓词函数。
- `onTrue`：当 `condition` 评估为 `truthy` 时要调用的函数。
- `onFalse`：当 `condition` 评估为 `falsy` 时要调用的函数。
- 返回 `function`：一个新的函数，它将根据 `condition` 谓词函数的结果来处理 `onTrue` 或 ` onFalse` 函数。

### 例子

```js
const incCount = R.ifElse(
    R.has('count'),
    R.over(R.lensProp('count'), R.inc),
    R.assoc('count', 1)
);
incCount({});           //=> { count: 1 }
incCount({ count: 1 }); //=> { count: 2 }
```

### 参考
- [https://ramdajs.com/docs/#ifElse](https://ramdajs.com/docs/#ifElse)

## isEmpty
检测给定值是否为其所属类型的空值，若是则返回 `true` ；否则返回 `false` 。

### 参数

```
a → Boolean
```

- `x`。
- 返回 `Boolean`。

### 例子

```js
R.isEmpty([1, 2, 3]);   //=> false
R.isEmpty([]);          //=> true
R.isEmpty('');          //=> true
R.isEmpty(null);        //=> false
R.isEmpty({});          //=> true
R.isEmpty({length: 0}); //=> false
```

### 参考
- [https://ramdajs.com/docs/#isEmpty](https://ramdajs.com/docs/#isEmpty)

## not
逻辑非运算。 当传入参数为 `false-y` 值时，返回 `true`；`truth-y` 值时，返回 `false`。

### 参数

```
* → Boolean
```

- `a`：任何值。
- 返回 `Boolean`：传递参数的逻辑非。

### 例子

```js
R.not(true); //=> false
R.not(false); //=> true
R.not(0); //=> true
R.not(1); //=> false
```

### 参考
- [https://ramdajs.com/docs/#not](https://ramdajs.com/docs/#not)

## or
逻辑或运算，只要有一个参数为真（`truth-y`），就返回 `true`；否则返回 `false`。

### 参数

```
a → b → a | b
```

- `a`。
- `b`。
- 返回 `Any`：第一个参数为真时未第一个参数，否则为第二个参数。

### 例子

```js
R.or(true, true); //=> true
R.or(true, false); //=> true
R.or(false, true); //=> true
R.or(false, false); //=> false
```

### 参考
- [https://ramdajs.com/docs/#or](https://ramdajs.com/docs/#or)

## pathSatisfies
如果对象的给定路径上的属性满足 `predicate`，返回 `ture`；否则返回 `false`。

### 参数

```
(a → Boolean) → [Idx] → {a} → Boolean
Idx = String | Int
```

- `pred`。
- `propPath`。
- `obj`。
- 返回 `Boolean`。

### 例子

```js
R.pathSatisfies(y => y > 0, ['x', 'y'], {x: {y: 2}}); //=> true
R.pathSatisfies(R.is(Object), [], {x: {y: 2}}); //=> true
```

### 参考
- [https://ramdajs.com/docs/#pathSatisfies](https://ramdajs.com/docs/#pathSatisfies)

## propSatisfies
如果指定的对象属性满足 `predicate`，返回 `true`；否则返回 `false`。可以使用 `R.where` 进行多个属性的判断。

### 参数

```
(a → Boolean) → String → {String: a} → Boolean
```

- `pred`。
- `name`。
- `obj`。
- 返回 `Boolean`。

### 例子

```js
R.propSatisfies(x => x > 0, 'x', {x: 1, y: 2}); //=> true
```

### 参考
- [https://ramdajs.com/docs/#propSatisfies](https://ramdajs.com/docs/#propSatisfies)

## unless
判断输入值是否满足 `predicate`，若不符合，则将输入值传给 `whenFalseFn` 处理，并将处理结果作为返回；若符合，则将输入值原样返回。

### 参数

```
(a → Boolean) → (a → a) → a → a
```

- `pred`：谓词函数。
- `whenFalseFn`：当 `pred` 计算为假值时要调用的函数。
- `x`：要使用 `pred` 函数进行测试的对象，并在必要时传递给 `whenFalseFn`。
- `*`：要么是 `x`，要么是是对 `whenFalseFn` 应用 `x` 的结果。

### 例子

```js
let safeInc = R.unless(R.isNil, R.inc);
safeInc(null); //=> null
safeInc(1); //=> 2
```

### 参考
- [https://ramdajs.com/docs/#unless](https://ramdajs.com/docs/#unless)

## until
接受一个 `predicate` ，`transform function` 和 初始值，返回一个与初始值相同类型的值。对输入值进行 `transform` ，直到 `transform` 的结果满足 `predicate`，此时返回这个满足 `predicate` 的值。

### 参数

```
(a → Boolean) → (a → a) → a → a
```

- `pred`：谓词函数。
- `fn`：迭代器函数。
- `init`：初始值
- 返回 `*`：满足谓词函数的最终值

### 例子

```js
R.until(R.gt(R.__, 100), R.multiply(2))(1) // => 128
```

### 参考
- [https://ramdajs.com/docs/#until](https://ramdajs.com/docs/#until)

## when
判断输入值是否满足 `predicate`，若符合，则将输入值传给 `whenTrueFn` 处理，并将处理结果作为返回；若不符合，则将输入值原样返回。

### 参数

```
(a → Boolean) → (a → a) → a → a
```

- `pred`：谓词函数。
- `whenTrueFn`：当条件评估为真值时要调用的函数。
- `x`：要使用 `pred` 函数进行测试的对象，并在必要时传递给 `whenTrueFn`。
- 返回 `*`：`x` 或将 `x` 应用于 `whenTrueFn` 的结果。

### 例子

```js
// truncate :: String -> String
const truncate = R.when(
    R.propSatisfies(R.gt(R.__, 10), 'length'),
    R.pipe(R.take(10), R.append('…'), R.join(''))
);
truncate('12345');         //=> '12345'
truncate('0123456789ABC'); //=> '0123456789…'
```

### 参考
- [https://ramdajs.com/docs/#when](https://ramdajs.com/docs/#when)

## xor
异或操作。如果其中一个参数为真，另一个参数为假，则返回 `true` ；否则返回 `false`。

### 参数

```
a → b → Boolean
```

- `a`
- `b`
- 返回 `Boolean`：如果其中一个参数为真，另一个参数为假，则为真。

### 例子

```js
R.xor(true, true); //=> false
R.xor(true, false); //=> true
R.xor(false, true); //=> true
R.xor(false, false); //=> false
```

### 参考
- [https://ramdajs.com/docs/#xor](https://ramdajs.com/docs/#xor)

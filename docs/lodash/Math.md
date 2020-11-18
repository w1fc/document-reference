## add

```js
_.add(augend, addend)
```

两个数相加。

### 参数
- `augend (number)`: 相加的第一个数。
- `addend (number)`: 相加的第二个数。

### 返回
- `(number)`: 返回总和。

### 例子

```js
_.add(6, 4);
// => 10
```

### 参考
- [https://lodash.com/docs/4.17.15#add](https://lodash.com/docs/4.17.15#add)

## ceil

```js
_.ceil(number, [precision=0])
```

根据精度 `precision` 向上舍入 `number`。（注：精度可以理解为保留几位小数。）

### 参数
- `number (number)`: 要向上舍入的值。
- `[precision=0] (number)`: 向上舍入的的精度。

### 返回
- `(number)`: 返回向上舍入的值。

### 例子

```js
_.ceil(4.006);
// => 5

_.ceil(6.004, 2);
// => 6.01

_.ceil(6040, -2);
// => 6100
```

### 参考
- [https://lodash.com/docs/4.17.15#ceil](https://lodash.com/docs/4.17.15#ceil)

## divide

```js
_.divide(dividend, divisor)
```

两个数相除。

### 参数
- `dividend (number)`: 相除的第一个数。
- `divisor (number)`: 相除的第二个数。

### 返回
- `(number)`: 返回商数。

### 例子

```js
_.divide(6, 4);
// => 1.5
```

### 参考
- [https://lodash.com/docs/4.17.15#divide](https://lodash.com/docs/4.17.15#divide)

## floor

```js
_.floor(number, [precision=0])
```

根据精度 `precision` 向下舍入 `number`。

### 参数
- `number (number)`: 要向下舍入的值。
- `[precision=0] (number)`: 向下舍入的精度。

### 返回
- `(number)`: 返回向下舍入的值。

### 例子

```js
_.floor(4.006);
// => 4

_.floor(0.046, 2);
// => 0.04

_.floor(4060, -2);
// => 4000
```

### 参考
- [https://lodash.com/docs/4.17.15#floor](https://lodash.com/docs/4.17.15#floor)

## max

```js
_.max(array)
```

计算 `array` 中的最大值。如果 `array` 是空的或者假值将会返回 `undefined`。

### 参数
- `array (Array)`: 要迭代的数组。

### 返回
- `(*)`: 返回最大的值。

### 例子

```js
_.max([4, 2, 8, 6]);
// => 8

_.max([]);
// => undefined
```

### 参考
- [https://lodash.com/docs/4.17.15#max](https://lodash.com/docs/4.17.15#max)

## maxBy

```js
_.maxBy(array, [iteratee=_.identity])
```

这个方法类似 `_.max`, 不同之处在于它接受 `iteratee` 来调用 `array` 中的每一个元素，来生成其值排序的标准。`iteratee` 会调用 1 个参数: `(value)` 。

### 参数
- `array (Array)`: 要迭代的数组。
- `[iteratee=_.identity] (Function)`: 调用每个元素的迭代函数。

### 返回
- `(*)`: 返回最大的值。

### 例子

```js
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.maxBy(objects, function (o) { return o.n; });
// => { 'n': 2 }

// The `_.property` iteratee shorthand.
_.maxBy(objects, 'n');
// => { 'n': 2 }
```

### 参考
- [https://lodash.com/docs/4.17.15#maxBy](https://lodash.com/docs/4.17.15#maxBy)

## mean

```js
_.mean(array)
```

计算 `array` 的平均值。

### 参数
- `array (Array)`: 要迭代的数组。

### 返回
- `(number)`: 返回平均值。

### 例子

```js
_.mean([4, 2, 8, 6]);
// => 5
```

### 参考
- [https://lodash.com/docs/4.17.15#mean](https://lodash.com/docs/4.17.15#mean)

## meanBy

```js
_.meanBy(array, [iteratee=_.identity])
```

这个方法类似 `_.mean`，不同之处在于它接受 `iteratee` 来调用 `array` 中的每一个元素，来生成其值排序的标准。`iteratee` 会调用 1 个参数: `(value)` 。

### 参数
- `array (Array)`: 要迭代的数组。
- `[iteratee=_.identity] (Function)`: 调用每个元素的迭代函数。

### 返回
- `(number)`: 返回平均值。

### 例子

```js
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.meanBy(objects, function (o) { return o.n; });
// => 5

// The `_.property` iteratee shorthand.
_.meanBy(objects, 'n');
// => 5
```

### 参考
- [https://lodash.com/docs/4.17.15#meanBy](https://lodash.com/docs/4.17.15#meanBy)

## min

```js
_.min(array)
```

计算 `array` 中的最小值。如果 `array` 是空的或者假值将会返回 `undefined`。

### 参数
- `array (Array)`: 要迭代的数组。

### 返回
- `(*)`: 返回最小的值。

### 例子

```js
_.min([4, 2, 8, 6]);
// => 2

_.min([]);
// => undefined
```

### 参考
- [https://lodash.com/docs/4.17.15#min](https://lodash.com/docs/4.17.15#min)

## minBy

```js
_.minBy(array, [iteratee=_.identity])
```

这个方法类似 `_.min`， 不同之处在于它接受 `iteratee` 来调用 `array` 中的每一个元素，来生成其值排序的标准。`iteratee` 会调用 1 个参数: `(value)` 。

### 参数
- `array (Array)`: 要迭代的数组。
- `[iteratee=_.identity] (Function)`: 调用每个元素的迭代函数。

### 返回
- `(*)`: 返回最小的值。

### 例子

```js
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.minBy(objects, function (o) { return o.n; });
// => { 'n': 1 }

// The `_.property` iteratee shorthand.
_.minBy(objects, 'n');
// => { 'n': 1 }
```

### 参考
- [https://lodash.com/docs/4.17.15#minBy](https://lodash.com/docs/4.17.15#minBy)

## multiply

```js
_.multiply(multiplier, multiplicand)
```

两个数相乘。


### 参数
- `augend (number)`: 相乘的第一个数。
- `addend (number)`: 相乘的第二个数。

### 返回
- `(number)`: 返回乘积。

### 例子

```js
_.multiply(6, 4);
// => 24
```

### 参考
- [https://lodash.com/docs/4.17.15#multiply](https://lodash.com/docs/4.17.15#multiply)

## round

```js
_.round(number, [precision=0])
```

根据精度 `precision` 四舍五入 `number`。

### 参数
- `number (number)`: 要四舍五入的数字。
- `[precision=0] (number)`: 四舍五入的精度。

### 返回
- `(number)`: 返回四舍五入的数字。

### 例子

```js
_.round(4.006);
// => 4

_.round(4.006, 2);
// => 4.01

_.round(4060, -2);
// => 4100
```

### 参考
- [https://lodash.com/docs/4.17.15#round](https://lodash.com/docs/4.17.15#round)

## subtract

```js
_.subtract(minuend, subtrahend)
```

两数相减。

### 参数
- `minuend (number)`: 相减的第一个数。
- `subtrahend (number)`: 相减的第二个数。

### 返回
- `(number)`: 返回差。

### 例子

```js
_.subtract(6, 4);
// => 2
```

### 参考
- [https://lodash.com/docs/4.17.15#subtract](https://lodash.com/docs/4.17.15#subtract)

## sum

```js
_.sum(array)
```

计算 `array` 中值的总和。

### 参数
- `array (Array)`: 要迭代的数组。

### 返回
- `(number)`: 返回总和。

### 例子

```js
_.sum([4, 2, 8, 6]);
// => 20
```

### 参考
- [https://lodash.com/docs/4.17.15#sum](https://lodash.com/docs/4.17.15#sum)

## sumBy

```js
_.sumBy(array, [iteratee=_.identity])
```

这个方法类似 `_.sum`，不同之处在于它接受 `iteratee` 来调用 `array` 中的每一个元素，来生成其值排序的标准。`iteratee` 会调用 1 个参数: `(value)` 。

### 参数
- `array (Array)`: 要迭代的数组。
- `[iteratee=_.identity] (Function)`: 调用每个元素的迭代函数。

### 返回
- `(number)`: 返回总和。

### 例子

```js
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.sumBy(objects, function (o) { return o.n; });
// => 20

// The `_.property` iteratee shorthand.
_.sumBy(objects, 'n');
// => 20
```

### 参考
- [https://lodash.com/docs/4.17.15#sumBy](https://lodash.com/docs/4.17.15#sumBy)

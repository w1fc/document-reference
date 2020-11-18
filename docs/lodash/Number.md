## clamp

```js
_.clamp(number, [lower], upper)
```

返回限制在 `lower` 和 `upper` 之间的值。

### 参数
- `number (number)`: 被限制的值。
- `[lower] (number)`: 下限。
- `upper (number)`: 上限。

### 返回
- `(number)`: 返回被限制的值。

### 例子

```js
_.clamp(-10, -5, 5);
// => -5

_.clamp(10, -5, 5);
// => 5
```

### 参考
- [https://lodash.com/docs/4.17.15#clamp](https://lodash.com/docs/4.17.15#clamp)

## inRange

```js
_.inRange(number, [start=0], end)
```

检查 `n` 是否在 `start` 与 `end` 之间，但不包括 `end`。 如果 `end` 没有指定，那么 `start` 设置为 `0`。如果 `start` 大于 `end`，那么参数会交换以便支持负范围。

### 参数
- `number (number)`: 要检查的值。
- `[start=0] (number)`: 开始范围。
- `end (number)`: 结束范围。

### 返回
- `(boolean)`: 如果 `number` 在范围内 ，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.inRange(3, 2, 4);
// => true

_.inRange(4, 8);
// => true

_.inRange(4, 2);
// => false

_.inRange(2, 2);
// => false

_.inRange(1.2, 2);
// => true

_.inRange(5.2, 4);
// => false

_.inRange(-3, -2, -6);
// => true
```

### 参考
- [https://lodash.com/docs/4.17.15#inRange](https://lodash.com/docs/4.17.15#inRange)

## random

```js
_.random([lower=0], [upper=1], [floating])
```

产生一个包括 `lower` 与 `upper` 之间的数。如果只提供一个参数返回一个 0 到提供数之间的数。如果 `floating` 设为 `true`，或者 `lower` 或 `upper` 是浮点数，结果返回浮点数。

注意: JavaScript 遵循 IEEE-754 标准处理无法预料的浮点数结果。

### 参数
- `[lower=0] (number)`: 下限。
- `[upper=1] (number)`: 上限。
- `[floating] (boolean)`: 指定是否返回浮点数。

### 返回
- `(number)`: 返回随机数。

### 例子

```js
_.random(0, 5);
// => an integer between 0 and 5

_.random(5);
// => also an integer between 0 and 5

_.random(5, true);
// => a floating-point number between 0 and 5

_.random(1.2, 5.2);
// => a floating-point number between 1.2 and 5.2
```

### 参考
- [https://lodash.com/docs/4.17.15#random](https://lodash.com/docs/4.17.15#random)


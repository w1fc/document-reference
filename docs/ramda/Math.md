## add
两数相加。

### 参数

```
Number → Number → Number
```

- `a`。
- `b`。
- 返回 `Number`。

### 例子

```js
R.add(2, 3);       //=>  5
R.add(7)(10);      //=> 17
```

### 参考
- [https://ramdajs.com/docs/#add](https://ramdajs.com/docs/#add)

## dec
减1。

### 参数

```
Number → Number
```

- `n`。
- 返回 `Number`：`n - 1`。

### 例子

```js
R.dec(42); //=> 41
```

### 参考
- [https://ramdajs.com/docs/#dec](https://ramdajs.com/docs/#dec)

## divide
两数相除。等价于 `a / b`。

### 参数

```
Number → Number → Number
```

- `a`：第一个值。
- `b`：第二个值。
- 返回 `Number`：`a / b` 的结果。

### 例子

```js
R.divide(71, 100); //=> 0.71

const half = R.divide(R.__, 2);
half(42); //=> 21

const reciprocal = R.divide(1);
reciprocal(4);   //=> 0.25
```

### 参考
- [https://ramdajs.com/docs/#divide](https://ramdajs.com/docs/#divide)

## inc
加1。

### 参数

```
Number → Number
```

- `n`。
- 返回 `Number`：`n + 1`。

### 例子

```js
R.inc(42); //=> 43
```

### 参考
- [https://ramdajs.com/docs/#inc](https://ramdajs.com/docs/#inc)

## mathMod
`mathMod` 和算术取模操作类似，而不像 `%` 操作符（或 `R.modulo`）。所以 `-17 % 5` 等于 `-2`，而 `mathMod(-17, 5)` 等于 `3` 。`mathMod` 要求参数为整型，并且当模数等于 `0` 或者负数时返回 `NaN` 。

### 参数

```
Number → Number → Number
```

- `m`：被除数。
- `p`：模数。
- `Number`：`b mod a`的结果。

### 例子

```js
R.mathMod(-17, 5);  //=> 3
R.mathMod(17, 5);   //=> 2
R.mathMod(17, -5);  //=> NaN
R.mathMod(17, 0);   //=> NaN
R.mathMod(17.2, 5); //=> NaN
R.mathMod(17, 5.3); //=> NaN

const clock = R.mathMod(R.__, 12);
clock(15); //=> 3
clock(24); //=> 0

const seventeenMod = R.mathMod(17);
seventeenMod(3);  //=> 2
seventeenMod(4);  //=> 1
seventeenMod(10); //=> 7
```

### 参考
- [https://ramdajs.com/docs/#mathMod](https://ramdajs.com/docs/#mathMod)

## mean
返回给定数字列表的平均值。

### 参数

```
[Number] → Number
```

- `list`。
- 返回 `Number`。

### 例子

```js
R.mean([2, 7, 9]); //=> 6
R.mean([]); //=> NaN
```

### 参考
- [https://ramdajs.com/docs/#mean](https://ramdajs.com/docs/#mean)

## median
返回给定数字列表的中位数。

### 参数

```
[Number] → Number
```

- `list`。
- 返回 `Number`。

### 例子

```js
R.median([2, 9, 7]); //=> 7
R.median([7, 2, 10, 9]); //=> 8
R.median([]); //=> NaN
```

### 参考
- [https://ramdajs.com/docs/#median](https://ramdajs.com/docs/#median)

## modulo
用第一个参数除以第二个参数，并返回余数。注意，该函数是 JavaScript-style 的求模操作。数学求模另见 `mathMod`。

### 参数

```
Number → Number → Number
```

- `a`：被除数。
- `b`：伪模数。
- 返回 `Number`：`b % a`的结果。

### 例子

```js
R.modulo(17, 3); //=> 2
// JS behavior:
R.modulo(-17, 3); //=> -2
R.modulo(17, -3); //=> 2

const isOdd = R.modulo(R.__, 2);
isOdd(42); //=> 0
isOdd(21); //=> 1
```

### 参考
- [https://ramdajs.com/docs/#modulo](https://ramdajs.com/docs/#modulo)

## multiply
两数相乘，等价于柯里化的 `a * b` 。

### 参数

```
Number → Number → Number
```

- `a`：第一个值。
- `b`：第二个值。
- 返回 `Number`：`a * b` 的结果。

### 例子

```js
const double = R.multiply(2);
const triple = R.multiply(3);
double(3);       //=>  6
triple(4);       //=> 12
R.multiply(2, 5);  //=> 10
```

### 参考
- [https://ramdajs.com/docs/#multiply](https://ramdajs.com/docs/#multiply)

## negate
取反操作。

### 参数

```
Number → Number
```

- `n`。
- 返回 `Number`。

### 例子

```js
R.negate(42); //=> -42
```

### 参考
- [https://ramdajs.com/docs/#negate](https://ramdajs.com/docs/#negate)

## product
列表中的所有元素相乘。

### 参数

```
[Number] → Number
```

- `list`：数字列表。
- 返回 `Number`：列表中所有数字的乘积。

### 例子

```js
R.product([2,4,6,8,100,1]); //=> 38400
```

### 参考
- [https://ramdajs.com/docs/#product](https://ramdajs.com/docs/#product)

## subtract
首个参数减去第二个参数。

### 参数

```
Number → Number → Number
```

- `a`：第一个值。
- `b`：第二个值。
- 返回 `Number`：`a * b` 的结果。

### 例子

```js
R.subtract(10, 8); //=> 2

const minus5 = R.subtract(R.__, 5);
minus5(17); //=> 12

const complementaryAngle = R.subtract(90);
complementaryAngle(30); //=> 60
complementaryAngle(72); //=> 18
```

### 参考
- [https://ramdajs.com/docs/#subtract](https://ramdajs.com/docs/#subtract)

## sum
对数组中所有元素求和。

### 参数
```
[Number] → Number
```

- `list`：数字列表。
- 返回 `Number`：列表中所有数字的和。

### 例子

```js
R.sum([2,4,6,8,100,1]); //=> 121
```

### 参考
- [https://ramdajs.com/docs/#sum](https://ramdajs.com/docs/#sum)

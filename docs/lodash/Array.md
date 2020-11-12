## chunk

```js
_.chunk(array, [size=1])
```

将 `array` 拆分成多个 `size` 长度的区块，并将这些区块组成一个新数组。如果 `array` 无法被分割成全部等长的区块，那么最后剩余的元素将组成一个区块。

### 参数
- `array (Array)`: 需要处理的数组。
- `[size=1] (number)`: 每个数组区块的长度。

### 返回
- `(Array)`: 返回一个包含拆分区块的新数组。

### 例子

```js
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]
 
_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

### 参考
- [https://lodash.com/docs/4.17.15#chunk](https://lodash.com/docs/4.17.15#chunk)

## compact

```js
_.compact(array)
```

创建一个新数组，包含原数组中所有的非假值元素。例如 `false`, `null`, `0`, `""`, `undefined`, 和 `NaN` 都是被认为是“假值”。

### 参数
- `array (Array)`: 待处理的数组。

### 返回
- `(Array)`: 返回过滤掉假值的新数组。

### 例子

```js
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

### 参考
- [https://lodash.com/docs/4.17.15#compact](https://lodash.com/docs/4.17.15#compact)

## concat

```js
_.concat(array, [values])
```

创建一个新数组，将 `array` 与任何**数组或值**连接在一起。

### 参数
- `array (Array)`: 被连接的数组。
- `[values] (...*)`: 连接的值。

### 返回
- `(Array)`: 返回连接后的新数组。

### 例子

```js
var array = [1];
var other = _.concat(array, 2, [3], [[4]]);

console.log(other);
// => [1, 2, 3, [4]]

console.log(array);
// => [1]
```

### 参考
- [https://lodash.com/docs/4.17.15#concat](https://lodash.com/docs/4.17.15#concat)


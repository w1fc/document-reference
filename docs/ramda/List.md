## adjust
将数组中指定索引处的值替换为经函数变换的值。

### 参数

```
Number → (a → a) → [a] → [a]
```

- `idx`：索引。
- `fn`：要应用的函数。
- `list`：类数组对象，其提供的索引处的值将被替换。
- 返回 `Array`：所提供的类数组对象的副本，其中元素在索引 `idx` 处被替换为通过对现有元素应用 `fn` 返回的值。

### 例子

```js
R.adjust(1, R.toUpper, ['a', 'b', 'c', 'd']);      //=> ['a', 'B', 'c', 'd']
R.adjust(-1, R.toUpper, ['a', 'b', 'c', 'd']);     //=> ['a', 'b', 'c', 'D']
```

### 参考
- [https://ramdajs.com/docs/#adjust](https://ramdajs.com/docs/#adjust)

## all
如果列表中的所有元素都满足 `predicate`，则返回 `true`；否则返回 `false`。

若第二个参数自身存在 `all` 方法，则调用自身的 `all` 方法。

若在列表位置中给出 `transfomer`，则用作 `transducer` 。

### 参数

```
(a → Boolean) → [a] → Boolean
```

- `fn`：谓词函数。
- `list`：要检验的数组。
- 返回 `Boolean`：如果每个元素都满足该谓词函数，则返回布尔值 `true`，否则返回 `false`。

### 例子

```js
const equals3 = R.equals(3);
R.all(equals3)([3, 3, 3, 3]); //=> true
R.all(equals3)([3, 3, 1, 3]); //=> false
```

### 参考
- [https://ramda.cn/docs/#all](https://ramda.cn/docs/#all)

## any
只要列表中有一个元素满足 `predicate`，就返回 `true`，否则返回 `false`。

若第二个参数自身存在 `any` 方法，则调用其自身的 `any`。

若在列表位置中给出 `transfomer`，则用作 `transducer` 。

### 参数

```
(a → Boolean) → [a] → Boolean
```

- `fn`：谓词函数。
- `list`：要检验的数组。
- 返回 `Boolean`：如果谓词至少被一个元素满足，则为 `true`；否则为 `false`。

### 例子

```js
const lessThan0 = R.flip(R.lt)(0);
const lessThan2 = R.flip(R.lt)(2);
R.any(lessThan0)([1, 2]); //=> false
R.any(lessThan2)([1, 2]); //=> true
```

### 参考
- [https://ramdajs.com/docs/#any](https://ramdajs.com/docs/#any)

## aperture
返回一个新列表，列表中的元素为由原列表相邻元素组成的 `n` 元组。如果 `n` 大于列表的长度，则返回空列表。

若在列表位置中给出 `transfomer`，则用作 `transducer` 。

### 参数

```
Number → [a] → [[a]]
```

- `n`：创建的元组的大小。
- `list`：要拆分为 `n` 长度元组的列表。
- 返回 `Array`：`n` 长度元组的结果列表。

### 例子

```js
R.aperture(2, [1, 2, 3, 4, 5]); //=> [[1, 2], [2, 3], [3, 4], [4, 5]]
R.aperture(3, [1, 2, 3, 4, 5]); //=> [[1, 2, 3], [2, 3, 4], [3, 4, 5]]
R.aperture(7, [1, 2, 3, 4, 5]); //=> []
```

### 参考
- [https://ramdajs.com/docs/#aperture](https://ramdajs.com/docs/#aperture)

## append
在列表末尾拼接一个元素。

### 参数

```
a → [a] → [a]
```

- `el`：要添加到新列表末尾的元素。
- `list`：要添加新项目的元素列表。
- 返回 `Array`：一个新列表，包含旧列表的元素和 `el`。

### 例子

```js
R.append('tests', ['write', 'more']); //=> ['write', 'more', 'tests']
R.append('tests', []); //=> ['tests']
R.append(['tests'], ['write', 'more']); //=> ['write', 'more', ['tests']]
```

### 参考
- [https://ramdajs.com/docs/#append](https://ramdajs.com/docs/#append)

## chain
`chain` 将函数映射到列表中每个元素，并将结果连接起来。`chain` 在一些库中也称为 `flatMap`（先 `map` 再 `flatten` ）。

若第二个参数存在 `chain` 方法，则调用其自身的 `chain` 方法。该参数需符合 [FantasyLand Chain 规范](https://github.com/fantasyland/fantasy-land#chain)。

如果第二个参数是函数，`chain(f, g)(x)` 等价于 `f(g(x), x)`。

若在列表位置中给出 `transfomer`，则用作 `transducer`。

### 参数

```
Chain m => (a → m b) → m a → m b
```

- `fn`：用于映射的函数。
- `list`：要映射的列表。
- 返回 `Array`：用 `fn` 映射 `list` 的结果。

### 例子

```js
const duplicate = n => [n, n];
R.chain(duplicate, [1, 2, 3]); //=> [1, 1, 2, 2, 3, 3]

R.chain(R.append, R.head)([1, 2, 3]); //=> [1, 2, 3, 1]
```

### 参考
- [https://ramdajs.com/docs/#chain](https://ramdajs.com/docs/#chain)

## concat
连接列表或字符串。

注意：不同于 `Array.prototype.concat`, `R.concat` 要求两个参数类型相同。如果将 `Array` 与非 `Array` 连接，将抛出错误。

若第一个参数自身存在 `concat` 方法，则调用自身的 `concat`。

也可以用于连接符合 [fantasy-land 半群](https://github.com/fantasyland/fantasy-land#semigroup) 类型的两个实例。

### 参数

```
[a] → [a] → [a]
String → String → String
```

- `firstList`：第一个列表。
- `secondList`：第二个列表。
- 返回 `Array`：由 `firstList` 元素和 `secondList` 元素组成的列表。

### 例子

```js
R.concat('ABC', 'DEF'); // 'ABCDEF'
R.concat([4, 5, 6], [1, 2, 3]); //=> [4, 5, 6, 1, 2, 3]
R.concat([], []); //=> []
```

### 参考
- [https://ramdajs.com/docs/#concat](https://ramdajs.com/docs/#concat)

## contains
`Deprecated`

只要列表中有一个元素等于指定值，则返回 `true`；否则返回 `false`。通过 `R.equals` 函数进行相等性判断。

也可以判断字符串中是否包含指定值。

### 参数

```
a → [a] → Boolean
```

- `a`：要比较的项。
- `list`：要检查的列表。
- 返回 `Boolean`：如果相等项在列表中，则为 `true`；否则为 `false`。

### 例子

```js
R.contains(3, [1, 2, 3]); //=> true
R.contains(4, [1, 2, 3]); //=> false
R.contains({ name: 'Fred' }, [{ name: 'Fred' }]); //=> true
R.contains([42], [[42]]); //=> true
R.contains('ba', 'banana'); //=>true
```

### 参考
- [https://ramdajs.com/docs/#contains](https://ramdajs.com/docs/#contains)

## drop
删除给定 `list`，`string` 或者 `transducer`/`transformer`（或者具有 `drop` 方法的对象）的前 `n` 个元素。

若第二个参数自身存在 `drop` 方法，则调用自身的 `drop` 方法。

若在 `list` 位置中给出 `transfomer` ，则用作 `transducer` 。

### 参数

```
Number → [a] → [a]
Number → String → String
```

- `n`。
- `list`。
- 返回 `*`：没有了前 `n` 个元素的列表的副本。

### 例子

```js
R.drop(1, ['foo', 'bar', 'baz']); //=> ['bar', 'baz']
R.drop(2, ['foo', 'bar', 'baz']); //=> ['baz']
R.drop(3, ['foo', 'bar', 'baz']); //=> []
R.drop(4, ['foo', 'bar', 'baz']); //=> []
R.drop(3, 'ramda');               //=> 'da'
```

### 参考
- [https://ramdajs.com/docs/#drop](https://ramdajs.com/docs/#drop)

## dropLast
删除 `list` 末尾的 `n` 个元素。

若在列表位置中给出 `transfomer`，则用作 `transducer` 。

### 参数

```
Number → [a] → [a]
Number → String → String
```

- `n`：要跳过的列表元素数。
- `list`：要考虑的元素列表。
- 返回 `Array`：仅具有前 `list.length-n` 个元素的列表的副本。

### 例子

```js
R.dropLast(1, ['foo', 'bar', 'baz']); //=> ['foo', 'bar']
R.dropLast(2, ['foo', 'bar', 'baz']); //=> ['foo']
R.dropLast(3, ['foo', 'bar', 'baz']); //=> []
R.dropLast(4, ['foo', 'bar', 'baz']); //=> []
R.dropLast(3, 'ramda');               //=> 'ra'
```

### 参考
- [https://ramdajs.com/docs/#dropLast](https://ramdajs.com/docs/#dropLast)

## dropLastWhile
对 `list` 从后向前一直删除满足 `predicate` 的尾部元素，直到遇到第一个 `falsy` 值，此时停止删除操作。

`predicate` 需要作为第一个参数传入。

若在列表位置中给出 `transfomer`，则用作 `transducer` 。

### 参数

```
(a → Boolean) → [a] → [a]
(a → Boolean) → String → String
```

- `predicate`：每个元素上要调用的函数。
- `xs`：要遍历的集合。
- 返回 `Array`：一个新数组，不包含任何从谓词返回“假”值的尾随元素。

### 例子

```js
const lteThree = x => x <= 3;

R.dropLastWhile(lteThree, [1, 2, 3, 4, 3, 2, 1]); //=> [1, 2, 3, 4]

R.dropLastWhile(x => x !== 'd', 'Ramda'); //=> 'Ramd'
```

### 参考
- [https://ramdajs.com/docs/#dropLastWhile](https://ramdajs.com/docs/#dropLastWhile)

## dropRepeats
返回一个没有连续重复元素的 `list`。通过 `R.equals` 函数进行相等性判断。

若在 `list` 位置中给出 `transfomer` ，则用作 `transducer` 。

### 参数

```
[a] → [a]
```

- `list`：要考虑的数组。
- 返回 `Array`：去除了重复元素的 `list`。

### 例子

```js
R.dropRepeats([1, 1, 1, 2, 3, 4, 4, 2, 2]); //=> [1, 2, 3, 4, 2]
```

### 参考
- [https://ramdajs.com/docs/#dropRepeats](https://ramdajs.com/docs/#dropRepeats)

## dropRepeatsWith

返回一个没有连续重复元素的 `list`。首个参数提供的 `predicate` 用于检测 `list` 中相邻的两个元素是否相等。一系列相等元素中的首个元素会被保留。

若在 `list` 位置中给出 `transfomer` ，则用作 `transducer` 。

### 参数

```
((a, a) → Boolean) → [a] → [a]
```

- `pred` 用于测试两个项目是否相等的谓词函数。
- `list`：要考虑的数组。
- 返回 `Array`：去除了重复元素的 `list`。

### 例子

```js
const l = [1, -1, 1, 3, 4, -4, -4, -5, 5, 3, 3];
R.dropRepeatsWith(R.eqBy(Math.abs), l); //=> [1, 3, 4, -5, 3]
```

### 参考
- [https://ramdajs.com/docs/#dropRepeatsWith](https://ramdajs.com/docs/#dropRepeatsWith)

## dropWhile
对 `list` 从前向后删除满足 `predicate` 的头部元素，直到遇到第一个 `falsy` 值。

`predicate` 需要作为第一个参数传入。

若第二个参数自身存在 `dropWhile` 方法，则调用自身的 `dropWhile` 方法。

若在 `list` 位置中给出 `transfomer` ，则用作 `transducer` 。

### 参数

```
(a → Boolean) → [a] → [a]
(a → Boolean) → String → String
```

- `fn` 每次迭代调用的函数。
- `xs`：要遍历的集合。
- 返回 `Array`：一个新数组。

### 例子

```js
const lteTwo = x => x <= 2;

R.dropWhile(lteTwo, [1, 2, 3, 4, 3, 2, 1]); //=> [3, 4, 3, 2, 1]

R.dropWhile(x => x !== 'd', 'Ramda'); //=> 'da'
```

### 参考
- [https://ramda.cn/docs/#dropWhile](https://ramda.cn/docs/#dropWhile)

## endsWith

检查列表是否以指定的子列表结尾。

同样的，检查字符串是否以指定的子字符串结尾。

### 参数

```
[a] → [a] → Boolean
String → String → Boolean
```

- `suffix`。
- `list`。
- `Boolean`。

### 例子

```js
R.endsWith('c', 'abc')                //=> true
R.endsWith('b', 'abc')                //=> false
R.endsWith(['c'], ['a', 'b', 'c'])    //=> true
R.endsWith(['b'], ['a', 'b', 'c'])    //=> false
```

### 参考
- [https://ramdajs.com/docs/#endsWith](https://ramdajs.com/docs/#endsWith)

## filter
使用 `predicate` 遍历传入的 `Filterable`，返回满足 `predicate` 的所有元素的新的 `Filterable`。新 `Filterable` 与原先的类型相同。`Filterable` 类型包括 `plain object` 或者任何带有 `filter` 方法的类型，如 `Array` 。

若第二个参数自身存在 `filter` 方法，则调用自身的 `filter` 方法。

若在 `list` 位置中给出 `transfomer` ，则用作 `transducer` 。

### 参数

```
Filterable f => (a → Boolean) → f a → f a
```

- `pred`。
- `filterable`。
- 返回 `Array`：`Filterable`。

### 例子

```js
const isEven = n => n % 2 === 0;

R.filter(isEven, [1, 2, 3, 4]); //=> [2, 4]

R.filter(isEven, { a: 1, b: 2, c: 3, d: 4 }); //=> {b: 2, d: 4}
```

### 参考
- [https://ramdajs.com/docs/#filter](https://ramdajs.com/docs/#filter)

## find
查找并返回 `list` 中首个满足 `predicate` 的元素；如果未找到满足条件的元素，则返回 `undefined` 。

若第二个参数自身存在 `find` 方法，则调用自身的 `find` 方法。

若在 `list` 位置中给出 `transfomer` ，则用作 `transducer` 。

### 参数

```
(a → Boolean) → [a] → a | undefined
```

- `fn`：谓词函数，用于确定元素是否为所需元素。
- `list`：要考虑的数组。
- 返回 `Object`：找到的元素，否则返回 `undefined`。

### 例子

```js
const xs = [{ a: 1 }, { a: 2 }, { a: 3 }];
R.find(R.propEq('a', 2))(xs); //=> {a: 2}
R.find(R.propEq('a', 4))(xs); //=> undefined
```

### 参考
- [https://ramdajs.com/docs/#find](https://ramdajs.com/docs/#find)

## findIndex
查找并返回 `list` 中首个满足 `predicate` 的元素的索引；如果未找到满足条件的元素，则返回 `-1` 。

若在 `list` 位置中给出 `transfomer` ，则用作 `transducer` 。

### 参数

```
(a → Boolean) → [a] → Number
```

- `fn`：谓词函数，用于确定元素是否为所需元素。
- `list`：要考虑的数组。
- 返回 `Number`：找到的元素的索引，否则返回 `-1`。

### 例子

```js
const xs = [{ a: 1 }, { a: 2 }, { a: 3 }];
R.findIndex(R.propEq('a', 2))(xs); //=> 1
R.findIndex(R.propEq('a', 4))(xs); //=> -1
```

### 参考
- [https://ramdajs.com/docs/#findIndex](https://ramdajs.com/docs/#findIndex)

## findLast
查找并返回 `list` 中最后一个满足 `predicate` 的元素；如果未找到满足条件的元素，则返回 `undefined` 。

若在 `list` 位置中给出 `transfomer` ，则用作 `transducer` 。

### 参数

```
(a → Boolean) → [a] → a | undefined
```

- `fn`：谓词函数，用于确定元素是否为所需元素。
- `list`：要考虑的数组。
- 返回 `Object`：找到的元素，否则返回 `undefined`。

### 例子

```js
const xs = [{ a: 1, b: 0 }, { a: 1, b: 1 }];
R.findLast(R.propEq('a', 1))(xs); //=> {a: 1, b: 1}
R.findLast(R.propEq('a', 4))(xs); //=> undefined
```

### 参考
- [https://ramdajs.com/docs/#findLast](https://ramdajs.com/docs/#findLast)

## findLastIndex
查找并返回 `list` 中最后一个满足 `predicate` 的元素的索引；如果未找到满足条件的元素，则返回 `-1` 。

若在 `list` 位置中给出 `transfomer` ，则用作 `transducer` 。

### 参数

```
(a → Boolean) → [a] → Number
```

- `fn`：谓词函数，用于确定元素是否为所需元素。
- `list`：要考虑的数组。
- 返回 `Number`：找到的元素的索引，否则返回 `-1`。

### 例子

```js
const xs = [{ a: 1, b: 0 }, { a: 1, b: 1 }];
R.findLastIndex(R.propEq('a', 1))(xs); //=> 1
R.findLastIndex(R.propEq('a', 4))(xs); //=> -1
```

### 参考
- [https://ramdajs.com/docs/#findLastIndex](https://ramdajs.com/docs/#findLastIndex)

## flatten
获取 `list` 的所有元素（包含所有子数组中的元素），然后由这些元素组成一个新的数组。深度优先。

### 参数

```
[a] → [b]
```

- `list`：要考虑的数组。
- 返回 `Array`：展平的列表。

### 例子

```js
R.flatten([1, 2, [3, 4], 5, [6, [7, 8, [9, [10, 11], 12]]]]);
//=> [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
```

### 参考
- [https://ramdajs.com/docs/#flatten](https://ramdajs.com/docs/#flatten)

## forEach
遍历 `list`，对 `list` 中的每个元素执行方法 `fn`。

`fn` 接收单个参数：`(value)`。

注意: `R.forEach` 并不会跳过已删除的或者未赋值的索引（sparse arrays），这一点和原生的 `Array.prototype.forEach` 方法不同。 获取更多相关信息, 请查阅: [Array.prototype.forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach#Description)。

还要注意, 不同于 `Array.prototype.forEach`，Ramda 的 `forEach` 会将原数组返回。在某些库中，该方法也被称为 `each`。

若第二个参数自身存在 `forEach` 方法，则调用自身的 `forEach` 方法。

### 参数

```
(a → *) → [a] → [a]
```

- `fn`：调用的函数。接收一个参数 `value`。
- `list`：要遍历的列表。
- 返回 `Array`：原始列表。

### 例子

```js
const printXPlusFive = x => console.log(x + 5);
R.forEach(printXPlusFive, [1, 2, 3]); //=> [1, 2, 3]
// logs 6
// logs 7
// logs 8
```

### 参考
- [https://ramdajs.com/docs/#forEach](https://ramdajs.com/docs/#forEach)

## fromPairs
由一系列 “键值对” 创建一个 `object`。如果某个键出现多次，选取最右侧的键值对。

### 参数
- `pairs`：一个由两个元素组成的数组，该数组将作为输出对象的键和值。
- 返回 `Object`：通过将“键”和“值”配对而制成的对象。

### 例子

```js
R.fromPairs([['a', 1], ['b', 2], ['c', 3]]); //=> {a: 1, b: 2, c: 3}
```

### 参考
- [https://ramda.cn/docs/#fromPairs](https://ramda.cn/docs/#fromPairs)

## groupBy
将列表根据一定规则拆分成多组子列表，并存储在一个对象中。

对列表中的每个元素调用函数，根据函数返回结果进行分组。函数返回字符串作为相等性判断，返回的字符串作为存储对象的键，具有相同返回字符串的元素聚合为数组，作为该键的值。

若第二个参数自身存在 `groupBy` 方法，则调用自身的 `groupBy` 方法。

若在 `list` 位置中给出 `transfomer` ，则用作 `transducer` 。

### 参数

```
(a → String) → [a] → {String: [a]}
```

- `fn`：用作相等性判断的函数。
- `list`：要分组的数组。
- 返回 `Object`：一个的 `fn` 输出为键的对象，映射到传递给 `fn` 时生成该键的元素数组。

### 例子

```js
const byGrade = R.groupBy(function (student) {
    const score = student.score;
    return score < 65 ? 'F' :
        score < 70 ? 'D' :
            score < 80 ? 'C' :
                score < 90 ? 'B' : 'A';
});
const students = [
    { name: 'Abby', score: 84 },
    { name: 'Eddy', score: 58 },
    // ...
    { name: 'Jack', score: 69 }
];
byGrade(students);

// {
//     'A': [{ name: 'Dianne', score: 99 }],
//         'B': [{ name: 'Abby', score: 84 }]
//     // ...,
//     'F': [{ name: 'Eddy', score: 58 }]
// }
```

### 参考
- [https://ramdajs.com/docs/#groupBy](https://ramdajs.com/docs/#groupBy)

## groupWith
通过给定的对比函数，将列表按顺序分割成多组子列表。

对比函数只比较相邻元素。

### 参数

```
((a, a) → Boolean) → [a] → [[a]]
```

- `fn`：确定两个给定（相邻）元素是否应在同一组中的函数。
- `list`：要分组的数组。还接受一个字符串，该字符串将被视为字符列表。
- 返回 `List`：包含元素子列表的列表，这些元素的串联等于原始列表。

### 例子

```js
R.groupWith(R.equals, [0, 1, 1, 2, 3, 5, 8, 13, 21])
//=> [[0], [1, 1], [2], [3], [5], [8], [13], [21]]

R.groupWith((a, b) => a + 1 === b, [0, 1, 1, 2, 3, 5, 8, 13, 21])
//=> [[0, 1], [1, 2, 3], [5], [8], [13], [21]]

R.groupWith((a, b) => a % 2 === b % 2, [0, 1, 1, 2, 3, 5, 8, 13, 21])
//=> [[0], [1, 1], [2], [3, 5], [8], [13, 21]]

R.groupWith(R.eqBy(isVowel), 'aestiou')
//=> ['ae', 'st', 'iou']
```

### 参考
- [https://ramdajs.com/docs/#groupWith](https://ramdajs.com/docs/#groupWith)

## head
求列表或字符串的首个元素。在某些库中，该函数也被称作 `first`。

### 参数

```
[a] → a | Undefined
String → String
```

- `list`。
- 返回 `*`。

### 例子

```js
R.head(['fi', 'fo', 'fum']); //=> 'fi'
R.head([]); //=> undefined

R.head('abc'); //=> 'a'
R.head(''); //=> ''
```

### 参考
- [https://ramdajs.com/docs/#head](https://ramdajs.com/docs/#head)

## includes
只要列表中有一个元素等于指定值，则返回 `true`；否则返回 `false`。通过 `R.equals` 函数进行相等性判断。

也可以判断字符串中是否包含指定值。

### 参数

```
a → [a] → Boolean
```

- `a`：要比较的项目。
- `list`：要考虑的数组。
- 返回 `Boolean`：如果等效项在列表中，则为 `true`；否则为 `false`。

### 例子

```js
R.includes(3, [1, 2, 3]); //=> true
R.includes(4, [1, 2, 3]); //=> false
R.includes({ name: 'Fred' }, [{ name: 'Fred' }]); //=> true
R.includes([42], [[42]]); //=> true
R.includes('ba', 'banana'); //=>true
```

### 参考
- [https://ramdajs.com/docs/#includes](https://ramdajs.com/docs/#includes)

## indexBy
通过生成键的函数，将元素为对象的 `list` 转换为以生成的键为索引的新对象。注意，如果 `list` 中多个对象元素生成相同的键，以最后一个对象元素作为该键的值。

若在 `list` 位置中给出 `transfomer` ，则用作 `transducer` 。

### 参数

```
(a → String) → [{k: v}] → {k: {k: v}}
```

- `fn`：生成键的函数
- `array`：要索引的对象数组
- 返回 `Object`：一个通过给定属性索引每个数组元素的对象。

### 例子

```js
const list = [{ id: 'xyz', title: 'A' }, { id: 'abc', title: 'B' }];
R.indexBy(R.prop('id'), list);
//=> {abc: {id: 'abc', title: 'B'}, xyz: {id: 'xyz', title: 'A'}}
```

### 参考
- [https://ramdajs.com/docs/#indexBy](https://ramdajs.com/docs/#indexBy)

## indexOf
返回给定元素在数组中首次出现时的索引值，如果数组中没有该元素，则返回 `-1`。通过 `R.equals` 函数进行相等性判断。

### 参数

```
a → [a] → Number
```

- `target`：要查找的项目。
- `xs`：要搜索的数组。
- 返回 `Number`：目标的索引；如果找不到目标，则为 `-1`。

### 例子

```js
R.indexOf(3, [1,2,3,4]); //=> 2
R.indexOf(10, [1,2,3,4]); //=> -1
```

### 参考
- [https://ramdajs.com/docs/#indexOf](https://ramdajs.com/docs/#indexOf)

## init
返回 `list` 或 `string` 删除最后一个元素后的部分。

### 参数

```
[a] → [a]
String → String
```

- `list`。
- 返回 `*`。

### 例子

```js
R.init([1, 2, 3]);  //=> [1, 2]
R.init([1, 2]);     //=> [1]
R.init([1]);        //=> []
R.init([]);         //=> []

R.init('abc');  //=> 'ab'
R.init('ab');   //=> 'a'
R.init('a');    //=> ''
R.init('');     //=> ''
```

### 参考
- [https://ramdajs.com/docs/#init](https://ramdajs.com/docs/#init)

## insert
将元素插入到 `list` 指定索引处。注意，该函数是非破坏性的：返回处理后列表的拷贝。函数运行过程中不会破坏任何列表。

### 参数

```
Number → a → [a] → [a]
```

- `index`： 插入元素的位置。
- `elt`： 要插入数组的元素。
- `list`： 要插入的列表。
- 返回 `Array`：在 `index` 处插入了带有 `elt` 的新数组。

### 例子

```js
R.insert(2, 'x', [1,2,3,4]); //=> [1,2,'x',3,4]
```

### 参考
- [https://ramdajs.com/docs/#insert](https://ramdajs.com/docs/#insert)

## insertAll

将子 `list` 插入到 `list` 指定索引处。注意，该函数是非破坏性的：返回处理后列表的拷贝。函数运行过程中不会破坏任何列表。

### 参数

```
Number → [a] → [a] → [a]
```

- `index`： 插入子列表的位置。
- `elts`： 要插入数组的子列表。
- `list`： 要插入的列表。
- 返回 `Array`：在 `index` 处插入了带有 `elts` 的新数组。

### 例子

```js
R.insertAll(2, ['x', 'y', 'z'], [1, 2, 3, 4]); //=> [1,2,'x','y','z',3,4]
```

### 参考
- [https://ramdajs.com/docs/#insertAll](https://ramdajs.com/docs/#insertAll)

## intersperse

在列表的元素之间插入分割元素。

若第二个参数自身存在 `intersperse` 方法，则调用自身的 `intersperse` 方法。

### 参数

```
a → [a] → [a]
```

- `separator`：要添加到列表中的元素。
- `list`：要插入的列表。
- 返回 `Array`：新列表。

### 例子

```js
R.intersperse('a', ['b', 'n', 'n', 's']); //=> ['b', 'a', 'n', 'a', 'n', 'a', 's']
```

### 参考
- [https://ramdajs.com/docs/#intersection](https://ramdajs.com/docs/#intersection)

## into
使用 `transducer` 对 `list` 中的元素进行转换，然后使用基于 `accumulator` 的类型的迭代器函数将转换后的元素依次添加到 `accumulator` 上。

`accumulator` 的类型可以是：`array`、`string`、`object` 或者 `transformer` 。如果 `accumulator` 类型是 `array` 或 `string`，则迭代元素将被添加到数组或连接到字符串上；如果是对象，迭代元素将会被直接合并；如果是二元素数组，迭代元素会以键值对形式进行合并。

`accumulator` 也可作为 `transformer` 对象，提供 `transformer` 所需要的二元 `reducing iterator`、`step`、零元 `init` 和 一元 `result` 函数。`step` 作为 `reduce` 过程中的迭代函数；`result` 将最终的 `accumulator` 转换为需要的返回类型（通常为 `R.identity`）；`init` 提供初始 `accumulator`。

在 `transducer` 初始化之后，使用 `R.reduce` 进行迭代操作。

### 参数

```
a → (b → b) → [c] → a
```

- `acc`：初始 `accumulator` 值。
- `xf`：`transducer` 函数。接收一个 `transformer` 并返回一个 `transformer`。
- `list`：要遍历的列表。
- 返回 `*`：最终的累计值。

### 例子

```js
const numbers = [1, 2, 3, 4];
const transducer = R.compose(R.map(R.add(1)), R.take(2));

R.into([], transducer, numbers); //=> [2, 3]

const intoArray = R.into([]);
intoArray(transducer, numbers); //=> [2, 3]
```

### 参考
- [https://ramdajs.com/docs/#into](https://ramdajs.com/docs/#into)

## join
将列表中所有元素通过 分隔符 串连为一个字符串。

### 参数

```
String → [a] → String
```

- `separator`：用于分隔元素的字符串。
- `xs`：要加入字符串的元素。
- 返回 `String`：`str` 通过将 `xs` 和 `separator` 串联而成的字符串。

### 例子

```js
const spacer = R.join(' ');
spacer(['a', 2, 3.4]);   //=> 'a 2 3.4'
R.join('|', [1, 2, 3]);    //=> '1|2|3'
```

### 参考
- [https://ramdajs.com/docs/#join](https://ramdajs.com/docs/#join)

## last
返回列表或字符串的最后一个元素。

### 参数

```
[a] → a | Undefined
String → String
```

- `list`
- 返回 `*`

### 例子

```js
R.last(['fi', 'fo', 'fum']); //=> 'fum'
R.last([]); //=> undefined

R.last('abc'); //=> 'c'
R.last(''); //=> ''
```

### 参考
- [https://ramdajs.com/docs/#last](https://ramdajs.com/docs/#last)

## lastIndexOf
返回数组中某元素最后一次出现的位置，如果数组中不包含该项则返回 `-1` 。通过 `R.equals` 函数进行相等性判断。

### 参数

```
a → [a] → Number
```

- `target`：要查找的项目。
- `xs`：要搜索的数组。
- 返回 `Number`：目标的索引；如果未找到目标，则返回 `-1`。

### 例子

```js
R.lastIndexOf(3, [-1,3,3,0,1,2,3,4]); //=> 6
R.lastIndexOf(10, [1,2,3,4]); //=> -1
```

### 参考
- [https://ramdajs.com/docs/#lastIndexOf](https://ramdajs.com/docs/#lastIndexOf)

## length
通过 `list.length`，返回数组的大小（数组中元素的数量）。

### 参数

```
[a] → Number
```

- `list`：要检查的数组。
- 返回 `Number`：数组的长度。

### 例子

```js
R.length([]); //=> 0
R.length([1, 2, 3]); //=> 3
```

### 参考
- [https://ramdajs.com/docs/#length](https://ramdajs.com/docs/#length)

## map
接收一个函数和一个 [functor](https://github.com/fantasyland/fantasy-land#functor), 将该函数应用到 `functor` 的每个值上，返回一个具有相同形态的 `functor`。

Ramda 为 `Array` 和 `Object` 提供了合适的 `map` 实现，因此 `R.map` 适用于 `[1, 2, 3]` 或 `{x: 1, y: 2, z: 3}`。

若第二个参数自身存在 `map` 方法，则调用自身的 `map` 方法。

若在列表位置中给出 `transfomer`，则用作 `transducer` 。

函数也是 `functors`，`map` 会将它们组合起来（相当于 R`.compose`）。

### 参数

```
Functor f => (a → b) → f a → f b
```

- `fn`：在输入列表的每个元素上调用的函数。
- `list`：要迭代的列表。
- 返回 `Array`：新列表。

### 例子

```js
const double = x => x * 2;

R.map(double, [1, 2, 3]); //=> [2, 4, 6]

R.map(double, { x: 1, y: 2, z: 3 }); //=> {x: 2, y: 4, z: 6}
```

### 参考
- [https://ramdajs.com/docs/#map](https://ramdajs.com/docs/#map)

## mapAccum
`mapAccum` 的行为类似于 `map` 和 `reduce` 的组合；它将迭代函数作用于列表中的每个元素，从左往右传递经迭代函数计算的累积值，并将最后的累积值和由所有中间的累积值组成的列表一起返回。迭代函数接收两个参数，`acc` 和 `value`，返回一个元组 `[acc, value]`。

### 参数

```
((acc, x) → (acc, y)) → acc → [x] → (acc, [y])
```

- `fn`：在输入列表的每个元素上调用的函数。
- `acc`：累加器值。
- `list`：要遍历的列表。
- 返回 `*`：最终的累计值。

### 例子

```js
const digits = ['1', '2', '3', '4'];
const appender = (a, b) => [a + b, a + b];

R.mapAccum(appender, 0, digits); //=> ['01234', ['01', '012', '0123', '01234']]
```

### 参考
- [https://ramdajs.com/docs/#mapAccum](https://ramdajs.com/docs/#mapAccum)

## mapAccumRight
`mapAccumRight` 的行为类似于 `map` 和 `reduce` 的组合；它将迭代函数作用于列表中的每个元素，从右往左传递经迭代函数计算的累积值，并将最后的累积值和由所有中间的累积值组成的列表一起返回。

和 `mapAccum` 类似，除了列表遍历顺序是从右往左的。

迭代函数接收两个参数，`acc` 和 `value` ，返回一个元组 `[acc, value]`。

### 参数

```
((acc, x) → (acc, y)) → acc → [x] → (acc, [y])
```

- `fn`：在输入列表的每个元素上调用的函数。
- `acc`：累加器值。
- `list`：要遍历的列表。
- 返回 `*`：最终的累计值。

### 例子

```js
const digits = ['1', '2', '3', '4'];
const appender = (a, b) => [b + a, b + a];

R.mapAccumRight(appender, 5, digits); //=> ['12345', ['12345', '2345', '345', '45']]
```

### 参考
- [https://ramdajs.com/docs/#mapAccumRight](https://ramdajs.com/docs/#mapAccumRight)

## mergeAll
将对象类型列表合并为一个对象。

### 参数

```
[{k: v}] → {k: v}
```

- `list`：对象数组
- 返回 `Object`：合并的对象。

### 例子

```js
R.mergeAll([{foo:1},{bar:2},{baz:3}]); //=> {foo:1,bar:2,baz:3}
R.mergeAll([{foo:1},{foo:2},{bar:2}]); //=> {foo:2,bar:2}
```

### 参考
- [https://ramdajs.com/docs/#mergeAll](https://ramdajs.com/docs/#mergeAll)

## move
将列表中 `from` 索引处的元素移动到索引 `to` 处。

### 参数

```
Number → Number → [a] → [a]
```

- `from`：源索引。
- `to`：目标索引。
- `list`：实现移动的列表。
- 返回 `Array`：重新排序的新列表。

### 例子

```js
R.move(0, 2, ['a', 'b', 'c', 'd', 'e', 'f']); //=> ['b', 'c', 'a', 'd', 'e', 'f']
R.move(-1, 0, ['a', 'b', 'c', 'd', 'e', 'f']); //=> ['f', 'a', 'b', 'c', 'd', 'e'] list rotation
```

### 参考
- [https://ramdajs.com/docs/#move](https://ramdajs.com/docs/#move)

## none

如果列表中的元素都不满足 `predicate`，返回 `true`；否则返回 `false`。

若第二个参数自身存在 `none` 方法，则调用自身的 `none` 方法。

### 参数

```
(a → Boolean) → [a] → Boolean
```

- `fn`：谓词函数。
- `list`：要考虑的数组。
- 返回 `Boolean`：如果谓词不是每个元素都满足，则返回 `true`，否则返回 `false`。

### 例子

```js
const isEven = n => n % 2 === 0;
const isOdd = n => n % 2 === 1;

R.none(isEven, [1, 3, 5, 7, 9, 11]); //=> true
R.none(isOdd, [1, 3, 5, 7, 8, 11]); //=> false
```

### 参考
- [https://ramdajs.com/docs/#none](https://ramdajs.com/docs/#none)

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

## nth
返回列表或字符串的第 `n` 个元素。如果 `n` 为负数，则返回索引为 `length + n` 的元素。

### 参数

```
Number → [a] → a | Undefined
Number → String → String
```

- `offset`。
- `list`。
- 返回 `*`。

### 例子

```js
const list = ['foo', 'bar', 'baz', 'quux'];
R.nth(1, list); //=> 'bar'
R.nth(-1, list); //=> 'quux'
R.nth(-99, list); //=> undefined

R.nth(2, 'abc'); //=> 'c'
R.nth(3, 'abc'); //=> ''
```

### 参考
- [https://ramdajs.com/docs/#nth](https://ramdajs.com/docs/#nth)

## pair
接收两个参数，`fst` 和 `snd`，返回数组 `[fst, snd]`。

### 参数

```
a → b → (a,b)
```

- `fst`。
- `snd`。
- 返回 `Array`。

### 例子

```js
R.pair('foo', 'bar'); //=> ['foo', 'bar']
```

### 参考
- [https://ramdajs.com/docs/#pair](https://ramdajs.com/docs/#pair)

## partition
通过 `predicate` 将列表或 `"Filterable"`（可过滤的）对象分成两部分，分别为满足 `predicate` 的元素和不满足 `predicate` 的元素。元素类型保持不变。`Filterable` 类型包括 `plain object` 或者任何带有 `filter` 方法的类型，如 `Array` 。

### 参数

```
Filterable f => (a → Boolean) → f a → [f a, f a]
```

- `pred`：确定该元素属于哪一侧的谓词。
- `filterable`：要分区的列表（或其他可过滤的列表）。
- 返回 `Array`：一个数组，首先包含满足谓词的元素子集，其次包含不满足条件的元素子集。

### 例子

```js
R.partition(R.includes('s'), ['sss', 'ttt', 'foo', 'bars']);
// => [ [ 'sss', 'bars' ],  [ 'ttt', 'foo' ] ]

R.partition(R.includes('s'), { a: 'sss', b: 'ttt', foo: 'bars' });
// => [ { a: 'sss', foo: 'bars' }, { b: 'ttt' }  ]
```

### 参考
- [https://ramdajs.com/docs/#partition](https://ramdajs.com/docs/#partition)

## pluck
从列表内的每个对象元素中取出特定名称的属性，组成一个新的列表。

`pluck` 可以作用于任何 [functor](https://github.com/fantasyland/fantasy-land#functor) ，包括 `Array`，因为它等价于 `R.map(R.prop(k), f)`。

### 参数

```
Functor f => k → f {k: v} → f v
```

- `key`：要从每个对象中提取的键名称。
- `f`：要考虑的数组或仿函数。
- 返回 `Array`：给定键的值列表。

### 例子

```js
var getAges = R.pluck('age');
getAges([{ name: 'fred', age: 29 }, { name: 'wilma', age: 27 }]); //=> [29, 27]

R.pluck(0, [[1, 2], [3, 4]]);               //=> [1, 3]
R.pluck('val', { a: { val: 3 }, b: { val: 5 } }); //=> {a: 3, b: 5}
```

### 参考
- [https://ramdajs.com/docs/#pluck](https://ramdajs.com/docs/#pluck)

## prepend
在列表头部之前拼接一个元素。

### 参数

```
a → [a] → [a]
```

- `el`：要添加到输出列表开头的项目。
- `list`：要添加到输出列表尾部的数组。
- 返回 `Array`：一个新的数组。

### 例子

```js
R.prepend('fee', ['fi', 'fo', 'fum']); //=> ['fee', 'fi', 'fo', 'fum']
```

### 参考
- [https://ramdajs.com/docs/#prepend](https://ramdajs.com/docs/#prepend)

## range
返回从 `from` 到 `to` 之间的所有数的升序列表。左闭右开（包含 `from`，不包含 `to`）。

### 参数

```
Number → Number → [Number]
```

- `from`：列表中的第一个数字。
- `to`：比列表中的最后一个数字多一个。
- 返回 `Array`：集合 `[a，b)` 中的数字列表。

### 例子

```js
R.range(1, 5);    //=> [1, 2, 3, 4]
R.range(50, 53);  //=> [50, 51, 52]
```

### 参考
- [https://ramdajs.com/docs/#range](https://ramdajs.com/docs/#range)

## reduce
左折叠操作。

遍历列表，相继调用二元迭代函数（参数为累积值和从数组中取出的当前元素），将本次迭代结果作为下次迭代的累积值。返回最终累积值。

可以用 `R.reduced` 提前终止遍历操作。

`reduce` 的迭代函数接收两个参数 `(acc, value)`，`reduceRight` 的迭代函数的参数顺序为 `(value, acc)` 。

注意：`R.reduce` 与原生 `Array.prototype.reduce` 方法不同，它不会跳过删除或未分配的索引项（稀疏矩阵）。更多关于原生 `reduce` 的行为，请参考：[Array/reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#Description)。

如果第三个参数自身有 `reduce` 方法，则调用自身的 `reduce` 方法。如果进行该步操作，则由用户自己来处理 `R.reduced` 短路操作，因为自身 `reduce` 方法的实现可能与 Ramda 中的 `reduce` 不同。

### 参数

```
((a, b) → a) → a → [b] → a
```

- `fn`：迭代器函数。从数组接收两个值，即累加器和当前元素。
- `acc`：累加器值。
- `list`：要遍历的列表。
- `*`：最终的累计值。

### 例子

```js
R.reduce(R.subtract, 0, [1, 2, 3, 4]) // => ((((0 - 1) - 2) - 3) - 4) = -10
//          -               -10
//         / \              / \
//        -   4           -6   4
//       / \              / \
//      -   3   ==>     -3   3
//     / \              / \
//    -   2           -1   2
//   / \              / \
//  0   1            0   1
```

### 参考
- [https://ramdajs.com/docs/#reduce](https://ramdajs.com/docs/#reduce)

## reduceBy
首先对列表中的每个元素调用函数 `keyFn` ，根据 `keyFn` 返回的字符串对列表元素进行分组。然后调用 `reducer` 函数 `valueFn`，对组内的元素进行折叠操作。

该函数相当于更通用的 `groupBy` 函数。

若在列表位置给出 `transformer`，则用做 `transducer`。

### 参数

```
((a, b) → a) → a → (b → String) → [b] → {String: a}
```

- `valueFn`：将每个组的元素减少为单个值的功能。接收两个值，即特定组的累加器和当前元素。
- `acc`：每个组的（初始）累加器值。
- `keyFn`：将列表的元素映射到键中的函数。
- `list`：要分组的数组。
- 返回 `Object`：一个对象，该对象的键输出为 `keyFn`，映射到元素的 `valueFn` 输出，该元素在传递给 `keyFn` 时生成该键。

### 例子

```js
const groupNames = (acc, { name }) => acc.concat(name)
const toGrade = ({ score }) =>
    score < 65 ? 'F' :
        score < 70 ? 'D' :
            score < 80 ? 'C' :
                score < 90 ? 'B' : 'A'

var students = [
    { name: 'Abby', score: 83 },
    { name: 'Bart', score: 62 },
    { name: 'Curt', score: 88 },
    { name: 'Dora', score: 92 },
]

reduceBy(groupNames, [], toGrade, students)
//=> {"A": ["Dora"], "B": ["Abby", "Curt"], "F": ["Bart"]}
```

### 参考
- [https://ramdajs.com/docs/#reduceBy](https://ramdajs.com/docs/#reduceBy)

## reduced
返回一个封装的值，该值代表 `reduce` 或 `transduce` 操作的最终结果。

返回值是一个黑盒：不保证其内部结构的稳定性。

注意：这个优化不适用于上面未明确列出的函数。例如，现在还不支持 `reduceRight`。

### 参数

```
a → *
```

- `x`：`reduce` 最终值。
- `*`：包装值。

### 例子

```js
R.reduce(
    (acc, item) => item > 3 ? R.reduced(acc) : acc.concat(item),
    [],
    [1, 2, 3, 4, 5]) // [1, 2, 3]
```

### 参考
- [https://ramdajs.com/docs/#reduced](https://ramdajs.com/docs/#reduced)

## reduceRight
右折叠操作。

遍历列表，相继调用二元迭代函数（参数为累积值和从数组中取出的当前元素），将本次迭代结果作为下次迭代的累积值。返回最终累积值。

类似于 `reduce`，除了遍历列表的顺序是从右向左的。

`reduceRight` 的迭代函数接收两个参数 `(value, acc)`。与之对应的，`reduce` 的迭代函数的参数顺序为 `(acc, value)`。

注意：`R.reduceRight` 与原生 `Array.prototype.reduceRight` 方法不同，它不会跳过删除或未分配的索引项（稀疏矩阵）。更多关于原生 `reduceRight` 的行为，请参考：[Array/reduceRight](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduceRight#Description)。

### 参数

((a, b) → b) → b → [a] → b

- `fn`：迭代器函数。接收两个值，即数组中的当前元素和累加器。
- `acc`：累加器值。
- `list`：要遍历的列表。
- `*`：最终的累计值。

### 例子

```js
R.reduceRight(R.subtract, 0, [1, 2, 3, 4]) // => (1 - (2 - (3 - (4 - 0)))) = -2
//    -               -2
//   / \              / \
//  1   -            1   3
//     / \              / \
//    2   -     ==>    2  -1
//       / \              / \
//      3   -            3   4
//         / \              / \
//        4   0            4   0
```

### 参考
- [https://ramdajs.com/docs/#reduceRight](https://ramdajs.com/docs/#reduceRight)

## reduceWhile
与 `reduce` 类似，`reduceWhile` 会遍历列表，相继调用二元迭代函数，并返回最终累积值。`reduceWhile` 在每次调用迭代函数前，先使用 `predicate` 进行判断，如果 `predicate` 返回 `false` ，则提前终止遍历操作，并返回当前累积值。


### 参数

```
((a, b) → Boolean) → ((a, b) → a) → a → [b] → a
```

- `pred`：谓词函数。它传递给累加器和当前元素。
- `fn`：迭代器函数。接收两个值，累加器和当前元素。
- `a`：累加器值。
- `list`：要遍历的列表。
- 返回 `*`：最终的累计值。

### 例子

```js
const isOdd = (acc, x) => x % 2 === 1;
const xs = [1, 3, 5, 60, 777, 800];
R.reduceWhile(isOdd, R.add, 0, xs); //=> 9

const ys = [2, 4, 6]
R.reduceWhile(isOdd, R.add, 111, ys); //=> 111
```

### 参考
- [https://ramdajs.com/docs/#reduceWhile](https://ramdajs.com/docs/#reduceWhile)

## reject
`filter` 的补操作。返回结果为 `R.filter` 操作结果的补集。

若在列表位置给出 `transformer`，则用作 `transducer`。`Filterable` 类型包括 `plain object` 或者任何带有 `filter` 方法的类型，如 `Array` 。

### 参数

```
Filterable f => (a → Boolean) → f a → f a
```

- `pred`。
- `filterable`。
- 返回 `Array`。

### 例子

```js
const isOdd = (n) => n % 2 === 1;

R.reject(isOdd, [1, 2, 3, 4]); //=> [2, 4]

R.reject(isOdd, { a: 1, b: 2, c: 3, d: 4 }); //=> {b: 2, d: 4}
```

### 参考
- [https://ramdajs.com/docs/#reject](https://ramdajs.com/docs/#reject)

## remove
删除列表中从 `start` 开始的 `count` 个元素。注意，该操作是非破坏性的：不改变原列表，返回处理后列表的拷贝。

### 参数

```
Number → Number → [a] → [a]
```

- `start`：开始删除元素的位置
- `count`：要删除的元素数
- `list`：要操作的列表
- 返回`Array`：从 `start` 中删除了 `count` 个元素的新数组。

### 例子

```js
R.remove(2, 3, [1,2,3,4,5,6,7,8]); //=> [1,2,6,7,8]
```

### 参考
- [https://ramdajs.com/docs/#remove](https://ramdajs.com/docs/#remove)

## repeat
生成包含 `n` 个同一元素的数组。

### 参数

```
a → n → [a]
```

- `value`：要重复的值。
- `n`：输出列表的所需大小。
- 返回`Array`：一个包含 `n` 个 `value` 的新数组。

### 例子

```js
R.repeat('hi', 5); //=> ['hi', 'hi', 'hi', 'hi', 'hi']

const obj = {};
const repeatedObjs = R.repeat(obj, 5); //=> [{}, {}, {}, {}, {}]
repeatedObjs[0] === repeatedObjs[1]; //=> true
```

### 参考
- [https://ramdajs.com/docs/#repeat](https://ramdajs.com/docs/#repeat)

## reverse
对列表或字符串的排列顺序取反。

### 参数

```
[a] → [a]
String → String
```

- `list`。
- 返回 `Array`。

### 例子

```js
R.reverse([1, 2, 3]);  //=> [3, 2, 1]
R.reverse([1, 2]);     //=> [2, 1]
R.reverse([1]);        //=> [1]
R.reverse([]);         //=> []

R.reverse('abc');      //=> 'cba'
R.reverse('ab');       //=> 'ba'
R.reverse('a');        //=> 'a'
R.reverse('');         //=> ''
```

### 参考
- [https://ramdajs.com/docs/#reverse](https://ramdajs.com/docs/#reverse)

## scan
`scan` 与 `reduce` 类似，但会将每次迭代计算的累积值记录下来，组成一个列表返回。

### 参数

```
((a, b) → a) → a → [b] → [a]
```

- `fn`：迭代器函数。从数组接收两个值，累加器和当前元素。
- `acc`：累加器值。
- 返回 `Array`：所有迭代计算的累积值的列表。

### 例子

```js
const numbers = [1, 2, 3, 4];
const factorials = R.scan(R.multiply, 1, numbers); //=> [1, 1, 2, 6, 24]
```

### 参考
- [https://ramdajs.com/docs/#scan](https://ramdajs.com/docs/#scan)

## sequence
将一个 [Applicative](https://github.com/fantasyland/fantasy-land#applicative) 的 [Traversable](https://github.com/fantasyland/fantasy-land#traversable) 转换成一个 Traversable 类型的 Applicative。

如果第二个参数自身存在 `sequence` 方法，则调用自身的 `sequence`。

### 参数

```
(Applicative f, Traversable t) => (a → f a) → t (f a) → f (t a)
```

- `of`。
- `traversable`。
- 返回 `*`。

### 例子

```js
R.sequence(Maybe.of, [Just(1), Just(2), Just(3)]);   //=> Just([1, 2, 3])
R.sequence(Maybe.of, [Just(1), Just(2), Nothing()]); //=> Nothing()

R.sequence(R.of, Just([1, 2, 3])); //=> [Just(1), Just(2), Just(3)]
R.sequence(R.of, Nothing());       //=> [Nothing()]
```

### 参考
- [https://ramdajs.com/docs/#sequence](https://ramdajs.com/docs/#sequence)

## slice
取出给定的列表或字符串（或带有 `slice` 方法的对象）中，从 `fromIndex`（包括）到 `toIndex`（不包括）的元素。

如果第三个参数自身存在 `slice` 方法，则调用自身的 `slice` 方法。

### 参数

```
Number → Number → [a] → [a]
Number → Number → String → String
```

- `fromIndex`：起始索引（包括）。
- `toIndex`：结束索引（不包括）。
- `list`。
- 返回 `*`。

### 例子

```js
R.slice(1, 3, ['a', 'b', 'c', 'd']);        //=> ['b', 'c']
R.slice(1, Infinity, ['a', 'b', 'c', 'd']); //=> ['b', 'c', 'd']
R.slice(0, -1, ['a', 'b', 'c', 'd']);       //=> ['a', 'b', 'c']
R.slice(-3, -1, ['a', 'b', 'c', 'd']);      //=> ['b', 'c']
R.slice(0, 3, 'ramda');                     //=> 'ram'
```

### 参考
- [https://ramdajs.com/docs/#slice](https://ramdajs.com/docs/#slice)

## sort
使用比较函数对列表进行排序。比较函数每次接受两个参数，如果第一个值较小，则返回负数；如果第一个值较大，则返回正数；如果两值相等，返回零。注意，返回的是列表的拷贝，不会修改原列表。

### 参数

```
((a, a) → Number) → [a] → [a]
```

- `comparator`：比较器函数。
- `list`：排序列表。
- `Array`：一个新数组，其元素由比较器函数排序。

### 例子

```js
const diff = function(a, b) { return a - b; };
R.sort(diff, [4,2,7,5]); //=> [2, 4, 5, 7]
```

### 参考
- [https://ramdajs.com/docs/#sort](https://ramdajs.com/docs/#sort)

## splitAt
在指定的索引处拆分列表或者字符串。

### 参数

```
Number → [a] → [[a], [a]]
Number → String → [String, String]
```

- `index`：数组/字符串被分割的索引。
- `array`：要拆分的数组/字符串。
- 返回 `Array`。

### 例子

```js
R.splitAt(1, [1, 2, 3]);          //=> [[1], [2, 3]]
R.splitAt(5, 'hello world');      //=> ['hello', ' world']
R.splitAt(-1, 'foobar');          //=> ['fooba', 'r']
```

### 参考
- [https://ramdajs.com/docs/#splitAt](https://ramdajs.com/docs/#splitAt)

## splitEvery
将列表拆分成指定长度的子列表集。

### 参数

```
Number → [a] → [[a]]
Number → String → [String]
```

- `n`。
- `list`。
- 返回 `Array`。

### 例子

```js
R.splitEvery(3, [1, 2, 3, 4, 5, 6, 7]); //=> [[1, 2, 3], [4, 5, 6], [7]]
R.splitEvery(3, 'foobarbaz'); //=> ['foo', 'bar', 'baz']
```

### 参考
- [https://ramdajs.com/docs/#splitEvery](https://ramdajs.com/docs/#splitEvery)

## splitWhen
查找列表中首个满足 `predicate` 的元素，在该处将列表拆分为两部分。首个满足 `predicate` 的元素包含在后一部分。

### 参数

```
(a → Boolean) → [a] → [[a], [a]]
```

- `pred`：确定数组拆分位置的谓词函数。
- `list`：要拆分的数组。
- 返回 `Array`。
### 例子

```js
R.splitWhen(R.equals(2), [1, 2, 3, 1, 2, 3]);   //=> [[1], [2, 3, 1, 2, 3]]
```

### 参考
- [https://ramdajs.com/docs/#splitWhen](https://ramdajs.com/docs/#splitWhen)

## startsWith
检查列表是否以给定的值开头。

### 参数

```
[a] → [a] → Boolean
String → String → Boolean
```

- `prefix`。
- `list`。
- 返回 `Boolean`。

### 例子

```js
R.startsWith('a', 'abc')                //=> true
R.startsWith('b', 'abc')                //=> false
R.startsWith(['a'], ['a', 'b', 'c'])    //=> true
R.startsWith(['b'], ['a', 'b', 'c'])    //=> false
```

### 参考
- [https://ramdajs.com/docs/#startsWith](https://ramdajs.com/docs/#startsWith)

## tail
删除列表中的首个元素（或者调用对象的 `tail` 方法）。

如果第一个参数自身存在 `slice` 方法，则调用自身的 `slice` 方法。

### 参数

```
[a] → [a]
String → String
```

- `list`。
- `*`。

### 例子

```js
R.tail([1, 2, 3]);  //=> [2, 3]
R.tail([1, 2]);     //=> [2]
R.tail([1]);        //=> []
R.tail([]);         //=> []

R.tail('abc');  //=> 'bc'
R.tail('ab');   //=> 'b'
R.tail('a');    //=> ''
R.tail('');     //=> ''
```

### 参考
- [https://ramdajs.com/docs/#tail](https://ramdajs.com/docs/#tail)

## take
返回列表的前 `n` 个元素、字符串的前 `n` 个字符或者用作 `transducer/transform`（或者调用对象的 `take` 方法）。

如果第二个参数自身存在 `take` 方法，则调用自身的 `take` 方法。

### 参数

```
Number → [a] → [a]
Number → String → String
```

- `n`。
- `list`。
- 返回 `*`。

### 例子

```js
R.take(1, ['foo', 'bar', 'baz']); //=> ['foo']
R.take(2, ['foo', 'bar', 'baz']); //=> ['foo', 'bar']
R.take(3, ['foo', 'bar', 'baz']); //=> ['foo', 'bar', 'baz']
R.take(4, ['foo', 'bar', 'baz']); //=> ['foo', 'bar', 'baz']
R.take(3, 'ramda');               //=> 'ram'

const personnel = [
    'Dave Brubeck',
    'Paul Desmond',
    'Eugene Wright',
    'Joe Morello',
    'Gerry Mulligan',
    'Bob Bates',
    'Joe Dodge',
    'Ron Crotty'
];

const takeFive = R.take(5);
takeFive(personnel);
//=> ['Dave Brubeck', 'Paul Desmond', 'Eugene Wright', 'Joe Morello', 'Gerry Mulligan']
```

### 参考
- [https://ramdajs.com/docs/#take](https://ramdajs.com/docs/#take)

## takeLast
返回列表的后 `n` 个元素。如果 `n > list.length`，则返回 `list.length` 个元素。

### 参数

```
Number → [a] → [a]
Number → String → String
```

- `n`：要返回的元素数。
- `xs`：要考虑的集合。
- 返回 `Array`。

### 例子

```js
R.takeLast(1, ['foo', 'bar', 'baz']); //=> ['baz']
R.takeLast(2, ['foo', 'bar', 'baz']); //=> ['bar', 'baz']
R.takeLast(3, ['foo', 'bar', 'baz']); //=> ['foo', 'bar', 'baz']
R.takeLast(4, ['foo', 'bar', 'baz']); //=> ['foo', 'bar', 'baz']
R.takeLast(3, 'ramda');               //=> 'mda'
```

### 参考
- [https://ramdajs.com/docs/#takeLast](https://ramdajs.com/docs/#takeLast)

## takeLastWhile
从后往前取出列表元素，直到遇到首个不满足 `predicate` 的元素为止。取出的元素中不包含首个不满足 `predicate` 的元素。

### 参数

```
(a → Boolean) → [a] → [a]
(a → Boolean) → String → String
```

- `fn`：每次迭代调用的函数。
- `xs`：要遍历的集合。
- 返回 `Array`：一个新的数组。

### 例子

```js
const isNotOne = x => x !== 1;

R.takeLastWhile(isNotOne, [1, 2, 3, 4]); //=> [2, 3, 4]

R.takeLastWhile(x => x !== 'R', 'Ramda'); //=> 'amda'
```

### 参考
- [https://ramdajs.com/docs/#takeLastWhile](https://ramdajs.com/docs/#takeLastWhile)

## takeWhile
从前往后取出列表元素，直到遇到首个不满足 `predicate` 的元素为止。取出的元素中不包含首个不满足 `predicate` 的元素。

若第二个参数自身存在 `takeWhile` 方法，则调用自身的 `takeWhile` 方法

若在列表位置中给出 `transfomer`，则用作 `transducer` 。

### 参数

```
(a → Boolean) → [a] → [a]
(a → Boolean) → String → String
```

- `fn`：每次迭代调用的函数。
- `xs`：要遍历的集合。
- 返回 `Array`：一个新的数组。

### 例子

```js
const isNotFour = x => x !== 4;

R.takeWhile(isNotFour, [1, 2, 3, 4, 3, 2, 1]); //=> [1, 2, 3]

R.takeWhile(x => x !== 'd', 'Ramda'); //=> 'Ram'
```

### 参考
- [https://ramdajs.com/docs/#takeWhile](https://ramdajs.com/docs/#takeWhile)

## times
执行输入的函数 `n` 次，返回由函数执行结果组成的数组。

`fn` 为一元函数，`n` 次调用接收的参数为：从 `0` 递增到 `n-1` 。

### 参数

```
(Number → a) → Number → [a]
```

- `fn`：要调用的函数。传递了一个参数，`n` 的当前值。
- `n`：介于 `0` 到 `n-1` 之间的值。每个函数调用后增加。
- 返回 `Array`：一个包含所有对 `fn` 调用的返回值的数组。

### 例子

```js
R.times(R.identity, 5); //=> [0, 1, 2, 3, 4]
```

### 参考
- [https://ramdajs.com/docs/#times](https://ramdajs.com/docs/#times)

## transduce
用 iterator function 初始化 transducer ，生成一个 transformed iterator function。然后顺次遍历列表，对每个列表元素先进行转换，然后与累积值进行归约，返回值作为下一轮迭代的累积值。最终返回与初始累积值类型相同的一个累积值。

iterator function 接收两个参数：`(acc, value)` ，iterator function 会被封装为 transformer 来初始化 transducer 。可以直接传递 transformer 来代替 iterator function。这两种情况下，可以使用 `R.reduced` 提前终止迭代操作。

transducer 函数接受一个 transformer ，返回一个新的 transformer ，并且 transducer 函数可以直接组合。

transformer 是一个对象，其中包含二元 reducing iterator、step、零元 init 和 一元 result 函数。step 作为 reduce 过程中的迭代函数；result 将最终的累积值转换为需要的返回类型（通常为 `R.identity` ）；init 提供初始累积值，但通常会被 transduce 函数忽略。

在 transducer 初始化之后，使用 `R.reduce` 进行迭代操作。

### 参数

```
(c → c) → ((a, b) → a) → a → [b] → a
```

- `xf`：transducer 函数。接收一个 transformer 并返回一个 transformer。
- `fn`：迭代器函数。从数组接收两个值，即 accumulator 和当前元素。包装成 transformer（如有必要），并用于初始化 transducer。
- `acc`：初始 accumulator 值。
- `list`：要遍历的列表。
- 返回 `*`：最终的累计值。

### 例子

```js
const numbers = [1, 2, 3, 4];
const transducer = R.compose(R.map(R.add(1)), R.take(2));
R.transduce(transducer, R.flip(R.append), [], numbers); //=> [2, 3]

const isOdd = (x) => x % 2 === 1;
const firstOddTransducer = R.compose(R.filter(isOdd), R.take(1));
R.transduce(firstOddTransducer, R.flip(R.append), [], R.range(0, 100)); //=> [1]
```

### 参考
- [https://ramdajs.com/docs/#transduce](https://ramdajs.com/docs/#transduce)

## transpose

二维数组行列转置。输入 `n` 个长度为 `x` 的数组，输出 `x` 个长度为 `n` 的数组。

### 参数

```
[[a]] → [[a]]
```

- `list`：2D 列表。
- 返回 `Array`：2D 列表。

### 例子

```js
R.transpose([[1, 'a'], [2, 'b'], [3, 'c']]) //=> [[1, 2, 3], ['a', 'b', 'c']]
R.transpose([[1, 2, 3], ['a', 'b', 'c']]) //=> [[1, 'a'], [2, 'b'], [3, 'c']]

// If some of the rows are shorter than the following rows, their elements are skipped:
R.transpose([[10, 11], [20], [], [30, 31, 32]]) //=> [[10, 20, 30], [11, 31], [32]]
```

### 参考
- [https://ramdajs.com/docs/#transpose](https://ramdajs.com/docs/#transpose)

## traverse
将返回值为 [Applicative](https://github.com/fantasyland/fantasy-land#applicative) 类型的函数映射到一个 [Traversable](https://github.com/fantasyland/fantasy-land#traversable) 上。然后使用 `sequence` 将结果由 Traversable of Applicative 转换为 Applicative of Traversable。

若第三个参数自身存在 `traverse` 方法，则调用自身的 `traverse` 方法。

### 参数

```
(Applicative f, Traversable t) => (a → f a) → (a → f b) → t a → f (t b)
```

- `of`。
- `f`。
- `traversable`。
- 返回 `*`。

### 例子

```js
// Returns `Maybe.Nothing` if the given divisor is `0`
const safeDiv = n => d => d === 0 ? Maybe.Nothing() : Maybe.Just(n / d)

R.traverse(Maybe.of, safeDiv(10), [2, 4, 5]); //=> Maybe.Just([5, 2.5, 2])
R.traverse(Maybe.of, safeDiv(10), [2, 0, 5]); //=> Maybe.Nothing
```

### 参考
- [https://ramdajs.com/docs/#traverse](https://ramdajs.com/docs/#traverse)

## unfold
通过一个种子值（ `seed` ）创建一个列表。`unfold` 接受一个迭代函数：该函数或者返回 `false` 停止迭代，或者返回一个长度为 2 的数组：数组首个元素添加到结果列表，第二个元素作为种子值传给下一轮迭代使用。

迭代函数接受单个参数：`(seed)` 。

### 参数

```
(a → [b]) → * → [b]
```

- `fn`：迭代器函数。接收一个参数 `seed` ，该函数或者返回 `false` 停止迭代，或者返回一个长度为 2 的数组。该数组索引 0 处的元素将被添加到结果数组中，索引 1 处的元素将被传递到对 `fn` 的下一次调用。
- `seed`：种子值。
- 返回 `Array`：最终列表。

### 例子

```js
const f = n => n > 50 ? false : [-n, n + 10];
R.unfold(f, 10); //=> [-10, -20, -30, -40, -50]
```

### 参考
- [https://ramdajs.com/docs/#unfold](https://ramdajs.com/docs/#unfold)

## uniq
列表去重操作。返回无重复元素的列表。通过 `R.equals` 函数进行相等性判断。

### 参数

```
[a] → [a]
```

- `list`：要考虑的数组。
- 返回 `Array`：无重复元素的列表。

### 例子

```js
R.uniq([1, 1, 2, 1]); //=> [1, 2]
R.uniq([1, '1']);     //=> [1, '1']
R.uniq([[42], [42]]); //=> [[42]]
```

### 参考
- [https://ramdajs.com/docs/#uniq](https://ramdajs.com/docs/#uniq)

## uniqBy
返回无重复元素的列表。元素通过给定的函数的返回值以及 `R.equals` 进行相同性判断。如果给定的函数返回值相同，保留第一个元素。

### 参数

```
(a → b) → [a] → [a]
```

- `fn`：用于产生在比较期间使用的值的函数。
- `list`：要考虑的数组。
- 返回 `Array`：无重复元素的列表。

### 例子

```js
R.uniqBy(Math.abs, [-1, -5, 2, 10, 1, 2]); //=> [-1, -5, 2, 10]
```

### 参考
- [https://ramdajs.com/docs/#uniqBy](https://ramdajs.com/docs/#uniqBy)

## uniqWith
返回无重复元素的列表。元素通过 `predicate` 进行相同性判断。如果通过 `predicate` 判断两元素相同，保留第一个元素。

### 参数

```
((a, a) → Boolean) → [a] → [a]
```

- `pred`：用于测试两个项目是否相等的谓词函数。
- `list`：要考虑的数组。
- 返回 `Array`：无重复元素的列表。

### 例子

```js
const strEq = R.eqBy(String);
R.uniqWith(strEq)([1, '1', 2, 1]); //=> [1, 2]
R.uniqWith(strEq)([{}, {}]);       //=> [{}]
R.uniqWith(strEq)([1, '1', 1]);    //=> [1]
R.uniqWith(strEq)(['1', 1, 1]);    //=> ['1']
```

### 参考
- [https://ramdajs.com/docs/#uniqWith](https://ramdajs.com/docs/#uniqWith)

## unnest
`R.chain(R.identity)` 的简写, 对 [Chain](https://github.com/fantasyland/fantasy-land#chain) 类型的数据消除一层嵌套.

### 参数

```
Chain c => c (c a) → c a
```

- `list`。
- 返回 `*`。

### 例子

```js
R.unnest([1, [2], [[3]]]); //=> [1, 2, [3]]
R.unnest([[1, 2], [3, 4], [5, 6]]); //=> [1, 2, 3, 4, 5, 6]
```

### 参考
- [https://ramdajs.com/docs/#unnest](https://ramdajs.com/docs/#unnest)

## update
替换数组中指定索引处的值。

### 参数

```
Number → a → [a] → [a]
```

- `idx`：要更新的索引。
- `x`：在返回数组的给定索引处存在的值。
- `list`：要更新的源类数组对象。
- 返回 `Array`：列表 `list` 的副本的值在索引 `​​idx` 处被 `x` 取代。

### 例子

```js
R.update(1, '_', ['a', 'b', 'c']);      //=> ['a', '_', 'c']
R.update(-1, '_', ['a', 'b', 'c']);     //=> ['a', 'b', '_']
```

### 参考
- [https://ramdajs.com/docs/#update](https://ramdajs.com/docs/#update)

## without
求第二个列表中，未包含在第一个列表中的任一元素的集合。通过 `R.equals` 函数进行相等性判断。

若在列表位置中给出 `transfomer`，则用作 `transducer` 。

### 参数

```
[a] → [a] → [a]
```

- `list1`：要从 `list2` 中删除的值。
- `list2`：要从中删除值的数组。
- 返回 `Array`：`list2`中，未包含 `list1` 中的任一元素的新数组。

### 例子

```js
R.without([1, 2], [1, 2, 1, 3, 4]); //=> [3, 4]
```

### 参考
- [https://ramdajs.com/docs/#without](https://ramdajs.com/docs/#without)

## xprod

将两个列表的元素两两组合，生成一个新的元素对列表。

### 参数

```
[a] → [b] → [[a,b]]
```

- `as`：第一个列表。
- `bs`：第二个列表。
- 返回 `Array`：通过将 `as` 和 `bs` 中的每个可能的对组合成 `[a，b]` 而制成的列表。

### 例子

```js
R.xprod([1, 2], ['a', 'b']); //=> [[1, 'a'], [1, 'b'], [2, 'a'], [2, 'b']]
```

### 参考
- [https://ramdajs.com/docs/#xprod](https://ramdajs.com/docs/#xprod)

## zip
将两个列表对应位置的元素组合，生成一个新的元素对列表。生成的列表长度取决于较短的输入列表的长度。

注意，`zip` 等价于 `zipWith(function(a, b) { return [a, b] })` 。

### 参数

```
[a] → [b] → [[a,b]]
```

- `list1`：要考虑的第一个数组。
- `list2`：要考虑的第二个数组。
- 返回 `Array`：该列表是通过将 `list1` 和 `list2` 的相同索引的元素配对而成的。

### 例子

```js
R.zip([1, 2, 3], ['a', 'b', 'c']); //=> [[1, 'a'], [2, 'b'], [3, 'c']]
```

### 参考
- [https://ramdajs.com/docs/#zip](https://ramdajs.com/docs/#zip)

## zipObj
将两个列表对应位置的元素作为键值对组合，生成一个新的键值对的列表。生成的列表长度取决于较短的输入列表的长度。

注意，`zipObj` 等价于 `pipe(zip, fromPairs)` 。

### 参数

```
[String] → [*] → {String: *}
```

- `keys`：将是输出对象上的属性的数组。
- `values`：输出对象上的值列表。
- 返回 `Object`：通过将 `keys` 和 `values` 的相同索引的元素配对来制成的对象。

### 例子

```js
R.zipObj(['a', 'b', 'c'], [1, 2, 3]); //=> {a: 1, b: 2, c: 3}
```

### 参考
- [https://ramdajs.com/docs/#zipObj](https://ramdajs.com/docs/#zipObj)

## zipWith
将两个列表对应位置的元素通过一个函数处理，生成一个新的元素的列表。生成的列表长度取决于较短的输入列表的长度。

### 参数

```
((a, b) → c) → [a] → [b] → [c]
```

- `fn`：该函数用于将两个元素组合为一个值。
- `list1`：要考虑的第一个数组。
- `list2`：要考虑的第二个数组。
- 返回 `Array`：通过使用 `fn`组合 `list1` 和 `list2` 的相同索引的元素配对而成的。

### 例子

```js
const f = (x, y) => {
    // ...
};
R.zipWith(f, [1, 2, 3], ['a', 'b', 'c']);
//=> [f(1, 'a'), f(2, 'b'), f(3, 'c')]
```

### 参考
- [https://ramdajs.com/docs/#zipWith](https://ramdajs.com/docs/#zipWith)

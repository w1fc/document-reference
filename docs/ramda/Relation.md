## clamp
将数字限制在指定的范围内。

`clamp` 也可用于其他有序类型，如字符串和日期。

### 参数

```
Ord a => a → a → a → a
```

- `minimum`：下限（含）
- `maximum`：上限（含）
- `value`：取值
- 返回`Number`“当 `val < minimum` 时返回 `minimum`，`val > maximum` 时返回 `maximum`，否则返回 `val`。

### 例子

```js
R.clamp(1, 10, -5) // => 1
R.clamp(1, 10, 15) // => 10
R.clamp(1, 10, 4)  // => 4
```

### 参考
- [https://ramdajs.com/docs/#clamp](https://ramdajs.com/docs/#clamp)

## countBy
根据给定函数提供的统计规则对列表中的元素进行分类计数。返回一个对象，其键值对为：`fn` 根据列表元素生成键，列表中通过 `fn` 映射为对应键的元素的个数作为值。注意，由于 JavaScript 对象的实现方式，所有键都被强制转换为字符串。

若在列表位置中给出 `transfomer`，则用作 `transducer` 。

### 参数

```
(a → String) → [a] → {*}
```

- `fn`：用于将值映射到键的函数。
- `list`：从中计数元素的列表。
- 返回`Object`：对象映射键指向列表中的出现次数。

### 例子

```js
const numbers = [1.0, 1.1, 1.2, 2.0, 3.0, 2.2];
R.countBy(Math.floor)(numbers);    //=> {'1': 3, '2': 2, '3': 1}

const letters = ['a', 'b', 'A', 'a', 'B', 'c'];
R.countBy(R.toLower)(letters);   //=> {'a': 3, 'b': 2, 'c': 1}
```

### 参考
- [https://ramdajs.com/docs/#countBy](https://ramdajs.com/docs/#countBy)

## difference
求差集。求第一个列表中，未包含在第二个列表中的任一元素的集合。对象和数组比较数值相等，而非引用相等。

### 参数

```
[*] → [*] → [*]
```

- `list1`：第一个列表。
- `list2`：第二个列表。
- `Array`：`list1` 中不在 `list2` 中的元素。

### 例子

```js
R.difference([1, 2, 3, 4], [7, 6, 5, 4, 3]); //=> [1,2]
R.difference([7, 6, 5, 4, 3], [1, 2, 3, 4]); //=> [7,6,5]
R.difference([{ a: 1 }, { b: 2 }], [{ a: 1 }, { c: 3 }]) //=> [{b: 2}]
```

### 参考
- [https://ramdajs.com/docs/#difference](https://ramdajs.com/docs/#difference)

## differenceWith
求第一个列表中未包含在第二个列表中的所有元素的集合（集合中没有重复元素）。两列表中的元素通过 `predicate` 判断相应元素是否同时 “包含在” 两列表中。

### 参数

```
((a, a) → Boolean) → [a] → [a] → [a]
```

- `pred`：用于测试两个项目是否相等的谓词函数。
- `list1`：第一个列表。
- `list2`：第二个列表。
- `Array`：`list1` 中不在 `list2` 中的元素。

### 例子

```js
const cmp = (x, y) => x.a === y.a;
const l1 = [{ a: 1 }, { a: 2 }, { a: 3 }];
const l2 = [{ a: 3 }, { a: 4 }];
R.differenceWith(cmp, l1, l2); //=> [{a: 1}, {a: 2}]
```

### 参考
- [https://ramdajs.com/docs/#differenceWith](https://ramdajs.com/docs/#differenceWith)

## eqBy
接受一个函数和两个值，通过传入函数对两个值进行相等性判断。如果两个值的计算结果相等，则返回 `true` ；否则返回 `false` 。

### 参数

```
(a → b) → a → a → Boolean
```

- `f`。
- `x`。
- `y`。
- 返回`Boolean`。

### 例子

```js
R.eqBy(Math.abs, 5, -5); //=> true
```

### 参考
- [https://ramdajs.com/docs/#eqBy](https://ramdajs.com/docs/#eqBy)

## equals
如果传入的参数相等，返回 `true`；否则返回 `false`。可以处理几乎所有 JavaScript 支持的数据结构。

若两个参数自身存在 `equals` 方法，则对称地调用自身的 `equals` 方法。

### 参数

```
a → b → Boolean
```

- `a`。
- `b`。
- 返回`Boolean`。

### 例子

```js
R.equals(1, 1); //=> true
R.equals(1, '1'); //=> false
R.equals([1, 2, 3], [1, 2, 3]); //=> true

const a = {}; a.v = a;
const b = {}; b.v = b;
R.equals(a, b); //=> true
```

### 参考
- [https://ramdajs.com/docs/#equals](https://ramdajs.com/docs/#equals)

## gt
如果首个参数大于第二个参数，返回 `true`；否则返回 `false`。

### 参数

```
Ord a => a → a → Boolean
```

- `a`。
- `b`。
- 返回`Boolean`。

### 例子

```js
R.gt(2, 1); //=> true
R.gt(2, 2); //=> false
R.gt(2, 3); //=> false
R.gt('a', 'z'); //=> false
R.gt('z', 'a'); //=> true
```

### 参考
- [https://ramdajs.com/docs/#gt](https://ramdajs.com/docs/#gt)

## gte
如果首个参数大于或等于第二个参数，返回 `true`；否则返回 `false`。

### 参数

```
Ord a => a → a → Boolean
```

- `a`。
- `b`。
- 返回`Boolean`。

### 例子

```js
R.gte(2, 1); //=> true
R.gte(2, 2); //=> true
R.gte(2, 3); //=> false
R.gte('a', 'z'); //=> false
R.gte('z', 'a'); //=> true
```

### 参考
- [https://ramdajs.com/docs/#gte](https://ramdajs.com/docs/#gte)

## identical
如果两个参数是完全相同，则返回 `true`，否则返回 `false`。如果它们引用相同的内存，也认为是完全相同的。`NaN` 和 `NaN` 是完全相同的；`0` 和 `-0` 不是完全相同的。

注意：这只是 ES6 `Object.is` 的柯里化版本而已。

### 参数

```
a → a → Boolean
```

- `a`。
- `b`。
- 返回`Boolean`。

### 例子

```js
const o = {};
R.identical(o, o); //=> true
R.identical(1, 1); //=> true
R.identical(1, '1'); //=> false
R.identical([], []); //=> false
R.identical(0, -0); //=> false
R.identical(NaN, NaN); //=> true
```

### 参考
- [https://ramdajs.com/docs/#identical](https://ramdajs.com/docs/#identical)

## innerJoin
接受一个谓词函数 `pred` 、列表 `xs` 和 `ys` ，返回列表 `xs'`。依次取出 `xs` 中的元素，若通过 `pred` 判断等于 `ys` 中的一个或多个元素，则放入 `xs'` 。

`pred` 必须为二元函数，两个参数分别来自于对应两个列表中的元素。

`xs`、`ys` 和 `xs'` 被当作集合处理，所以从语义上讲，元素的顺序并不重要，但由于 `xs'` 是列表（列表中元素有排列顺序），所以本实现保证 `xs'` 中元素的顺序与 `xs` 中的一致。重复的元素也不会被移除，因此，若 `xs` 中含重复元素，`xs'` 中也会包含元素。

### 参数

```
((a, b) → Boolean) → [a] → [b] → [a]
```

- `pred`。
- `xs`。
- `ys`。
- `Array`。

### 例子

```js
R.innerJoin(
    (record, id) => record.id === id,
    [{ id: 824, name: 'Richie Furay' },
    { id: 956, name: 'Dewey Martin' },
    { id: 313, name: 'Bruce Palmer' },
    { id: 456, name: 'Stephen Stills' },
    { id: 177, name: 'Neil Young' }],
    [177, 456, 999]
);
//=> [{id: 456, name: 'Stephen Stills'}, {id: 177, name: 'Neil Young'}]
```

### 参考
- [https://ramdajs.com/docs/#innerJoin](https://ramdajs.com/docs/#innerJoin)

## intersection
取出两个 `list` 中相同的元素组成的 `set` 。

### 参数

```
[*] → [*] → [*]
```

- `list1`：第一个列表。
- `list2`：第二个列表。
- 返回`Array`：在 `list1` 和 `list2` 中都可以找到的元素列表。

### 例子

```js
R.intersection([1, 2, 3, 4], [7, 6, 5, 4, 3]); //=> [4, 3]
```

### 参考
- [https://ramdajs.com/docs/#intersection](https://ramdajs.com/docs/#intersection)

## lt
如果首个参数小于第二个参数，返回 `true`；否则返回 `false`。

### 参数

```
Ord a => a → a → Boolean
```

- `a`。
- `b`。
- 返回`Boolean`。

### 例子

```js
R.lt(2, 1); //=> false
R.lt(2, 2); //=> false
R.lt(2, 3); //=> true
R.lt('a', 'z'); //=> true
R.lt('z', 'a'); //=> false
```

### 参考
- [https://ramdajs.com/docs/#lt](https://ramdajs.com/docs/#lt)

## lte
如果首个参数小于或等于第二个参数，返回 `true`；否则返回 `false`。

### 参数

```
Ord a => a → a → Boolean
```

- `a`。
- `b`。
- 返回`Boolean`。

### 例子

```js
R.lte(2, 1); //=> false
R.lte(2, 2); //=> true
R.lte(2, 3); //=> true
R.lte('a', 'z'); //=> true
R.lte('z', 'a'); //=> false
```

### 参考
- [https://ramdajs.com/docs/#lte](https://ramdajs.com/docs/#lte)

## max
返回两个参数中的较大值。

### 参数

```
Ord a => a → a → a
```

- `a`。
- ``b`。
- 返回`*`。

### 例子

```js
R.max(789, 123); //=> 789
R.max('a', 'b'); //=> 'b'
```

### 参考
- [https://ramdajs.com/docs/#max](https://ramdajs.com/docs/#max)

## maxBy
接收一个函数和两个值，返回使给定函数执行结果较大的值。

### 参数

```
Ord b => (a → b) → a → a → a
```

- `f`。
- `a`。
- `b`。
- 返回`*`。

### 例子

```js
//  square :: Number -> Number
const square = n => n * n;

R.maxBy(square, -3, 2); //=> -3

R.reduce(R.maxBy(square), 0, [3, -5, 4, 1, -2]); //=> -5
R.reduce(R.maxBy(square), 0, []); //=> 0
```

### 参考
- [https://ramdajs.com/docs/#maxBy](https://ramdajs.com/docs/#maxBy)

## min
返回两个参数中的较小值。

### 参数

```
Ord a => a → a → a
```

- `a`。
- ``b`。
- 返回`*`。

### 例子

```js
R.min(789, 123); //=> 123
R.min('a', 'b'); //=> 'a'
```

### 参考
- [https://ramdajs.com/docs/#min](https://ramdajs.com/docs/#min)

## minBy
接收一个函数和两个值，返回使给定函数执行结果较小的值。

### 参数

```
Ord b => (a → b) → a → a → a
```

- `f`。
- `a`。
- `b`。
- 返回`*`。

### 例子

```js
//  square :: Number -> Number
const square = n => n * n;

R.minBy(square, -3, 2); //=> 2

R.reduce(R.minBy(square), Infinity, [3, -5, 4, 1, -2]); //=> 1
R.reduce(R.minBy(square), Infinity, []); //=> Infinity
```

### 参考
- [https://ramdajs.com/docs/#minBy](https://ramdajs.com/docs/#minBy)

## pathEq
判断对象的嵌套路径上是否为给定的值，通过 `R.equals` 函数进行相等性判断。常用于列表过滤。

### 参数

```
[Idx] → a → {a} → Boolean
Idx = String | Int
```

- `path`：要使用的嵌套属性的路径
- `val`：与嵌套属性进行比较的值
- `obj`：检查嵌套属性的对象
- 返回`Boolean`：如果该值等于嵌套对象的属性，则为 `true`；否则为 `false`。

### 例子

```js
const user1 = { address: { zipCode: 90210 } };
const user2 = { address: { zipCode: 55555 } };
const user3 = { name: 'Bob' };
const users = [user1, user2, user3];
const isFamous = R.pathEq(['address', 'zipCode'], 90210);
R.filter(isFamous, users); //=> [ user1 ]
```

### 参考
- [https://ramdajs.com/docs/#pathEq](https://ramdajs.com/docs/#pathEq)

## propEq
如果指定对象属性与给定的值相等，则返回 `true` ；否则返回 `false` 。通过 `R.equals` 函数进行相等性判断。可以使用 `R.whereEq` 进行多个属性的相等性判断。

### 参数

```
String → a → Object → Boolean
```

- `name`。
- `val`。
- `obj`。
- 返回`Boolean`。

### 例子

```js
const abby = { name: 'Abby', age: 7, hair: 'blond' };
const fred = { name: 'Fred', age: 12, hair: 'brown' };
const rusty = { name: 'Rusty', age: 10, hair: 'brown' };
const alois = { name: 'Alois', age: 15, disposition: 'surly' };
const kids = [abby, fred, rusty, alois];
const hasBrownHair = R.propEq('hair', 'brown');
R.filter(hasBrownHair, kids); //=> [fred, rusty]
```

### 参考
- [https://ramdajs.com/docs/#propEq](https://ramdajs.com/docs/#propEq)

## sortBy
根据给定的函数对列表进行排序。

### 参数

```
Ord b => (a → b) → [a] → [a]
```

- `fn`
- `list`：要进行排序的列表。
- 返回`Array`：一个新列表，按 `fn` 生成的键排序。

### 例子

```js
const sortByFirstItem = R.sortBy(R.prop(0));
const pairs = [[-1, 1], [-2, 2], [-3, 3]];
sortByFirstItem(pairs); //=> [[-3, 3], [-2, 2], [-1, 1]]

const sortByNameCaseInsensitive = R.sortBy(R.compose(R.toLower, R.prop('name')));
const alice = {
    name: 'ALICE',
    age: 101
};
const bob = {
    name: 'Bob',
    age: -10
};
const clara = {
    name: 'clara',
    age: 314.159
};
const people = [clara, bob, alice];
sortByNameCaseInsensitive(people); //=> [alice, bob, clara]
```

### 参考
- [https://ramdajs.com/docs/#sortBy](https://ramdajs.com/docs/#sortBy)

## sortWith
依据比较函数列表对输入列表进行排序。

### 参数

```
[(a, a) → Number] → [a] → [a]
```

- `functions`：比较器函数列表。
- `list`：要进行排序的列表。
- `Array`：根据比较器函数排序的新列表。

### 例子

```js
const alice = {
    name: 'alice',
    age: 40
};
const bob = {
    name: 'bob',
    age: 30
};
const clara = {
    name: 'clara',
    age: 40
};
const people = [clara, bob, alice];
const ageNameSort = R.sortWith([
    R.descend(R.prop('age')),
    R.ascend(R.prop('name'))
]);
ageNameSort(people); //=> [alice, clara, bob]
```

### 参考
- [https://ramdajs.com/docs/#sortWith](https://ramdajs.com/docs/#sortWith)

## symmetricDifference
求对称差集。所有不属于两列表交集元素的集合，其元素在且仅在给定列表中的一个里面出现。

### 参数

```
[*] → [*] → [*]
```

- `list1`：第一个列表。
- `list2`：第二个列表。
- `Array`：`list1` 或 `list2` 中的元素，但不能同时包含两者。

### 例子

```js
R.symmetricDifference([1,2,3,4], [7,6,5,4,3]); //=> [1,2,7,6,5]
R.symmetricDifference([7,6,5,4,3], [1,2,3,4]); //=> [7,6,5,1,2]
```

### 参考
- [https://ramdajs.com/docs/#symmetricDifference](https://ramdajs.com/docs/#symmetricDifference)

## symmetricDifferenceWith
求对称差集。所有不属于两列表交集元素的集合。交集的元素由条件函数的返回值决定。

### 参数

```
((a, a) → Boolean) → [a] → [a] → [a]
```

- `pred`：用于测试两个项目是否相等的谓词函数。
- `list1`：第一个列表。
- `list2`：第二个列表。
- `Array`：`list1` 或 `list2` 中的元素，但不能同时包含两者。

### 例子

```js
const eqA = R.eqBy(R.prop('a'));
const l1 = [{ a: 1 }, { a: 2 }, { a: 3 }, { a: 4 }];
const l2 = [{ a: 3 }, { a: 4 }, { a: 5 }, { a: 6 }];
R.symmetricDifferenceWith(eqA, l1, l2); //=> [{a: 1}, {a: 2}, {a: 5}, {a: 6}]
```

### 参考
- [https://ramdajs.com/docs/#symmetricDifferenceWith](https://ramdajs.com/docs/#symmetricDifferenceWith)

## union
集合并运算，合并两个列表为新列表（新列表中无重复元素）。

### 参数

```
[*] → [*] → [*]
```

- `as`：第一个列表。
- `bs`：第二个列表。
- 返回`Array`：第一和第二个列表串联在一起，删除了重复项。

### 例子

```js
R.union([1, 2, 3], [2, 3, 4]); //=> [1, 2, 3, 4]
```

### 参考
- [https://ramdajs.com/docs/#union](https://ramdajs.com/docs/#union)

## unionWith
集合并运算，合并两个列表为新列表（新列表中无重复元素）。由 `predicate` 的返回值决定两元素是否重复。

### 参数

```
((a, a) → Boolean) → [*] → [*] → [*]
```

- `pred`：用于测试两个项目是否相等的谓词函数。
- `list1`：第一个列表。
- `list2`：第二个列表。
- `Array`：第一和第二个列表串联在一起，删除了重复项。

### 例子

```js
const l1 = [{ a: 1 }, { a: 2 }];
const l2 = [{ a: 1 }, { a: 4 }];
R.unionWith(R.eqBy(R.prop('a')), l1, l2); //=> [{a: 1}, {a: 2}, {a: 4}]
```

### 参考
- [https://ramdajs.com/docs/#unionWith](https://ramdajs.com/docs/#unionWith)

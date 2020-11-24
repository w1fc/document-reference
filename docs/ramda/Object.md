## assoc
浅复制对象，然后设置或覆盖对象的指定属性。

注意，该函数也会将 `prototype` 属性复制到新的对象中。所有 `non-primitive` 属性都通过引用复制。

### 参数

```
String → a → {k: v} → {k: v}
```

- `prop`：要设置的属性名称。
- `val`：新值。
- `obj`：要克隆的对象。
- 返回`Object`：一个与原始对象等效的新对象，但更改后的属性除外。

### 例子

```js
R.assoc('c', 3, {a: 1, b: 2}); //=> {a: 1, b: 2, c: 3}
```

### 参考
- [https://ramdajs.com/docs/#assoc](https://ramdajs.com/docs/#assoc)

## assocPath
浅复制对象，设置或覆盖即将创建的给定路径所需的节点，并将特定值放在该路径的末端。

注意，这也会将 `prototype` 属性复制到新对象上。所有 `non-primitive` 属性都通过引用复制。

### 参数

```
[Idx] → a → {a} → {a}
Idx = String | Int
```

- `path`：要设置的路径。
- `val`：新值。
- `obj`：要克隆的对象。
- `Object`：一个新对象，它与原始对象相同，但沿着指定路径的对象除外。

### 例子

```js
R.assocPath(['a', 'b', 'c'], 42, { a: { b: { c: 0 } } }); //=> {a: {b: {c: 42}}}

// Any missing or non-object keys in path will be overridden
R.assocPath(['a', 'b', 'c'], 42, { a: 5 }); //=> {a: {b: {c: 42}}}
```

### 参考
- [https://ramdajs.com/docs/#assocPath](https://ramdajs.com/docs/#assocPath)

## clone
深复制。其值可能（嵌套）包含 `Array`、`Object`、`Number`、`String`、`Boolean`、`Date` 类型的数据。`Function` 通过引用复制。

若自身存在 `clone` 方法，则调用自身的 `clone` 方法。

### 参数

```
{*} → {*}
```

- `value`：要克隆的对象或数组。
- 返回`*`：`value` 的深克隆副本

### 例子

```js
const objects = [{}, {}, {}];
const objectsClone = R.clone(objects);
objects === objectsClone; //=> false
objects[0] === objectsClone[0]; //=> false
```

### 参考
- [https://ramdajs.com/docs/#clone](https://ramdajs.com/docs/#clone)

## dissoc

删除对象中指定 `prop` 属性。

### 参数

```
String → {k: v} → {k: v}
```

- `prop`：要分离的属性的名称。
- `obj`：要克隆的对象。
- 返回`Object`：与原始对象等效但没有指定属性的新对象。

### 例子

```js
R.dissoc('b', { a: 1, b: 2, c: 3 }); //=> {a: 1, c: 3}
```

### 参考
- [https://ramdajs.com/docs/#dissoc](https://ramdajs.com/docs/#dissoc)

## dissocPath
浅复制对象，删除返回对象中指定路径上的属性。

注意，这也会将 `prototype` 属性复制到新对象上并展开。所有 `non-primitive` 属性都通过引用复制。

### 参数

```
[Idx] → {k: v} → {k: v}
Idx = String | Int
```

- `path`：省略值的路径。
- `obj`：要克隆的对象。
- 返回`Object`：在路径中去除了属性的新对象。

### 例子

```js
R.dissocPath(['a', 'b', 'c'], { a: { b: { c: 42 } } }); //=> {a: {b: {}}}
```

### 参考
- [https://ramdajs.com/docs/#dissocPath](https://ramdajs.com/docs/#dissocPath)

## eqProps
判断两个对象指定的属性值是否相等。通过 `R.equals` 函数进行相等性判断。可用作柯里化的 `predicate` 。

### 参数

```
k → {k: v} → {k: v} → Boolean
```

- `prop`：要比较的属性名称。
- `obj1`。
- `obj2`。
- 返回`Boolean`。

### 例子

```js
const o1 = { a: 1, b: 2, c: 3, d: 4 };
const o2 = { a: 10, b: 20, c: 3, d: 40 };
R.eqProps('a', o1, o2); //=> false
R.eqProps('c', o1, o2); //=> true
```

### 参考
- [https://ramdajs.com/docs/#eqProps](https://ramdajs.com/docs/#eqProps)

## evolve
递归地对 `object` 的属性进行变换，变换方式由 `transformation` 函数定义。所有非原始类型属性都通过引用来复制。

如果某个 `transformation` 函数对应的键在被变换的 `object` 中不存在，那么该方法将不会执行。

### 参数

```
{k: (v → v)} → {k: v} → {k: v}
```

- `transformations`：该对象指定要应用于该对象的转换函数。
- `object`：要转换的对象。
- 返回`Object`：转换后的对象。

### 例子

```js
const tomato = { firstName: '  Tomato ', data: { elapsed: 100, remaining: 1400 }, id: 123 };
const transformations = {
    firstName: R.trim,
    lastName: R.trim, // Will not get invoked.
    data: { elapsed: R.add(1), remaining: R.add(-1) }
};
R.evolve(transformations, tomato); //=> {firstName: 'Tomato', data: {elapsed: 101, remaining: 1399}, id:123}
```

### 参考
- [https://ramdajs.com/docs/#evolve](https://ramdajs.com/docs/#evolve)

## forEachObjIndexed
遍历 `object`，对 `object` 中的每对 `key` 和 `value` 执行方法 `fn`。

`fn` 接收三个参数：`(value, key, obj)`。

### 参数

```
((a, String, StrMap a) → Any) → StrMap a → StrMap a
```

- `fn`：要调用的函数。接收三个参数 `(value, key, obj)`。
- `obj`：要遍历的对象。
- 返回`Object`：原始对象。

### 例子

```js
const printKeyConcatValue = (value, key) => console.log(key + ':' + value);
R.forEachObjIndexed(printKeyConcatValue, { x: 1, y: 2 }); //=> {x: 1, y: 2}
// logs x:1
// logs y:2
```

### 参考
- [https://ramdajs.com/docs/#forEachObjIndexed](https://ramdajs.com/docs/#forEachObjIndexed)

## has
如果对象自身含有指定的属性，则返回 `true`；否则返回 `false`。

### 参数

```
s → {s: x} → Boolean
```

- `prop`：要检查的属性的名称。
- `obj`：要查询的对象。
- 返回`Boolean`：该属性是否存在。

### 例子

```js
const hasName = R.has('name');
hasName({ name: 'alice' });   //=> true
hasName({ name: 'bob' });     //=> true
hasName({});                //=> false

const point = { x: 0, y: 0 };
const pointHas = R.has(R.__, point);
pointHas('x');  //=> true
pointHas('y');  //=> true
pointHas('z');  //=> false
```

### 参考
- [https://ramdajs.com/docs/#has](https://ramdajs.com/docs/#has)

## hasIn
如果对象自身或其原型链上含有指定的属性，则返回 `true`；否则返回 `false`。

### 参数

```
s → {s: x} → Boolean
```

- `prop`：要检查的属性的名称。
- `obj`：要查询的对象。
- `Boolean`：该属性是否存在。

### 例子

```js
function Rectangle(width, height) {
    this.width = width;
    this.height = height;
}
Rectangle.prototype.area = function () {
    return this.width * this.height;
};

const square = new Rectangle(2, 2);
R.hasIn('width', square);  //=> true
R.hasIn('area', square);  //=> true
```

### 参考
- [https://ramdajs.com/docs/#hasIn](https://ramdajs.com/docs/#hasIn)

## hasPath
检查对象中是否存在指定的路径。只检查对象自身的属性。

### 参数

```
[Idx] → {a} → Boolean
Idx = String | Int
```

- `path`：使用的路径。
- `obj`：要检查路径的对象。
- 返回`Boolean`：路径是否存在。

### 例子

```js
R.hasPath(['a', 'b'], { a: { b: 2 } });         // => true
R.hasPath(['a', 'b'], { a: { b: undefined } }); // => true
R.hasPath(['a', 'b'], { a: { c: 2 } });         // => false
R.hasPath(['a', 'b'], {});                  // => false
```

### 参考
- [https://ramdajs.com/docs/#hasPath](https://ramdajs.com/docs/#hasPath)

## invert
与 `R.invertObj` 类似，但会将值放入数组中，来处理一个键对应多个值的情况。

### 参数

```
{s: x} → {x: [ s, … ]}
```

- `obj`：要反转的对象或数组。
- 返回`Object`：带有键在数组中的新对象。

### 例子

```js
const raceResultsByFirstName = {
    first: 'alice',
    second: 'jake',
    third: 'alice',
};
R.invert(raceResultsByFirstName);
//=> { 'alice': ['first', 'third'], 'jake':['second'] }
```

### 参考
- [https://ramdajs.com/docs/#invert](https://ramdajs.com/docs/#invert)

## invertObj
将对象的键、值交换位置：值作为键，对应的键作为值。交换后的键会被强制转换为字符串。注意，如果原对象同一值对应多个键，采用最后遍历到的键。

### 参数

```
{s: x} → {x: s}
```

- `obj`：要反转的对象或数组。
- 返回`Object`：新对象。

### 例子

```js
const raceResults = {
    first: 'alice',
    second: 'jake'
};
R.invertObj(raceResults);
//=> { 'alice': 'first', 'jake':'second' }

// Alternatively:
const raceResults = ['alice', 'jake'];
R.invertObj(raceResults);
//=> { 'alice': '0', 'jake':'1' }
```

### 参考
- [https://ramdajs.com/docs/#invertObj](https://ramdajs.com/docs/#invertObj)

## keys
返回给定对象所有可枚举的、自身属性的属性名组成的列表。注意，不同 JS 运行环境输出数组的顺序可能不一致。

### 参数

```
{k: v} → [k]
```

- `obj`：从中提取属性的对象。
- 返回`Array`：对象自身属性的数组。

### 例子

```js
R.keys({ a: 1, b: 2, c: 3 }); //=> ['a', 'b', 'c']
```

### 参考
- [https://ramdajs.com/docs/#keys](https://ramdajs.com/docs/#keys)

## keysIn
返回给定对象所有属性（包括 `prototype` 属性）的属性名组成的列表。注意，不同 JS 运行环境输出数组的顺序可能不一致。

### 参数

```
{k: v} → [k]
```

- `obj`：从中提取属性的对象
- 返回`Array`：对象自身和原型属性的数组。

### 例子

```js
const F = function () { this.x = 'X'; };
F.prototype.y = 'Y';
const f = new F();
R.keysIn(f); //=> ['x', 'y']
```

### 参考
- [https://ramdajs.com/docs/#keysIn](https://ramdajs.com/docs/#keysIn)

## lens
返回封装了给定 `getter` 和 `setter` 方法的 `lens` 。`getter` 和 `setter` 分别用于 “获取” 和 “设置” 焦点（`lens` 聚焦的值）。`setter` 不会改变原数据。

### 参数

```
(s → a) → ((a, s) → s) → Lens s a
Lens s a = Functor f => (a → f a) → s → f s
```

- `getter`。
- `setter`。
- 返回`Lens`。

### 例子

```js
const xLens = R.lens(R.prop('x'), R.assoc('x'));

R.view(xLens, { x: 1, y: 2 });            //=> 1
R.set(xLens, 4, { x: 1, y: 2 });          //=> {x: 4, y: 2}
R.over(xLens, R.negate, { x: 1, y: 2 });  //=> {x: -1, y: 2}
```

### 参考
- [https://ramdajs.com/docs/#lens](https://ramdajs.com/docs/#lens)

## lensIndex
返回聚焦到指定索引的 `lens`。

### 参数

```
Number → Lens s a
Lens s a = Functor f => (a → f a) → s → f s
```

- `n`。
- 返回`Lens`。

### 例子

```js
const headLens = R.lensIndex(0);

R.view(headLens, ['a', 'b', 'c']);            //=> 'a'
R.set(headLens, 'x', ['a', 'b', 'c']);        //=> ['x', 'b', 'c']
R.over(headLens, R.toUpper, ['a', 'b', 'c']); //=> ['A', 'b', 'c']
```

### 参考
- [https://ramdajs.com/docs/#lensIndex](https://ramdajs.com/docs/#lensIndex)

## lensPath
返回聚焦到指定路径的 `lens`。

### 参数

```
[Idx] → Lens s a
Idx = String | Int
Lens s a = Functor f => (a → f a) → s → f s
```

- `path`：使用的路径。
- 返回`Lens`。

### 例子

```js
const xHeadYLens = R.lensPath(['x', 0, 'y']);

R.view(xHeadYLens, { x: [{ y: 2, z: 3 }, { y: 4, z: 5 }] });
//=> 2
R.set(xHeadYLens, 1, { x: [{ y: 2, z: 3 }, { y: 4, z: 5 }] });
//=> {x: [{y: 1, z: 3}, {y: 4, z: 5}]}
R.over(xHeadYLens, R.negate, { x: [{ y: 2, z: 3 }, { y: 4, z: 5 }] });
//=> {x: [{y: -2, z: 3}, {y: 4, z: 5}]}
```

### 参考
- [https://ramdajs.com/docs/#lensPath](https://ramdajs.com/docs/#lensPath)

## lensProp
返回聚焦到指定属性的 `lens`。

### 参数

```
String → Lens s a
Lens s a = Functor f => (a → f a) → s → f s
```

- `k`。
- `Lens`。

### 例子

```js
const xLens = R.lensProp('x');

R.view(xLens, { x: 1, y: 2 });            //=> 1
R.set(xLens, 4, { x: 1, y: 2 });          //=> {x: 4, y: 2}
R.over(xLens, R.negate, { x: 1, y: 2 });  //=> {x: -1, y: 2}
```

### 参考
- [https://ramdajs.com/docs/#lensProp](https://ramdajs.com/docs/#lensProp)

## mapObjIndexed
`Object` 版本的 `map`。mapping function 接受三个参数：`(value, key, obj)` 。如果仅用到参数 `value`，则用 `map` 即可。


### 参数

```
((*, String, Object) → *) → Object → Object
```

- `fn`。
- `obj`。
- 返回`Object`。

### 例子

```js
const xyz = { x: 1, y: 2, z: 3 };
const prependKeyAndDouble = (num, key, obj) => key + (num * 2);

R.mapObjIndexed(prependKeyAndDouble, xyz); //=> { x: 'x2', y: 'y4', z: 'z6' }
```

### 参考
- [https://ramdajs.com/docs/#mapObjIndexed](https://ramdajs.com/docs/#mapObjIndexed)

## merge
`Deprecated`

合并两个对象的自身属性（不包括 `prototype` 属性）。如果某个 `key` 在两个对象中都存在，使用后一个对象对应的属性值。

### 参数

```
{k: v} → {k: v} → {k: v}
```

- `l`。
- `r`。
- 返回`Object`。

### 例子

```js
R.merge({ 'name': 'fred', 'age': 10 }, { 'age': 40 });
//=> { 'name': 'fred', 'age': 40 }

const withDefaults = R.merge({ x: 0, y: 0 });
withDefaults({ y: 2 }); //=> {x: 0, y: 2}
```

### 参考
- [https://ramdajs.com/docs/#merge](https://ramdajs.com/docs/#merge)

## mergeDeepLeft
合并两个对象的自身属性（不包括 `prototype` 属性）。如果某个 `key` 在两个对象中都存在：
- 并且两个值都是对象，则继续递归合并这两个值。
- 否则，采用第一个对象的值。

### 参数

```
{a} → {a} → {a}
```

- `lObj`。
- `rObj`。
- 返回：`Object`。

### 例子

```js
R.mergeDeepLeft({ name: 'fred', age: 10, contact: { email: 'moo@example.com' } },
    { age: 40, contact: { email: 'baa@example.com' } });
//=> { name: 'fred', age: 10, contact: { email: 'moo@example.com' }}
```

### 参考
- [https://ramdajs.com/docs/#mergeDeepLeft](https://ramdajs.com/docs/#mergeDeepLeft)

## mergeDeepRight
合并两个对象的自身属性（不包括 `prototype` 属性）。如果某个 `key` 在两个对象中都存在：
- 并且两个值都是对象，则继续递归合并这两个值。
- 否则，采用第二个对象的值。

### 参数

```
{a} → {a} → {a}
```

- `lObj`。
- `rObj`。
- 返回：`Object`。

### 例子

```js
R.mergeDeepRight({ name: 'fred', age: 10, contact: { email: 'moo@example.com' } },
    { age: 40, contact: { email: 'baa@example.com' } });
//=> { name: 'fred', age: 40, contact: { email: 'baa@example.com' }}
```

### 参考
- [https://ramdajs.com/docs/#mergeDeepRight](https://ramdajs.com/docs/#mergeDeepRight)

## mergeDeepWith
合并两个对象的自身属性（不包括 `prototype` 属性）。如果某个 `key` 在两个对象中都存在：
- 并且两个关联的值都是对象，则继续递归合并这两个值。
- 否则，使用给定函数对两个值进行处理，并将返回值作为该 key 的新值。

如果某 `key` 只存在于一个对象中，该键值对将作为结果对象的键值对。

### 参数

```
((a, a) → a) → {a} → {a} → {a}
```

- `fn`。
- `lObj`。
- `rObj`。
- 返回`Object`。

### 例子

```js
R.mergeDeepWith(R.concat,
    { a: true, c: { values: [10, 20] } },
    { b: true, c: { values: [15, 35] } });
//=> { a: true, b: true, c: { values: [10, 20, 15, 35] }}
```

### 参考
- [https://ramdajs.com/docs/#mergeDeepWith](https://ramdajs.com/docs/#mergeDeepWith)

## mergeDeepWithKey
合并两个对象的自身属性（不包括 `prototype` 属性）。如果某个 `key` 在两个对象中都存在：
- 并且两个关联的值都是对象，则继续递归合并这两个值。
- 否则，使用给定函数对该 `key` 和对应的两个值进行处理，并将返回值作为该 `key` 的新值。

如果某 `key` 只存在于一个对象中，该键值对将作为结果对象的键值对。

### 参数

```
((String, a, a) → a) → {a} → {a} → {a}
```

- `fn`。
- `lObj`。
- `rObj`。
- 返回`Object`。

### 例子

```js
let concatValues = (k, l, r) => k == 'values' ? R.concat(l, r) : r
R.mergeDeepWithKey(concatValues,
    { a: true, c: { thing: 'foo', values: [10, 20] } },
    { b: true, c: { thing: 'bar', values: [15, 35] } });
//=> { a: true, b: true, c: { thing: 'bar', values: [10, 20, 15, 35] }}
```

### 参考
- [https://ramdajs.com/docs/#mergeDeepWithKey](https://ramdajs.com/docs/#mergeDeepWithKey)

## mergeLeft
合并两个对象的自身属性（不包括 `prototype` 属性）。如果某个 `key` 在两个对象中都存在，使用前一个对象对应的属性值。

### 参数

```
{k: v} → {k: v} → {k: v}
```

- `l`。
- `r`。
- 返回`Object`。

### 例子

```js
R.mergeLeft({ 'age': 40 }, { 'name': 'fred', 'age': 10 });
//=> { 'name': 'fred', 'age': 40 }

const resetToDefault = R.mergeLeft({ x: 0 });
resetToDefault({ x: 5, y: 2 }); //=> {x: 0, y: 2}
```

### 参考
- [https://ramdajs.com/docs/#mergeLeft](https://ramdajs.com/docs/#mergeLeft)

## mergeRight
合并两个对象的自身属性（不包括 `prototype` 属性）。如果某个 `key` 在两个对象中都存在，使用后一个对象对应的属性值。

### 参数

```
{k: v} → {k: v} → {k: v}
```

- `l`。
- `r`。
- 返回`Object`。

### 例子

```js
R.mergeRight({ 'name': 'fred', 'age': 10 }, { 'age': 40 });
//=> { 'name': 'fred', 'age': 40 }

const withDefaults = R.mergeRight({ x: 0, y: 0 });
withDefaults({ y: 2 }); //=> {x: 0, y: 2}
```

### 参考
- [https://ramdajs.com/docs/#mergeRight](https://ramdajs.com/docs/#mergeRight)

## mergeWith
使用给定的两个对象自身属性（不包括 `prototype` 属性）来创建一个新对象。

如果某个 `key` 在两个对象中都存在，则使用给定的函数对每个对象该 `key` 对应的 `value` 进行处理，处理结果作为新对象该 `key` 对应的值。

### 参数

```
((a, a) → a) → {a} → {a} → {a}
```

- `fn`。
- `l`。
- `r`。
- 返回`Object`。

### 例子

```js
R.mergeWith(R.concat,
    { a: true, values: [10, 20] },
    { b: true, values: [15, 35] });
//=> { a: true, b: true, values: [10, 20, 15, 35] }
```

### 参考
- [https://ramdajs.com/docs/#mergeWith](https://ramdajs.com/docs/#mergeWith)

## mergeWithKey
使用给定的两个对象自身属性（不包括 `prototype` 属性）来创建一个新对象。

如果某个 `key` 在两个对象中都存在，则使用给定的函数对该 `key` 和每个对象该 `key` 对应的 `value` 进行处理，处理结果作为新对象该 `key` 对应的值。

### 参数

```
((String, a, a) → a) → {a} → {a} → {a}
```

- `fn`。
- `l`。
- `r`。
- 返回`Object`。

### 例子

```js
let concatValues = (k, l, r) => k == 'values' ? R.concat(l, r) : r
R.mergeWithKey(concatValues,
    { a: true, thing: 'foo', values: [10, 20] },
    { b: true, thing: 'bar', values: [15, 35] });
//=> { a: true, b: true, thing: 'bar', values: [10, 20, 15, 35] }
```

### 参考
- [https://ramdajs.com/docs/#mergeWithKey](https://ramdajs.com/docs/#mergeWithKey)

## objOf
创建一个包含单个键值对的对象。

### 参数

```
String → a → {String:a}
```

- `key`。
- `val`。
- 返回`Object`。

### 例子

```js
const matchPhrases = R.compose(
    R.objOf('must'),
    R.map(R.objOf('match_phrase'))
);
matchPhrases(['foo', 'bar', 'baz']); //=> {must: [{match_phrase: 'foo'}, {match_phrase: 'bar'}, {match_phrase: 'baz'}]}
```

### 参考
- [https://ramdajs.com/docs/#objOf](https://ramdajs.com/docs/#objOf)

## omit
删除对象中给定的 `keys` 对应的属性。

### 参数

```
[String] → {String: *} → {String: *}
```

- `names`：要从新对象中省略的 String 属性名称数组。
- `obj`：要复制的对象。
- 返回`Object`：一个具有来自 `names` 属性的新对象。

### 例子

```js
R.omit(['a', 'd'], {a: 1, b: 2, c: 3, d: 4}); //=> {b: 2, c: 3}
```

### 参考
- [https://ramdajs.com/docs/#omit](https://ramdajs.com/docs/#omit)

## over
对数据结构中被 `lens` 聚焦的部分进行函数变换。

### 参数

```
Lens s a → (a → a) → s → s
Lens s a = Functor f => (a → f a) → s → f s
```

- `lens`
- `v`
- `x`
- 返回`*`。

### 例子

```js
const headLens = R.lensIndex(0);

R.over(headLens, R.toUpper, ['foo', 'bar', 'baz']); //=> ['FOO', 'bar', 'baz']
```

### 参考
- [https://ramdajs.com/docs/#over](https://ramdajs.com/docs/#over)

## path
取出给定路径上的值。

### 参数

```
[Idx] → {a} → a | Undefined
Idx = String | Int
```

- `path`：使用的路径。
- `obj`：从中检索嵌套属性的对象。
- 返回`*`：路径中的数据。

### 例子

```js
R.path(['a', 'b'], {a: {b: 2}}); //=> 2
R.path(['a', 'b'], {c: {b: 2}}); //=> undefined
R.path(['a', 'b', 0], {a: {b: [1, 2, 3]}}); //=> 1
R.path(['a', 'b', -2], {a: {b: [1, 2, 3]}}); //=> 2
```

### 参考
- [https://ramdajs.com/docs/#path](https://ramdajs.com/docs/#path)

## pathOr
对于给定的非空对象，如果指定属性存在，则返回该属性值；否则返回给定的默认值。

### 参数

```
a → String → Object → a
```

- `val`：默认值。
- `p`：要返回的属性的名称。
- `obj`：要查询的对象。
- 返回`*`：提供的对象的给定属性的值或默认值。

### 例子

```js
const alice = {
    name: 'ALICE',
    age: 101
};
const favorite = R.prop('favoriteLibrary');
const favoriteWithDefault = R.propOr('Ramda', 'favoriteLibrary');

favorite(alice);  //=> undefined
favoriteWithDefault(alice);  //=> 'Ramda'
```

### 参考
- [https://ramdajs.com/docs/#pathOr](https://ramdajs.com/docs/#pathOr)

## paths
提取对象中指定路径数组（`paths`）上的对应的值（`values`）。

### 参数

```
[Idx] → {a} → [a | Undefined]
Idx = [String | Int]
```

- `pathsArray`：要获取的路径数组。
- `obj`：从中检索嵌套属性的对象。
- 返回`Array`：由 `pathsArray` 指定的路径上的值组成的列表。

### 例子

```js
R.paths([['a', 'b'], ['p', 0, 'q']], { a: { b: 2 }, p: [{ q: 3 }] }); //=> [2, 3]
R.paths([['a', 'b'], ['p', 'r']], { a: { b: 2 }, p: [{ q: 3 }] }); //=> [2, undefined]
```

### 参考
- [https://ramdajs.com/docs/#paths](https://ramdajs.com/docs/#paths)

## pick
返回对象的部分拷贝，其中仅包含指定键对应的属性。如果某个键不存在，则忽略该属性。

### 参数

```
[k] → {k: v} → {k: v}
```

- `names`：字符串属性名称数组，可复制到新对象上。
- `obj`：要复制的对象。
- 返回`Object`：一个仅具有 `names` 属性的新对象。

### 例子

```js
R.pick(['a', 'd'], { a: 1, b: 2, c: 3, d: 4 }); //=> {a: 1, d: 4}
R.pick(['a', 'e', 'f'], { a: 1, b: 2, c: 3, d: 4 }); //=> {a: 1}
```

### 参考
- [https://ramdajs.com/docs/#pick](https://ramdajs.com/docs/#pick)

## pickAll
与 `pick` 类似，但 `pickAll` 会将不存在的属性以 `key: undefined` 键值对的形式返回。

### 参数
```
[k] → {k: v} → {k: v}
```

- `names`：字符串属性名称数组，可复制到新对象上。
- `obj`：要复制的对象。
- 返回`Object`：一个仅具有 `names` 属性的新对象。

### 例子

```js
R.pickAll(['a', 'd'], { a: 1, b: 2, c: 3, d: 4 }); //=> {a: 1, d: 4}
R.pickAll(['a', 'e', 'f'], { a: 1, b: 2, c: 3, d: 4 }); //=> {a: 1, e: undefined, f: undefined}
```

### 参考
- [https://ramdajs.com/docs/#pickAll](https://ramdajs.com/docs/#pickAll)

## pickBy
返回对象的部分拷贝，其中仅包含 `key` 满足 `predicate` 的属性。

### 参数

```
((v, k) → Boolean) → {k: v} → {k: v}
```

- `pred`：确定是否应在输出对象上包含键的谓词函数。
- `obj`：要复制的对象。
- `Object`：一个仅具有满足 `pred` 属性的新对象。

### 例子

```js
const isUpperCase = (val, key) => key.toUpperCase() === key;
R.pickBy(isUpperCase, { a: 1, b: 2, A: 3, B: 4 }); //=> {A: 3, B: 4}
```

### 参考
- [https://ramdajs.com/docs/#pickBy](https://ramdajs.com/docs/#pickBy)

## project
模拟 SQL 中的 `select` 语句。

### 参数

```
[k] → [{k: v}] → [{k: v}]
```

- `props`：要投影的属性名称。
- `objs`：要查询的对象。
- 返回`Array`：仅具有`props`属性的对象数组。

### 例子

```js
const abby = { name: 'Abby', age: 7, hair: 'blond', grade: 2 };
const fred = { name: 'Fred', age: 12, hair: 'brown', grade: 7 };
const kids = [abby, fred];
R.project(['name', 'grade'], kids); //=> [{name: 'Abby', grade: 2}, {name: 'Fred', grade: 7}]
```

### 参考
- [https://ramdajs.com/docs/#project](https://ramdajs.com/docs/#project)

## prop
取出对象中指定属性的值。如果不存在，则返回 `undefined`。

### 参数

```
Idx → {s: a} → a | Undefined
Idx = String | Int
```

- `p`：属性名称或数组索引。
- `obj`：要查询的对象。
- `*`：`obj.p`中的值。

### 例子

```js
R.prop('x', { x: 100 }); //=> 100
R.prop('x', {}); //=> undefined
R.prop(0, [100]); //=> 100
R.compose(R.inc, R.prop('x'))({ x: 3 }) //=> 4
```

### 参考
- [https://ramdajs.com/docs/#prop](https://ramdajs.com/docs/#prop)

## propOr
对于给定的非空对象，如果指定属性存在，则返回该属性值；否则返回给定的默认值。

### 参数

```
a → String → Object → a
```

- `val`：默认值。
- `p`：要返回的属性的名称。
- `obj`：要查询的对象。
- `*`：提供的对象的给定属性的值或默认值。

### 例子

```js
const alice = {
    name: 'ALICE',
    age: 101
};
const favorite = R.prop('favoriteLibrary');
const favoriteWithDefault = R.propOr('Ramda', 'favoriteLibrary');

favorite(alice);  //=> undefined
favoriteWithDefault(alice);  //=> 'Ramda'
```

### 参考
- [https://ramdajs.com/docs/#propOr](https://ramdajs.com/docs/#propOr)

## props
返回 `prop` 的数组：输入为 `keys` 数组，输出为对应的 `values` 数组。`values` 数组的顺序与 `keys` 的相同。

### 参数

```
[k] → {k: v} → [v]
```

- `ps`：要获取的属性名称。
- `obj`：要查询的对象。
- 返回`Array`：相应的值或部分应用的函数。

### 例子

```js
R.props(['x', 'y'], { x: 1, y: 2 }); //=> [1, 2]
R.props(['c', 'a', 'b'], { b: 2, a: 1 }); //=> [undefined, 1, 2]

const fullName = R.compose(R.join(' '), R.props(['first', 'last']));
fullName({ last: 'Bullet-Tooth', age: 33, first: 'Tony' }); //=> 'Tony Bullet-Tooth'
```

### 参考
- [https://ramdajs.com/docs/#props](https://ramdajs.com/docs/#props)

## set
通过 `lens` 对数据结构聚焦的部分进行设置。

### 参数

```
Lens s a → a → s → s
Lens s a = Functor f => (a → f a) → s → f s
```

- `lens`。
- `v`。
- `x`。
- 返回 `*`。

### 例子

```js
const xLens = R.lensProp('x');

R.set(xLens, 4, { x: 1, y: 2 });  //=> {x: 4, y: 2}
R.set(xLens, 8, { x: 1, y: 2 });  //=> {x: 8, y: 2}
```

### 参考
- [https://ramdajs.com/docs/#set](https://ramdajs.com/docs/#set)

## toPairs
将一个对象的属性转换成键、值二元组类型的数组，只处理对象自身的属性。注意：不同 JS 运行环境输出数组的顺序可能不一致。

### 参数

```
{String: *} → [[String,*]]
```

- `obj`：要提取的对象。
- 返回`Array`：来自对象自身属性的键，值数组。

### 例子

```js
R.toPairs({ a: 1, b: 2, c: 3 }); //=> [['a', 1], ['b', 2], ['c', 3]]
```

### 参考
- [https://ramdajs.com/docs/#toPairs](https://ramdajs.com/docs/#toPairs)

## toPairsIn
将一个对象的属性转换成键、值二元组类型的数组，包括原型链上的属性。注意，不同 JS 运行环境输出数组的顺序可能不一致。

### 参数

```
{String: *} → [[String,*]]
```

- `obj`：要提取的对象。
- `Array`：来自对象自身和原型属性的键，值数组的数组。

### 例子

```js
const F = function () { this.x = 'X'; };
F.prototype.y = 'Y';
const f = new F();
R.toPairsIn(f); //=> [['x','X'], ['y','Y']]
```

### 参考
- [https://ramdajs.com/docs/#toPairsIn](https://ramdajs.com/docs/#toPairsIn)

## values
返回对象所有自身可枚举的属性的值。注意：不同 JS 运行环境输出数组的顺序可能不一致。

### 参数

```
{k: v} → [v]
```

- `obj`：从中提取值的对象。
- `Array`：对象自身属性的值的数组。

### 例子

```js
R.values({a: 1, b: 2, c: 3}); //=> [1, 2, 3]
```

### 参考
- [https://ramdajs.com/docs/#values](https://ramdajs.com/docs/#values)

## valuesIn
返回对象所有属性的值，包括原型链上的属性。注意：不同 JS 运行环境输出数组的顺序可能不一致。

### 参数

```
{k: v} → [v]
```

- `obj`：从中提取值的对象。
- `Array`：对象自身和原型属性的值的数组。

### 例子

```js
const F = function () { this.x = 'X'; };
F.prototype.y = 'Y';
const f = new F();
R.valuesIn(f); //=> ['X', 'Y']
```

### 参考
- [https://ramdajs.com/docs/#valuesIn](https://ramdajs.com/docs/#valuesIn)

## view
返回数据结构中，`lens` 聚焦的部分。`lens` 的焦点决定了数据结构中的哪部分是可见的。

### 参数

```
Lens s a → s → a
Lens s a = Functor f => (a → f a) → s → f s
```

- `lens`。
- `x`。
- 返回 `*`。

### 例子

```js
const xLens = R.lensProp('x');

R.view(xLens, { x: 1, y: 2 });  //=> 1
R.view(xLens, { x: 4, y: 2 });  //=> 4
```

### 参考
- [https://ramdajs.com/docs/#view](https://ramdajs.com/docs/#view)

## where
接受一个测试规范对象和一个待检测对象，如果测试满足规范，则返回 `true`，否则返回 `false`。测试规范对象的每个属性值都必须是 `predicate` 。每个 `predicate` 作用于待检测对象对应的属性值，如果所有 `predicate` 都返回 `true`，则 `where` 返回 `true`，否则返回 `false` 。

`where` 非常适合于需要声明式表示约束的函数，比如 `filter` 和 `find` 。

### 参数

```
{String: (* → Boolean)} → {String: *} → Boolean
```

- `spec`。
- `testObj`。
- 返回 `Boolean`。

### 例子

```js
// pred :: Object -> Boolean
const pred = R.where({
    a: R.equals('foo'),
    b: R.complement(R.equals('bar')),
    x: R.gt(R.__, 10),
    y: R.lt(R.__, 20)
});

pred({ a: 'foo', b: 'xxx', x: 11, y: 19 }); //=> true
pred({ a: 'xxx', b: 'xxx', x: 11, y: 19 }); //=> false
pred({ a: 'foo', b: 'bar', x: 11, y: 19 }); //=> false
pred({ a: 'foo', b: 'xxx', x: 10, y: 19 }); //=> false
pred({ a: 'foo', b: 'xxx', x: 11, y: 20 }); //=> false
```

### 参考
- [https://ramdajs.com/docs/#where](https://ramdajs.com/docs/#where)

## whereEq
接受一个测试规范对象和一个待检测对象，如果测试满足规范，则返回 `true`，否则返回 `false`。如果对于每一个测试规范对象的属性值，待检测对象中都有一个对应的相同属性值，则 `where` 返回 `true`，否则返回 `false` 。

`whereEq` 是 `where` 的一种特殊形式。

### 参数

```
{String: *} → {String: *} → Boolean
```

- `spec`。
- `testObj`。
- 返回 `Boolean`。

### 例子

```js
// pred :: Object -> Boolean
const pred = R.whereEq({ a: 1, b: 2 });

pred({ a: 1 });              //=> false
pred({ a: 1, b: 2 });        //=> true
pred({ a: 1, b: 2, c: 3 });  //=> true
pred({ a: 1, b: 1 });        //=> false
```

### 参考
- [https://ramdajs.com/docs/#whereEq](https://ramdajs.com/docs/#whereEq)

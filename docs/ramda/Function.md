## __

柯里化函数的参数占位符。允许部分应用于任何位置的参数。

假设 `g` 代表柯里化的三元函数，`_` 代表 `R.__`，则下面几种写法是等价的：

- `g(1, 2, 3)`
- `g(_, 2, 3)(1)`
- `g(_, _, 3)(1)(2)`
- `g(_, _, 3)(1, 2)`
- `g(_, 2, _)(1, 3)`
- `g(_, 2)(1)(3)`
- `g(_, 2)(1, 3)`
- `g(_, 2)(_, 3)(1)`

### 例子

```js
const greet = R.replace('{name}', R.__, 'Hello, {name}!');
greet('Alice'); //=> 'Hello, Alice!'
```

### 参考
- [https://ramdajs.com/docs/#__](https://ramdajs.com/docs/#__)

## addIndex
通过向列表迭代函数的回调函数添加两个新的参数：当前索引、整个列表，创建新的列表迭代函数。

例如，`addIndex` 可以将 `R.map` 转换为类似于 `Array.prototype.map` 的函数。注意，`addIndex` 只适用于迭代回调函数是首个参数、列表是最后一个参数的函数。（如果列表参数没有用到，后一个条件可以忽略）。

### 参数

```
((a … → b) … → [a] → *) → ((a …, Int, [a] → b) … → [a] → *)
```

- `fn`: 列表迭代函数，不将索引或列表传递给其回调。
- 返回函数更改后的列表迭代函数，将其 `(item, index, list)` 传递给其回调。

### 例子

```js
const mapIndexed = R.addIndex(R.map);
mapIndexed((val, idx) => idx + '-' + val, ['f', 'o', 'o', 'b', 'a', 'r']);
//=> ['0-f', '1-o', '2-o', '3-b', '4-a', '5-r']
```

### 参考
- [https://ramdajs.com/docs/#addIndex](https://ramdajs.com/docs/#addIndex)

## always
返回一个返回恒定值的函数。注意，对于非原始值，返回的值是对原始值的引用。

此函数在其他语言或库中也被称作：`const`、`constant`、或 `K` (K combinator 中)。

### 参数

```js
a → (* → a)
```

- `val`：包装在函数中的值。
- 返回一个返回恒定值的函数。

### 例子

```js
const t = R.always('Tee');
t(); //=> 'Tee'
```

### 参考
- [https://ramdajs.com/docs/#always](https://ramdajs.com/docs/#always)

## andThen
将 `onSuccess` 函数应用于一个 `fulfilled Promise` 的内部值，并将计算结果放入新的 `Promise` 中返回。这对于处理函数组合内的  `promises` 很有用。

### 参数

```
(a → b) → (Promise e a) → (Promise e b)
(a → (Promise e b)) → (Promise e a) → (Promise e b)
```

- `onSuccess`：要应用的函数。可以返回值或值的 `Promise`。
- `p`。
- 返回 Promise 调用 `p.then（onSuccess）`的结果。

### 例子

```js
var makeQuery = (email) => ({ query: { email } });

//getMemberName :: String -> Promise ({firstName, lastName})
var getMemberName = R.pipe(
    makeQuery,
    fetchMember,
    R.andThen(R.pick(['firstName', 'lastName']))
);
```

### 参考
- [https://ramdajs.com/docs/#andThen](https://ramdajs.com/docs/#andThen)

## ap

`ap` 将函数列表作用于值列表上。

若第二个参数自身存在 `ap` 方法，则调用自身的 `ap` 方法。柯里化函数也可以作为 applicative。

### 参数

```js
[a → b] → [a] → [b]
Apply f => f (a → b) → f a → f b
(r → a → b) → (r → a) → (r → b)
```

- `applyF`。
- `applyX`。
- 返回 `*`。

### 例子

```js
R.ap([R.multiply(2), R.add(3)], [1, 2, 3]); //=> [2, 4, 6, 4, 5, 6]
R.ap([R.concat('tasty '), R.toUpper], ['pizza', 'salad']); //=> ["tasty pizza", "tasty salad", "PIZZA", "SALAD"]

// R.ap can also be used as S combinator
// when only two functions are passed
R.ap(R.concat, R.toUpper)('Ramda') //=> 'RamdaRAMDA'
```

### 参考
- [https://ramdajs.com/docs/#ap](https://ramdajs.com/docs/#ap)

## apply
将函数 `fn` 作用于参数列表 `args`。`apply` 可以将变参函数转换为为定参函数。如果上下文很重要，则 `fn` 应该绑定其上下文。

### 参数

```
(*… → a) → [*] → a
```

- `fn`: 将用 `args` 调用的函数。
- `args`：用 `fn` 调用的参数。
- 返回 `*`，结果相当于 `fn(...args)`。

### 例子

```js
const nums = [1, 2, 3, -99, 42, 6, 7];
R.apply(Math.max, nums); //=> 42
```

### 参考
- [https://ramdajs.com/docs/#apply](https://ramdajs.com/docs/#apply)

## applySpec
接受一个属性值为函数的对象，返回一个能生成相同结构对象的函数。返回的函数使用传入的参数调用对象的每个属性位对应的函数，来生成相应属性的值。

### 参数

```
{k: ((a, b, …, m) → v)} → ((a, b, …, m) → {k: v})
```

- `spec`：对象将属性递归地映射到用于为这些属性生成值的函数。
- 返回 `function`：返回一个与 `spec` 具有相同结构的对象的函数，每个属性都设置为通过使用提供的参数调用其关联函数而返回的值。

### 例子

```js
const getMetrics = R.applySpec({
    sum: R.add,
    nested: { mul: R.multiply }
});
getMetrics(2, 4); // => { sum: 6, nested: { mul: 8 } }
```

### 参考
- [https://ramdajs.com/docs/#applySpec](https://ramdajs.com/docs/#applySpec)

## applyTo
接受一个值，并将一个函数作用于其上。

该函数又被称为 thrush combinator。

### 参数

```js
a → (a → b) → b
```

- `x`：值。
- `f`：要应用的函数。
- 返回 `*`：将 `f` 应用于 `x` 的结果。

### 例子

```js
const t42 = R.applyTo(42);
t42(R.identity); //=> 42
t42(R.add(1)); //=> 43
```

### 参考
- [https://ramdajs.com/docs/#applyTo](https://ramdajs.com/docs/#applyTo)

## ascend
由返回值可与 `<` 和 `>` 比较的函数，创建一个升序比较函数。

### 参数

```
Ord b => (a → b) → a → a → Number
```

- `fn`：一个返回值是可以比较的值的函数。
- `a`：要比较的第一项。
- `b`：要比较的第二项。
- 返回 `Number`：如果 `fn(a) < fn(b)` 返回 `-1`，`fn(b) < fn(a)` 返回 `1`，否则返回 `0`。

### 例子

```js
const byAge = R.ascend(R.prop('age'));
const people = [
    { name: 'Emma', age: 70 },
    { name: 'Peter', age: 78 },
    { name: 'Mikhail', age: 62 },
];
const peopleByYoungestFirst = R.sort(byAge, people);
//=> [{ name: 'Mikhail', age: 62 },{ name: 'Emma', age: 70 }, { name: 'Peter', age: 78 }]
```

### 参考
- [https://ramdajs.com/docs/#ascend](https://ramdajs.com/docs/#ascend)

## binary
将任意元函数封装为二元函数（只接受 2 个参数）中。任何额外的参数都不会传递给被封装的函数。

### 参数

```
(* → c) → (a, b → c)
```

- `fn`: 要包装的函数。
- 返回 `function`：一个包装 `fn` 的新函数。保证新函数具有 2 个参数。

### 例子

```js
const takesThreeArgs = function (a, b, c) {
    return [a, b, c];
};
takesThreeArgs.length; //=> 3
takesThreeArgs(1, 2, 3); //=> [1, 2, 3]

const takesTwoArgs = R.binary(takesThreeArgs);
takesTwoArgs.length; //=> 2
// Only 2 arguments are passed to the wrapped function
takesTwoArgs(1, 2, 3); //=> [1, 2, undefined]
```

### 参考
- [https://ramdajs.com/docs/#binary](https://ramdajs.com/docs/#binary)

## bind
创建一个绑定了上下文的函数。

注意：与 `Function.prototype.bind` 不同，`R.bind` 不会绑定额外参数。

### 参数

```
(* → *) → {*} → (* → *)
```

- `fn`：绑定到上下文的函数。
- `thisObj`：将 `fn` 绑定到的上下文。
- 返回 `function`：将在 `thisObj` 上下文中执行的函数。

### 例子

```js
const log = R.bind(console.log, console);
R.pipe(R.assoc('a', 2), R.tap(log), R.assoc('a', 3))({ a: 1 }); //=> {a: 3}
// logs {a: 2}
```

### 参考
- [https://ramdajs.com/docs/#bind](https://ramdajs.com/docs/#bind)

## call

提取第一个参数作为函数，其余参数作为刚提取的函数的参数，调用该函数并将结果返回。

`R.call` 可以用作 `R.converge` 的 `convergeing` 函数：第一个分支函数生成函数，其余分支函数生成一系列值作为该函数的参数。（`R.converge` 第二个参数为一个分支函数列表）。

### 参数

```
(*… → a),*… → a
```

- `fn`：应用于其余参数的函数。
- `args`：任意数量的位置参数。
- 返回 `*`。

### 例子

```js
R.call(R.add, 1, 2); //=> 3

const indentN = R.pipe(R.repeat(' '),
    R.join(''),
    R.replace(/^(?!$)/gm));

const format = R.converge(R.call, [
    R.pipe(R.prop('indent'), indentN),
    R.prop('value')
]);

format({ indent: 2, value: 'foo\nbar\nbaz\n' }); //=> '  foo\n  bar\n  baz\n'
```

### 参考
- [https://ramdajs.com/docs/#call](https://ramdajs.com/docs/#call)

## comparator
由首个参数是否小于第二个参数的判断函数，生成一个比较函数。

### 参数

```
((a, b) → Boolean) → ((a, b) → Number)
```

- `pred`：二元的谓词函数，如果第一个参数小于第二个参数，则返回 `true`，否则返回 `false`。
- 返回 `function`：如果 `a < b` 则返回 `-1`，如果 `b < a` 则返回 `1`，否则返回 `0`。

### 例子

```js
const byAge = R.comparator((a, b) => a.age < b.age);
const people = [
    { name: 'Emma', age: 70 },
    { name: 'Peter', age: 78 },
    { name: 'Mikhail', age: 62 },
];
const peopleByIncreasingAge = R.sort(byAge, people);
//=> [{ name: 'Mikhail', age: 62 },{ name: 'Emma', age: 70 }, { name: 'Peter', age: 78 }]
```

### 参考
- [https://ramdajs.com/docs/#comparator](https://ramdajs.com/docs/#comparator)

## compose
从右往左执行函数组合（右侧函数的输出作为左侧函数的输入）。最后一个函数可以是任意元函数（参数个数不限），其余函数必须是一元函数。

注意：`compose` 输出的函数不会自动进行柯里化。

### 参数

```
((y → z), (x → y), …, (o → p), ((a, b, …, n) → o)) → ((a, b, …, n) → z)
```

- `...functions`：要进行组合的函数。
- 返回 `function`。

### 例子

```js
const classyGreeting = (firstName, lastName) => "The name's " + lastName + ", " + firstName + " " + lastName
const yellGreeting = R.compose(R.toUpper, classyGreeting);
yellGreeting('James', 'Bond'); //=> "THE NAME'S BOND, JAMES BOND"

R.compose(Math.abs, R.add(1), R.multiply(2))(-4) //=> 7
```

### 参考
- [https://ramdajs.com/docs/#compose](https://ramdajs.com/docs/#compose)

## composeK
`Deprecated`

接受一系列函数，返回从右向左的 Kleisli 组合，每个函数必须返回支持 `chain` 操作的值。

`R.composeK(h, g, f)` 等同于 `R.compose(R.chain(h)，R.chain(g)，f)`。

### 参数

```
Chain m => ((y → m z), (x → m y), …, (a → m b)) → (a → m z)
```

- `...functions`：要进行组合的函数。
- 返回 `function`。

### 例子

```js
//  get :: String -> Object -> Maybe *
const get = R.curry((propName, obj) => Maybe(obj[propName]))

//  getStateCode :: Maybe String -> Maybe String
const getStateCode = R.composeK(
    R.compose(Maybe.of, R.toUpper),
    get('state'),
    get('address'),
    get('user'),
);
getStateCode({ "user": { "address": { "state": "ny" } } }); //=> Maybe.Just("NY")
getStateCode({}); //=> Maybe.Nothing()
```

### 参考
- [https://ramdajs.com/docs/#composeK](https://ramdajs.com/docs/#composeK)

## composeP
`Deprecated`

从右向左执行返回 Promise 的函数的组合。最后一个函数可以是任意元函数（参数个数不限）; 其余函数必须是一元函数。

### 参数

```
((y → Promise z), (x → Promise y), …, (a → Promise b)) → (a → Promise z)
```

- `...functions`：要进行组合的函数。
- 返回 `function`。

### 例子

```js
const db = {
    users: {
        JOE: {
            name: 'Joe',
            followers: ['STEVE', 'SUZY']
        }
    }
}

// We'll pretend to do a db lookup which returns a promise
const lookupUser = (userId) => Promise.resolve(db.users[userId])
const lookupFollowers = (user) => Promise.resolve(user.followers)
lookupUser('JOE').then(lookupFollowers)

//  followersForUser :: String -> Promise [UserId]
const followersForUser = R.composeP(lookupFollowers, lookupUser);
followersForUser('JOE').then(followers => console.log('Followers:', followers))
// Followers: ["STEVE","SUZY"]
```

### 参考
- [https://ramdajs.com/docs/#composeP](https://ramdajs.com/docs/#composeP)

## composeWith
利用转换函数从右往左执行函数组合。最后一个函数可以是任意元函数（参数个数不限），其余函数必须是一元函数。

注意：`composeWith` 输出的函数不会自动进行柯里化。
### 参数

```js
((* → *), [(y → z), (x → y), …, (o → p), ((a, b, …, n) → o)]) → ((a, b, …, n) → z)
```

- `...functions`：要进行组合的函数。
- 返回 `function`。

### 例子

```js
const composeWhileNotNil = R.composeWith((f, res) => R.isNil(res) ? res : f(res));

composeWhileNotNil([R.inc, R.prop('age')])({ age: 1 }) //=> 2
composeWhileNotNil([R.inc, R.prop('age')])({}) //=> undefined
```

### 参考
- [https://ramdajs.com/docs/#composeWith](https://ramdajs.com/docs/#composeWith)

## construct
将构造函数封装进柯里化函数，新函数与原构造函数的传入参数类型及返回值类型相同。

### 参数

```
(* → {*}) → (* → {*})
```

- `fn`：要包装的构造函数。
- 返回 `function`：一个包装的，经过柯里化的构造函数。

### 例子

```js
// Constructor function
function Animal(kind) {
    this.kind = kind;
};
Animal.prototype.sighting = function () {
    return "It's a " + this.kind + "!";
}

const AnimalConstructor = R.construct(Animal)

// Notice we no longer need the 'new' keyword:
AnimalConstructor('Pig'); //=> {"kind": "Pig", "sighting": function (){...}};

const animalTypes = ["Lion", "Tiger", "Bear"];
const animalSighting = R.invoker(0, 'sighting');
const sightNewAnimal = R.compose(animalSighting, AnimalConstructor);
R.map(sightNewAnimal, animalTypes); //=> ["It's a Lion!", "It's a Tiger!", "It's a Bear!"]
```

### 参考
- [https://ramdajs.com/docs/#construct](https://ramdajs.com/docs/#construct)

## constructN

将构造函数封装进柯里化函数，新函数与原构造函数的传入参数类型及返回值类型相同。为了能够使用变参的构造函数，返回函数的元数需要明确指定。

### 参数

```
Number → (* → {*}) → (* → {*})
```

- `n`： 构造函数的参数。
- `fn`：要包装的构造函数。
- 返回 `function`：一个包装的，经过柯里化的构造函数。

### 例子

```js
// Variadic Constructor function
function Salad() {
    this.ingredients = arguments;
}

Salad.prototype.recipe = function () {
    const instructions = R.map(ingredient => 'Add a dollop of ' + ingredient, this.ingredients);
    return R.join('\n', instructions);
};

const ThreeLayerSalad = R.constructN(3, Salad);

// Notice we no longer need the 'new' keyword, and the constructor is curried for 3 arguments.
const salad = ThreeLayerSalad('Mayonnaise')('Potato Chips')('Ketchup');

console.log(salad.recipe());
// Add a dollop of Mayonnaise
// Add a dollop of Potato Chips
// Add a dollop of Ketchup
```

### 参考
- [https://ramdajs.com/docs/#constructN](https://ramdajs.com/docs/#constructN)

## converge
接受一个 `converging` 函数和一个分支函数列表，返回一个新函数。新函数的元数（参数个数）等于最长分支函数的元数。当被调用时，新函数接受参数，并将这些参数转发给每个分支函数；然后将每个分支函数的计算结果作为参数传递给 `converging` 函数，`converging` 函数的计算结果即新函数的返回值。

### 参数

```
((x1, x2, …) → z) → [((a, b, …) → x1), ((a, b, …) → x2), …] → (a → b → … → z)
```

- `after`：一个函数，`after` 将使用 `fn1` 和 `fn2` 的返回值作为参数来调用。
- `functions`：功能列表。
- 返回 `function`：一个新函数。

### 例子

```js
const average = R.converge(R.divide, [R.sum, R.length])
average([1, 2, 3, 4, 5, 6, 7]) //=> 4

const strangeConcat = R.converge(R.concat, [R.toUpper, R.toLower])
strangeConcat("Yodel") //=> "YODELyodel"
```

### 参考
- [https://ramdajs.com/docs/#converge](https://ramdajs.com/docs/#converge)

## curry
对函数进行柯里化。柯里化函数与其他语言中的柯里化函数相比，有两个非常好的特性：

1. 参数不需要一次只传入一个。如果 `f` 是三元函数，`g` 是 `R.curry(f)` ，则下列写法是等价的：
   - `g(1)(2)(3)`
   - `g(1)(2, 3)`
   - `g(1, 2)(3)`
   - `g(1, 2, 3)`

2. 占位符值 `R.__` 可用于标记暂未传入参数的位置。允许部分应用于任何参数组合，而无需关心它们的位置和顺序。假设 `g` 定义如前所示，`_` 代表 `R.__` ，则下列写法是等价的：
   - `g(1, 2, 3)`
   - `g(_, 2, 3)(1)`
   - `g(_, _, 3)(1)(2)`
   - `g(_, _, 3)(1, 2)`
   - `g(_, 2)(1)(3)`
   - `g(_, 2)(1, 3)`
   - `g(_, 2)(_, 3)(1)`

### 参数

```
(* → a) → (* → a)
```

- `fn`：要柯里化的函数。
- 返回 `function`：一个新的柯里化的函数。

### 例子

```js
const addFourNumbers = (a, b, c, d) => a + b + c + d;

const curriedAddFourNumbers = R.curry(addFourNumbers);
const f = curriedAddFourNumbers(1, 2);
const g = f(3);
g(4); //=> 10
```

### 参考
- [https://ramdajs.com/docs/#curry](https://ramdajs.com/docs/#curry)

## curryN

对函数进行柯里化，并限制柯里化函数的元数。柯里化函数有两个很好的特性：

1. 参数不需要一次只传入一个。假设 `g` 由 `R.curryN(3, f)` 生成，则下列写法是等价的：
   - `g(1)(2)(3)`
   - `g(1)(2, 3)`
   - `g(1, 2)(3)`
   - `g(1, 2, 3)`

2. 占位符值 `R.__` 可用于标记暂未传入参数的位置，允许部分应用于任何参数组合，而无需关心它们的位置和顺序。假设 `g` 定义如前所示，`_` 代表 `R.__` ，则下列写法是等价的：
   - `g(1, 2, 3)`
   - `g(_, 2, 3)(1)`
   - `g(_, _, 3)(1)(2)`
   - `g(_, _, 3)(1, 2)`
   - `g(_, 2)(1)(3)`
   - `g(_, 2)(1, 3)`
   - `g(_, 2)(_, 3)(1)`

### 参数

```
Number → (* → a) → (* → a)
```

- `length`：返回函数的元树。
- `fn`：要柯里化的函数。
- 返回 `function`：一个新的柯里化的函数。

### 例子

```js
const sumArgs = (...args) => R.sum(args);

const curriedAddFourNumbers = R.curryN(4, sumArgs);
const f = curriedAddFourNumbers(1, 2);
const g = f(3);
g(4); //=> 10
```

### 参考
- [https://ramdajs.com/docs/#curryN](https://ramdajs.com/docs/#curryN)

## descend
由返回值可与 `<` 和 `>` 比较的函数，创建一个降序比较函数。

### 参数

```
Ord b => (a → b) → a → a → Number

```

- `fn`：一个返回值是可以比较的值的函数。
- `a`：要比较的第一项。
- `b`：要比较的第二项。
- 返回 `Number`：如果 `fn(a) > fn(b)` 返回 `-1`，`fn(b) > fn(a)` 返回 `1`，否则返回 `0`。

### 例子

```js
const byAge = R.descend(R.prop('age'));
const people = [
    { name: 'Emma', age: 70 },
    { name: 'Peter', age: 78 },
    { name: 'Mikhail', age: 62 },
];
const peopleByOldestFirst = R.sort(byAge, people);
//=> [{ name: 'Peter', age: 78 }, { name: 'Emma', age: 70 }, { name: 'Mikhail', age: 62 }]
```

### 参考
- [https://ramdajs.com/docs/#descend](https://ramdajs.com/docs/#descend)

## empty
根据传入参数的类型返回其对应的空值。Ramda 定义了各类型的空值如下：Array (`[]`)，Object (`{}`)，String (`''`)，和 Arguments。`empty` 还支持其它定义了 `<Type>.empty` 、`<Type>.prototype.empty` 或 实现了 [FantasyLand Monoid 规范](https://github.com/fantasyland/fantasy-land#monoid) 的类型。

若第一个参数自身存在 `empty` 方法，则调用自身的 `empty` 方法。

### 参数

```
a → a
```

- `x`。
- 返回 `*`。

### 例子

```js
R.empty(Just(42));      //=> Nothing()
R.empty([1, 2, 3]);     //=> []
R.empty('unicorns');    //=> ''
R.empty({ x: 1, y: 2 });  //=> {}
```

### 参考
- [https://ramdajs.com/docs/#empty](https://ramdajs.com/docs/#empty)

## F
恒定返回 `false` 的函数。忽略所有的输入参数。

### 参数

```
* → Boolean
```

- 返回 `Boolean`。

### 例子

```js
R.F(); //=> false
```

### 参考
- [https://ramdajs.com/docs/#F](https://ramdajs.com/docs/#F)

## flip
交换函数前两个参数的位置。

### 参数

```
((a, b, c, …) → z) → (b → a → c → … → z)
```

- `fn`：要调用的前两个参数相反的函数。
- 返回 `*` ：调用 `fn` 的结果，其前两个参数的顺序相反。

### 例子

```js
const mergeThree = (a, b, c) => [].concat(a, b, c);

mergeThree(1, 2, 3); //=> [1, 2, 3]

R.flip(mergeThree)(1, 2, 3); //=> [2, 1, 3]
```

### 参考
- [https://ramdajs.com/docs/#flip](https://ramdajs.com/docs/#flip)

## identity
将输入值原样返回。适合用作默认或占位函数。

### 参数

```
a → a
```

- `x`：要返回的值。
- 返回 `*`：输入值 `x`。

### 例子

```js
R.identity(1); //=> 1

const obj = {};
R.identity(obj) === obj; //=> true
```

### 参考
- [https://ramdajs.com/docs/#identity](https://ramdajs.com/docs/#identity)

## invoker
将具有指定元数（参数个数）的具名方法，转换为可以被给定参数和目标对象直接调用的函数。

返回的函数是柯里化的，它接收 `arity + 1` 个参数，其中最后一个参数是目标对象。

### 参数

```
Number → String → (a → b → … → n → Object → *)
```

- `arity`：返回的函数应在目标对象之前接受的参数数量。
- `method`：目标对象要调用的任何方法的名称。
- 返回 `function`：一个新的柯里化的函数。

### 例子

```js
const sliceFrom = R.invoker(1, 'slice');
sliceFrom(6, 'abcdefghijklm'); //=> 'ghijklm'
const sliceFrom6 = R.invoker(2, 'slice')(6);
sliceFrom6(8, 'abcdefghijklm'); //=> 'gh'

const dog = {
    speak: async () => 'Woof!'
};
const speak = R.invoker(0, 'speak');
speak(dog).then(console.log) //~> 'Woof!'
```

### 参考
- [https://ramdajs.com/docs/#invoker](https://ramdajs.com/docs/#invoker)

## juxt
将函数列表作用于值列表。

### 参数

```
[(a, b, …, m) → n] → ((a, b, …, m) → [n])
```

- `fns`：函数数组
- 返回 `function`：一个函数，该函数在将每个原始 `fns` 应用于其参数后返回值列表。

### 例子

```js
const getRange = R.juxt([Math.min, Math.max]);
getRange(3, 4, 9, -3); //=> [-3, 9]
```

### 参考
- [https://ramdajs.com/docs/#juxt](https://ramdajs.com/docs/#juxt)

## lift
提升一个多元函数，使之能映射到列表、函数或其他符合 [FantasyLand Apply spec](https://github.com/fantasyland/fantasy-land#apply) 规范的对象上。

### 参数

```
(*… → *) → ([*]… → [*])
```

- `fn`：要提升到更高环境的函数
- 返回 `function`：提升的函数。

### 例子

```js
const madd3 = R.lift((a, b, c) => a + b + c);

madd3([1, 2, 3], [1, 2, 3], [1]); //=> [3, 4, 5, 4, 5, 6, 5, 6, 7]

const madd5 = R.lift((a, b, c, d, e) => a + b + c + d + e);

madd5([1, 2], [3], [4, 5], [6], [7, 8]); //=> [21, 22, 22, 23, 22, 23, 23, 24]
```

### 参考
- [https://ramdajs.com/docs/#lift](https://ramdajs.com/docs/#lift)

## liftN
将一个函数提升为指定元数的函数，使之能映射到多个列表、函数或其他符合 [FantasyLand Apply spec](https://github.com/fantasyland/fantasy-land#apply) 规范的对象上。

### 参数

```
Number → (*… → *) → ([*]… → [*])
```

- `fn`：要提升到更高环境的函数
- 返回 `function`：提升的函数。

### 例子

```js
const madd3 = R.liftN(3, (...args) => R.sum(args));
madd3([1, 2, 3], [1, 2, 3], [1]); //=> [3, 4, 5, 4, 5, 6, 5, 6, 7]
```

### 参考
- [https://ramdajs.com/docs/#liftN](https://ramdajs.com/docs/#liftN)

## memoizeWith
创建一个新函数，当调用时，会执行原函数，输出结果；并且缓存本次的输入参数及其对应的结果。后续，若用相同的参数对缓存函数进行调用，不会再执行原函数，而是直接返回该参数对应的缓存值。

`memoizeWith` 接受两个函数，第一个会将输入参数序列化为缓存键值对的“键值”，第二个是需要缓存的函数。

### 参数

```
(*… → String) → (*… → a) → (*… → a)
```

- `fn`：生成缓存键的函数。
- `fn`：记忆函数。
- 返回 `function`：`fn` 的记忆版本。

### 例子

```js
let count = 0;
const factorial = R.memoizeWith(R.identity, n => {
    count += 1;
    return R.product(R.range(1, n + 1));
});
factorial(5); //=> 120
factorial(5); //=> 120
factorial(5); //=> 120
count; //=> 1
```

### 参考
- [https://ramdajs.com/docs/#memoizeWith](https://ramdajs.com/docs/#memoizeWith)

## nAry
将一个任意元（包括零元）的函数，封装成一个确定元数（参数个数）的函数。任何多余的参数都不会传入被封装的函数。

### 参数

```
Number → (* → a) → (* → a)
```

- `n`：新函数的期望元数。
- `fn`：要包装的函数。
- 返回 `function`：一个包装 `fn` 的新函数。保证新函数的元数为 `n`。

### 例子

```js
const takesTwoArgs = (a, b) => [a, b];

takesTwoArgs.length; //=> 2
takesTwoArgs(1, 2); //=> [1, 2]

const takesOneArg = R.nAry(1, takesTwoArgs);
takesOneArg.length; //=> 1
// Only `n` arguments are passed to the wrapped function
takesOneArg(1, 2); //=> [1, undefined]
```

### 参考
- [https://ramdajs.com/docs/#nAry](https://ramdajs.com/docs/#nAry)

## nthArg
返回一个函数，该函数返回它的第 `n` 个参数。

### 参数

```
Number → *… → *
```

- `n`。
- 返回 `function`。

### 例子

```js
R.nthArg(1)('a', 'b', 'c'); //=> 'b'
R.nthArg(-1)('a', 'b', 'c'); //=> 'c'
```

### 参考
- [https://ramdajs.com/docs/#nthArg](https://ramdajs.com/docs/#nthArg)

## o
`o` 是一个柯里化组合函数，返回一元函数。

类似于 `compose`，`o` 从右到左执行函数组合。但与 `compose` 不同的是，传递给 `o` 的最右边的函数为一元函数。

### 参数

```
(b → c) → (a → b) → a → c
```

- `f`。
- `g`。
- 返回 `function`。

### 例子

```js
const classyGreeting = name => "The name's " + name.last + ", " + name.first + " " + name.last
const yellGreeting = R.o(R.toUpper, classyGreeting);
yellGreeting({ first: 'James', last: 'Bond' }); //=> "THE NAME'S BOND, JAMES BOND"

R.o(R.multiply(10), R.add(10))(-4) //=> 60
```

### 参考
- [https://ramdajs.com/docs/#o](https://ramdajs.com/docs/#o)

## of
将给定值作为元素，封装成单元素数组。

注意，`R.of` 与 ES6 的 `of` 不同；详见 [Array.of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/of)。

### 参数
- `x`：任何值。
- 返回 `Array`：包裹着 `x` 的数组。

### 例子

```js
R.of(null); //=> [null]
R.of([42]); //=> [[42]]
```

### 参考
- [https://ramdajs.com/docs/#of](https://ramdajs.com/docs/#of)

## once
创建一个只执行一次的函数。

将给定函数 `fn` 封装到新函数 `fn'` 中，`fn'` 确保 `fn` 只能调用一次。重复调用 `fn'` ，只会返回第一次执行时的结果。

### 参数

```js
(a… → b) → (a… → b)
```

- `fn`：包裹一次性调用包装器的函数。
- 返回`function`：包装的函数。

### 例子

```js
const addOneOnce = R.once(x => x + 1);
addOneOnce(10); //=> 11
addOneOnce(addOneOnce(50)); //=> 11
```

### 参考
- [https://ramdajs.com/docs/#once](https://ramdajs.com/docs/#once)

## otherwise
将 `onFailure` 函数应用于一个失败 Promise 的内部值，并将计算结果放入新的 Promise 中返回。这对于处理函数组合内的 rejected promises 很有用。

相当于 Promise 的 `catch`。

### 参数

```js
(e → b) → (Promise e a) → (Promise e b)
(e → (Promise f b)) → (Promise e a) → (Promise f b)
```

- `onFailure`：要应用的函数。可以返回值或值的 Promise 包装。
- `p`：返回 Promise 调用 `p.then(null，onFailure)` 的结果。

### 例子

```js
var failedFetch = (id) => Promise.reject('bad ID');
var useDefault = () => ({ firstName: 'Bob', lastName: 'Loblaw' })

//recoverFromFailure :: String -> Promise ({firstName, lastName})
var recoverFromFailure = R.pipe(
    failedFetch,
    R.otherwise(useDefault),
    R.then(R.pick(['firstName', 'lastName'])),
);
recoverFromFailure(12345).then(console.log)
```

### 参考
- [https://ramdajs.com/docs/#otherwise](https://ramdajs.com/docs/#otherwise)

## partial

部分应用。

接收两个参数：函数 `f` 和 参数列表，返回函数 `g`。当调用 `g` 时，将初始参数和 `g` 的参数顺次传给 `f`，并返回 `f` 的执行结果。

### 参数

```
((a, b, c, …, n) → x) → [a, b, c, …] → ((d, e, f, …, n) → x)
```

- `f`。
- `args`。
- 返回 `function`。

### 例子

```js
const multiply2 = (a, b) => a * b;
const double = R.partial(multiply2, [2]);
double(2); //=> 4

const greet = (salutation, title, firstName, lastName) =>
    salutation + ', ' + title + ' ' + firstName + ' ' + lastName + '!';

const sayHello = R.partial(greet, ['Hello']);
const sayHelloToMs = R.partial(sayHello, ['Ms.']);
sayHelloToMs('Jane', 'Jones'); //=> 'Hello, Ms. Jane Jones!'
```

### 参考
- [https://ramdajs.com/docs/#partial](https://ramdajs.com/docs/#partial)

## partialRight
部分应用。

接收两个参数：函数 `f` 和 参数列表，返回函数 `g`。当调用 `g` 时，将 `g` 的参数和初始参数顺序传给 `f`，并返回 `f` 的执行结果。

### 参数

```
((a, b, c, …, n) → x) → [d, e, f, …, n] → ((a, b, c, …) → x)
```

- `f`。
- `args`。
- 返回 `function`。

### 例子

```js
const greet = (salutation, title, firstName, lastName) =>
    salutation + ', ' + title + ' ' + firstName + ' ' + lastName + '!';

const greetMsJaneJones = R.partialRight(greet, ['Ms.', 'Jane', 'Jones']);

greetMsJaneJones('Hello'); //=> 'Hello, Ms. Jane Jones!'
```

### 参考
- [https://ramdajs.com/docs/#partialRight](https://ramdajs.com/docs/#partialRight)

## pipe
从左往右执行函数组合。第一个函数可以是任意元函数（参数个数不限），其余函数必须是一元函数。

在一些库中，此函数也被称为 `sequence`。

注意：`pipe` 函数的结果不是自动柯里化的。

### 参数

```
(((a, b, …, n) → o), (o → p), …, (x → y), (y → z)) → ((a, b, …, n) → z)
```

- `functions`。
- 返回 `function`。

### 例子

```js
const f = R.pipe(Math.pow, R.negate, R.inc);

f(3, 4); // -(3^4) + 1
```

### 参考
- [https://ramdajs.com/docs/#pipe](https://ramdajs.com/docs/#pipe)

## pipeK
`Deprecated`

将一系列函数，转换成从左到右的 Kleisli 组合，每个函数必须返回支持 `chain` 操作的值。

`R.pipeK(f, g, h)` 等价于 `R.pipe(f, R.chain(g), R.chain(h))`。

### 参数

```
Chain m => ((a → m b), (b → m c), …, (y → m z)) → (a → m z)
```

- 返回 `function`。

### 例子

```js
//  parseJson :: String -> Maybe *
//  get :: String -> Object -> Maybe *

//  getStateCode :: Maybe String -> Maybe String
const getStateCode = R.pipeK(
    parseJson,
    get('user'),
    get('address'),
    get('state'),
    R.compose(Maybe.of, R.toUpper)
);

getStateCode('{"user":{"address":{"state":"ny"}}}');
//=> Just('NY')
getStateCode('[Invalid JSON]');
//=> Nothing()
```

### 参考
- [https://ramdajs.com/docs/#pipeK](https://ramdajs.com/docs/#pipeK)

## pipeP
`Deprecated`

从左往右执行返回 Promise 的函数的组合。第一个函数可以是任意元函数（参数个数不限）；其余函数必须是一元函数。

### 参数

```
((a → Promise b), (b → Promise c), …, (y → Promise z)) → (a → Promise z)
```

- `functions`。
- 返回 `function`。

### 例子

```js
//  followersForUser :: String -> Promise [User]
const followersForUser = R.pipeP(db.getUserById, db.getFollowers);
```

### 参考
- [https://ramdajs.com/docs/#pipeP](https://ramdajs.com/docs/#pipeP)

## pipeWith
利用转换函数从左往右执行函数组合。第一个函数可以是任意元函数（参数个数不限），其余函数必须是一元函数。

注意：`pipe` 输出的函数不会自动进行柯里化。

### 参数

```
((* → *), [((a, b, …, n) → o), (o → p), …, (x → y), (y → z)]) → ((a, b, …, n) → z)
```

- `functions`。
- 返回 `function`。

### 例子

```js
const pipeWhileNotNil = R.pipeWith((f, res) => R.isNil(res) ? res : f(res));
const f = pipeWhileNotNil([Math.pow, R.negate, R.inc])

f(3, 4); // -(3^4) + 1
```

### 参考
- [https://ramdajs.com/docs/#pipeWith](https://ramdajs.com/docs/#pipeWith)

## T
恒定返回 `true` 的函数。忽略所有的输入参数。

### 参数

```
* → Boolean
```

- 返回 `Boolean`。

### 例子

```js
R.T(); //=> true
```

### 参考
- [https://ramdajs.com/docs/#T](https://ramdajs.com/docs/#T)

## tap
对输入的值执行给定的函数，然后返回输入的值。

若在列表位置给出 transformer，则用做 transducer 。

### 参数

```
(a → *) → a → a
```

- `fn`：用 `x` 调用的函数。`fn` 的返回值将被丢弃。
- `x`。
- 返回 `*`： `x`。

### 例子

```js
const sayX = x => console.log('x is ' + x);
R.tap(sayX, 100); //=> 100
// logs 'x is 100'
```

### 参考
- [https://ramdajs.com/docs/#tap](https://ramdajs.com/docs/#tap)

## thunkify
创建一个 thunk 版本的函数。 thunk 会延迟计算直到需要其结果，从而实现惰性求值。

### 参数

```
((a, b, …, j) → k) → (a, b, …, j) → (() → k)
```

- `fn`：包装进 thunk 的函数。
- 返回 `function`：期望参数为 `fn`，并返回一个新函数，该函数在调用时将这些参数应用于 `fn`。

### 例子

```js
R.thunkify(R.identity)(42)(); //=> 42
R.thunkify((a, b) => a + b)(25, 17)(); //=> 42
```

### 参考
- [https://ramdajs.com/docs/#thunkify](https://ramdajs.com/docs/#thunkify)

## tryCatch
`tryCatch` 接受两个函数：`tryer` 和 `catcher`，生成的函数执行 `tryer`，若未抛出异常，则返回执行结果。若抛出异常，则执行 `catcher`，返回 `catcher` 的执行结果。注意，为了有效的组合该函数，`tryer` 和 `catcher` 应返回相同类型的值。

### 参数

```js
(…x → a) → ((e, …x) → a) → (…x → a)
```

- `tryer`：可能抛出的函数。
- `catcher`：如果 `tryer` 抛出，将执行的函数。
- 返回 `function`：一个新函数，它将捕获异常并将其发送给捕获器。

### 例子

```js
R.tryCatch(R.prop('x'), R.F)({ x: true }); //=> true
R.tryCatch(() => { throw 'foo' }, R.always('catched'))('bar') // => 'catched'
R.tryCatch(R.times(R.identity), R.always([]))('s') // => []
R.tryCatch(() => { throw 'this is not a valid value' }, (err, value) => ({ error: err, value }))('bar') // => {'error': 'this is not a valid value', 'value': 'bar'}
```

### 参考
- [https://ramdajs.com/docs/#tryCatch](https://ramdajs.com/docs/#tryCatch)

## unapply

输入一个只接收单个数组作为参数的函数，返回一个新函数：
- 接收任意个参数；
- 将参数组成数组传递给 `fn` ；
- 返回执行结果。

换言之，`R.unapply` 将一个使用数组作为参数的函数，变为一个不定参函数。`R.unapply` 是 `R.apply` 的逆函数。

### 参数

```
([*…] → a) → (*… → a)
```

- `fn`。
- 返回 `function`。

### 例子

```js
R.unapply(JSON.stringify)(1, 2, 3); //=> '[1,2,3]'
```

### 参考
- [https://ramdajs.com/docs/#unapply](https://ramdajs.com/docs/#unapply)

## unary
将任意元（包括零元）函数封装成一元函数。任何额外的参数都不会传递给被封装的函数。

### 参数

```
(* → b) → (a → b)
```

- `fn` 要包装的函数。
- 返回 `function`： 一个包装 `fn` 的新函数。保证新函数具有一元参数。

### 例子

```js
const takesTwoArgs = function (a, b) {
    return [a, b];
};
takesTwoArgs.length; //=> 2
takesTwoArgs(1, 2); //=> [1, 2]

const takesOneArg = R.unary(takesTwoArgs);
takesOneArg.length; //=> 1
// Only 1 argument is passed to the wrapped function
takesOneArg(1, 2); //=> [1, undefined]
```

### 参考
- [https://ramdajs.com/docs/#unary](https://ramdajs.com/docs/#unary)

## uncurryN
将一个柯里化的函数转换为一个 `n` 元函数。

### 参数

```
Number → (a → b) → (a → c)
```

- `length`：返回函数的元数。
- `fn`：去柯里化的函数。
- 返回 `function`： 一个新函数。

### 例子

```js
const addFour = a => b => c => d => a + b + c + d;

const uncurriedAddFour = R.uncurryN(4, addFour);
uncurriedAddFour(1, 2, 3, 4); //=> 10
```

### 参考
- [https://ramdajs.com/docs/#uncurryN](https://ramdajs.com/docs/#uncurryN)

## useWith
接受一个函数 `fn` 和一个 `transformer` 函数的列表，返回一个柯里化的新函数。当被调用时，新函数将每个参数转发给对应位置的 `transformer` 函数，然后将每个 `transformer` 函数的计算结果作为参数传递给 `fn`，`fn` 的计算结果即新函数的返回值。

如果新函数传传入参数的数量比 `transformer` 函数的数量多，多出的参数会作为附加参数直接传给 `fn` 。如果不需要处理多出的那部分参数，除了忽略之外，也可以用 `identity` 函数来作为 `transformer`，以保证新函数的参数数量是确定的。

### 参数

```
((x1, x2, …) → z) → [(a → x1), (b → x2), …] → (a → b → … → z)
```

- `fn`：要包装的函数。
- `transformers`：`transformer` 函数列表。
- 返回 `function`：包装的函数。

### 例子

```js
R.useWith(Math.pow, [R.identity, R.identity])(3, 4); //=> 81
R.useWith(Math.pow, [R.identity, R.identity])(3)(4); //=> 81
R.useWith(Math.pow, [R.dec, R.inc])(3, 4); //=> 32
R.useWith(Math.pow, [R.dec, R.inc])(3)(4); //=> 32
```

### 参考
- [https://ramdajs.com/docs/#useWith](https://ramdajs.com/docs/#useWith)

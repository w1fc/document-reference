## is
检测一个对象（`val`）是否是给定构造函数的实例。该函数会依次检测其原型链，如果存在的话。

### 参数

```
(* → {*}) → a → Boolean
```

- `ctor`：构造函数。
- `val`：要测试的值。
- 返回`Boolean`。

### 例子

```js
R.is(Object, {}); //=> true
R.is(Number, 1); //=> true
R.is(Object, 1); //=> false
R.is(String, 's'); //=> true
R.is(String, new String('')); //=> true
R.is(Object, new String('')); //=> true
R.is(Object, 's'); //=> false
R.is(Number, {}); //=> false
```

### 参考
- [https://ramdajs.com/docs/#is](https://ramdajs.com/docs/#is)

## isNil
检测输入值是否为 `null` 或 `undefined` 。

### 参数

```
* → Boolean
```

- `x`：要测试的值。
- 返回`Boolean`：如果 `x` 是 `undefined` 或 `null`，则为 `true`；否则为 `false`。

### 例子

```js
R.isNil(null); //=> true
R.isNil(undefined); //=> true
R.isNil(0); //=> false
R.isNil([]); //=> false
```

### 参考
- [https://ramdajs.com/docs/#isNil](https://ramdajs.com/docs/#isNil)

## propIs
判断指定对象的属性是否为给定的数据类型，是则返回 `true` ；否则返回 `false` 。

### 参数

```
Type → String → Object → Boolean
```

- `type`。
- `name`。
- `obj`。
- 返回`Boolean`。

### 例子

```js
R.propIs(Number, 'x', {x: 1, y: 2});  //=> true
R.propIs(Number, 'x', {x: 'foo'});    //=> false
R.propIs(Number, 'x', {});            //=> false
```

### 参考
- [https://ramdajs.com/docs/#propIs](https://ramdajs.com/docs/#propIs)

## type
用一个单词来描述输入值的（原生）类型，返回诸如 `'Object'`、`'Number'`、`'Array'`、`'Null'` 之类的结果。不区分用户自定义的类型，统一返回 `'Object'`。

### 参数

```
(* → {*}) → String
```

- `val`：要测试的值。
- 返回`String`。

### 例子

```js
R.type({}); //=> "Object"
R.type(1); //=> "Number"
R.type(false); //=> "Boolean"
R.type('s'); //=> "String"
R.type(null); //=> "Null"
R.type([]); //=> "Array"
R.type(/[A-z]/); //=> "RegExp"
R.type(() => {}); //=> "Function"
R.type(undefined); //=> "Undefined"
```

### 参考
- [https://ramdajs.com/docs/#type](https://ramdajs.com/docs/#type)

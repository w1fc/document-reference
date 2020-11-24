## match
正则匹配字符串。注意，如果没有匹配项，则返回空数组。和 `String.prototype.match` 不同，后者在没有匹配项时会返回 `null`。

### 参数

```
RegExp → String → [String | Undefined]
```

- `rx`：正则表达式。
- `str`：要匹配的字符串。
- 返回`Array`：匹配项列表或空数组。

### 例子

```js
R.match(/([a-z]a)/g, 'bananas'); //=> ['ba', 'na', 'na']
R.match(/a/, 'b'); //=> []
R.match(/a/, null); //=> TypeError: null does not have a method named "match"
```

### 参考
- [https://ramdajs.com/docs/#match](https://ramdajs.com/docs/#match)

## replace
替换字符串的子串或正则匹配到的值。

### 参数

```
RegExp|String → String → String → String
```

- `pattern`：正则表达式或要匹配的子字符串。
- `replacement`：用于替换匹配项的字符串。
- `str`：用于搜索和替换的字符串。
- 返回`String`：结果。

### 例子

```js
R.replace('foo', 'bar', 'foo foo foo'); //=> 'bar foo foo'
R.replace(/foo/, 'bar', 'foo foo foo'); //=> 'bar foo foo'

// Use the "g" (global) flag to replace all occurrences:
R.replace(/foo/g, 'bar', 'foo foo foo'); //=> 'bar bar bar'
```

### 参考
- [https://ramdajs.com/docs/#replace](https://ramdajs.com/docs/#replace)

## split
根据指定的分隔符将字符串拆分为字符串类型的数组。

### 参数

```
(String | RegExp) → String → [String]
```

- `sep`：模式。
- `str`：要分离成数组的字符串。
- 返回`Array`：数组 `str` 中的字符串，由 `sep` 分隔。

### 例子

```js
const pathComponents = R.split('/');
R.tail(pathComponents('/usr/local/bin/node')); //=> ['usr', 'local', 'bin', 'node']

R.split('.', 'a.b.c.xyz.d'); //=> ['a', 'b', 'c', 'xyz', 'd']
```

### 参考
- [https://ramdajs.com/docs/#split](https://ramdajs.com/docs/#split)

## test
检测字符串是否匹配给定的正则表达式。

### 参数

```
RegExp → String → Boolean
```

- `pattern`。
- `str`。
- 返回`Boolean`。

### 例子

```js
R.test(/^x/, 'xyz'); //=> true
R.test(/^y/, 'xyz'); //=> false
```

### 参考
- [https://ramdajs.com/docs/#test](https://ramdajs.com/docs/#test)

## toLower
将字符串转换成小写。

### 参数

```
String → String
```

- `str`：要转为小写的字符串。
- 返回`String`：小写的 `str` 版本。

### 例子

```js
R.toLower('XYZ'); //=> 'xyz'
```

### 参考
- [https://ramdajs.com/docs/#toLower](https://ramdajs.com/docs/#toLower)

## toString
返回代表输入元素的字符串。求得的输出结果应该等价于输入的值。许多内建的 `toString` 方法都不满足这一条件。

如果输入值是 `[object Object]` 对象，且自身含有 `toString` 方法（不是 `Object.prototype.toString` 方法），那么直接调用这个方法求返回值。这意味着，通过用户自定义的构造函数可以提供合适的 `toString` 方法。

### 参数

```
* → String
```

- `val`。
- 返回 `String`。

### 例子

```js
function Point(x, y) {
    this.x = x;
    this.y = y;
}

Point.prototype.toString = function () {
    return 'new Point(' + this.x + ', ' + this.y + ')';
};

R.toString(new Point(1, 2)); //=> 'new Point(1, 2)'
R.toString(42); //=> '42'
R.toString('abc'); //=> '"abc"'
R.toString([1, 2, 3]); //=> '[1, 2, 3]'
R.toString({ foo: 1, bar: 2, baz: 3 }); //=> '{"bar": 2, "baz": 3, "foo": 1}'
R.toString(new Date('2001-02-03T04:05:06Z')); //=> 'new Date("2001-02-03T04:05:06.000Z")'
```

### 参考
- [https://ramdajs.com/docs/#toString](https://ramdajs.com/docs/#toString)

## toUpper
将字符串转换为大写。

### 参数

```
String → String
```

- `str`：要转为大写的字符串。
- 返回`String`：大写的 `str` 版本。

### 例子

```js
R.toUpper('abc'); //=> 'ABC'
```

### 参考
- [https://ramdajs.com/docs/#toUpper](https://ramdajs.com/docs/#toUpper)

## trim
删除字符串首、尾两端的空白字符。

### 参数

```
String → String
```

- `str`：待修剪的字符串。
- 返回`String`：修剪后的`str`。

### 例子

```js
R.trim('   xyz  '); //=> 'xyz'
R.map(R.trim, R.split(',', 'x, y, z')); //=> ['x', 'y', 'z']
```

### 参考
- [https://ramdajs.com/docs/#trim](https://ramdajs.com/docs/#trim)

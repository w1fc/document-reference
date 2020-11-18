## camelCase

```js
_.camelCase([string=''])
```

转换字符串 `string` 为 [驼峰写法](https://en.wikipedia.org/wiki/CamelCase)。

### 参数
- `[string=''] (string)`: 要转换的字符串。

### 返回
- `(string)`: 返回驼峰写法的字符串。

### 例子

```js
_.camelCase('Foo Bar');
// => 'fooBar'

_.camelCase('--foo-bar--');
// => 'fooBar'

_.camelCase('__FOO_BAR__');
// => 'fooBar'
```

### 参考
- [https://lodash.com/docs/4.17.15#camelCase](https://lodash.com/docs/4.17.15#camelCase)

## capitalize

```js
_.capitalize([string=''])
```

转换字符串 `string` 首字母为大写，剩下为小写。

### 参数
- `[string=''] (string)`: 要大写开头的字符串。

### 返回
- `(string)`: 返回大写开头的字符串。

### 例子

```js
_.capitalize('FRED');
// => 'Fred'
```

### 参考
- [https://lodash.com/docs/4.17.15#capitalize](https://lodash.com/docs/4.17.15#capitalize)

## deburr

```js
_.deburr([string=''])
```

转换字符串 `string` 中 [拉丁语-1补充字母](https://en.wikipedia.org/wiki/Latin-1_Supplement_(Unicode_block)#Character_table) 和 [拉丁语扩展字母-A](https://en.wikipedia.org/wiki/Latin_Extended-A) 为基本的拉丁字母，并且去除组合变音标记。

### 参数
- `[string=''] (string)`: 要处理的字符串。

### 返回
- `(string)`: 返回处理后的字符串。

### 例子

```js
_.deburr('déjà vu');
// => 'deja vu'
```

### 参考
- [https://lodash.com/docs/4.17.15#deburr](https://lodash.com/docs/4.17.15#deburr)

## endsWith

```js
_.endsWith([string=''], [target], [position=string.length])
```

检查字符串 `string` 是否以给定的 `target` 字符串结尾。

### 参数
- `[string=''] (string)`: 要检索的字符串。
- `[target] (string)`: 要检索字符。
- `[position=string.length] (number)`: 检索的位置。

### 返回
- `(boolean)`: 如果字符串 `string` 以 `target` 字符串结尾，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.endsWith('abc', 'c');
// => true

_.endsWith('abc', 'b');
// => false

_.endsWith('abc', 'b', 2);
// => true
```

### 参考
- [https://lodash.com/docs/4.17.15#endsWith](https://lodash.com/docs/4.17.15#endsWith)

## escape

```js
_.escape([string=''])
```

转义string中的 `"&"`, `"<"`, `">"`, `'"'`, `"'"`, 和 <code>"`"</code> 字符为 HTML 实体字符。

注意: 不会转义其他字符。如果需要，可以使用第三方库，例如 [he](https://github.com/mathiasbynens/he)。

虽然 `">"` 是对称转义的，字符如 `">"` 和 `"/"` 没有特殊的意义，所以不需要在 HTML 转义。除非它们是标签的一部分，或者是不带引号的属性值。查看 [Mathias Bynens's article](https://mathiasbynens.be/notes/ambiguous-ampersands) 了解详情 。

当解析 HTML 时，总应该在 [属性值上使用引号](http://wonko.com/post/html-escaping) 以减少 XSS 的可能性。

### 参数
- `[string=''] (string)`: 要转义的字符串。

### 返回
- `(string)`: 返回转义后的字符串。

### 例子

```js
_.escape('fred, barney, & pebbles');
// => 'fred, barney, &amp; pebbles'
```

### 参考
- [https://lodash.com/docs/4.17.15#escape](https://lodash.com/docs/4.17.15#escape)

## escapeRegExp

```js
_.escapeRegExp([string=''])
```

转义 `RegExp` 字符串中特殊的字符 `"^"`, `"$"`, `""`, `"."`, `"*"`, `"+"`, `"?"`, `"("`, `")"`, `"["`, `"]"`, `"{"`, `"}"`, 和 `"|"`。

### 参数
- `[string=''] (string)`: 要转义的字符串。

### 返回
- `(string)`: 返回转义后的字符串。

### 例子

```js
_.escapeRegExp('[lodash](https://lodash.com/)');
// => '\[lodash\]\(https://lodash\.com/\)'
```

### 参考
- [https://lodash.com/docs/4.17.15#escapeRegExp](https://lodash.com/docs/4.17.15#escapeRegExp)

## kebabCase

```js
_.kebabCase([string=''])
```

转换字符串 `string` 为 [kebab case](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles).

### 参数
- `[string=''] (string)`: 要转换的字符串。

### 返回
- `(string)`: 返回转换后的字符串。

### 例子

```js
_.kebabCase('Foo Bar');
// => 'foo-bar'

_.kebabCase('fooBar');
// => 'foo-bar'

_.kebabCase('__FOO_BAR__');
// => 'foo-bar'
```

### 参考
- [https://lodash.com/docs/4.17.15#kebabCase](https://lodash.com/docs/4.17.15#kebabCase)

## lowerCase

```js
_.lowerCase([string=''])
```

转换字符串 `string` 以空格分开单词，并转换为小写。

### 参数
- `[string=''] (string)`: 要转换的字符串。

### 返回
- `(string)`: 返回转换后的字符串。

### 例子

```js
_.lowerCase('--Foo-Bar--');
// => 'foo bar'

_.lowerCase('fooBar');
// => 'foo bar'

_.lowerCase('__FOO_BAR__');
// => 'foo bar'
```

### 参考
- [https://lodash.com/docs/4.17.15#lowerCase](https://lodash.com/docs/4.17.15#lowerCase)

## lowerFirst

```js
_.lowerFirst([string=''])
```

转换字符串 `string` 的首字母为小写。

### 参数
- `[string=''] (string)`: 要转换的字符串。

### 返回
- `(string)`: 返回转换后的字符串。

### 例子

```js
_.lowerFirst('Fred');
// => 'fred'

_.lowerFirst('FRED');
// => 'fRED'
```

### 参考
- [https://lodash.com/docs/4.17.15#lowerFirst](https://lodash.com/docs/4.17.15#lowerFirst)

## pad

```js
_.pad([string=''], [length=0], [chars=' '])
```

如果 `string` 字符串长度小于 `length` 则从左侧和右侧填充字符。如果没法平均分配，则截断超出的长度。

### 参数
- `[string=''] (string)`: 要填充的字符串。
- `[length=0] (number)`: 填充的长度。
- `[chars=' '] (string)`: 填充字符。

### 返回
- `(string)`: 返回填充后的字符串。

### 例子

```js
_.pad('abc', 8);
// => '  abc   '

_.pad('abc', 8, '_-');
// => '_-abc_-_'

_.pad('abc', 3);
// => 'abc'
```

### 参考
- [https://lodash.com/docs/4.17.15#pad](https://lodash.com/docs/4.17.15#pad)

## padEnd

```js
_.padEnd([string=''], [length=0], [chars=' '])
```

如果 `string` 字符串长度小于 `length` 则在右侧填充字符。如果超出 `length` 长度则截断超出的部分。

### 参数
- `[string=''] (string)`: 要填充的字符串。
- `[length=0] (number)`: 填充的长度。
- `[chars=' '] (string)`: 填充字符。

### 返回
- `(string)`: 返回填充后的字符串。

### 例子

```js
_.padEnd('abc', 6);
// => 'abc   '

_.padEnd('abc', 6, '_-');
// => 'abc_-_'

_.padEnd('abc', 3);
// => 'abc'
```

### 参考
- [https://lodash.com/docs/4.17.15#padEnd](https://lodash.com/docs/4.17.15#padEnd)

## padStart

```js
_.padStart([string=''], [length=0], [chars=' '])
```

如果 `string` 字符串长度小于 `length` 则在左侧填充字符。如果超出 `length` 长度则截断超出的部分。

### 参数
- `[string=''] (string)`: 要填充的字符串。
- `[length=0] (number)`: 填充的长度。
- `[chars=' '] (string)`: 填充字符。

### 返回
- `(string)`: 返回填充后的字符串。

### 例子

```js
_.padStart('abc', 6);
// => '   abc'

_.padStart('abc', 6, '_-');
// => '_-_abc'

_.padStart('abc', 3);
// => 'abc'
```

### 参考
- [https://lodash.com/docs/4.17.15#padStart](https://lodash.com/docs/4.17.15#padStart)

## parseInt

```js
_.parseInt(string, [radix=10])
```

转换 `string` 字符串为指定基数的整数。如果基数是 `undefined` 或者 `0`，则 `radix` 基数默认是 `10`，如果 `string` 字符串是 16 进制，则 `radix` 基数为 `16`。

注意: 这个方法与 [ES5 implementation](https://es5.github.io/#x15.1.2.2) 的 `parseInt` 是一样的。

### 参数
- `string (string)`: 要转换的字符串。
- `[radix=10] (number)`: 转换基数。

### 返回
- `(number)`: 返回转换后的整数。

### 例子

```js
_.parseInt('08');
// => 8

_.map(['6', '08', '10'], _.parseInt);
// => [6, 8, 10]
```

### 参考
- [https://lodash.com/docs/4.17.15#parseInt](https://lodash.com/docs/4.17.15#parseInt)

## repeat

```js
_.repeat([string=''], [n=1])
```

重复 N 次给定字符串。

### 参数
- `[string=''] (string)`: 要重复的字符串。
- `[n=1] (number)`: 重复的次数。

### 返回
- `(string)`: 返回重复的字符串。

### 例子

```js
_.repeat('*', 3);
// => '***'
 
_.repeat('abc', 2);
// => 'abcabc'
 
_.repeat('abc', 0);
// => ''
```

### 参考
- [https://lodash.com/docs/4.17.15#repeat](https://lodash.com/docs/4.17.15#repeat)

## replace

```js
_.replace([string=''], pattern, replacement)
```

替换 `string` 字符串中匹配的 `pattern` 为给定的 `replacement` 。

注意: 这个方法基于 [String#replace](https://mdn.io/String/replace)。

### 参数
- `[string=''] (string)`: 待替换的字符串。
- `pattern (RegExp|string)`: 要匹配的内容。
- `replacement (Function|string)`: 替换的内容。

### 返回
- `(string)`: 返回替换后的字符串。

### 例子

```js
_.replace('Hi Fred', 'Fred', 'Barney');
// => 'Hi Barney'
```

### 参考
- [https://lodash.com/docs/4.17.15#replace](https://lodash.com/docs/4.17.15#replace)

## snakeCase

```js
_.snakeCase([string=''])
```

转换字符串 `string` 为 [snake case](https://en.wikipedia.org/wiki/Snake_case).

### 参数
- `[string=''] (string)`: 要转换的字符串。

### 返回
- `(string)`: 返回转换后的字符串。

### 例子

```js
_.snakeCase('Foo Bar');
// => 'foo_bar'

_.snakeCase('fooBar');
// => 'foo_bar'

_.snakeCase('--FOO-BAR--');
// => 'foo_bar'
```

### 参考
- [https://lodash.com/docs/4.17.15#snakeCase](https://lodash.com/docs/4.17.15#snakeCase)

## split

```js
_.split([string=''], separator, [limit])
```

根据 `separator` 拆分字符串 `string`。

注意: 这个方法基于 [String#split](https://mdn.io/String/split).

### 参数
- `[string=''] (string)`: 要拆分的字符串。
- `separator (RegExp|string)`: 拆分的分隔符。
- `[limit] (number)`: 限制结果的数量。

### 返回
- `(Array)`: 返回拆分部分的字符串的数组。

### 例子

```js
_.split('a-b-c', '-', 2);
// => ['a', 'b']
```

### 参考
- [https://lodash.com/docs/4.17.15#split](https://lodash.com/docs/4.17.15#split)

## startCase

```js
_.startCase([string=''])
```

转换 `string` 字符串为 [start case]()https://en.wikipedia.org/wiki/Letter_case#Stylistic_or_specialised_usage.

### 参数
- `[string=''] (string)`: 要转换的字符串。

### 返回
- `(string)`: 返回转换后的字符串。

### 例子

```js
_.startCase('--foo-bar--');
// => 'Foo Bar'

_.startCase('fooBar');
// => 'Foo Bar'

_.startCase('__FOO_BAR__');
// => 'FOO BAR'
```

### 参考
- [https://lodash.com/docs/4.17.15#startCase](https://lodash.com/docs/4.17.15#startCase)

## startsWith

```js
_.startsWith([string=''], [target], [position=0])
```

检查字符串 `string` 是否以 `target` 开头。

### 参数
- `[string=''] (string)`: 要检索的字符串。
- `[target] (string)`: 要检查的字符串。
- `[position=0] (number)`: 检索的位置。

### 返回
- `(boolean)`: 如果 `string` 以 `target`，那么返回 `true`，否则返回 `false`。

### 例子

```js
_.startsWith('abc', 'a');
// => true

_.startsWith('abc', 'b');
// => false

_.startsWith('abc', 'b', 1);
// => true
```

### 参考
- [https://lodash.com/docs/4.17.15#startsWith](https://lodash.com/docs/4.17.15#startsWith)

## template

```js
_.template([string=''], [options={}])
```

创建一个预编译模板方法，可以插入数据到模板中 `"interpolate"` 分隔符相应的位置。HTML 会在 `"escape"` 分隔符中转换为相应实体。 在 `"evaluate"` 分隔符中允许执行 JavaScript 代码。在模板中可以自由访问变量。如果设置了选项对象，则会优先覆盖 `_.templateSettings` 的值。

注意: 在开发过程中，构建 `_.template` 可以使用 [sourceURLs](http://www.html5rocks.com/en/tutorials/developertools/sourcemaps/#toc-sourceurl)， 便于调试。

了解更多预编译模板的信息查看 [lodash 的自定义构建文档](https://lodash.com/custom-builds)。

了解更多 Chrome 沙箱扩展的信息查看 [Chrome的扩展文档](https://developer.chrome.com/extensions/sandboxingEval)。

### 参数
- `[string=''] (string)`: 模板字符串.
- `[options={}] (Object)`: 选项对象.
- `[options.escape=_.templateSettings.escape] (RegExp)`: `"escape"` 分隔符.
- `[options.evaluate=_.templateSettings.evaluate] (RegExp)`: `"evaluate"` 分隔符.
- `[options.imports=_.templateSettings.imports] (Object)`: 导入对象到模板中作为自由变量。
- `[options.interpolate=_.templateSettings.interpolate] (RegExp)`: `"interpolate"` 分隔符。
- `[options.sourceURL='lodash.templateSources[n]'] (string)`: 模板编译的来源URL。
- `[options.variable='obj'] (string)`: 数据对象的变量名。

### 返回
- `(Function)`: 返回编译模板函数。

### 例子

```js
// Use the "interpolate" delimiter to create a compiled template.
var compiled = _.template('hello <%= user %>!');
compiled({ 'user': 'fred' });
// => 'hello fred!'

// Use the HTML "escape" delimiter to escape data property values.
var compiled = _.template('<b><%- value %></b>');
compiled({ 'value': '<script>' });
// => '<b>&lt;script&gt;</b>'

// Use the "evaluate" delimiter to execute JavaScript and generate HTML.
var compiled = _.template('<% _.forEach(users, function(user) { %><li><%- user %></li><% }); %>');
compiled({ 'users': ['fred', 'barney'] });
// => '<li>fred</li><li>barney</li>'

// Use the internal `print` function in "evaluate" delimiters.
var compiled = _.template('<% print("hello " + user); %>!');
compiled({ 'user': 'barney' });
// => 'hello barney!'

// Use the ES template literal delimiter as an "interpolate" delimiter.
// Disable support by replacing the "interpolate" delimiter.
var compiled = _.template('hello ${ user }!');
compiled({ 'user': 'pebbles' });
// => 'hello pebbles!'

// Use backslashes to treat delimiters as plain text.
var compiled = _.template('<%= "\\<%- value %\\>" %>');
compiled({ 'value': 'ignored' });
// => '<%- value %>'

// Use the `imports` option to import `jQuery` as `jq`.
var text = '<% jq.each(users, function(user) { %><li><%- user %></li><% }); %>';
var compiled = _.template(text, { 'imports': { 'jq': jQuery } });
compiled({ 'users': ['fred', 'barney'] });
// => '<li>fred</li><li>barney</li>'

// Use the `sourceURL` option to specify a custom sourceURL for the template.
var compiled = _.template('hello <%= user %>!', { 'sourceURL': '/basic/greeting.jst' });
compiled(data);
// => Find the source of "greeting.jst" under the Sources tab or Resources panel of the web inspector.

// Use the `variable` option to ensure a with-statement isn't used in the compiled template.
var compiled = _.template('hi <%= data.user %>!', { 'variable': 'data' });
compiled.source;
// => function(data) {
//   var __t, __p = '';
//   __p += 'hi ' + ((__t = ( data.user )) == null ? '' : __t) + '!';
//   return __p;
// }

// Use custom template delimiters.
_.templateSettings.interpolate = /{{([\s\S]+?)}}/g;
var compiled = _.template('hello {{ user }}!');
compiled({ 'user': 'mustache' });
// => 'hello mustache!'

// Use the `source` property to inline compiled templates for meaningful
// line numbers in error messages and stack traces.
fs.writeFileSync(path.join(process.cwd(), 'jst.js'), '\
  var JST = {\
    "main": ' + _.template(mainText).source + '\
  };\
');
```

### 参考
- [https://lodash.com/docs/4.17.15#template](https://lodash.com/docs/4.17.15#template)

## toLower

```js
_.toLower([string=''])
```

转换整个 `string` 字符串的字符为小写，类似 [String#toLowerCase](https://mdn.io/toLowerCase)。

### 参数
- `[string=''] (string)`: 要转换的字符串。

### 返回
- `(string)`: 返回小写的字符串。

### 例子

```js
_.toLower('--Foo-Bar--');
// => '--foo-bar--'

_.toLower('fooBar');
// => 'foobar'

_.toLower('__FOO_BAR__');
// => '__foo_bar__'
```

### 参考
- [https://lodash.com/docs/4.17.15#toLower](https://lodash.com/docs/4.17.15#toLower)

## toUpper

```js
_.toUpper([string=''])
```

转换整个 `string` 字符串的字符为大写，类似 [String#toUpperCase](https://mdn.io/toUpperCase).

### 参数
- `[string=''] (string)`: 要转换的字符串。

### 返回
- `(string)`: 返回大写的字符串。

### 例子

```js
_.toUpper('--foo-bar--');
// => '--FOO-BAR--'

_.toUpper('fooBar');
// => 'FOOBAR'

_.toUpper('__foo_bar__');
// => '__FOO_BAR__'
```

### 参考
- [https://lodash.com/docs/4.17.15#toLower](https://lodash.com/docs/4.17.15#toLower)

## trim

```js
_.trim([string=''], [chars=whitespace])
```

从 `string` 字符串中移除前面和后面的空格或指定的字符。

### 参数
- `[string=''] (string)`: 要处理的字符串。
- `[chars=whitespace] (string)`: 要移除的字符。

### 返回
- `(string)`: 返回处理后的字符串。

### 例子

```js
_.trim('  abc  ');
// => 'abc'

_.trim('-_-abc-_-', '_-');
// => 'abc'

_.map(['  foo  ', '  bar  '], _.trim);
// => ['foo', 'bar']
```

### 参考
- [https://lodash.com/docs/4.17.15#trim](https://lodash.com/docs/4.17.15#trim)

## trimEnd

```js
_.trimEnd([string=''], [chars=whitespace])
```

从 `string` 字符串中移除后面的空格或指定的字符。

### 参数
- `[string=''] (string)`: 要处理的字符串。
- `[chars=whitespace] (string)`: 要移除的字符。

### 返回
- `(string)`: 返回处理后的字符串。

### 例子

```js
_.trimEnd('  abc  ');
// => '  abc'

_.trimEnd('-_-abc-_-', '_-');
// => '-_-abc'
```

### 参考
- [https://lodash.com/docs/4.17.15#trimEnd](https://lodash.com/docs/4.17.15#trimEnd)

## trimStart

```js
_.trimStart([string=''], [chars=whitespace])
```

从 `string` 字符串中移除前面的空格或指定的字符。

### 参数
- `[string=''] (string)`: 要处理的字符串。
- `[chars=whitespace] (string)`: 要移除的字符。

### 返回
- `(string)`: 返回处理后的字符串。

### 例子

```js
_.trimStart('  abc  ');
// => 'abc  '

_.trimStart('-_-abc-_-', '_-');
// => 'abc-_-'
```

### 参考
- [https://lodash.com/docs/4.17.15#trimStart](https://lodash.com/docs/4.17.15#trimStart)

## truncate

```js
_.truncate([string=''], [options={}])
```

截断 `string` 字符串，如果字符串超出了限定的最大值。被截断的字符串后面会以 `omission` 代替，`omission` 默认是 `"..."`。

### 参数
- `[string=''] (string)`: 要截断的字符串。
- `[options={}] (Object)`: 选项对象。
- `[options.length=30] (number)`: 允许的最大长度。
- `[options.omission='...'] (string)`: 超出后的代替字符。
- `[options.separator] (RegExp|string)`: 截断点。

### 返回
- `(string)`: 返回截断的字符串。

### 例子

```js
_.truncate('hi-diddly-ho there, neighborino');
// => 'hi-diddly-ho there, neighbo...'

_.truncate('hi-diddly-ho there, neighborino', {
    'length': 24,
    'separator': ' '
});
// => 'hi-diddly-ho there,...'

_.truncate('hi-diddly-ho there, neighborino', {
    'length': 24,
    'separator': /,? +/
});
// => 'hi-diddly-ho there...'

_.truncate('hi-diddly-ho there, neighborino', {
    'omission': ' [...]'
});
// => 'hi-diddly-ho there, neig [...]'
```

### 参考
- [https://lodash.com/docs/4.17.15#truncate](https://lodash.com/docs/4.17.15#truncate)

## unescape

```js
_.unescape([string=''])
```

`_.escape` 的反向版。这个方法转换 `string` 字符串中的 HTML 实体 `&`, `<`, `>`, `"`, `'`, 和 <code>`</code> 为对应的字符。

注意: 不会转换其他的 HTML 实体，需要转换可以使用类似 [he](https://mths.be/he) 的第三方库。

### 参数
- `[string=''] (string)`: 要转换的字符串。

### 返回
- `(string)`: 返回转换后的字符串。

### 例子

```js
_.unescape('fred, barney, &amp; pebbles');
// => 'fred, barney, & pebbles'
```

### 参考
- [https://lodash.com/docs/4.17.15#unescape](https://lodash.com/docs/4.17.15#unescape)


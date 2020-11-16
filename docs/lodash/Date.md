## now

```js
_.now()
```

获得 Unix 纪元 (`1 January 1970 00:00:00 UTC`) 直到现在的毫秒数。

### 返回
- `(number)`: 返回时间戳。

### 例子

```js
_.defer(function(stamp) {
  console.log(_.now() - stamp);
}, _.now());
// => Logs the number of milliseconds it took for the deferred invocation.
```

### 参考
- [https://lodash.com/docs/4.17.15#now](https://lodash.com/docs/4.17.15#now)

> 每天一题，坚持思考



实现indexOf函数，返回首次要查询的值在数组中的索引值。

**问题**

```js
indexOf([1, 4, 5], 5);  // 2
indexOf([4, 6, 8, 10], 10, 2) // 3
```



**具体实现**

```js
function indexOf(array, value, fromIndex) {
  if (Object.prototype.toString.call(array) !== "[object Array]") {
    return -1;
  }

  var length = array.length;
  if (length === 0) return -1;

  fromIndex = Number.parseInt(fromIndex);
  fromIndex = Number.isNaN(fromIndex) ? 0 : fromIndex;

  if (fromIndex < 0) {
    fromIndex = Math.max(length + fromIndex, 0);
  }

  var index = fromIndex - 1;

  while (++index < length) {
    if (array[index] === value) {
      return index;
    }
  }
  return -1;
}
```



**实现思路**

**参数：**

1. `array`（Array）：被查询的数组；
2. `value`（*）：需要查询的值；
3. `fromIndex` （Number）：查询的起始位置 ;

**步骤：**

1. 判断当前的`array`参数是否为数组，并且判断该数组的长度；

2. 对查询的起始位置值进行类型转换`fromIndex`，还要对改值进行`isNaN`的判断；如果当前值是负数，那么对`fromIndex`进行处理`fromIndex+数组长度`；
3. `while`进行遍历，查询数组中是否存在需要查询的值，如果有返回该索引值，否则返回-1；



如果读者发现有不妥或者可以改善的地方，欢迎在评论区指出。如果觉得写得不错或者对你有所帮助，可以点赞、评论、转发分享，谢谢~
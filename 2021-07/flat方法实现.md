> 每天一题，坚持思考



有时候数组里面的成员依然是数组，那么这个时候如果要对这个数组进行"压平"，变成一个一维数组，就是今天要实现的方法（flat）。

**问题**

```js
把数组：[1, [6, 7], [2, [3, [4]], 5]]
变成：[1, 6, 7, 2, 3, 4, 5]
```



**具体实现**

```js
function flattenArr(array, result) {
  let index = -1, // 索引值
      length = array.length; // 当前数组的长度

  result = result || [];

  while (++index < length) {
    let value = array[index];
    // 判断每一次数组的成员是否是数组
    if (Object.prototype.toString.call(value) === "[object Array]") {
      // 递归调用，把当前成员数组作为参数传入，还有result也一并传入
      flattenArr(value, result);
    } else {
      // 往新数组最后一位添加成员
      result[result.length] = value;
    }
  }
  return result;
}
```



**实现思路**

**参数：**

1. `array`（Array）：需要压平的数组；
2. `result`（Array）：记录每一次的数组成员；

该方法主要是实现思路，把每一递归"拍平"的结果都用`result`这个数组记录，再通过`while`实现数组的遍历，遍历过程中通过`Object.prototype.toString.call(value) === "[object Array]"`判断当前成员是否为数组，如果当前数组成员的类型是数组，那么就`递归`调用该方法，如果不是则把当前数组成员添加到`result`数组最末尾位置。



如果读者发现有不妥或者可以改善的地方，欢迎在评论区指出。如果觉得写得不错或者对你有所帮助，可以点赞、评论、转发分享，谢谢~
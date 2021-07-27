> 每天一题，坚持思考



今天要实现的是forEach函数，既可以遍历数组，也可以遍历对象，还有一个"小众"功能，改变函数内this的指向。

**问题**

```js
// 对象
forEach({a: 1, b: 2, c: 3}, function eachHandler(item, index, obj) {
       ...
}, null);
// 数组
forEach([1, 2, 3], function eachHandler(item, index, obj) {
       ...
}, null);
```



**具体实现**

```js
function forEach(obj, fn, context) {
  // 判断是null或者undefined
  if (obj === null || typeof obj === 'undefined') {
    return;
  }
	// 其他类型，则成为新数组里的成员
  if (typeof obj !== 'object') {
    obj = [obj];
  }
	// 判断是否是数组
  if (Object.prototype.toString.call(obj) === '[object Array]') {
    var index = -1,
        length = obj.length;
    // 利用while遍历
    while (++index < length) {
      fn.call(context, obj[index], index, obj);
    }
  } else {
    for (var key in obj) {
      // 借用对象上的hasOwnProperty，排除原型链上的属性
      if (Object.prototype.hasOwnProperty.call(obj, key)) {
        fn.call(context, obj[key], key, obj);
      }
    }
  }
}
```



**实现思路**

**参数：**

1. `obj`（Array | Object）：需要遍历的值；
2. `fn`（Function）：回调函数，参数(`当前遍历的值`,`键或者索引值`,`原数组或对象`)；
3. `context` : 上下文对象，也就是回调函数中的this绑定的值，默认就是`undefined`;

该方法主要是实现思路，主要通过判断是否为数组，通过`call`方法执行每次调用的函数`fn`。开始的判断用了`typeof obj`，用`typeof`判断是否为`undefined`，也可以避免`obj`是`undeclared`（未声明）出错的问题。其他非`object`类型（`string`，`boolean`，`number`）则添加到新的数组里。接下来分为对象和数组，数组用`while`遍历，最后用`call`方法绑定`fn`方法的`this`指向；对象使用`for...in`遍历，但这种遍历会遍历原型链上的属性，所以使用`hasOwnProperty`方法来判断当前属性是否属于当前对象而不是原型链，但这里为了防止当前对象上改写了`hasOwnPropery`属性，所以这里借用`Object`原型上`hasOwnProperty`方法进行判断。



如果读者发现有不妥或者可以改善的地方，欢迎在评论区指出。如果觉得写得不错或者对你有所帮助，可以点赞、评论、转发分享，谢谢~
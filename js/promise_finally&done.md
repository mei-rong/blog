#Promise: finally vs done
[Reference URL](https://blog.csdn.net/ixygj197875/article/details/79188199)

## done()
Promise 对象的回调链，无法捕捉then方法或catch方法抛出的内部（非全局）错误。done方法，处于回调链的尾端，可以抛出任何可能出现的错误。
```js
asyncFunc()
.then(f1)
.catch(r1)
.then(f2)
.done();
```
它的实现代码相当简单。
```js
Promise.prototype.done = function (onFulfilled, onRejected) {
    this.then(onFulfilled, onRejected)
    .catch(function (reason) {
        // 抛出一个全局错误
        setTimeout(() => { throw reason }, 0);
    });
};
```
从上面代码可见，done捕捉任何可能出现的错误，并向全局抛出。

## finally()
finally方法用于指定不管 Promise 对象最后状态如何，都会执行的操作。它与done方法的最大区别，它接受一个普通的回调函数作为参数，该函数不管怎样都必须执行。

它的实现也很简单。

```js
Promise.prototype.finally = function (callback) {
    let P = this.constructor;
    return this.then(
        value => P.resolve(callback()).then(() => value),
        reason => P.resolve(callback()).then(() => { throw reason })
    );
};
```
上面代码中，不管前面的 Promise 是fulfilled还是rejected，都会执行回调函数callback。
#### 突然想起要自己写一个函数实现forEach的功能，如有错误，求指正

> forEach的特点是，只循环数组中的元素，并且不能return

```javascript
Array.prototype.myForEach = function(callback) {
    for (var i = 0; i < this.length; i++) { //保证只循环数组元素
        callback(this[i], i, this); //return不能跳出循环
    }
}

var test = [1, 2, 3];
test.a = 'ailing';

test.myForEach(((item, index) => {
    console.log(item + 1);
    console.log(index);
}))
```

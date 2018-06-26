---
　　layout: default
　　title: Array构造的数组使用map函数失效
---


```javascript
var test = new Array(100)
var newArr = test.map((item, index)=>index);
newArr[0] // undefined
```

为什么上述的newArr[0]是Undefined而不是我们期待的下下标0呢？


- 数组在Js中其实也是一个对象，包含length属性,以及下标的值作为属性。利用Array来构造数组的时候，引擎只是给这个对象的Length属性赋值为100，并没有初始化这些下标的值，访问这个数组的下表得到的值是undefined并不是因为这些下标对应的值是undefined而是这些下标就不存在返回的这个默认值
- 并且如果数组下标不存在的话，其实map函数并没有真正的对每一个元素执行操作。因为只有当下标存在的时候，map的回调函数才会执行。
- 所以在对test数组用高阶函数map进行遍历的时候, index的值都为undefined，最后生成的数组newArr中所有的值都是undefined，是空的，在console控制台显示的是[empty * 100]

```javascript
//利用数组的展开运算符

var newArr = [...test].map((item, index)=>index)
newArr[0] // 0
```

利用展开运算符得到的结果如下，数组的下标产生了，只不过值是undefined

```javascript
{
  0: undefined,
  1: undefined,
  ...,
  100: undefined,
  length: 100
}
```
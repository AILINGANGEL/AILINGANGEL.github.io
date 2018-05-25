## 1.虚拟Dom
- vue会把单文件组件中的template或者用render函数写的都转换成虚拟dom
- 虚拟dom也是一个Js 对象

普通dom

```html
<div id="main">
   <p>文本内容<p>
</div>
```

虚拟dom是一个标准的js对象

```javascript
var vNode = {
   tag: 'div',
   attributes: {
       id: 'main'
   },
   children: [
   //p节点
   ]
}
```

## 2. vNode的类型

- TextVNode 文本节点
- ComponentVNode 组件节点
- ElementVNode 普通元素节点
- EmptyVNode 没有内容的注释节点
- CloneVNode 克隆节点，可以是以上任意类型的节点，唯一的区别在于isCloned属性为true

## 3. 为什么用render函数

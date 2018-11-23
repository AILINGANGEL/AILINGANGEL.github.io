---
　　layout: default
　　title:scoped对render不生效
---
```js
render(h){
   return h('div', {
   	class: ['current-row']
   })
}
```

```css
.current-row {
   background-color: red;
}
```

上述render函数是我写在表头中的,其中current-row这个css类对我渲染的div并不生效。查阅文档发现scoped css对动态生成的内容是不work的，虽然官网文档只提到了v-html这种动态生成内容的方式。但其实上述的render函数也是动态生成内容的一种。最后通过深度选择器解决了这个问题.

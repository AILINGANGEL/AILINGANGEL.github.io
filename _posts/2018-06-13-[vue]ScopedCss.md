---
　　layout: default
　　title: vue scoped css
---
背景:在项目中使用iview组件库中的表格组件的时候,表格里面有渲染链接,希望链接点击之后可以变成紫色，用来标识链接已经被访问过了。代码如下

```html
<template>
	<div>
		<Table :data="data" :columns="colums" class="my-table"></Table>
	</div>
</template>
<script>
	export default {
		data(){
			return {
				columns: [{
					title:'text',
					render: (h, params) => {
						return h('a', params.row.text);
					}
				}],
				data: [{text:'测试'}]
			}
		}
	}
</script>
<style scoped>
.my-table a:visited {
	red: purple;
}
</style>
```
###结果
上述代码并不能修改表格中链接的访问之后的样式

### 原因
`当<style>标签带有scoped属性时，css只能作用域当前组件中的元素.当使用scoped之后，父组件的样式将不会渗透到子组件中.`但是子组件的根节点会同时受到父组件的scoped css和子组件自己的scoped css影响, 这样可以让父组件从布局的角度出发，调整根元素的样式

### 解决方案

- 混用<style scoped>和<style>，但是这样做的缺点是,所有表格中的链接都会采用这个样式,但这可能并不是我们想要的.
- `深度作用选择器`



```css
<style scoped>
.my-table >>> a:visited {
	red:purple;
}
</style>
```

### 注意事项
- 当标签选择器和属性选择器一起作用的时候，会慢很多倍，所以在scoped css中尽量使用class 或者 id， 减少使用标签选择器的次数，或者尽量不用
- `动态生成的内容，比如通过v-html创建的dom也不会受到scoped css的影响`，同样可以采用深度作用选择器来解决这个问题.
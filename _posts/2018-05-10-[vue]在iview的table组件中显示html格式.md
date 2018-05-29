接到项目需求，需要用富文本编辑器设置一堆有格式的文本，然后在表格的列表页中展示这个格式。由于富文本编辑器显示的格式都是带html标签的字符串，在iview组件中要渲染文本
肯定不能把html标签页显示出来。总结一句话，其实这个就是考`如何用vue的render函数渲染html内容`,最开始的想法是v-html指令，但是尝试了说不能解析html指令，于是找到了另
一种方法，用`innerHtml属性`
```javascript
render: (h, params) => {
    return h('div', {
      domProps: {
        innerHTML: params.row.task_desc
      }
    })
  }
```

`
render函数中不存在指令！！！
`
---
　　layout: default
　　title: css box-sizing属性
---

经常看到很多地方都将css中box-sizing属性设置成border-box值，但都不知道什么意思。今天特意查看了一下，对box-sizing属性做一下总结.


### box-sizing用途

简单的数来该属性就是用来设置css盒子模型中的高度和宽度计算方式. box-sizing有如下几个值

* content-box(默认)
* border-box

### content-box

如果设置成content-box, 那么这个设置这个元素的width和height的值就是纯内容的值, 在页面上这个盒子展示的宽度将是 width + padding * 2 + border * 2

```html
<div class="box">
  box-sizing
</div>
```


```css
.box {
  width: 100px;
  height: 100px;
  background-color: pink;
  border: 10px solid black;
  padding: 5px;
}
```

如上，在界面上该div元素实际的大小是100 + 10 * 2 + 5 * 2 = 130

![content-box]({{ site.url }}/images/content-box.png)


### border-box

```css
.box {
  width: 100px;
  height: 100px;
  background-color: pink;
  border: 10px solid black;
  padding: 5px;
  box-sizing: border-box;
}
```

如上，如果设置成boder-box,那么整个元素的宽度就是100，内容区缩短为100 - 5 * 2 - 10*2 = 70

![border-box]({{ site.url }}/images/border-box.png)
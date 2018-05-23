## 行内元素的margin和padding属性
- 行内元素也有盒子模型
- 行内元素垂直方向上的设置，比如margin-top, margin-bottom, padding-top, padding-bottom的设置是无效的
- 行内元素水平方向上的设置, 比如margin-left, margin-right, padding-left, padding-right的设置是有效果的
- 行内元素的padding-top、padding-bottom从显示的效果上是增加的，但其实设置的是无效的。并不会对他周围的元素产生任何影响

```html
<html>
<<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        span{
            background-color: red;
            margin:10px;
            padding: 30px;
        }
    </style>
</head>
<body>
    <span>我是span</span>
    <div>我是div</div>
</body>
</html>
```


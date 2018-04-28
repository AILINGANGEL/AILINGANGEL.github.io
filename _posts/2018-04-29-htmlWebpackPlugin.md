最近在做代码重构的项目需要在单页面引用的html文件里定义一些该项目使用的常亮.定义常亮的时候我使用了const关键字，这是es6的语法，但是这个时候项目报错了，错误信息如下
```
html webpack plugin reference error APP is not defined
```
查了很久，可能跟html-webpack-plugin 这个插件的配置有关
最后使用raw-loader来解决了这个问题

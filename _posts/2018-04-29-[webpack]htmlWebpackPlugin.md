最近在做代码重构的项目需要在单页面引用的html文件里定义一些该项目使用的常量.定义常量的时候我使用了es6的模板字符串，但是这个时候项目报错了，错误信息如下
```javascript
const APP = 'wa';
const COOKIE_NAME = `${APP}_name`;
```
报错信息如下:

```
html webpack plugin reference error APP is not defined
```

查了很久，可能跟html-webpack-plugin 这个插件的配置有关, 当该插件解析index.html文档的时候,不能识别这个模板字符串里面的变量,
因此使用raw-loader来对html文件进行处理,以便变量能被识别.(我自己都觉得写的不清楚，因为官网的api显示raw-loader是用来处理诸如txt文件之类的)

```javascript
  new HtmlWebpackPlugin({
    // For details on `!!` see https://webpack.github.io/docs/loaders.html#loader-order
    template: '!!raw-loader!src/index.hbs'
  })
```

顺便简单说下Html-webpack-plugin, **webpack只是会帮忙生成依赖的关系图和最终的js文件,但是Html-webpack-plugin能帮住我们解析index.html文件，并把生成的js文件注入到这个html文件中**

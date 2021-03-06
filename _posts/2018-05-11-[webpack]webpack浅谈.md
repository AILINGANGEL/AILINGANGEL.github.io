
Webpack是前端资源模块化管理和打包工具。它可以将许多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源。还可以将按需加载的模块进行代码分隔，等到实际需要的时候再异步加载。

在webpack的世界里一个图片，一个css，甚至是一个字体都叫做一个模块，彼此之间存在一个依赖关系，webpack就是用来处理这些模块之间的关系，病对其进行打包，打包之后这些资源都变成了js。

webpack应用场景 `单页面应用`

es6的模块, export and import 

```javascript
var config = { version: 1.0 }
export { config };

export var config = { version: 1.0 }

export function add (a, b) { return a + b }

import { config } from './config.js';
import { add } from './add.js';

export default { version: 1.0 }
import config from './config.js';

//npm安装的模块也可以直接导入
import Vue from 'vue';

```

Webpack主要包括四个核心概念:
> - 入口entry
> - 输出output
> - loader
> - 插件(plugins)

## 1.入口
webpack会创建应用程序所依赖的关系图，图的起点被认为是入口,入口告诉webpack从哪里开始，并根据依赖关系图确定需要打包的内容.

```javascript
module.exports = {
  entry: './path/to/entry/file.js'
}
```

## 2.出口
webpack打包完成的文件会放在出口

```javascript
const path = resolve('path');
module.exports = {
  entry: './path/to/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'test.js'
  }
}

```
上述代码会在当前路径的dist目录下生成一个test.js文件

## 3.loader

webpack自身只理解javascript, 但是项目中会有很多非javascript的文件，比如图片，或者css文件.webpack会把每个文件都作为模块来进行处理,如何处理这些
非js的文件就需要loader来进行处理了.根据官网的描述loader主要有两个目标:
- 识别出应该被对应的loader进行转换的文件
- 转换这些文件，并把他们添加到依赖图中
- 在进行编译前，先对各个文件用对应的loader进行处理
- use如果是数组，那么编译顺序是从后往前的，比如对.css文件先用style-loader进行处理，再用css-loader进行处理

```javascript
  const path = resolve('path');
  module.exports = {
    entry: './path/to/entry/file.js',
    output: {
      path: path.resolve(__dirname, 'dist'),
      filename: 'test.js'
    },
    module: {
      rules: [{
        test: /\.txt$/, use: 'raw-loader',
      },{
        test: /\.css/, use: ['css-loader', 'style-loader']
      }]
    }
  }
```

> “嘿，webpack 编译器，当你碰到「在 require()/import 语句中被解析为 '.txt' 的路径」时，在你对它打包之前，先使用 raw-loader 转换一下。”


## 4.插件

插件可以帮助解决Loader不能解决的其他事情, loader仅在每个文件的基础上执行转换,而 **插件更常用于在打包模块的compilation 和 chunk生命周期执行操作和自定义功能** 
如果要使用插件，只需要require它，然后把它添加到plugins数组中

- extract-text-webpack-plugin: 把散落在各个地方的css提取出来，最终生成一个css静态文件，然后通过Link标签的形式导入

```javascript
const path = resolve('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = {
  entry: './path/to/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'test.js'
  },
  module: {
    rules: [{
      test: /\.txt$/, use: 'raw-loader'
    }]
  },
  plugins: [
    new HtmlWebpackPlugin({template: 'index.html'});
  ]
}
```

### 实战
安装 webpack 和 webpack-dev-server

webpack打包命令 `webpack --progress --hide-modules`

## 1.处理css

- "css-loader": "^0.28.11"
- "style-loader": "^0.21.0"
- "extract-text-webpack-plugin": "^2.1.2" 

## 1.单文件组件与vue-loader
需要的loader有:
- "babel": "^6.23.0",
- "babel-loader": "^7.1.4",
- "babel-plugin-transform-runtime": "^6.23.0",
- "babel-preset-es2015": "^6.24.1",
- "babel-runtime": "^6.26.0",

- "vue-hot-reload-api": "^2.3.0",
- "vue-loader": "^11.3.4",
- "vue-style-loader": "^4.1.0",
- "vue-template-compiler": "^2.5.16",

## 2.生产环境
- webpack-merge 把两个配置文件合并成一个
- html-webpack-plug 生成html模板的



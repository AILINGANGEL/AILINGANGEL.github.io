---
　　layout: default
　　title: 你好，世界
---
背景: 开发vue的Icon组件,集成开源图标库ionicons时,需要将开源库中的svg作为新的字体来源也就是@font-face规则中src属性中url函数中的路径值. 当拷贝到我的webpack项目下，url使用相对路径引用的svg或其他格式的文件时，始终报错用不能解析这个相对路径.

sass-loader可以使用传统的解析路径的方法来解析scss文件中的@import 引用路径问题,因此可以使用@import来引入各种相对路径的文件, 但是`sass-loader`不能解析css中使用url来引用相对路径的问题。官网说可以使用resolve-url-loader放到sass-loader之前来解决这个问题，由于我使用的是vue-cli3来配置的，很桑，不知道如何把这个loader房到sass-loader之前,所以果断弃用。因为webpack可以配置根路径的别名，通过vue inspect命令把配置输出来，查看文件发现src路径的别名是@,最后通过使用`url(~@styles/common/iconfont/font)`才发文件正确导入. ~告诉webpack这不是一个相对路径 @是项目根路径的别名.

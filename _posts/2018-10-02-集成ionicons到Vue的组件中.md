---
　　layout: default
　　title: 你好，世界
---

本文主要介绍如何集成第三方图标库到自己的组件中.

> 第三方图标库选用 [ionicons](https://ionicons.com/v2/)
> 框架采用vue


## 集成流程
### 1.下载文件
从ionicons的[官网](https://ionicons.com/v2/)下载文件
![download-ionicons]({{ site.url }}/images/ionicons-1.png)


### 2.将文件放到项目的样式目录下
如果使用了第三方的构建工具，注意其中引用文件的路径问题，参见上一偏[博文](https://ailingangel.github.io/2018/10/01/webpack%E4%B8%ADscss%E4%BD%BF%E7%94%A8url%E5%BC%95%E7%94%A8%E8%B7%AF%E5%BE%84%E9%97%AE%E9%A2%98.html)

![import-ionicons]({{ site.url }}/images/ionicons-2.png)


### 3.使用
下载下来的文件已经定义好了各个css的类名，只需要在组件中使用
`<li class="xxx"></li>`方式来给li元素添加上各个图标对应的类名

## 原理
集成上述开源图标库的原理利用了webfont技术.概括来说就是提前定义好图标的unicode编码，然后通过伪元素before的css属性content来引用这些unicode编码，从而展示各个图标。

### 1.font-face
在网页上的字体一般来说用户只能使用系统中存在的字体，但是通过@font-face规则，网页开发者可以让用户使用除了自己电脑上的其他的字体。将要使用的特殊字体放到服务器上，然后下载到自己的电脑上. 然后定义一个类，其中的字体类型就是我们自己定义的这个字体.

![font-ionicons]({{ site.url }}/images/ionicons-3.png)

*集成ionicon的关键一步就是在@font-face规则中把这些图标文件作为字体的原文件.*


### 2.图标进行unicode编码
unicode编码中存在一段范围的值，用户可以自定义这些值的含义,在下载下来的svg文件中已经对各个图标定义了相应的Unicode编码

![unicode-ionicons]({{ site.url }}/images/ionicons-4.png)


### 3.利用伪元素before的content属性展示相应的图标


## 总结
利用@font-face规则来集成图标的好处就是可以像控制字体一样设置这些图标的样式,比如font-size, color , font-weight属性等等

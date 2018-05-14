开发移动版的应用通常需要编写如下的代码:

```html
<meta name="viewport" content="width=device-width,initial-scale=1,minimum-scale=1,maximum-scale=1,user-scalable=no,minimal-ui">
```
手机浏览器把页面放在一个虚拟的窗口中,一般情况下这个虚拟的窗口比屏幕宽，这样就不用把每个网页挤到很小的窗口中（破坏布局），用户可以通过平移和缩放来看网页的不同部分,
viewport属性实现了让开发者来控制viewport的大小和缩放，所有的手机浏览器都支持.


- width：控制 viewport 的大小，可以指定的一个值，如果 600，或者特殊的值，如 device-width 为设备的宽度（单位为缩放为 100% 时的 CSS 的像素）。
- height：和 width 相对应，指定高度。
- initial-scale：初始缩放比例，也即是当页面第一次 load 的时候缩放比例。
- maximum-scale：允许用户缩放到的最大比例。
- minimum-scale：允许用户缩放到的最小比例。
- user-scalable：用户是否可以手动缩放
- minimal-ui: Safari中为meta标签新增minimal-ui属性，让网页在加载时便可隐藏顶部的地址栏与底部的导航栏。[参考这里](https://36kr.com/p/210516.html)

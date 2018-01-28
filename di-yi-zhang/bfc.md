## BFC（Block Formatting Contexts）块级格式化上下文（边距重叠解决方案）

概念：块格式化上下文（block formatting context） 是页面上的一个独立的渲染区域，容器里面的子元素不会在布局上影响到外面的元素。它是决定块盒子的布局及浮动元素相互影响的一个因素。

BFC布局规则如下(注意BFC只影响块儿级盒)：
* 内部Box按垂直方向一个接一个的放置
* Box垂直方向的距离由margin值决定，并且属于同一个BFC的两个相邻的box的margin值会重叠
* 每个元素的 margin-box 的左边与包含块儿 border-box 的左边相接触
* BFC的区域不会与浮动盒子重叠
* BFC就是一个隔绝的容器，容器里面的子元素不影响外面元素的布局，反之亦然
* 计算BFC的高度时，浮动元素也参与计算

以下情况，将会触发BFC：
* 根元素，即 <html>
* float 属性值不为 none
* position 属性的值为 absolute 或 fixed
* overflow 属性值不为 visible
* display 属性值为 inline-block, table-cell, table-caption


### IE haslayout
IE 是个奇葩，自己搞一个叫做 haslayout 的东西，类似 BFC，一般在 IE 中显示有问题的东西都可以通过触发 haslayout 来解决，触发方法有很多：
* zoom 属性设置为除 normal 以外的值
* width/height 除 auto 以外的值
* float 除 none 以外的值

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

BFC的应用
* 自适应两栏布局
  * 利用的是 BFC 不与浮动元素重叠的特性
* 清楚浮动
  * 利用BFC内浮动元素也参与BFC高度计算的特性
* 解决margin折叠(传递)
  * 子元素的margin-top传递到父级
* 防止margin重叠
  * 因为BFC内相邻元素的margin值会重叠，如果给其中一个元素包一层，并设置为BFC，又因为BFC内子元素的布局与外部元素互不影响的特性，就可以解决重叠的问题

扩展：
**IFC**(Inline Formatting Contexts)直译为"内联格式化上下文"，IFC的line box（线框）高度由其包含行内元素中最高的实际高度计算而来（不受到竖直方向的padding/margin影响)

**GFC**(GridLayout Formatting Contexts)直译为"网格布局格式化上下文"，当为一个元素设置display值为grid的时候，此元素将会获得一个独立的渲染区域，我们可以通过在网格容器（grid container）上定义网格定义行（grid definition rows）和网格定义列（grid definition columns）属性各在网格项目（grid item）上定义网格行（grid row）和网格列（grid columns）为每一个网格项目（grid item）定义位置和空间。

**FFC**(Flex Formatting Contexts)直译为"自适应格式化上下文"，display值为flex或者inline-flex的元素将会生成自适应容器（flex container），可惜这个牛逼的属性只有谷歌和火狐支持，不过在移动端也足够了，至少safari和chrome还是OK的，毕竟这俩在移动端才是王道。

### IE haslayout
IE 是个奇葩，自己搞一个叫做 haslayout 的东西，类似 BFC，一般在 IE 中显示有问题的东西都可以通过触发 haslayout 来解决，触发方法有很多：
* zoom 属性设置为除 normal 以外的值
* width/height 除 auto 以外的值
* float 除 none 以外的值

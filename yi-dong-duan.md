#### 说说你知道的移动端web的兼容性bug

1、一些情况下对非可点击元素如(label,span)监听click事件，ios下不会触发，css增加cursor:pointer就搞定了。

2.position 在Safari下的两个定位需要都写，只写一个容易发生错乱

3.Input 的placeholder会出现文本位置偏上的情况

input 的placeholder会出现文本位置偏上的情况：PC端设置line-height等于height能够对齐，而移动端仍然是偏上，解决是设置line-height：normal

4.zepto点击穿透问题

引入fastclick解决；event.preventDefault

5.当输入框在最底部的时候，弹起的虚拟键盘会把输入框挡住。
```
Element.scrollIntoViewIfNeeded(opt_center)
```
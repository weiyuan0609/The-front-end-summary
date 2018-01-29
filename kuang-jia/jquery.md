参考：
http://blog.csdn.net/SUFEIDEYEYE/article/details/51810912 

#### body中的onload()函数和jQuery中的document.ready()有什么区别？
1、我们可以在页面中使用多个document.ready()，但只能使用一次onload()。
2、document.ready()函数在页面DOM元素加载完以后就会被调用，而onload()函数则要在所有的关联资源（包括图像、音频）加载完毕后才会调用。

#### query有哪些好处？
轻量级的框架，大小不到30kb,强大的选择器，出色的DOM封装，可靠的事件处理机制，完善的Ajax，出色的浏览器兼容，支持链式操作，隐式迭代，行为层与结构层分离，丰富的插件机制，文档完善且开源的。
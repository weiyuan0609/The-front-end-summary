参考：
http://blog.csdn.net/SUFEIDEYEYE/article/details/51810912 
https://www.cnblogs.com/changyangzhe/p/5762061.html

#### body中的onload()函数和jQuery中的document.ready()有什么区别？
1、我们可以在页面中使用多个document.ready()，但只能使用一次onload()。
2、document.ready()函数在页面DOM元素加载完以后就会被调用，而onload()函数则要在所有的关联资源（包括图像、音频）加载完毕后才会调用。

#### jquery有哪些好处？
轻量级的框架，大小不到50kb,强大的选择器，出色的DOM封装，可靠的事件处理机制，完善的Ajax，出色的浏览器兼容，支持链式操作，隐式迭代，行为层与结构层分离，丰富的插件机制，文档完善且开源的。

#### 在jquery中你有没有编写过插件，插件有什么好处？你编写过那些插件？它应该注意那些？
答: 插件的好处：对已有的一系列方法或函数的封装，以便在其他地方重新利用，方便后期维护和提高开发效率
插件的分类：封装对象方法插件 、封装全局函数插件、选择器插件
注意的地方：
1.插件的文件名推荐命名为jquery.[插件名].js，以免和其他的javaScript库插件混淆
2.所有的对象方法都应当附加到jQuery.fn对象上，而所有的全局函数都应当附加到jQuery对象本身上
3.插件应该返回一个jQuery对象，以保证插件的可链式操作
4.避免在插件内部使用$作为jQuery对象的别名,而应使用完整的jQuery来表示，这样可以避免冲突或使用闭包来避免
5.所有的方法或函数插件，都应当一分好结尾，否则压缩的时候可能出现问题。在插件头部加上分号，这样可以避免他人的不规范代码给插件带来影响
6.在插件中通过$.extent({})封装全局函数,选择器插件，扩展已有的object对象通过$.fn.extend({})封装对象方法插件

#### jquery性能优化
参考： http://caibaojian.com/jquery-performance-optimization.html

#### jQuery UI 与 jquery 的主要区别是： 　
(1) jQuery是一个js库，主要提供的功能是选择器，属性修改和事件绑定等等。 　
(2) jQuery UI则是在jQuery的基础上，利用jQuery的扩展性，设计的插件。提供了一些常用的界面元素，诸如对话框、拖动行为、改变大小行为等等。 　
(3) jQuery本身注重于后台，没有漂亮的界面，而jQuery UI则补充了前者的不足，他提供了华丽的展示界面，使人更容易接受。既有强大的后台，又有华丽的前台。jQuery UI是jQuery插件，只不过专指由jQuery官方维护的UI方向的插件。
#### DOM事件的级别

 * DOM0 element.onclick=function(){}
 * DOM2 element.addEventListener('click', function(){}, false)(false是冒泡，true是捕获)
 * DOM3 element.addEventListener('keyup', function(){}, false)(DOM3级事件模块在DOM2级事件的基础上重新定义了一些事件，也添加了一些新事件，如下。包括IE9在内的主流浏览器都支持DOM2级事件，IE9也支持DOM3级事件。)
   * UI事件，当用户与页面上的元素交互时触发；
   * 焦点事件，当元素获得或者失去焦点时触发；
   * 鼠标事件，当用户通过鼠标在页面上执行操作时触发；
   * 滚轮事件，当使用鼠标滚轮（或类似设备）时触发；
   * 文本事件，当在文档中，输入文本时触发；
   * 键盘事件，当用户通过键盘在页面上执行操作时触发；
   * 合成事件，当为IME（Input Method Editor，输入法编辑器）输入字符时触发；
   * 变动事件，当底层Dom结构发生变化时触发
 
 DOM1存在，但是没有关于DOM事件相关的定义。
 
#### DOM事件流和事件模型（冒泡和捕获） 
##### 事件流
页面中接收事件的顺序。分为三个阶段：事件捕获阶段、处于目标阶段、事件冒泡阶段

##### 事件冒泡
事件首先由嵌套层次最深的节点接收，然后沿DOM树依次逐级向父代节点传播。

##### 事件捕获
不太具体的节点(或嵌套层次最浅的节点，通常是document)应该最先接收事件，然后沿DOM树依次向子代节点传递直到一个具体的子节点

DOM事件捕获的流程：window->document->html->body->....->目标元素

#### 绑定事件

##### 标准方法

###### el.addEventListener(eventName, handle, useCapture)

* 描述：给DOM元素添加指定的事件处理函数

* 参数：
    * `{String} eventName` 事件名称
    * `{Function} handle` 事件函数
    * `{Boolean} useCapture` 是否在事件捕获阶段触发事件，true 代表捕获阶段触发，false 代表在冒泡阶段触发

###### el.removeEventListener(eventName, handle)

* 描述：移除通过 addEventListener 添加的事件处理函数

* 参数：
    * `{String} eventName` 事件名称
    * `{Function} handle` 事件函数
    
<p class="tip">
如果要移除一个通过 addEventListener 添加的事件处理函数，那么给 removeEventListener 传递的两个参数必须与 addEventListener 的前两个参数完全相同。这意味着，给一个元素绑定匿名事件处理函数将无法被移除
</p>

##### IE8及以下

addEventListener 和 removeEventListener 在IE8及以下不被支持

###### el.attachEvent(eventName, handle)

* 描述：给DOM元素添加指定的事件处理函数

* 参数：
    * `{String} eventName` 事件名称
    * `{Function} handle` 事件函数

###### el.detachEvent(eventName, handle)

* 描述：移除通过 addEventListener 添加的事件处理函数

* 参数：
    * `{String} eventName` 事件名称
    * `{Function} handle` 事件函数
    
##### 对比
attachEvent/detachEvent 与 addEventListener/removeEventListener 的区别：
* 由于IE8不支持事件捕获，所以通过 attachEvent/detachEvent 绑定的时间也只能在冒泡阶段触发
* 通过 attachEvent/detachEvent 绑定的事件函数会在全局作用域中运行，即： this === window
* 通过 attachEvent/detachEvent 绑定的事件函数以绑定时的先后顺序倒序被执行
* attachEvent/detachEvent 的第一个参数要在事件名称前面加 'on'
 
#### Event对象的常见应用
* event.target 获取触发事件的元素
* event.currentTarget 事件所绑定到的元素
* event.bubbles 事件是否冒泡
* event.cancelable 事件是否可以取消事件默认行为
* event.preventDefault() 阻止默认行为，例如a链接(只有 event.cancelable 属性为 true 的事件，才能够通过 preventDefault() 方法取消默认行为)







 
#### DOM事件的级别

 * DOM0 element.onclick=function(){}
 * DOM2 element.addEventListener('click', function(){}, false)(false是冒泡，true是捕获)
 * DOM3 element.addEventListener('keyup', function(){}, false)(DOM3级事件模块在DOM2级事件的基础上重新定义了下方事件，也添加了一些新事件。包括IE9在内的主流浏览器都支持DOM2级事件，IE9也支持DOM3级事件。)
   * UI事件，当用户与页面上的元素交互时触发；
   * 焦点事件，当元素获得或者失去焦点时触发；
   * 鼠标事件，当用户通过鼠标在页面上执行操作时触发；
   * 滚轮事件，当使用鼠标滚轮（或类似设备）时触发；
   * 文本事件，当在文档中，输入文本时触发；
   * 键盘事件，当用户通过键盘在页面上执行操作时触发；
   * 合成事件，当为IME（Input Method Editor，输入法编辑器）输入字符时触发；
   * 变动事件，当底层Dom结构发生变化时触发
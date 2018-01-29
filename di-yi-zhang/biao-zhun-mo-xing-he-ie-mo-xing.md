#### 标准模型和IE模型
区别：IE模型高度和宽度计算了border和padding，而标准模型没有

box-sizing属性主要用来控制元素盒模型的解析模式，默认是content-box

content-box(标准模式)
border-box(IE模式)

Js设置和获取盒模型的宽和高的方式：

1. element.style.width/height
2. element.currentStyle.width/height(只有IE支持)
3. window.getComputedStyle(element).getPropertyValue(width/height)
4. element.getBoundingClientRect().width/height
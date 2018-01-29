JS基础知识： ECMA-262标准
JS-web-api: w3c标准（没有规定任何JS基础相关的东西只管定义用于浏览器中JS操作页面的API和全局变量）

[js核心内容参考博客](http://www.cnblogs.com/wangfupeng1988/p/3977924.html)

#### js使用typeof能得到哪些类型
值类型和引用类型，即
undefined
string
number
boolean
object({},[],null)
function

#### 强制类型转换发生的场景
1. 字符串拼接 例如：100+ ‘10’
2. ==运算符
3. if语句
4. 逻辑运算 && ||。。。

#### 何时使用==和===
jquery源码中推荐的写法：
当判断obj.a ==null（相当于obj.a===null||obj.a===undefined）
除这个以外其他都用===
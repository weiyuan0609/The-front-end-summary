#### this的几种不同的使用场景
1. 作为构造函数执行
2. 作为对象属性执行
3. 作为普通函数执行
4. call apply bind

#### 闭包
闭包实际应用中主要用于封装变量，收敛权限
使用场景：
1. 函数作为返回值
2. 函数作为参数传递
参考： [https://segmentfault.com/a/1190000000652891](https://segmentfault.com/a/1190000000652891)

#### call apply bind 区别
参考答案：三者都可以把一个函数应用到其他对象上，call、apply是修改函数的作用域（修改this指向），并且立即执行，而bind是返回了一个新的函数，不是立即执行．apply和call的区别是apply接受数组作为参数，而call是接受逗号分隔的无限多个参数列表，如果该方法是非严格模式代码中的函数，则null和undefined将替换为全局对象，并且原始值将被包装。当你调用apply传递给它null时，就像是调用函数而不提供任何对象

#### 作用域链
作用域链的作用是保证执行环境里有权访问的变量和函数是有序的，作用域链的变量只能向上访问，变量访问到window对象即被终止，作用域链向下访问变量是不被允许的。
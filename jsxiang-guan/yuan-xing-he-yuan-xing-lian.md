#### 创建对象的几种方式
1. 字面量

    var o1 = {name: 'o1'}
    var 02 = new Object({name:'o2'})
    
2. 构造函数
    
    var M = function(){this.name='03'}
    var o3 = new M()

3. Object.create()

    var o4 = Object.create({name:'o4'})
    
#### instanceof的原理
判断实力对象的\_\_proto__与构造函数的prototype是否引用同一个地址。

#### new 运算符
1、创建一个空对象，并且this变量引用该对象，同时继承了该函数的原型（实例对象通过\_\_proto\_\_属性指向原型对象；obj.\_\_proto__ = Base.prototype;）
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
2、属性和方法被加入到 this 引用的对象中。

#### 原型链
当从一个对象那里调取属性或方法时，如果该对象自身不存在这样的属性或方法，就会去自己关联的prototype对象那里寻找，如果prototype没有，就会去prototype关联的前辈prototype那里寻找，如果再没有则继续查找Prototype.Prototype引用的对象，依次类推，直到Prototype.….Prototype为undefined（Object的Prototype就是undefined）从而形成了所谓的“原型链”。
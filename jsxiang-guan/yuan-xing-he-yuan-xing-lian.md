#### 创建对象的几种方式
1. 字面量

    var o1 = {name: 'o1'}
    var 02 = new Object({name:'o2'})
    
2. 构造函数
    
    var M = function(){this.name='03'}
    var o3 = new M()

3. Object.create()

    var o4 = Object.create({name:'o4'})
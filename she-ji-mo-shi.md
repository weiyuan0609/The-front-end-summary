#### 设计模式（23种）(如何实现,应用,优缺点)

1. 单例模式
定义: 产生一个类的唯一实例
实现: 
        
        const createMask = ()=>{
          let mask = null;
          return ()=> mask || document.appendChild(document.createElement('div'))
        }
        
        const mask = createMask();
      
优点:
    * 提供了对唯一实例的受控访问
    * 避免对共享资源的多重占用
    * 节约系统资源

缺点:
    * 扩展性差
    * 职责过重


2. 工厂模式

定义: 创建对象时无须指定创建对象的具体灯
实现:
```   
        const Example = function(name,age){
          this.name = name || 'Tom',
          this.age = age || '18'
          this.say = function(){
              console.log(`name:${this.name},age:${this.age}`)
          }
        }
```
优点:
    * 结构清淅,有效的封装变化 
    * 对调用者屏蔽具体实现， 调用者只需关心产品的接口
    * 降低耦合度

缺点:
    * 添加新的类，需要改写工厂类


3. 发布订阅模式

定义: 定义对象间一种一对多的依赖关系，使得当每一个对象改变状态，则所有依赖于它的对象都会得到通知并自动更新。
实现: 

      const Example = {};
      Example.clientList = [];
      Example.listen = function(fn){
          this.clientList.push(fn)
      }
      Example.trigger = function(){
          for(let i=0,fn; fn=this.clientList[i++]){
              fn.apply(this,arguments)
          }
      }    
      Example.listen(function(message){
          console.log(message) // 我发布了一个消息，此时订阅者会收到消息
      })  
    
      Example.trigger(function(){
          console.log('我发布了一个消息，此时订阅者会收到消息')
      })
优点:
    * 时间上的解藕 
    * 对象之间的解藕
    * 支持广播通信


缺点:
    * 如果一个观察目标对象有很多直接和间接的观察者的话，将所有的观察者都通知到会花费很多时间
    * 如果在观察者和观察目标之间有循环依赖的话，观察目标会触发它们之间进行循环调用，可能导致系统崩溃
    * 观察者模式没有相应的机制让观察者知道所观察的目标对象是怎么发生变化的，而仅仅只是知道观察目标发生了变化
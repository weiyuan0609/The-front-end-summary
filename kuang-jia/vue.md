参考：
http://hcysun.me/2017/03/03/Vue%E6%BA%90%E7%A0%81%E5%AD%A6%E4%B9%A0/ 

#### vue-双向绑定底层实现原理
vue.js 采用数据劫持的方式，结合发布者-订阅者模式，通过`Object.defineProperty()`来劫持各个属性的setter，getter以监听属性的变动，在数据变动时发布消息给订阅者，触发相应的监听回调

参考： https://github.com/hawx1993/tech-blog/issues/11
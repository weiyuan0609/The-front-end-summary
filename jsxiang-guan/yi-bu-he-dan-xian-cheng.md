#### 异步场景
1. 定时任务： setTimeout steInterval
2. 网络请求 ajax请求，动态img加载
3. 事件绑定

#### 异步加载方式
1. 动态脚本添加
2. defer
3. async

async 和 defer区别：
1. defer是在HTML解析后才执行，如果是多个，按照加载顺序依次执行
2. async是在加载完之后立即执行，如果是多个，执行顺序和加载顺序无关

#### 异步流程控制
1. callback
2. Promise
3. Stream
4. Generator
5. async function
6. Rxjs

es5异步编程模型：
* 回调函数（callback）陷入回调地狱，解耦程度特别低
* 事件监听（Listener）JS 和浏览器提供的原生方法基本都是基于事件触发机制的
* 发布/订阅（观察者模式）把事件全部交给控制器管理，可以完全掌握事件被订阅的次数，以及订阅者的信息，管理起来特别方便。
* Promise 对象实现方式
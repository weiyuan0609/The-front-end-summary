#### 异步场景
1. 定时任务： setTimeout steInterval
2. 网络请求 ajax请求，动态img加载
3. 事件绑定

#### 异步流程控制
1. callback
2. Promise
3. Stream
4. Generator（可以把它理解成一个函数的内部状态的遍历器，Generator重点在解决异步回调金字塔问题，巧妙的使用它可以写出看起来同步的代码。）
5. **async function**(async...await写法最简洁，最符合语义。async/await让异步代码看起来、表现起来更像同步代码，这正是其威力所在。async 函数就是 Generator 函数的语法糖，只不过async内置了自动执行器。async 函数就是将 Generator 函数的星号（*）替换成 async，将 yield 替换成 await)
6. Rxjs

es5异步编程模型：
* 回调函数（callback）陷入回调地狱，解耦程度特别低
* 事件监听（Listener）JS 和浏览器提供的原生方法基本都是基于事件触发机制的
* 发布/订阅（观察者模式）把事件全部交给控制器管理，可以完全掌握事件被订阅的次数，以及订阅者的信息，管理起来特别方便。
* Promise 对象实现方式

async 好处：
1）Generator 函数必须靠执行器，所以才有CO函数库，async函数自带执行器
2）更好的语义
3）更广的适用性。co函数库yield后面只能是Thunk函数或者Promise对象，await后面可以跟Promise对象和原始类型值（等同于同步操作）

co函数库：
* co可以说是给generator增加了promise实现。co是利用Generator的方式实现了async/await（co返回Promise对象，async也返回Promise对象，co内部的generator函数即async，yield相当于await）
* co 函数库其实就是将两种自动执行器（Thunk 函数和 Promise 对象），包装成一个库。
* co函数接收一个Generator生成器函数作为参数。执行co函数的时候，生成器函数内部的逻辑像async函数调用时一样被执行。不同之处只是这里的await变成了yield（产出）。
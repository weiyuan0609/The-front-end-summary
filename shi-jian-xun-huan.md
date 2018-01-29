#### 事件循环

浏览器中, js引擎线程会循环从 任务队列 中读取事件并且执行, 这种运行机制称作 Event Loop \(事件循环\).

每个浏览器环境，至多有一个event loop。  
一个event loop可以有1个或多个task queue\(任务队列\)

先执行同步的代码，然后js会跑去消息队列中执行异步的代码，异步完成后，再轮到回调函数，然后是去下个事件循环中执行setTimeout

它从script\(整体代码\)开始第一次循环。之后全局上下文进入函数调用栈。直到调用栈清空\(只剩全局\)，然后执行所有的micro-task。当所有可执行的micro-task执行完毕之后。循环再次从macro-task开始，找到其中一个任务队列执行完毕，然后再执行所有的micro-task，这样一直循环下去。

从规范上来讲，setTimeout有一个4ms的最短时间，也就是说不管你设定多少，反正最少都要间隔4ms才运行里面的回调。而Promise的异步没有这个问题。Promise所在的那个异步队列优先级要高一些  
Promise是异步的，是指他的then\(\)和catch\(\)方法，Promise本身还是同步的  
Promise的任务会在当前事件循环末尾中执行，而setTimeout中的任务是在下一次事件循环执行

```javascript
//依次输出 12354
setTimeout(function(){
  console.log(4)
  },0);
new Promise(function(resolve){
  console.log(1)
  for( var i=0 ; i<10000 ; i++ ){
    i===9999 && resolve()
  }
  console.log(2)
}).then(function(){
  console.log(5)
});
console.log(3);
```






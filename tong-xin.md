https://segmentfault.com/a/1190000000652891]#### 什么是同源策略及限制
协议，域名，端口三者构成源

同源策略限制从一个源加载的文档式脚本如何与来自另一个源的资源进行交互，这是一个用于隔离潜在恶意文件的关键的安全机制
* cookie， localStorage和IndexDB无法读取
* DOM无法获得
* Ajax请求不能发送

#### 前后端如何通讯
1. Ajax（参考：https://segmentfault.com/a/1190000006669043
2. websocket(不受同源策略影响)(参考：http://www.ruanyifeng.com/blog/2017/05/websocket.html)
3. CORS(参考：http://www.ruanyifeng.com/blog/2016/04/cors.html)

#### AJax请求和原理（IE低版本ActiveXObjext）

    var xhr = new XMLHTTPRequest()
    // 请求method 和url
    xhr.open(‘GET’, URL)
    // 请求内容
    xhr.send()
    // 响应状态
    xhr.status
    // xhr的事件响应
    xhr.onreadystatuschange=function(){}
    xhr.readyState
    // 响应内容
    xhr.responseText
    
工作原理：Ajax的工作原理相当于在用户和服务器之间加了—个中间层(AJAX引擎),使用户操作与服务器响应异步化。　Ajax的原理简单来说通过XmlHttpRequest对象来向服务器发异步请求，从服务器获得数据，然后用javascript来操作DOM而更新页面。

优点：无刷新更新数据,异步与服务器通信,前后端负载均衡
缺点： 
1）ajax干掉了Back和history功能，对浏览器机制的破坏
2）对搜索引擎支持较弱
3）违背了URI和资源定位的初衷

#### fetch 和ajax区别
* XMLHTTPRequest是一个设计粗糙的 API，不符合关注分离（Separation of Concerns）的原则，配置和调用方式非常混乱，而且基于事件的异步模型写起来也没有现代的 Promise，generator/yield，async/await友好
* fetch 是浏览器提供的一个新的 web API，它用来代替 Ajax（XMLHttpRequest），其提供了更优雅的接口，更灵活强大的功能。
Fetch 优点主要有：
  * 语法简洁，更加语义化
  * 基于标准 Promise 实现，支持 async/await

    fetch(url).then(response=>response.json())
        .then(data=>console.log(data))
        .catch(e=>console.log('error',e))
        
        
#### websoket
WebSocket 使用ws或wss协议，Websocket是一个持久化的协议，相对于HTTP这种非持久的协议来说。WebSocket API最伟大之处在于服务器和客户端可以在给定的时间范围内的任意时刻，相互推送信息。WebSocket并不限于以Ajax(或XHR)方式通信，因为Ajax技术需要客户端发起请求，而WebSocket服务器和客户端可以彼此相互推送信息；XHR受到域的限制，而WebSocket允许跨域通信。
```
// 创建一个Socket实例
var socket = new WebSocket('ws://localhost:8080');
// 打开Socket
socket.onopen = function(event) {
  // 发送一个初始化消息
  socket.send('I am the client and I\'m listening!');
  // 监听消息
  socket.onmessage = function(event) {
    console.log('Client received a message',event);
  };
  // 监听Socket的关闭
  socket.onclose = function(event) {
    console.log('Client notified socket has closed',event);
  };
  // 关闭Socket....
  //socket.close()
};
```

#### 跨域通信的几种方式
1. JSONP
2. Hash 
3. postMessage
4. webSocket
5. cors（origin fetch）

#### JSONP
* 原理：JSONP 的原理是利用 `<script> `标签的 src 属性加载资源不受同源策略影响，其本质是向服务端请求一段 js 代码。
* 实现：
  
    let scriptTag = document.createElement('script')
    // 其中cb是回调函数参数的名字，cbname是回调函数的名字，这两个名字要与服务端沟通定义
    scriptTag.src = 'http://baidu.com/xxx?cb=cbname'
    document.body.appendChild(scriptTag)
* 优点
1. 可跨域
2. 兼容性好，基本全部兼容
* 缺点
1. 只支持 GET 请求
2. 确定JSONP请求是否失败并不容易，一般根据超时时间来判断

#### hash和postMessage
    // 利用hash，场景是当前页面 A 通过iframe或frame嵌入了跨域的页面 B
      // 在A中伪代码如下：
      var B = document.getElementsByTagName('iframe');
      B.src = B.src + '#' + 'data';
      // 在B中的伪代码如下
      window.onhashchange = function () {
          var data = window.location.hash;
      };

      // postMessage
      // 窗口A(http:A.com)向跨域的窗口B(http:B.com)发送信息
      Bwindow.postMessage('data', 'http://B.com');
      // 在窗口B中监听
      Awindow.addEventListener('message', function (event) {
          console.log(event.origin);
          console.log(event.source);
          console.log(event.data);
      }, false);
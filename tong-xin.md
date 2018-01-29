#### 什么是同源策略及限制
协议，域名，端口三者构成源

同源策略限制从一个源加载的文档式脚本如何与来自另一个源的资源进行交互，这是一个用于隔离潜在恶意文件的关键的安全机制
* cookie， localStorage和IndexDB无法读取
* DOM无法获得
* Ajax请求不能发送

#### 前后端如何通讯
1. Ajax
2. websocket(不受同源策略影响)
3. CORS

#### AJax请求和原理（IE低版本ActiveXObjext）

    var xhr = new XMLHTTPRequest()
    // 请求method 和url
    xhr.open(‘GET’, URL)
    // 请求内容
    xhr.send()
    // 响应状态
    xhr.status
    // xhr的事件响应
    xhr.onreadystatusrchange=function(){}
    xhr.readyState
    // 响应内容
    xhr.responseText
    
工作原理：Ajax的工作原理相当于在用户和服务器之间加了—个中间层(AJAX引擎),使用户操作与服务器响应异步化。　Ajax的原理简单来说通过XmlHttpRequest对象来向服务器发异步请求，从服务器获得数据，然后用javascript来操作DOM而更新页面。

优点：无刷新更新数据,异步与服务器通信,前后端负载均衡
缺点： 
1）ajax干掉了Back和history功能，对浏览器机制的破坏
2）对搜索引擎支持较弱
3）违背了URI和资源定位的初衷
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

#### AJax请求和原理

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
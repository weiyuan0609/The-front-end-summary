#### 前端错误分类
1. 即时运行错误：代码错误
2. 资源加载错误

#### 错误的捕获方式
代码错误捕获：
1. try...catch
2. window.onerror
资源加载错误捕获：
1. object.onerror
2. performance.getEntrice()
3. error事件捕获
    window.addEventListener('error',function(e){console.log('捕获',e)},true)

注意：跨域的js运行错误可以捕获，
1. 在script标签增加crossorigin属性（客户端）
2. 设置js资源响应头Access-control-allow-origin:* (服务器)


#### HTTP协议的主要特点
简单快速，灵活，无连接，无状态

#### HTTP报文的组成部分
* 请求报文：请求行（HTTP方法，页面地址，HTTP协议，版本），请求头（key-value值），空行（告诉服务器下一个是请求体），请求体
* 响应报文：状态码，响应头，空行，响应体

请求头：
1. Accept
2. Cache-control
3. HOST
4. User-agent
5. Accenp-Lanuage

响应头：
1. Cache-Control:max-age  避免了服务端和客户端时间不一致的问题。
2. content-type
3. Date
4. Expires
5. Last-Modified   标记此文件在服务期端最后被修改的时间

#### HTTP方法
GET, POST, PUT, DELETE, HEAD

#### POST和GET的区别


#### HTTP状态码

#### 什么是持久连接（keep-Alive模式，1.1版本才支持，1.0不支持）

#### 什么是管线化
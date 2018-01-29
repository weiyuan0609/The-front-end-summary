#### cookie localStorage sessionStorage区别
* cookie:他有本地存储的功能，使用document.cookie=..获取和修改

优点：
1. 可以解决HTTP无状态的问题，与服务器进行交互

缺点：
1. 数量和长度限制，每个域名最多20条，每个cookie长度不能超过4kb
2. 安全性问题。容易被人拦截
3. 浪费带宽，每次请求新页面，cookie都会被发送过去 

* localStorage和sessionStrorage：sessionStorage是当前对话的缓存，浏览器窗口关闭即消失，localStorage持久存在，除非清除浏览器缓存。

优点：
API简单
html5专门为存储而设计，最大容量5M
localStorage.setItem(key,value),localStorage.getItem(key, value)

**注意： ISO safari隐藏模式下，localStorage.getItem会报错，建议统一使用try-catch封装   
**


#### cookie 和 session区别
1. cookie数据存放在客户的浏览器上，session数据放在服务器上。
2. session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能。考虑到减轻服务器性能方面，应当使用COOKIE。


#### CSRF Cross-site request forgery（跨站请求伪造）
参考： http://www.imooc.com/article/13552

过程：用户小明在你的网站A上面登录了，A返回了一个session ID（使用cookie存储）,小明的浏览器保持着A网站的登录状态，攻击者小强给小明发送了一个链接地址，小明打开了地址的时候，这个页面已经自动的对网站a发送了一个请求，通过使用小明的cookie信息，这样攻击者小强就可以随意更改小明在A上的信息。

#### XSS cross sit script 跨站请求攻击
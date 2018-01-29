#### CSRF Cross-site request forgery（跨站请求伪造）
参考： http://www.imooc.com/article/13552

过程：用户小明在你的网站A上面登录了，A返回了一个session ID（使用cookie存储）,小明的浏览器保持着A网站的登录状态，攻击者小强给小明发送了一个链接地址，小明打开了地址的时候，这个页面已经自动的对网站a发送了一个请求，通过使用小明的cookie信息，这样攻击者小强就可以随意更改小明在A上的信息。

防御措施：
1）使用token：服务器随机产生tooken，然后以tooken为秘钥产生一段密文，把token和密文都随cookie交给前端，前端发起请求时把密文和token交给后端，后端对token和密文进行验证，看token能不能生成同样的密文，这样即使黑客拿到了token也无法拿到密文
2）使用验证码：每一个重要的post提交页面，使用一个验证码，因为第三方网站是无法获得验证码的
3）检测http的头信息refer。Referer记录了请求的来源地址，服务器要做的是验证这个来源地址是否合法
4）涉及敏感操作的请求改为POST请求

#### XSS cross sit script 跨站请求攻击
参考: http://www.imooc.com/learn/812
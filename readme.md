### Node.js小技巧
```
$node
let a = 1
let b = 2
console.log(a+b) // 3 就跟控制台是一样的

热更新
npm i -g supervisor
执行 supervisor http.js
```

### Node.js开篇

##### Node.js简介
> Node.js 是一个 Javascript 运行环境(runtime)。Nodejs 是基于 V8 引擎, V8 是 Google 发布的开源 JavaScript 引擎 ,本身就是用于 Chrome 浏览器
的 JS 解释部分。

##### Node.js超强的高并发能力
> 在 Java、PHP 或者.net 等服务器端语言
中,会为每一个客户端连接创建一个新的线程。而每个线程需要耗费大约 2MB 内存。也就是说,理论上,一个 8GB 内存的服务器可以同时连接的最大用户数为 4000 个左右。要让 Web 应用程序支持更多的用户,就需要增加服务器的数量,而 Web 应用程序的硬件成本当然就上升了。
Node.js不为每个客户连接创建一个新的线程,而仅仅使用一个线程。当有用户连接了,就触发一个内部事件,通过非阻塞 I/O、事件驱动机制,让 Node.js 程序宏观上也是并行的。使用 Node.js ,一个 8GB内存的服务器,可以同时处理超过 4 万用户的连接。

##### Node.js不仅可以实现应用，还实现了整个HTTP服务器
> 如果我们使用 PHP 来编写后端的代码时,需要 Apache 或者 Nginx 的 HTTP 服务器,来处理客户端的请求相应。但是Node.js只需要引入HTTP模块就可以了。

### Node.js模块
##### HTTP模块启动HTTP服务器
```
// http.js文件
var http = require('http') // 引入模块
// req:获取url信息
// res浏览器响应信息
http.createServer(function(req, res){ // 创建HTTP服务器

  if (req.url!=='/favicon.ico') { // 因为当前有2个请求，其中一个是/favicon.ico
    console.log(req.url) // 获取当前页面的url（除去host）信息
    var query = url.parse(req.url, true) // 解析当前url获取get参数
    console.log(query.query.aid)
  }

  // 设置响应的HTTP头，状态码为200，文件类型是html,字符集是utf-8
  res.writeHead(200, {"content-Type": "text/html;charset='utf-8'"})

  res.write('hello') // 书写到页面中，跟document.write()差不多

  res.end() // 结束响应
}).listen(8001) // 用listen设置端口号

// 启动服务器: $ node http.js
```

##### url模块
```
let url = require('url')
let obj = url.parse('http://www.baidu.com/news?name=zhangsan') // 用来解析url
console.log(obj)
// {
  protocol: 'http:',
  slashes: true,
  auth: null,
  host: 'www.baidu.com',
  port: null,
  hostname: 'www.baidu.com',
  hash: null,
  search: '?name=zhangsan',
  query: 'name=zhangsan',
  pathname: '/nes',
  path: '/nes?name=zhangsan',
  href: 'http://www.baidu.com/nes?name=zhangsan'
}
let obj1 =  url.parse('http://www.baidu.com/news?name=zhangsan', true) // 将query转为对象
console.log(obj1)
// {
  protocol: 'http:',
  slashes: true,
  auth: null,
  host: 'www.baidu.com',
  port: null,
  hostname: 'www.baidu.com',
  hash: null,
  search: '?name=zhangsan',
  query: [Object: null prototype] { name: 'zhangsan' },
  pathname: '/nes',
  path: '/nes?name=zhangsan',
  href: 'http://www.baidu.com/nes?name=zhangsan'
}
```

##### CommonJS自定义模块
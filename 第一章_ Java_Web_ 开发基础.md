## Http 的理解:
* 超文本传输协议, 一开始是为了传输超文本文档的协议
* 规定了客户端(也可以是服务器)和服务器端通信的规范

##Http 的特点:
* 无连接: 服务器处理完请求就断开, 好处是节约传输时间, 坏处是传完就断开了.
* 无状态: 对事务的处理没有状态这个概念, 如果后面需要用到前面的信息, 需要重传.

##Http 通信具体信息:
###所有版本: 
HTTP 1.0 ; HTTP 1.1 ;   HTTP-NG;

###HTTP请求:
1. 请求行(必须) 

    方法 + 资源 URI + HTTP 版本
    `GET /index.html HTTP/1.1`
    
2. 请求报头(可选)

    包含客户端信息, 和请求附加的信息
    常见的有: Accept, User-Agent
    
    ```
    GET /index.html HTTP/1.1
    Accept: text/plain
    Accept: html
    User-Agent: Mozilla/4.5(WinNT)
    /*空行*/
    ```
    
3. GET & POST 的请求提体(可选)
    
    * 使用 GET: 请求的参数会直接放到 URL 后面, 放在请求报头中
    * 使用 POST: 请求参数放在请求体中, 如下:

    ```
    POST /index.html HTTP/1.1
    HOST: www.javait.com
    User-Agent:Mozilla/4.5(WinNT)
    Accept: text/html
    Accept-language:zh-cn
    Content-Length:22
    Connection: keep-alive
    
    param1=abc&param2=def
    ```
    
###HTTP响应:
1. 状态行

    HTTP 版本 + 状态码 + 状态码简单描述 string, 例:
    `HTTP 1.0 200 ok`
    
2. 响应报头

    附加的响应信息, 比如接下来应该访问的资源链接, 一些服务器的信息等
    常见的有:
    
    * Allow: 支持的请求方法, 如 GET, POST...
    * Content-Encoding
    * Content-Length
    * Content-Tyoe 回送数据的 MIME 类型(MIME，Multipurpose Internet Mail Extensions)
    * Date
    * Last-Modified
    * Location   重定向的链接
    * Refresh   指定浏览器刷新时间
    * Expores    指定浏览器缓存数据时间
    * Server

    例:
    
    ```html
    HTTP/1.1 200 OK
    Connection: close
    Date: Wed, 19 Nov 2011 02:20:45 GMT
    Server: Apache/2.0.54(Unix)
    Content-Length:397
    Contnt-Type:text/html
    
    <html>
    <body>
    </body>
    </html>
    ```

##关于软件体系架构

###C/S: client & server
* 客户端和服务器,r 也就是桌面或手机客户端, 加上服务器.
* 其本质是: TCP/IP 网络中两个进程之间的通信.
* 有部分逻辑在客户端进行实现, 即利用部分客户端的性能.

###B/S: browser & server
* 浏览器和服务器.
* 好处在于各个客户端的浏览器环境基本是相同的, 一次开发, 处处运行.
* 逻辑主要在服务器端实现, 当然随着现在 JavaScript 脚本的流行, 浏览器端可以实现更加酷炫的效果.


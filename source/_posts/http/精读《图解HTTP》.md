---
title: 精读《图解HTTP》
date: 2023-04-30
---

# Web及网络基础
## HTTP 诞生
### 为知识共享而规划 Web
1989年，CERN 提出了一种能让远隔两地的研究者们共享文档的设想，这就是万维网（World Wide Web）的雏形。
并提出了三项基本技术。即：
1. 作为页面的文本标记语言 - HTML
2. 作为文档传输协议 - HTTP
3. 文档所在地址 - URL（统一资源定位符）

1990年，CERN 成功研发了世界上第一台**Web**浏览器和**Web**服务器

### Web 成长时代
1993年1月，现代浏览器的祖先NCSA研发的MOsaic 问世了。它以内联等形式显示出HTML 的图像。
1994年，网景公司发布了Netscape
1995年微软发布了IE 1.0 和 IE 2.0，同期Apache 发布了Web 服务器
接下来的一段时间内是，网景公司和微软关于浏览器打架。每家公司都有不同的更新，导致最痛苦的便是前端开发工程师，要同时兼容多家的浏览器适配。
2000年左右，网景公司衰落，这场战争才平息。
2004年Mozilla 基金会发布了**Firfox**浏览器

### HTTP 发展
HTTP 问世于1990年。为区别于HTTP/1.0 被称为HTTP/0.9。
1996 HTTP/1.0 作为标准被公布
1997年 HTTP 1.1 被公布
2015年 发布了 HTTP2
2020年 发布了 HTTP3

## TCP/IP
### TCP/IP 协议族
### TCP/IP 的分层
> 分层的好处；1. 便于修改，只需要修改变动的层即可；2. 便于通讯；3. 设计简单，只需考虑应用层。
1. 应用层 - HTTP，FTP、DNS
2. 传输层 - TCP、UDP
3. 网络层 - IP
4. 数据链路层 - (物理层)


#### 应用层
最上层的路线。

#### 传输层
数据传输

##### 可靠的TCP协议
**数据分割**
    为了方便传输，TCP 将大块数据分割成 报文段 为单位的数据包进行管理。
**确认**
    TCP 协议能够确认数据最终能够传输到接收方。
    **三次握手** TODO

#### 网络层
用来处理网络上流动的数据包。数据包是网络上流通的最小单元。
在与对方计算机通讯时，网络层在多条路线中选择一条路线。

IP 协议最重要的两个事情是绑定目的地的 IP 地址和 MAC 地址（IP地址一般指的是在一个区域内，被分配的网络地址，MAC 地址一般指的是网卡地址）

**ARP协议**
通过目的地的IP地址反查出来对应的MAC 地址

另一个重要的专有名词**路由**选择
网络通信是通过不停的中转实现的。在到达通信的目的地之前，设备和人都不会知道选择的是那一条路线。不会掌握互联网的细节。


#### 数据链路层
用来处理连接网络的硬件部分。包括操作系统，驱动，网络适配器（网卡），光纤。

### TCP/IP通信传输流

利用TCP/IP进行通讯时，会通过分层顺序与对方进行通信。发送端从**应用层**往下走，接收端从**链路层**往上走。

发送端：
每发送一层添加首部

接收端：
每接收一层删除首部

### DNS 解析
应用层
提供域名地址到IP地址之间的解析


## URL 和 URI 的区别
URL - 统一资源定位符
    表示资源的地点
URI - 统一资源标识符
    用来表示某一确定资源的地址

**URL 是 URI 的子集**

# HTTP 协议

## 请求必须由客户端发出，服务端回复响应。客户端首先去建立通信。

**请求报文包括：**
    请求方法 请求URI 协议版本
    请求首部字段
    内容实体

**响应报文包括**
    协议版本 状态码 状态码短语
    响应的首部字段
    内容实体

## 无状态
HTTP 是一种无状态的协议。为了简单。
在HTTP 1.1 中引入了Cookie 解决了状态问题。

## HTTP 方法
GET
POST
PUT
DELETE
OPTIONS 询问支持的方法
HEAD 获得报文首部

## 持久化连接

场景：电商网站上的多个商品图片请求，每次请求产生的TCP连接和断开，都会增加开销。
### 持久连接：
    旨在解决这种问题，任意一端没有提出断开连接，则保持**TCP**连接状态。
HTTP 1.1
    默认都是持久连接
## 使用cookie

# HTTP 报文

HTTP 报文本身是由多行数据组成的字符串文本。
HTTP 报文可分为 
    报文首部
    报文主体
也可分为请求报文和响应报文。

## 报文首部
### 请求报文首部
    请求行 - 请求方法 请求URI 协议版本
    请求首部字段
    通用首部字段
    实体首部字段
    其他
### 响应报文首部
    响应行 - 协议版本 状态码 状态码短语
    响应首部字段
    通用首部字段
    实体首部字段
    其他

### 各类首部列举
#### 通用首部字段
    Cache-Control: 
    Pragma
#### 请求首部字段(不是全部，但是是重要的)
Clinent-IP
From
Host
Referer
User-Agent
1. Accept 首部
> 是客户端用来告知服务器，能够发送那些媒体类型的数据。媒体类型用 MIME 类型来表示。
![Google demo](https://cdn.jsdelivr.net/gh/xuchao996/gallary@main/imgs/202305141504053.png)
    - Accept
    - Accept-Charset
    - Accept-Encoding
    - Accept-Language

![字段解释](https://cdn.jsdelivr.net/gh/xuchao996/gallary@main/imgs/202305141505103.png)

2. 条件请求字段 首部
> 如果客户端存在一份资源的副本，那么对于再次请求时需要判断是否和服务端的内容是否有差异，如果没有差异，就可以直接使用客户端的副本，而不需要再次下载。这样可以减少网络带宽的消耗。可以根据实际情况，使用不同的首部字段。
    - If-Match
    - If-Modified-Since
    - If-None-Match
    - If-Range
    - If-Unmodified-Since
3. 安全首部字段
    - Authorization
    - Cookie
    - Cookie2
     
#### 响应首部字段
1. 信息首部 
    - Date
    - Server
    - Transfer-Encoding
    - Via
    - Warning
2. 协商首部（内容协商，非协商缓存）

3. 安全响应首部字段
    - Set-Cookie
    - Set-Cookie2
    - 
#### 实体首部字段
1. 内容首部 
    - Allow
    - Content-Encoding
    - Content-Language
    - Content-Length （核心）
    - Content-Location
    - Content-MD5
    - Content-Range
    - Content-Type （核心）
![内容首部](https://cdn.jsdelivr.net/gh/xuchao996/gallary@main/imgs/202305141515957.png)

1. 实体缓存首部
    - ETag （实体内容MD5后的标识符）
    - Expires
    - Last-Modified（实体最后一次修改的时间）

## 提升编码速率
报文主体和实体主体
HTTP 报文主体主要用于请求或响应的实体主体。

### 压缩
    Gzip

### 分块
Chunked transfer Coding 分块传输编码

# HTTP 连接

# 返回的HTTP 状态码
状态码的功能是描述 返回的请求结果。

状态码的类别
1xx     
2xx     成功
3xx     重定向
    304 Not Modified 

4xx     not found 客户端错误
5xx     服务端异常


## 304 Not Modified
一般用在浏览器缓存中。
对于相同资源的第二次请求，浏览器进行的条件请求，即请求头里会添加类似（If-Match, If-Modified-Since, If-None-Match, If-Rage, If-Unmodified-Since），中的任一字段，服务器接到请求之后，进行条件判断，如果资源已经被修改，那么将返回新的资源，否则，返回304状态码。注意返回304的同时是不会带报文主体的。304代表资源可以从缓存中取。
浏览器本身会在本地维护一个缓存资源，以存储最近访问的资源。

## 缓存

### 什么是浏览器强缓存
HTTP 强缓存是通过设置 HTTP 头来实现的一种缓存机制，用于在浏览器中缓存静态资源，例如图片、CSS 和 JavaScript 文件等。当使用 HTTP 强缓存时，浏览器将在本地缓存中存储资源，并在下一次请求时使用缓存中的资源，而不是向服务器发送请求。这可以提高网站的性能和加载速度，减少对服务器的负载。HTTP 强缓存通常使用 Cache-Control 和 Expires 头来控制缓存。Cache-Control 头允许设置缓存的最大年龄、是否允许缓存和是否允许在 HTTPS 上缓存资源等选项。Expires 头指定资源过期的时间，以便浏览器可以确定何时需要更新缓存中的资源。
注意：Cache-Control 头比 Expires 头具有更高的优先级。当这两个头都存在时，Cache-Control 头将覆盖 Expires 头。Cache-Control 头允许更精细的缓存控制，例如设置缓存的最大年龄、是否允许缓存和是否允许在 HTTPS 上缓存资源等选项。而 Expires 头则指定资源过期的时间，缺乏灵活性。因此，建议使用 Cache-Control 头来控制缓存，而不是 Expires 头。
### 什么是协商缓存
协商缓存是一种 HTTP 缓存机制，用于检查浏览器中缓存的资源是否仍然有效，从而减少对服务器的请求。当使用协商缓存时，浏览器将向服务器发送一个条件请求，以检查资源是否已更改。服务器将根据请求中的条件进行比较，并返回一个状态码，以指示资源是否已更改。如果资源未更改，则服务器将返回一个 304 Not Modified 响应，浏览器将使用缓存中的资源。如果资源已更改，则服务器将返回一个新的资源，浏览器将使用新的资源更新缓存。协商缓存通常使用 If-Modified-Since 和 If-None-Match 头来实现。If-Modified-Since 头指定上次修改时间，而 If-None-Match 头指定资源的 ETag（实体标签），这是一个字符串，用于标识资源的特定版本。

## 3xx
301
永久重定向
302
临时重定向

## 4xx
400 Bad request
401 Unauthorized
403 Forbidden
404 Not Found

## 5xx
500 Internal Server Error
503 Service Unavailable


# 附录

> Nginx/1.21.0默认添加的HTTP头信息如下：

1. Server：指定Web服务器软件名称和版本号，例如"nginx/1.21.0"。
2. Date：指定响应生成的日期和时间，例如"Tue, 22 Jun 2021 10:30:00 GMT"。
3. Content-Type：指定响应的MIME类型，例如"text/html"。
4. Content-Length：指定响应正文的长度，单位为字节。
5. Connection：指定是否保持连接，例如"keep-alive"或"close"。
6. Cache-Control：指定缓存控制策略，例如"no-cache"或"max-age=3600"。
7. Expires：指定响应过期的日期和时间，例如"Thu, 01 Dec 2022 16:00:00 GMT"。
8. Last-Modified：指定响应的最后修改日期和时间，例如"Tue, 22 Jun 2021 10:00:00 GMT"。

需要注意的是，这些默认HTTP头信息可以通过Nginx配置文件进行修改或删除。

# 引用
- 图解HTTP
- HTTP权威指南
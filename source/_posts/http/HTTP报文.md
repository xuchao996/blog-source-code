---
title: http-报文
date: 2023.06.19
---

# 报文流
上游（client）-下游（server）
上游（server）-下游（client）
对于HTTP请求来说，client 和 server 不是固定的上下游，是根据谁发起，谁接收进行判定的。
![所有的报文都向下游流动](https://cdn.jsdelivr.net/gh/xuchao996/gallary@main/imgs/202306171839491.png)

# 报文的组成

## 请求报文和响应报文
对于HTTP报文来说，任何报文都可以分为两类。请求和响应报文。
![](https://cdn.jsdelivr.net/gh/xuchao996/gallary@main/imgs/202306171841189.png)

由上图可以看出报文的格式
- 行
- 首部
- 实体主体
请求和响应还是有些许不同。

请求报文的格式
```
method url protocol
headers
entity-body
````
响应报文的格式
```
protocol status-code phrase
headers
entity-body
```

### 具体解释下每个参数的含义

- method 请求方法
- request-url 请求的资源地址
- protocol 协议&&协议版本
- status-code 状态码
- phrase 状态码短语，状态码和状态短语是一组的，状态码是数字，状态短语是对应的文字描述

请求方法（method）：
    代表着客户端对服务器的请求动作，是一个动词。

不同的请求方法，对应的请求报文中，实体主体可能有也可能没有。`Get` 请求中，实体主体是没有的，`Post` 请求中，实体主体是有的。

协议&& 协议版本（protocol）
HTTP/major.minor 
major.minor 代表着协议的版本号，major 代表着主版本号，minor 代表着次版本号。

状态码（status-code）
状态码是一个三位数的数字，代表着服务器对请求的处理结果。状态码是有约定的，不同的状态码代表着不同的含义。HTTP对状态码有一个简单的划分。
![](https://cdn.jsdelivr.net/gh/xuchao996/gallary@main/imgs/202306171904527.png)

状态码短语（phrase）
又叫原因短语。和状态码是一一对应的关系。用来描述状态码。方便理解。

首部（headers）
一系列的字段。描述了除method url protocol 之外的其他信息。上述三个行信息是必要的，不可更改的，但首部不一样。它是有约定的，且可以自定义信息。常见的首部操作是在字段中存放token字段，用于验证身份。
具体可以学习[首部](../http/首部.md)

实体主体（entity-body）
实体数据是任意数据组成一个数据块。
请求报文中，实体主体是可选的，响应报文中，实体主体是必选的。
它是响应的负载，是HTTP要传输的内容。

表单[^1]

# 引用
 - HTTP 权威指南

# 脚注（不一定生效）
[^1] : 表单是一种常见的实体主体，它是由一系列的键值对组成的。
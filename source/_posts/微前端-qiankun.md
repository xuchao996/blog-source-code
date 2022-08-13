---
title: 微前端-qiankun
date: 2022-08-08
description: 今天是个好日子
---



### 微前端

#### 一般分为两pa

1. 主应用（基座）
2. 子应用

#### 常规方法

iframe

iframe也算是常规方法。

在chrome浏览器一家独大的情况下，iframe也显的平平无奇了。

|          | iframe                                            | qiankun                                                      |
| -------- | ------------------------------------------------- | ------------------------------------------------------------ |
| 隔离     |                                                   |                                                              |
| 通讯     | postMessage、cookie（不跨域的情况）               |                                                              |
| 生命周期 | 依赖iframe抛出的原生方法<br />onload<br />onerror | 自带相关的生命周期，比iframe要全。包括load<br /> mount<br /> unmount |


---
title: 02 溯源：CSharp的运行环境
date: 2022-08-04
categories: Csharp
---

一个集成的，面向对象的框架。

多平台，性能好的框架。

#### .NET 的组成

执行环境 ---- CLR（common language runtime lib）

>  在运行时管理程序的运行。

-  内存管理和垃圾收集
-  代码安全验证
-  代码执行、线程管理和异常处理

BCL（bass class lib，基类库）

 包括通用基础类，集合类，线程和同步类、XML 类

 **BCL 是专供于代码使用的**

FCL（框架类库）

 BCL 是 FCL 的一个子集。

#### 编译成为 CIL（Common Inter Language 公共中间语言）

源代码 ---------被编译------------程序集（CIL，类型的元数据、对其他程序集引用的元数据）

#### 编译成本机代码并执行

CIL 顾名思义，只是中间语言。当程序运行时，CLR 会去执行：（CLR 做的事）

1. 检查安全特性
2. 分配内存空间
3. 把程序集中的可执行代码发送给 JIT 编译器去编译，编译成本机代码

#### CLI

它把所有.NET 框架的组件连接在一起组成一个内聚的。一致的系统。

 CLR

 BCL

 CTS（common types system）

 CLS（common language system）

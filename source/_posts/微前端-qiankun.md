---
title: 微前端-qiankun
date: 2022-08-08
updateDate: 2022-11-29
description: 今天是个好日子
---



### 微前端（按主从分）

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





### 常规集成

#### 主应用

两类API 实现

1，register  start

​	依赖路由 base

2，loadMicroApp

​	直接渲染到具体dom上，不依赖路由

```js
import {register} from qiankun

const app = register([
  {
    name: "",
    entry: "",
    activeRule: ""
  }
])

app.start();
-------------------------------------
var microApp = qiankun.loadMicroApp(
  {
    name: '91edcWeb',
    entry: 'http://localhost:8000',
    // entry: 'http://127.0.0.1:5173/login',
    container: '#newVisitContainer',
    props: {
    name: 'kuitos',
  },
   configuration: {
      jsSandbox: true,
      prefetch: true,
      sandbox: { experimentalStyleIsolation: true }
    },
	},
  );

```



#### 子应用

```javascript
1. 修改window.publicPath

2. 修改 router base

3. 在 mainjs 里添加钩子，注意钩子是固定api
	3.1 onMounted(传入props)
  3.2 onUpdate
  3.3 onDestroy

```



### umi集成

#### 主应用

```javascript
0. 安装 umi-plugin-qiankun 插件
1. umijs 注册 子应用
    master: {
      // 注册子应用信息
      apps: [
        {
          name: 'epro', // 唯一 id
          // html entry
          entry: 'http://localhost:8080'
        },
      ],
      jsSandbox: true,
			prefetch: true

    },
2. 路由声明

3. dom tree 上注册
	import { MicroApp } from 'umi';
	export function Page() {
    return (
    	<div>
      	<MicroApp name="epro" ...props>
      	</MicroApp>
      </div>
    )
  }
```



**资源共享问题**

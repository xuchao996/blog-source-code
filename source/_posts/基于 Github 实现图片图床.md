---
title: 基于 Github 实现图片图床
date: 2022-08-08
---



承接上文，目的是为了给博客系统接入一个图床的功能。图片做为一个重要的展示能力是一个博客必不可少的功能。
但基于免费（白嫖）的原则，这次我们选择的还是 GitHub 作为图片存储的首选。（Github repo 可以存放大概100G的内容）

所以我们开始了---

大致规划了一下步骤：
1，申请一个 GitHub repo ，申请一个token 用来做三方认证
2，本质是图片上传到这个repo 里，然后通过 GitHub content url去获取
3，当编辑Markdown文档时，我需要插入本地图片，当 deploy 的时候我需要整个上传我的当前图片资源包，然后替换url为对应的网络图片
    3.1 这里其实需要区分一下，一般上传分为两类图片，一类是本地图片，一类是网络图片，这里网络图片也应该转为本地图片


网上找了一下，有一个叫做 [picGo的开源工具](https://picgo.github.io/PicGo-Doc/)，可以简化我的操作，所以我改了方案。
picGo的功能是做一个上传的工具。
在picGo里可以配置GitHub repo 和 GitHub 申请的token，通过可视化上传（这里支持本地和remote ）。

``` shell
$
$ 

```

1. 创建一个 repo 这个比较简单，不多说了，如果有不清楚的朋友可以直接找我
2. 申请一个token
首先我们去到这里 (https://github.com/settings/tokens) 可以看到
![截图1](https://cdn.jsdelivr.net/gh/xuchao996/gallary@main/imgs/20220711201930.png)
我这里是申请过了。我起的名字是save image，过期时间我给的是never 这俩个可以随便，但关键是key，这个要保存下来，最好是立即存下来。
这个也要勾选授权。
![](https://cdn.jsdelivr.net/gh/xuchao996/gallary@main/imgs/20220730145539.png)
3. picGo 真是一个有趣的项目，因为我在里面看到了各种版本和很多技术的picGo，大家有空可以看下。
我装的是Windows版本的，配置很简单，选择图床设置的GitHub
![](https://cdn.jsdelivr.net/gh/xuchao996/gallary@main/imgs/20220711235754.png)

4. typora 关联
这个很简单了 我是mac 电脑，直接查看typora 的偏好设置，在图像里的配置上勾选，就妥了。
![](https://cdn.jsdelivr.net/gh/xuchao996/gallary@main/imgs/20220730150140.png)

5. Q&A
期间也遇见一些问题，但都是配置层面的东西，比如picgo 的GitHub设置，如果你配置有问题的话，基本上是配置出错了，所以需要多多检查下是不是哪里配错了。

6. 完。
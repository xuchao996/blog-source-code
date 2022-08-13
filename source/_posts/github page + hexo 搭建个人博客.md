---
title: github page + hexo 搭建个人博客
---



# 一  初步共识

GitHub Page 是一个免费免费，开源的website ，你可以用来搭建个人网站。准备的来说，一切静态网站的事，它都可以做。
我选择这个主要是看中了有一个免费的domain。GitHub 默认的也有blog系统，但是主题没有hexo多。所以选了Hexo。相关网
站如下。
GitHub Page （https://pages.github.com/）
HEXO（https://hexo.io/zh-cn/index.html）
但需要注意，GitHub Page 是没有百度seo 的，所以没人能在百度上搜索到你的个人Blog。

# 二 创建一个 GitHub Page

其实比较简单，直接看上面的官网就行了，唯一需要注意的是create repo 的项目命名。需要和你的 GitHub 账户名一致。如下图；


最后生成的是这样一个地址
https://xuchao996.github.io/

如果不行就强制刷新一下，大概率是缓存问题。


# 三 本地 run 一个 hexo 项目

这里其实要好好说一下，我其实是参考了一篇教程。https://zhuanlan.zhihu.com/p/96641789，我就不在赘述了。
但其本质是通过安装一个node 工具去生成一套hexo 的模板。按照这个模板的约定，我们可以去修改模板，也可以去关联 github。
在这里我使用的是 theme （tufu9441/maupassant-hexo: A simple Hexo theme forked from icylogic.）这个觉得比较简约，符合个人爱好。
在约定的地方，我们去写上Markdown格式的博客文档。

``` shell
// Generate static files (生成静态系统)
$ hexo generate
// Deploy to remote sites (部署到remote site，即GitHub Page 上)
$ hexo deploy
```

去我们的GitHub Page (https://xuchao996.github.io/) 上看就行了。
注意这里还是实时的，如果发现没有更新，那就强制刷新一下，因为大概率是缓存问题。

# 四 评论

突然发现博客没有评论功能，急忙看了看。但好像还是要 依赖 GitHub 的 GitHub issues 功能。
我在这里使用的 gitalk （gitalk集成了github issue的功能）
site如下
https://gitalk.github.io/


要做几件事情。
    4.1 做一下授权。即我们需要在Github 里做一下授权，我们可以在第三方去使用issue 功能。这里做的是一个申请。site 如下 （https://github.com/settings/applications/new）
    
    4.2 这个就很简单，因为很多主题里集成了 gitalk，我这里需要在config.yml里，填写我们在第一步申请的id, screct。我这里repo
    又重新申请了一个，但实际上来说一个repo就足够了，我们仍然可以重复去用 xuchao996.github.io 这个repo。
    重新build deploy 就行了

```yml
gitalk: ## See: https://github.com/gitalk/gitalk
  enable: true ## If you want to use Gitment comment system please set the value to true.
  owner: xuchao996 ## Your GitHub ID, e.g. username
  repo: gitalk-comments ## 这里应该用一个项目 The repository to store your comments, make sure you're the repo's owner, e.g. gitalk.github.io
  client_id:  ## GitHub client ID, e.g. 75752dafe7907a897619
  client_secret:  ## GitHub client secret, e.g. ec2fb9054972c891289640354993b662f4cccc50
  id: location.pathname
  admin: xuchao996 

```
its done.

# 本以为结束了，但是其实是少了图片的图床的。在 Markdown 里图片都是以外链的形式引进来。时间不找了所以没有做。等下次有时间了弄下。

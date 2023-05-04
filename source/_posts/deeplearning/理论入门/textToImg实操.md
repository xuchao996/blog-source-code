---
title: textToImg实操
date: 2023-05-04
---

> 无意间刷B站获取到知识。在线服务器运行模型。生成可爱的~~妹子图片~~（爱了爱了）。说干就干。

# 操作步骤
1. 首先通过[GitHub stable_diffusion_webui_colab](https://github.com/camenduru/stable-diffusion-webui-colab#-colab) 进入到云服务器，选哪一个应该都行；

![image-20230504215421410](https://cdn.jsdelivr.net/gh/xuchao996/gallary@main/imgs/image-20230504215421410.png)

2. **执行**云服务器提前准备好的Python 代码（这里不用想了，因为好像都是Python写的）；

3. 点击执行按钮后（小三角按钮），过程会很久 -- loading

4. 脚本执行完成之后会产生一个IP地址（类似于我这样的`http://3oxdianfrmrgn3grbrzbqjvn2k2qyfid6mkwxld3eyf62xqrfnxq.remote.moe/?__theme=dark`）

5. 点击打开，或者复制到浏览器打开，可以看到一整个可视界面

6. 这里我需要介绍另一个网站[C站](https://civitai.com/)，大家可以搜索一下。这个网站主要提供了生成式图片的prompt，而我们可以拿到这个prompt 也可以去生成这样一些萌妹。类似于这样。

![image-20230504204815468](https://cdn.jsdelivr.net/gh/xuchao996/gallary@main/imgs/image-20230504204815468.png)

7. 点击一张图片进去，在右下角可以看到Prompt。而Resource 代表着使用模型。比如下图的女孩。

![image-20230504211822718](https://cdn.jsdelivr.net/gh/xuchao996/gallary@main/imgs/image-20230504211822718.png)

8. 回到第四点，打开网站之后，也可以找到 `civitai`。经历以下6步。

![image-20230504212909836](https://cdn.jsdelivr.net/gh/xuchao996/gallary@main/imgs/image-20230504212909836.png)

9. 点击下载模型后，我们需要回到脚本页面去观察是否下载完成。

10. 下载完成之后，我们需要刷新我们的UI 界面，或者不用刷新，切换左上角的checkpoint。选择这张图片使用过调优后的模型。然后选择text2Img。在这里去输入相关参数。

11. 后面应该都比较傻瓜了，就是把参数整个拷过来，点击生成。

![image-20230504214330131](https://cdn.jsdelivr.net/gh/xuchao996/gallary@main/imgs/image-20230504214332172.png)



# 坑或者槽点

1. 网络很关键，我51在老家跑的时候一直很稳定， 不会出现脚本跑步下来的情况，但是回到SH 以后确实跑步下来，然后我把节点切到香港，但是也就成功了一次，后面的下载模型就挂了。所以需要一个稳定的节点，最好是在欧美。
2. 我没注意到的一点是下载模型切模型时，需要刷新整个webUI。然后才能把下载后的模型倒进去。其实这也是有一个刷新icon的原因。我完全没意识到。
3. C站黄图太多了，其实这也是一个问题，后面生成H图成本应该拉的很低了，可能就是一两句话，换脸，Sex 什么的，xdm 慎重。



# 引用

stable_diffusion_webui_colab https://github.com/camenduru/stable-diffusion-webui-colab#-colab

C站 https://civitai.com/

Q:  Colab 是什么？

A:  一个在线运行的Python 运行时。谷歌云提供。

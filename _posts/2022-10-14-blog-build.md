---
layout: post
title: "博客搭建过程中的问题记录"
subtitle: "当你整合了一些垃圾却恰好能够运行时"
date: 2022-10-14
author: "夜雨声烦"
header-img: "img/bg1.png"
header-mask: 0.5
catalog: true
tags: []
---
# 图片插入问题

本地编辑md时图片插入的逻辑和在网页上实际显示图片的逻辑是不一样的，jekyll编译的本地静态网站会创建_site文件夹，里面的img文件夹会包含和外面的img里相同的图片内容，只有将图片加入到外面的img文件夹并用相对路径 `/img/xxx.png`添加图片才能够被正确找到和显示。

![](/img/截屏2022-10-14%2016.33.43.png)

# Disqus评论加载问题

一开始无法正确加载评论功能，虽然_config.yml里也修改了：

```yaml
# Disqus settings
disqus_username: yeyushengfan
```

阅读官方的[Troubleshooting](https://help.disqus.com/en/articles/1717301-i-m-receiving-the-message-we-were-unable-to-load-disqus)后，从上到下一个个测试，最终找到原因为：

> **Your shortname is missing or incorrect**
>
> Disqus won't load if you haven't yet [registered a forum shortname](http://disqus.com/register) or if the shortname you have entered is incorrect (See [What&#39;s a shortname?](https://help.disqus.com/customer/en/portal/articles/466208-what-s-a-shortname-)). We suggest double-checking your shortname in the Disqus embed code, which should appear in place of EXAMPLE in this line: `s.src = '//EXAMPLE.disqus.com/embed.js';` of your code, or the settings page for your respective platform.

如下配置后，评论区可以正常加载。

![](/img/截屏2022-10-14%2016.42.16.png)

# 自定义域名

在[name](https://www.name.com/)网站购买了自己的域名 `yeyushengfam.com`，在[这里](https://www.name.com/account/domain/details/yeyushengfan.com#dns)进行DNS记录管理，很方便地一键配置和Github Pages的关联。

![](/img/截屏2022-10-14%2017.10.29.png)

同时在Github的`yeyushengfan0508.github.io`仓库下，找到`Settings->Pages`，关联自己的域名，并勾选只能通过自定义域名访问。

![](/img/截屏2022-10-14%2017.14.08.png)
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

同时在Github的 `yeyushengfan0508.github.io`仓库下，找到 `Settings->Pages`，关联自己的域名，并勾选只能通过自定义域名访问。

![](/img/截屏2022-10-14%2017.14.08.png)

# 添加Google Analytics

虽然但是，还是配置了谷歌分析来查看网站的访问情况。通过搜索发现已有的教程或者帖子用的都是Universal Analytics，而现在已经迁移至Google Analytics 4。所以就按照官网的教程来进行配置。

首先你当然得有一个谷歌账号，在自己的账号下新建一个媒体资源，关联到博客地址：

![](/img/截屏2022-10-16%2000.26.52.png)

然后会提醒你将代码加入你的网站（这里为了截图随便新建了一个媒体资源）：

![](/img/截屏2022-10-16%2000.30.31.png)

查看代码说明，由于jekyll不对Google提供原生支持，所以进行手动添加。我将这段代码加在了 `/_include/head.html`里的 `<head>`元素之后。

![](/img/截屏2022-10-16%2000.32.30.png)

谷歌分析开始收集数据流并显示：

![](/img/截屏2022-10-16%2000.37.45.png)

# 通过Mathjax添加数学公式支持[10.25]

理论上原博客仓库是支持数学公式编辑的，最近要记录学习内容的时候才发现有问题。查看了一下这部分的代码，不得不吐槽一下确实是很久不维护了，逻辑也有一定问题。查看文档发现Mathjax也已经从 `v2`全面升级到 `v3`，之前的代码基本是不能用了，因此决定完全舍弃。

根据[Mathjax官方文档](https://docs.mathjax.org/en/latest/web/configuration.html)，将如下代码复制到 `_includes/mathjax_support.html`：

```html
<script>
MathJax = {
  tex: {
    inlineMath: [['$', '$'], ['\\(', '\\)']],
    tags: 'ams'
  },
  svg: {
    fontCache: 'global'
  }
};
</script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js">
</script>
```

然后在 `/_layouts/post.html`和 `page.html`中`include`这个文件。

再渲染可以成功显示公式，后续需要时再添加其他支持。

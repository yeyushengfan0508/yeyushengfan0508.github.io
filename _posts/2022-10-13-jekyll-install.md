---
layout:       post
title:        "安装jekyll"
subtitle:     "过程的一些记录"
author:       "夜雨声烦"
header-img:   img/night-car.png
catalog:      true
tags:
    - ruby
    - jekyll
---
按照Jekyll主页的Quickstart，在命令行输入指令：

```shell
gem install jekyll bundler
```

显示问题信息:

> You don't have write permissions for the /Library/Ruby/Gems/2.3.0 directory.

根据Stack Overflow上的[高亮回答](https://stackoverflow.com/questions/51126403/you-dont-have-write-permissions-for-the-library-ruby-gems-2-3-0-directory-ma "monfresh")解决：

> You are correct that macOS won't let you change anything with the Ruby version that comes installed with your Mac. However, it's possible to install gems like `bundler` using a separate version of Ruby that doesn't interfere with the one provided by Apple.

下为**Monfresh**推荐的解决办法：

```shell
# 用Homebrew下载chruby和ruby-install
brew install chruby ruby-install

# 安装最新版本的Ruby，下载完按照提示向.zshrc中加入一些export
ruby-install ruby

# 切换到下载的最新版本，我的是3.1.2，如果是其他版本会报错
chruby 3.1.2
```

然后顺利安装了**jekyll**和**bundler gems**，运行下述指令：

```shell
# Build the site and make it available on a local server.
bundle exec jekyll serve
```

但是出现了一些报错，是由于缺失一些依赖包，运行 `bundle install`下载，这次成功运行了！

打开[https://127.0.0.1:4000]()，成功展现网页：

![](/img/截屏2022-10-13%2014.26.02.png)
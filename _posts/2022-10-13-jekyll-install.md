---
layout:       post
title:        "安装jekyll"
subtitle:     "过程的一些记录"
author:       "夜雨声烦"
header-img:   img/night-car.png
header-mask:  0
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
# Build the site and make it available on a local server.[from Quickstart]
# Github Pages官网推荐使用Bundler运行Jekyll
bundle exec jekyll serve

# 同时推荐使用该指令
# Pass the --livereload option to serve to automatically refresh the page with each change you make to the source files
bundle exec jekyll serve --livereload
```

但是出现了一些报错，是由于缺失一些依赖包，运行 `bundle install`下载，这次成功运行了！

打开[https://127.0.0.1:4000](https://127.0.0.1:4000)，成功展现网页：

![](/img/截屏2022-10-13%2014.26.02.png)

# 10月25日更新

虽然之前已经将下列语句加入到 `~/.zshrc`中：

```shell
source /usr/local/opt/chruby/share/chruby/chruby.sh
# To enable auto-switching of Rubies specified by .ruby-version files
source /usr/local/opt/chruby/share/chruby/auto.sh
```

但是每次打开终端发现并没有自动切换到 `ruby-3.1.2`，去[Github](https://github.com/postmodern/chruby)上查看发现是没有创建`.ruby-version`文件：

![](/img/截屏2022-10-25%2013.45.31.png)

在终端输入指令：

```shell
echo "ruby-3.1.2" > ~/.ruby-version
```

重新打开终端发现已自动切换。
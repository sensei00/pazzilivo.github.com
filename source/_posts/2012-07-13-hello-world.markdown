---
layout: post
title: "Hello OctoPress"
date: 2012-07-13 15:40
comments: true
categories: Octopress
---

折腾了两天，终于把Blog搭建好了，过程中遇到不少问题，非常感谢twitter上 [@lucifr](https://twitter.com/lucifr) ， [@truthurt](https://twitter.com/truthurt) ，[@clipppit](https://twitter.com/clipppit)的热心帮助。

!["Octopress"](http://ww1.sinaimg.cn/large/62152bc3gw1duw7actx3pj.jpg, 'Hello Octopress')

总结一些过程中的问题主要有以下几点，希望在今后大家搭建的过程中有所帮助。

###1.安装RVM
```sh
bash -s stable < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)
```
Next add RVM to your shell as a function.
```sh
echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm" # Load RVM function' >> ~/.bash_profile
source ~/.bash_profile
```
**PS.最好改一下配置文件，在主文件夹下边的 .bashrc文件，在最后加一行代码**

```sh
# This loads RVM into a shell session.
[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm"
```
Install Ruby 1.9.2 and ensure RVM has the latest RubyGems.

```sh
rvm install 1.9.2 && rvm use 1.9.2
rvm rubygems latest
```

###2.安装Octopress

{% codeblock install Octopress lang:sh %}
git clone git://github.com/imathis/octopress.git octopress
cd octopress    # If you use RVM, You'll be asked if you trust the .rvmrc file (say yes).
ruby --version  # Should report Ruby 1.9.2

gem install bundler
rbenv rehash    # If you use rbenv, rehash to be able to run the bundle command
bundle install

rake install
{% endcodeblock %}

###3.部署

申请一个你用户名命名的仓库地址，就像这样`username.github.com`，然后在终端里执行

```sh
rake setup_github_pages
```
然后让你输入一个地址，这样，用户名当然得换了，注意大小写。
```sh
git@github.com:username/username.github.com.git
```
静态化代码，部署
```sh
rake generate
rake deploy
```
提交到source分支
```sh
git add .
git commit -m 'blog source'
git push origin source
```
原则很简单，只要记住`your_local_octopress_directory`对应的的remote source branch，而`_deploy`对应的是remote master branch即可。

###4.第三方主题

[Octopress Wiki Theme List](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes)

{% codeblock install new theme lang:sh %}
$ cd octopress
$ git clone theme-git-url .themes/theme_name
$ rake install['theme_name']
$ rake generate
{% endcodeblock %}
使用 zsh 時發生問題嗎？試試看`rake install\['theme_name'\]`。
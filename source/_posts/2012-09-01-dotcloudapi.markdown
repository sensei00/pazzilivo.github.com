---
layout: post
title: "使用 Dotcloud 搭建 Twip4 的 Twitter API"
date: 2012-09-01 02:12
comments: true
categories: twitter
summary: 应该已经失效了，搞不了~
cover: http://ww2.sinaimg.cn/large/62152bc3jw1ecj64srmgoj20qe0eu74q.jpg
banner: false
---
前几个月经过[@forzaRicky](https://twitter.com/forzaRicky )提及到dotcloud可以搭建twitter的api，由于在ubuntu下搭建比较方便，苦于没有环境，一直没有折腾，前一阵因为想搞这个Blog，所以装了个Ubuntu，正好折腾一下，在搜索的过程中发现可以搭建TWIP4的api，甚是Happy。

下边是教程，大部分参考[@sooulp](https://twitter.com/soooulp)的Blog，但是也遇到了一些问题。

####1.在ubuntu终端上安装dotcloud客户端

首先请确认你的python版本至少是2.6版的，如果不是2.6版本，请更新你的python。

	$ python -V

安装有setuptools开发包的请使用easy_install安装DotCloud:

	$ sudo easy_install dotcloud //官方推荐方式

如果没有setuptools开发包请使用下面的方式安装DotCloud客户端：

	$ sudo apt-get install python-pip   //基于Debian的系统，获取pip(原pyinstall)
	$ sudo pip install dotcloud       //通过pip安装DotCloud

####2.配置dotcloud

	$ dotcloud setup //按提示输入用户名密码
	
	$ dotcloud create xxxx //Created application "xxxx"

####3.Twip的配置

	$ git clone git@github.com:twip/twip.git twip //从github下载twip源码

修改key，secret，basic-url值（格式为https://xxxx-usename.dotcloud.com/,xxxx为上一步创建的app名，切记后面的/不能少）

twip.php 第二行新建行输入

	error_reporting(0); 

然后在文件夹内添加新文档，内容为
	if (!-e $request_filename){rewrite ^/(.*)$ /index.php last;}
然后命名为 `nginx.conf`

新建文档，内容为
	www:
	  type: php //注意前边是两个空格，不能用tab键                                                                          
命名为`dotcloud.yml`

	$ dotcloud connect XXXX //与应用建立关联

####4.文件部署

在终端进twip文件所在文件夹，然后上传文件

	$ dotcloud push
	Deployment finished. Your application is available at the following URLs www: http://xxxx-usename.dotcloud.com/

然后浏览器访问这个地址，会显示空白，然后再访问

	http://xxxx-usename.dotcloud.com/index.html

出现twip4界面，搭建成功。



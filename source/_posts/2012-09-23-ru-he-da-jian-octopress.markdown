---
layout: post
title: "如何搭建octopress"
date: 2012-09-23 00:36
comments: true
categories: geek
---
在参考了许多资料之后，我终于也搭建出了octopress这个比较cooool的博客系统。所以第二篇日志就献给他了。希望可以帮助到那些需要搭建ocotopress的人，也为自己日后维护留下参考。（我是搭建在github pages上的所以这篇文章不会涉及其他的发布方式）

## 如何开始

1. 拥有一个[github](https://github.com)账号
2. 下载并安装git
3. 安装ruby（由于不同的系统环境有不同的安装方式，推荐用rvm）
4. 拥有一颗不怕折腾的心


## 第一步：本地安装octopress

1. 从github上把octopress拿到自己硬盘上  
`git clone git://github.com/imathis/octopress.git octopress`
2. 进入octopress的目录（如果用rvm的话这里会问你要不要用新版本的ruby，选yes就好）  
`cd octopress`
3. 安装依赖包  
`gem install bundler`  
这一步我卡了很久，因为我安装的ruby貌似少了一些东西。所以在安装ruby前应该按照列表把一些必要的包安装到位。  
`bundle install`
4. 安装octopress  
`rake install`
5. 这个时候你的网站应该已经生成了。输入命令`rake preview`来搭建临时的本地服务器。然后在[127.0.0.1:4000](http://127.0.0.1:4000)中查看是否成功。

## 第二步：部署到github pages

1. 在github的个人设置里添加ssh keys(根据github的指南来吧)
2. 创建一个git，名字叫"xxxxxx.github.com",如图。  
![image](http://ww1.sinaimg.cn/large/a74ecc4cjw1dx5srhrfy1j.jpg)
3. 输入命令`rake setup_github_pages`  
之后程序会问你你的git地址，根据提示输入就好。  
这是程序会帮助你生成github的二级域名，帮你管理这个git。  
如果成功的话，你应该会立刻在你github绑定的邮箱中收到一封邮件
4. 现在就是生成博客并上传的时候了  
`rake gen_deploy`  
至此，部署就完成了。

## 第三步：配置octopress，并开始博客
1. 在octopress的目录下有个文件_config.yml，这是octopress的控制中心，更改你所需要的内容，然后`rake preview`。
2. 发布新的博客  
`rake new_post["your post article"]`  
这会在`source/_post/`下生成一个markdown文件。  
之后你只需编辑这个文件即可书写博文。
3. 完成更改  
在每一次写完博客或作出更改后都应该使用`rake gen_deploy`来发布内容。  
并且在github上push source分支  
方法如下：  
`git add .`  
`git commit -m "changes you made"`  
`git push origin source`

## 小结
github pages所提供的空间，稳定无限制。不过最大的缺点是有非常长的缓存更新时间。一些更改作出之后，不刷新浏览器是看不到更改的。所以，如果你有虚拟空间或者vps的话，还是推荐使用自己的。更多的内容可以google或者访问[octopress.org](http://octopress.org)来获取。
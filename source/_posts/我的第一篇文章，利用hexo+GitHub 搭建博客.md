---
title: 利用hexo+GitHub 搭建博客
date: 2018-08-24 19:30:06
categories: 项目
tags:
- hexo
- GitHub
- 博客
- next
---


# 为什么要搭建自己的博客呢#
----------
> 种一棵树最好的时候是十年前，其次是现在




## 两个原因 ##
- 想有一个属于自己的写文章的地方
- 身为一个程序员这还需要理由吗？


 这篇文章不是教程，只是搭建博客的过程中的一些感受，
首先特别感谢
吴润的知乎专栏 [https://zhuanlan.zhihu.com/p/26625249](https://zhuanlan.zhihu.com/p/26625249 "吴润的专栏-GitHub+Hexo 搭建个人网站详细教程")

以及
jmyblog 的博客
[http://jmyblog.top](http://jmyblog.top "Hexo+GithubPages&CodingPages搭建自己的个人博客")

nMask's 的博客
[https://thief.one](https://thief.one)

我的博客是参考了这两篇文章搭建好的，期间也遇到了很多莫名其妙的bug
好在有万能的Google，在此建议想要搭建博客的同学一定要有耐心，出问题是必然的，不要担心，你遇到的坑很多人都遇到过，所以请保持一个平常心。接下来是我总结的搭建过程，比较简洁。

----------

# 搭建博客步骤

1. 获得个人网站域名（阿里云）
2. GitHub创建个人仓库
3. 安装Git 和 Node.js
4. 安装Hexo
5. 推送网站
6. 绑定域名
7. 个性化设置

# 具体的搭建过程参考上面的几篇文章，我的建议和遇到的bug是：
- 域名买一个简单并且便宜的，我在阿里云买了一个.top的，只要5/年。
- 在安装Hexo这一步，hexo init blog之后的命令都是在blog/blog这个目录下进行的，一定要注意，不能弄错了。
- 如果你在安装Hexo或者之前的步骤中有报错，建议你重新下载安装。因为这之前的过程全是安装的部分，一旦出错，没有别的原因，一定是你的操作有问题。而且你解决错误的时间一定要比重新安装耗费的时间长。
- 关于Markdown，建议用文中推荐的markdownPad2，下载后预览功能不能使用的问题需要下载awesomium插件,部分功能要升级到专业版才可以使用。
- 域名绑定时遇到了问题，只能采取A 记录， 映射到haitang10.github.io 的IP地址。
- next主题竟然改地址了，可恶！！！ 新地址为[https://github.com/theme-next](https://github.com/theme-next)，
`git clone https://github.com/theme-next/hexo-theme-next themes / next`


# 个性化
参考 next文档[http://theme-next.iissnan.com/getting-started.html](http://theme-next.iissnan.com/getting-started.html)

# 友情链接 #
- [https://www.jianshu.com/p/0c3663c4f0ef](https://www.jianshu.com/p/0c3663c4f0ef)
- 
未完，待续

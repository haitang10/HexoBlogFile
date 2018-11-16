---
title: 博客个性化设置
date: 2018-08-25 15:30:06
categories: 项目
tags:
- 博客
- next
---
# next 主题 个性化设置 #

![](https://haitang10-blog.oss-cn-beijing.aliyuncs.com/next.jpg?Expires=1538746238&OSSAccessKeyId=TMP.AQGgfSbZJ_lWknMIdblvXuFuAdUPVBfxMAZ_VruW6QLImiJYH-E5rdlglhAsADAtAhUAgTLUEMO7IGAEy3dQ1-zXvRJdI5kCFD1wf7QWp_gUr_SfpquzL0wNFyS8&Signature=XXLUdaL7jezOrrRcrZXOtIXEk40%3D)

<!-- more -->
参考资料

next 常见问题

 [http://theme-next.iissnan.com/faqs.html](http://theme-next.iissnan.com/faqs.html "next常见问题")

nMask 的博客

[https://thief.one/2017/03/03/Hexo搭建博客教程/](https://thief.one/2017/03/03/Hexo搭建博客教程/ "nMask 的博客")

为NexT主题添加文章阅读量统计功能

[https://notes.wanghao.work](https://notes.wanghao.work)

33种个性化设置，打造炫酷网站

[http://shenzekun.cn/hexo主题个性化配置教程.html](http://shenzekun.cn/hexo主题个性化配置教程.html)

----------


# 首先是主题的一些简单设定，主要是更改站点配置文件和主题配置文件，包括： #
- 选择主题和语言
- 菜单项和图标
- 头像，选择图片路径
- 站点描述
- 添加标签和分类页面
- 设置字体（没有设置）
- 侧边栏social连接（此处有bug）
- 打赏功能
- 腾讯404页面
- 动画（未设置）

# 第三方服务 #
- 评论系统（来必力）
- 搜索服务（采用Local Search）
- 数据统计和分析，统计浏览人数和文章阅读次数


# 进阶内容 #

- 设置阅读全文，在文章中使用 <!-- more --> 手动进行截断，
- 图床（七牛云）
- 文章加密访问
- 鼠标点击小红心
- 异地同步博客内容
- 加上宠物，npm install hexo-helper-live2d


----------
# 遇到的坑 #

## leancloud 无法加载##
leancloud 无法加载，原因是缺少security 这个安全插件，用来修复计数中存在的安全漏洞。

    A plugin to fix a serious security bug in leancloud visitor counter for
	NexT theme site and other site that integrated this function using a similar way.

具体信息请看 GitHub文档[https://github.com/theme-next/hexo-leancloud-counter-security](https://github.com/theme-next/hexo-leancloud-counter-security)

修复此问题见[https://github.com/theme-next/hexo-theme-next/blob/master/docs/zh-CN/LEANCLOUD-COUNTER-SECURITY.md](https://github.com/theme-next/hexo-theme-next/blob/master/docs/zh-CN/LEANCLOUD-COUNTER-SECURITY.md)

## 某些主题设置不会立即生效，请耐心等待几分钟！！！ ##

## 返回顶部按钮在屏幕尺寸小于991px时自动隐藏 ##
在移动端发现没有返回顶部按钮，调试时发现在页面宽度小于991px时，存在下列css 代码：

    media (min-width: 768px) and (max-width: 991px) {
  	.back-to-top {
    display: none !important;
  		}
	}
	@media (max-width: 767px) {
  	.back-to-top {
    display: none !important;
  		}
	}
解决办法：

在`\themes\next-reloaded\source\css\_common\components`
中的`back-to-top.styl`和 `back-to-top-sidebar.styl`文件中删除

    
  	+tablet() {
    	fixbutton() if hexo-config('sidebar.onmobile');
    	hide() if not hexo-config('sidebar.onmobile');
  		}
  	+mobile() {
    	fixbutton() if hexo-config('sidebar.onmobile');
    	hide() if not hexo-config('sidebar.onmobile');
 		}

出现这个现象的原因是在 

`\themes\next-reloaded\source\css\_common\scaffolding\mobile.styl` 

文件中存在这几行代码

     > 768px & < 991px
		+tablet() {
		}
	 < 767px
		+mobile() {
		}



导致在页面宽度小于991px时返回顶部按钮消失


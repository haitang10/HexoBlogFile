---
title: DOM操作中的querySelector和getElementsby 的区别
date: 2018-09-05 10:03:02
tags: 
- js
- DOM
- querySelector

categories: 学习笔记
password:
---

> 首先，什么是DOM？

<!-- more -->

# DOM概述 #
## DOM ##
DOM 是 JavaScript 操作网页的接口，全称为“文档对象模型”（Document Object Model）。它的作用是将网页转为一个 JavaScript 对象，从而可以用脚本进行各种操作（比如增删内容）。

浏览器会根据 DOM 模型，将结构化文档（比如 HTML 和 XML）解析成一系列的节点，再由这些节点组成一个树状结构（DOM Tree）。所有的节点和最终的树状结构，都有规范的对外接口。每一个节点都是一个对象，有各自的属性和方法。

DOM 只是一个接口规范，可以用各种语言实现。所以严格地说，DOM 不是 JavaScript 语法的一部分，但是 DOM 操作是 JavaScript 最常见的任务，离开了 DOM，JavaScript 就无法控制网页。另一方面，JavaScript 也是最常用于 DOM 操作的语言。后面介绍的就是 JavaScript 对 DOM 标准的实现和用法。

## 节点（node） ##

DOM 的最小组成单位叫做节点（node）。文档的树形结构（DOM 树），就是由各种不同类型的节点组成。每个节点可以看作是文档树的一片叶子。

节点的类型有七种。

- Document：整个文档树的顶层节点
- DocumentType：doctype标签（`<!D``OCTYPE html>`）
- Element：网页的各种HTML标签(`<body>`)
- Attribute：网页元素的属性（比如`class="right"`）
- Text：标签之间或标签包含的文本
- Comment：注释
- DocumentFragment：文档的片段

  浏览器提供一个原生的节点对象Node，上面这七种节点都继承了Node，因此具有一些共同的属性和方法。


## 关于node节点的详细内容如下 ##
[https://wangdoc.com/javascript/dom/general.html](https://wangdoc.com/javascript/dom/general.html)


# 操作节点异同#

document节点对象代表整个文档，每张网页都有自己的document对象，document对象还有很多自己的属性和方法。这里我们只涉及操作节点的方法。
今天讨论的两个方法有各自的优点和缺点，querySelector 方便，因为它是接受选择器作为参数，可以直接定位到要选择的元素，无需多次getElementby
而后者性能更好，鱼与熊掌，不可兼得。
## document.querySelector()  ##

document.querySelector方法接受一个 CSS 选择器作为参数，返回匹配该选择器的元素节点。如果有多个节点满足匹配条件，则返回第一个匹配的节点。如果没有发现匹配的节点，则返回null。

    var el1 = document.querySelector('.myclass');
	var el2 = document.querySelector('#myParent > [ng-click]');

document.querySelectorAll方法与querySelector用法类似，区别是返回一个NodeList对象，包含所有匹配给定选择器的节点。
这两个方法都支持复杂的 CSS 选择器。

	// 选中 data-foo-bar 属性等于 someval 的元素
	document.querySelectorAll('[data-foo-bar="someval"]');

	// 选中 myForm 表单中所有不通过验证的元素
	document.querySelectorAll('#myForm :invalid');

	// 选中div元素，那些 class 含 ignore 的除外
	document.querySelectorAll('DIV:not(.ignore)');

	// 同时选中 div，a，script 三类元素
	document.querySelectorAll('DIV, A, SCRIPT');
	
但是，它们不支持 CSS 伪元素的选择器（比如:first-line和:first-letter）和伪类的选择器（比如:link和:visited），即无法选中伪元素和伪类。

如果querySelectorAll方法的参数是字符串*，则会返回文档中的所有元素节点。另外，querySelectorAll的返回结果不是动态集合，不会实时反映元素节点的变化。

最后，这两个方法除了定义在document对象上，还定义在元素节点上，即在元素节点上也可以调用。
## document.getElementsBy ##
这个方法有 
- document.getElementsByTagName()
- document.getElementsByClassName()
- document.getElementsByName()
- document.getElementById() （只能用在document上，不能element）

## 不同点 ##


1. querySelectorAll 返回的是一个 静态节点集合Static Node List，而 getElementsBy 系列的返回的是一个动态的集合 Live Node List。两种方法的区别就在于这个集合会不会自动更新。
	
		x = document.querySelectorAll('img')
		y = document.getElementsByTagName('img')
		document.body.appendChild(new Image())
		x.length // 0
		y.length // 1


2. 实际上getElementsBy 返回的是HTMLcollection 对象。二者区别在于NodeList 对象会包含文档中的所有节点，如 Element、Text 和 Comment 等。HTMLCollection 对象只会包含文档中的 Element 节点。

		var ul = document.getElementsByTagName('ul')[0],
	    lis1 = ul.childNodes,
	    lis2 = ul.children;
		console.log(lis1.toString(), lis1.length);    // "[object NodeList]" 11
		console.log(lis2.toString(), lis2.length);    // "[object HTMLCollection]" 4




3. getElementBy系列的执行速度基本都是querySelectorAll的100+倍
4. elem.children和elem.childNodes的区别？
elem.children属于html集合接口，将返回一个当前节点的所有子元素的动态的伪数组（元素节点）
elem.childNodes属于NodeList接口，将分返回一个当前节点的所有子节点的伪数组（所有子节点）






----------


参考资料： 

[https://www.zhihu.com/question/24702250](https://www.zhihu.com/question/24702250)

[https://wangdoc.com/javascript/dom/general.html](https://wangdoc.com/javascript/dom/general.html)
	
---
title: js的作用域与声明提升
date: 2018-09-06 17:15:56
tags:
- 作用域
- js

categories: 学习笔记
password:
---
# js的作用域问题 #

## 首先js没有块级作用域（ES6中实际上增加了这一点） ##

<!-- more -->

1.在es5中，js没有块级作用域，意思是函数内部可以读取全局变量，并且函数内部的变量（局部变量）可以覆盖掉全局变量的值！！这一点非常令人头疼。

看例子 

    　var n=1
	  function f1(){
		alert(n);
     }
	 f1(); // 1

函数f1中并没有定义n 这个变量，但是还是正确输出了，为什么？因为alert(n)会先在函数内部查找1是否声明n,2是否赋值n,没有找到，自动查找外层，找到全局变量n。这就是作用域链，先在内部查找，没有的话逐步向外层寻找。

2。函数外部无法读取函数内部变量（局部变量），当然可以采用闭包的形式，这一点不难理解。

## 局部变量可以覆盖全局变量 ##
    
首先说明一点，在函数内部如果不声明变量，实际上定义的是全局变量，bb的值被改变例如  

	`bb = 1;
	function aa(cc) {
      bb = 2;
    console.log(bb);
	};
	aa(bb); //2
	console.log(bb)`//2
但是如果声明了局部变量（无论是传参数还是使用var，都声明了一个新的变量）函数运行时会在内存中新建一个名为bb的变量，函数内部的操作只对新的bb产生影响，只在函数内部有效，函数结束时变量被释放。不会影响到全局变量bb。这一点从作用域来解释是函数内的console.log() 执行的时候要先在函数内部寻找bb，发现已经声明，并且赋值，就不会再向上层去寻找了，作用域链停止在函数内。

    bb = 1;
	function aa(bb) {     
      bb = 2;
    console.log(bb);
	};
	aa(bb); //2
	console.log(bb)//1


下面的代码也是同样的效果,因为用var 声明了bb，在内存中新建了bb变量。函数内对bb的操作不会影响到全局的bb

	 bb = 1;
	function aa(cc) {
      var bb = 2;
    console.log(bb);
	};
	aa(bb);//2
	console.log(bb)//1

归根到底，是js作用域链的问题。可参考
[https://www.bbsmax.com/A/B0zq64o3Jv/](https://www.bbsmax.com/A/B0zq64o3Jv/)
这篇文章对作用域链的理解较为深刻。

所以建议函数内部的变量都要用var来声明，并且要先声明后调用（var竟然存在变量声明提升！！！）！避免同全局变量产生冲突。

# js中声明提升的问题 #

这个问题可以参考

[http://www.cnblogs.com/damonlan/archive/2012/07/01/2553425.html](http://www.cnblogs.com/damonlan/archive/2012/07/01/2553425.html)



简单来说，就是作用域链底层的变量或函数被提升到了顶层（也可以说顶层到底层，没有关系）

变量提升

    var a = 1
	var f1 = function() {
		console.log(a)
		var a = 2
	}
	f1() // undefined

首先看a的作用域链  f1> global ，按理说console.log之前并没有声明a ，应该去global找，但实际上因为 `var a = 2` 的存在，使得a 的声明被提升，但并没有赋值，所以在f1的作用域可以找到a，只是没有赋值，所以输出undefined，所以一定要先声明后调用！！！

用let代替var！！！


函数声明提升看这里

[https://github.com/Wscats/Good-text-Share/issues/73](https://github.com/Wscats/Good-text-Share/issues/73)

经典代码

    getName()//oaoafly 
	函数被提升 这里受函数声明的影响，虽然函数声明在最后可以被提升到最前面了
	var getName = function() {
	console.log('wscat')
	}
	//函数表达式此时才开始覆盖函数声明的定义
	getName()//wscat
	function getName() {
	console.log('oaoafly')
	}
	getName()//wscat 这里就执行了函数表达式的值
	
	// 结果是 oaoafly   wscat  wscat

> JavaScript 解释器中存在一种变量声明被提升的机制，也就是说函数声明会被提升到作用域的最前面，即使写代码的时候是写在最后面，也还是会被提升至最前面。
而用函数表达式创建的函数是在运行时进行赋值，且要等到表达式赋值完成后才能调用


		console.log(g)//undefined
        var g = 1;
		getName()//Uncaught TypeError: getName is not a function
		var getName = function() {
			console.log('wscat')
		}

为什么会这样？   

原因是var 声明了g这个变量，导致其提升，而var getName = function(){} 
并没有声明一个函数，而是把一个匿名函数赋值给了getName.

	只有声明才会提升，函数表达式并未声明一个函数。


> 总结：Javascript中函数声明和函数表达式是存在区别的，函数声明在JS解析时进行函数提升，因此在同一个作用域内，不管函数声明在哪里定义，该函数都可以进行调用。而函数表达式的值是在JS运行时确定，并且在表达式赋值完成后，该函数才能调用。这个微小的区别，可能会导致JS代码出现意外

参考资料：

 [https://www.bbsmax.com/A/B0zq64o3Jv/](https://www.bbsmax.com/A/B0zq64o3Jv/)

----------
下一节写关于闭包的问题。。。。。
头疼！！！！
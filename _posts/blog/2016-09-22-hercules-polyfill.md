---
layout: post
title: hercules polyfill 
description: 
category: blog
---


## 概述

hercules polyfill 

下载地址

[hercules polyfill](http://wikieswan.github.io/vera3/build/hercules.polyfill.js)


h5 页面常用的场景是嵌入特卖会的 app 中。嵌入特卖会的app的h5页面，如果需要和app交互，就需要引入 Hercules 库。一般为了更好的交互效果，对于嵌入app的h5页面，我们会选择优先使用app提供的交互组件，比如：loading、dialog、toast。

为了能保证同样的写法能再app和浏览器中同时能使用，我们开发了一个叫做 hercules.polyfill.js 的库，弥补了app和浏览器调用这些组件的鸿沟。 

- 注意，hercules.polyfill.js 可以单独使用，不依赖 vera 、jquery 或者 zepto。



### 使用方法

引入app那边提供的 hercules.js，然后引入 hercules.polyfill.js

	<script type="text/javascript" src="path/to/hercules.js"></script>
	<script type="text/javascript" src="path/to/hercules.polyfill.js"></script>
	<script type="text/javascript">
		//入口文件出，判断h5所在的环境，给 hercules.polyfill.js 传递标志
		// 一般是根据 url 中是否含有 特卖会 对url的处理 source=app
		//如果没有这个处理，默认是 h5
		var isInApp = xxxx 
		VHPF.ui.env = isInApp?'app':'h5'
		//之后 VHPF 会根据 VHPF.ui.env ，选择是否使用特卖会的 ui 组件
	</script>


### api

0 设置入口

	//入口文件出，判断h5所在的环境，给 hercules.polyfill.js 传递标志
	// 一般是根据 url 中是否含有 特卖会 对url的处理 source=app
	//如果没有这个处理，默认是 h5
	var isInApp = xxxx 
	VHPF.ui.env = isInApp?'app':'h5'
	//之后 VHPF 会根据 VHPF.ui.env ，选择是否使用特卖会的 ui 组件

1 Toast
	
	//显示一个 toast 3s 消失
	VHPF.ui.showToast({
		content: '修改密码成功'
	})


2 Loading

	VHPF.ui.showLoading() //显示loading 

	VHPF.ui.hideLoading() //隐藏loading

3 Dialog

	//显示一个底部有两个按钮的 dialog
	var param ={
        content: "为了你的账户安全，请先进行实名认证",
        buttonType: "BUTTON_TYPE_LEFTRIGHT",//BUTTON_TYPE_CENTER BUTTON_TYPE_LEFTRIGHT
        buttonLeftText: "取消",
        buttonLeftEventMethod: function(){},
        buttonRightText: "去认证",
        buttonRightEventMethod: function(){
        	alert("去认证")
        }
    }
    VHPF.ui.showDialog(param)

    //显示一个底部有一个按钮的 dialog 
	var param ={
        content: "网络异常，请重试",
        buttonType: "BUTTON_TYPE_CENTER",//BUTTON_TYPE_CENTER BUTTON_TYPE_LEFTRIGHT
        buttonCenterText: "取消",
        buttonCenterEventMethod: function(){}
    }
    VHPF.ui.showDialog(param)

4 nav

嵌入特卖会app 的页面跳转是不能使用 location.href = 'xxxx' 来进行页面跳转的。前端必须模拟一个 a 标签的点击事件来进行跳转，否则页面跳转后表现是不正常的。为了更加方便页面跳转， VHPF 还提供一个跳转函数

	//url 可以是一个 h5 url 地址或者是 -1
	VHPF.nav.goto(url)



### 效果如下

[hercules.polyfill.js](http://wikieswan.github.io/vera3/example/index.html#herculespolyfill)

<iframe src="http://wikieswan.github.io/vera3/example/index.html#herculespolyfill"
 style="width:375px; height: 667px;border: 2px solid #ddd;border-bottom: 50px solid #6D6767;border-top: 50px solid #6D6767;border-radius: 10px;"></iframe>



关于特卖会提供的 hercules.js 详细信息，可以参考下面的链接


hercules 相关的文档

[http://wiki.corp.vipshop.com/pages/viewpage.action?pageId=91001767](http://wiki.corp.vipshop.com/pages/viewpage.action?pageId=91001767)

[http://wiki.corp.vipshop.com/pages/viewpage.action?pageId=74752365&src=search](http://wiki.corp.vipshop.com/pages/viewpage.action?pageId=74752365&src=search)

[http://gitlab.tools.vipshop.com/h5_dev/hercules/blob/master/1/index.js](http://gitlab.tools.vipshop.com/h5_dev/hercules/blob/master/1/index.js)
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

	VHPH.ui.env = 'app' //'app'|'h5'

	/**
	 弹出Toast提示
	 param:{
		    content: ""
		}
	 **/
	VHPH.ui.showToast(param)

	/**
	 弹出App Dialog提示
	 param:{
		    content: "",
		    buttonType: "", //string BUTTON_TYPE_CENTER: 中间一个按钮类型  BUTTON_TYPE_LEFTRIGHT: 左右两边都存在按钮类型
		    buttonCenterText: "",//string ,buttonType 为 BUTTON_TYPE_CENTER 时必传
		    buttonCenterEventMethod: function() {},function ,buttonType 为 BUTTON_TYPE_CENTER 时必传
		    buttonLeftText: "", //string ,buttonType 为 BUTTON_TYPE_LEFTRIGHT 时必传
		    buttonLeftEventMethod: function() {}, //function(),buttonType 为 BUTTON_TYPE_LEFTRIGHT 时必传
		    buttonRightText: "", //string ,buttonType 为 BUTTON_TYPE_LEFTRIGHT 时必传
		    buttonRightEventMethod: function() {} //function() ,buttonType 为 BUTTON_TYPE_LEFTRIGHT 时必传
		}
	 **/
	VHPH.ui.showDialog(param)

	/**
	 弹出loading提示
	 **/
	VHPH.ui.showLoading()

	/**
	 隐藏loading提示
	 **/
	VHPH.ui.hideLoading()

	//跳转到新页面,-1 或者 str
	VHPH.nav.goto(url)


### 效果如下

[hercules.polyfill.js](http://wikieswan.github.io/vera3/example/index.html#herculespolyfill)

<iframe src="http://wikieswan.github.io/vera3/example/index.html#herculespolyfill"
 style="width:375px; height: 667px;border: 2px solid #ddd;border-bottom: 50px solid #6D6767;border-top: 50px solid #6D6767;border-radius: 10px;"></iframe>



关于特卖会提供的 hercules.js 详细信息，可以参考下面的链接


hercules 相关的文档

[http://wiki.corp.vipshop.com/pages/viewpage.action?pageId=91001767](http://wiki.corp.vipshop.com/pages/viewpage.action?pageId=91001767)

[http://wiki.corp.vipshop.com/pages/viewpage.action?pageId=74752365&src=search](http://wiki.corp.vipshop.com/pages/viewpage.action?pageId=74752365&src=search)

[http://gitlab.tools.vipshop.com/h5_dev/hercules/blob/master/1/index.js](http://gitlab.tools.vipshop.com/h5_dev/hercules/blob/master/1/index.js)
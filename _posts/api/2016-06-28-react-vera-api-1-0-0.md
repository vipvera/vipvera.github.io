---
layout: post
title:  react vera component 1.0.0 api
category: api
description: react vera component 1.0.0版本的api文档
---

## 写在前面

### 代码地址

1 vera component 源码地址

	git@gitlab.tools.vipshop.com:wikies.wan/vera.git

	分支 react-vera

2 样例地址：

	git@gitlab.tools.vipshop.com:wikies.wan/vera-react-demo.git

	分支 master


### 使用方法

采用 git clone 方式进行代码同步，具体操作的 gulp task


	gulp.task('vera', function(){
	    del('./lib/vera')
	    setTimeout(function(){
	        exe('cd lib && git clone git@gitlab.tools.vipshop.com:wikies.wan/vera.git && cd vera && git checkout react-vera',function(){
	            del('./lib/vera/.git')
	            del('./lib/vera/.gitignore')
	        })
	    },1000)
	})

作用是在项目根目录下的 lib 新增一个最新的 vera 代码 ，生成路径 /lib/vera

### 组件开发原则

Redux 和 React 是没有必然关系的，Redux 用于管理 state，与具体的 View 框架无关。不过，Redux 特别适合那些 state => UI 的框架（比如：React, Deku）。

可以使用 react-redux 来绑定 React，react-redux 绑定的组件我们一般称之为 smart components，Smart and Dumb Components 在 react-redux 中区分如下：

组件分为两种：smart component vs dumb component

  null | Location | Use React-Redux | To read data, they | To change data, they
 ----|----|----|----|----
 “Smart” Components	 | Top level, route handlers	 | Yes	 | Subscribe to Redux state | 	Dispatch Redux actions
“Dumb” Components | Middle and leaf components | 	No | 	Read data from props | 	Invoke callbacks from props

简单来看：Smart component` 是连接 Redux 的组件（@connect），一般不可复用。Dumb component 是纯粹的组件，一般可复用。
两者的共同点是：无状态，或者说状态提取到上层，统一由 redux 的 store 来管理。redux state -> Smart component -> Dumb component -> Dumb component（通过 props 传递）。在实践中，少量 Dumb component 允许自带 UI 状态信息（组件 unmount 后，不需要保留 UI 状态）。
值得注意的是，Smart component 是应用更新状态的最小单元。实践中，可以将 route handlers 作为 Smart component，一个 Smart component 对应一个 reducer。

为了开发可复用的组件，首先要保证组件的 dumb component 性。组件状态的管理分为两部分：自有状态和 store 状态。划分组件状态的原则是：需要外部传递进来的用 store 状态，否则是自有状态。

组件只实现 view 层——传递什么样的state就展示什么样的UI，事件句柄传递的是什么函数就执行对应的 callback 。这样，组件保持自己的独立性，与 store 的设计和 action 的操作都没有关系，开发者只要实现对应的 store 或者 action 就可以了。

api 详情如下

## 栅格系统

同vera2.0

## Header

### 用法：

	import Header from '../lib/vera/Header'
	....
	<Header text="快捷支付" isBack={true} isClose={true}/>

### 参数	

	Header.propTypes = {
	  text: PropTypes.string.isRequired,
	  isBack: PropTypes.bool.isRequired,
	  isClose: PropTypes.bool.isRequired
	}

+ text 展示的文字

+ isBack 是否带返回箭头

+ isClose 是否带关闭按钮

## Button










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










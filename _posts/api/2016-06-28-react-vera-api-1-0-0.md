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

## Header页头

### 用法：

	import Header from '../lib/vera/Header'
	....
	<Header text="快捷支付" isBack={true} isClose={true}/>

### 参数:	

	Header.propTypes = {
	  text: PropTypes.string.isRequired,
	  isBack: PropTypes.bool.isRequired,
	  isClose: PropTypes.bool.isRequired
	}

+ text 展示的文字

+ isBack 是否带返回箭头

+ isClose 是否带关闭按钮

## Banner横幅

### 用法：

	<div className="banner">这是一个默认的 banner 条</div>

### 参数：

    无

## Button按钮

### 用法：

	import Button from '../components/vera/Button'
	...
	<Button text="确定" isAble={stores.pub.mybtnBlock} handleClick={actions.fetchUserName}/>

### 参数：
	
	Button.propTypes = {
	  text: PropTypes.string.isRequired,
	  isAble: PropTypes.bool.isRequired,
	  handleClick: PropTypes.func
	}

	+ text 按钮上文字

	+ isAble 是否可点击

	+ handleClick 按钮点击事件

## Radio单选框

### 用法：

	import Radio from '../components/vera/Radio'
	import RadioButton from '../components/vera/RadioButton'
	...
	<Radio handleToggle={actions.toggleRadioGroup}>
      <RadioButton text={stores.pub.myRadioGroup.group[0].text} isDisabled={stores.pub.myRadioGroup.group[0].isDisabled} isChecked={stores.pub.myRadioGroup.group[0].isChecked} value={stores.pub.myRadioGroup.group[0].value} ></RadioButton>
      <RadioButton text={stores.pub.myRadioGroup.group[1].text} isDisabled={stores.pub.myRadioGroup.group[1].isDisabled} isChecked={stores.pub.myRadioGroup.group[1].isChecked} value={stores.pub.myRadioGroup.group[1].value}></RadioButton>
      <RadioButton text={stores.pub.myRadioGroup.group[2].text} isDisabled={stores.pub.myRadioGroup.group[2].isDisabled} isChecked={stores.pub.myRadioGroup.group[2].isChecked} value={stores.pub.myRadioGroup.group[2].value} ></RadioButton>
      <RadioButton text={stores.pub.myRadioGroup.group[3].text} isDisabled={stores.pub.myRadioGroup.group[3].isDisabled} isChecked={stores.pub.myRadioGroup.group[3].isChecked} value={stores.pub.myRadioGroup.group[3].value} ></RadioButton>
    </Radio>

### 参数：

	Radio.propTypes = {
	  handleToggle: PropTypes.func.isRequired,
	  children: childrenPropType
	}

	+ handleToggle 单选点击事件，返回当前单选框组选中的项value值

	RadioButton.propTypes = {
	  text: PropTypes.string.isRequired,
	  value: PropTypes.string.isRequired,
	  isChecked: PropTypes.bool,
	  isDisabled: PropTypes.bool
	}

	+ text 单选选项文字

	+ value 单选选项值

	+ isChecked 单选选项是否已选中，可不填写，默认未选中

	+ isDisabled 单选选项是否可选，可不填写，默认可选

## Checkbox多选框

### 用法：

	import Checkbox from '../components/vera/Checkbox'
	...
	 <Checkbox text={stores.pub.myCheckboxList[0].text} isDisabled={stores.pub.myCheckboxList[0].isDisabled } isChecked={stores.pub.myCheckboxList[0].isChecked} handleToggle={actions.toggleCB1}></Checkbox>

### 参数：

	Checkbox.propTypes = {
	  text: PropTypes.string.isRequired,
	  isDisabled: PropTypes.bool,
	  isChecked: PropTypes.bool,
	  handleToggle: PropTypes.func.isRequired
	}

	+ text 多选框选项文字

	+ isDisabled 多选框是否可选，可不填写，默认可选

	+ isChecked 多选框是否已选中，可不填写，默认未选中

	+ handleToggle 多选框点击事件，返回当前选项是否选中

## Input输入框

### 用法：

	import Input from '../components/vera/Input'
	...
	<Input value={stores.pub.myIpt.val} type="password" placeholder="用户名" id="myIpt" isError={stores.pub.myIpt.isError} writeValue={actions.myIptValue}/>

### 参数：

	Input.propTypes = {
	  id: PropTypes.string.isRequired,
	  type: PropTypes.string.isRequired,
	  placeholder: PropTypes.string.isRequired,
	  isError: PropTypes.bool.isRequired,
	  writeValue: PropTypes.func.isRequired
	}

	+ id 输入框ID

	+ type 输入框类型，同html input原生类型

	+ placeholder 输入框未输入时默认显示文字

	+ isError 输入框是否报错显示

	+ writeValue 输入框值有变化时的事件，返回输入框内容

## IdentifyingCodeInput获取验证码输入验证码

### 用法：

	import IdentifyingCodeInput from '../components/vera/IdentifyingCodeInput'
	...
	<IdentifyingCodeInput id="myIdentifying" writeValue={actions.writeIdentifyCode} getIdentifyCode={actions.fetchIdentifyCode}/>

### 参数：







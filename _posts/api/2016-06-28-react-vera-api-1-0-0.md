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

+ isBack 是否带返回箭头，bool类型true/false

+ isClose 是否带关闭按钮，bool类型true/false

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

+ isAble 是否可点击，bool类型true/false

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

+ handleToggle 单选点击事件，返回当前单选框组选中的项value值！

### 
	RadioButton.propTypes = {
	  text: PropTypes.string.isRequired,
	  value: PropTypes.string.isRequired,
	  isChecked: PropTypes.bool,
	  isDisabled: PropTypes.bool
	}

+ text 单选选项文字

+ value 单选选项值

+ isChecked 单选选项是否已选中，bool类型true/false，可不填写，默认未选中

+ isDisabled 单选选项是否可选，bool类型true/false，可不填写，默认可选

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

+ isDisabled 多选框是否可选，bool类型true/false，可不填写，默认可选

+ isChecked 多选框是否已选中，bool类型true/false，可不填写，默认未选中

+ handleToggle 多选框点击事件，返回当前选项是否选中！

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

+ isError 输入框是否报错显示，bool类型true/false

+ writeValue 输入框值变化事件，返回输入框内容！

## IdentifyingCodeInput获取验证码输入验证码

### 用法：

	import IdentifyingCodeInput from '../components/vera/IdentifyingCodeInput'
	...
	<IdentifyingCodeInput id="myIdentifying" writeValue={actions.writeIdentifyCode} getIdentifyCode={actions.fetchIdentifyCode}/>

### 参数：

	无

## Tab

### 用法：

	import Tab from '../components/vera/Tab'
	...
	<Tab lists={stores.pub.myTab} schemaTitle="tabButton" schemaContent="tabPanel"></Tab>

### 参数：

	Tab.propTypes = {
	  lists: PropTypes.array.isRequired,
	  schemaTitle: PropTypes.string.isRequired,
	  schemaContent: PropTypes.string.isRequired
	}

+ lists 给tab提供数据的列表，array类型

+ schemaTitle Tab的title绑定的数据字段

+ schemaContent Tab的panel绑定的数据字段

	例如myTab:[
        {tabButton:"信用卡",tabPanel:"Food truck fixie locavore, accusamus mcsweeney's marfa nulla single-origin coffee squid. Exercitation +1 labore velit, blog sartorial PBR leggings next level wes anderson artisan four loko farm-to-table craft beer twee. Qui photo booth letterpress, commodo enim craft beer mlkshk aliquip jean shorts ullamco ad vinyl cillum PBR. Homo nostrud organic, assumenda labore aesthetic magna delectus mollit. Keytar helvetica VHS salvia yr, vero magna velit sapiente labore stumptown. Vegan fanny pack odio cillum wes anderson 8-bit, sustainable jean shorts beard ut DIY ethical culpa terry richardson biodiesel. Art party scenester stumptown, tumblr butcher vero sint qui sapiente accusamus tattooed echo park."},
        {tabButton:"储蓄卡",tabPanel:"Raw denim you probably haven't heard of them jean shorts Austin. Nesciunt tofu stumptown aliqua, retro synth master cleanse. Mustache cliche tempor, williamsburg carles vegan helvetica. Reprehenderit butcher retro keffiyeh dreamcatcher synth. Cosby sweater eu banh mi, qui irure terry richardson ex squid. Aliquip placeat salvia cillum iphone. Seitan aliquip quis cardigan american apparel, butcher voluptate nisi qui."},
        {tabButton:"测试",tabPanel:"feafefaeefae"}
      ]

    按照移动端的业务需求，目前最多支持2个tab切换，如果输入更多，最多显示两个，剩余忽略

## Trace提示框

### 用法：

	import Trace from '../components/vera/Trace'
	...
	<Trace isShow={stores.pub.myTrace.traceBlock} text={stores.pub.myTrace.text} >this is trace</Trace>

### 参数：

	Trace.propTypes = {
	    text: PropTypes.string.isRequired,
	    isShow:PropTypes.string.isRequired
	}

+ text 提示框内显示文字

+ isShow 是否显示，string类型，需要显示的时候此值只要和上次不一样的字符串!

	例如{ isShow: new Date().getTime().toString() }

## Toast对话框

### 用法：

	import Toast from '../components/vera/Toast'
	...
	<Toast isShow={stores.pub.toastBlock} contentData={toast}>this is toast</Toast>

### 参数：

	Toast.propTypes = {
	    contentData: PropTypes.shape({
	      title: PropTypes.string,
	      text: PropTypes.string,
	      bottom:PropTypes.object.isRequired,
	    }).isRequired,
	    children: PropTypes.node,
	    isShow:PropTypes.bool.isRequired,
	}

+ contentData 对话框内的显示内容，必须有title 提示标题、text 提示内容、bottom 提示底部信息，例如底部可包含ok和cancel两个按钮相关显示信息和点击后的操作

	例如var toast = {
				      title:"提示信息",
				      text:"提示内容",
				      bottom:{
				        cancel:"cancel",
				        ok:"ok",
				        disabled:false,
				        okEvent:actions.myToastHide,
				        cancelEvent:actions.myToastHide
				      }
				    }

+ isShow 是否显示，bool类型true/false

## Dialoge对话框

### 用法：

	import Dialog from '../components/vera/Dialog'
	...
	<Dialog  isShow={stores.pub.dialogBlock} contentData={dialog}>
      	<h1>this is dialog </h1>
      	<Input 
	        value={stores.pub.myIpt.val} 
	        type="password"
	        placeholder="用户名"
	        id="myIpt"
	        isError={stores.pub.myIpt.isError}
	        writeValue={actions.myIptValue}/>
	         <p>this is dialog bottom</p>
    </Dialog>

### 参数：

	Dialog.propTypes = {
		contentData:PropTypes.shape({
		    title: PropTypes.string,
		    subTitle: PropTypes.string,
		    bottom:PropTypes.object.isRequired,
		}).isRequired,
		children: PropTypes.node,
		isShow:PropTypes.bool.isRequired,
	}

+ contentData 对话框显示的内容，可以有title 对话框标题、subTitle 对话框副标题，必须有bottom 底部信息例如cancel提供相关显示信息和点击后的操作

	例如var dialog = {
					    title:"提示信息",
					    subTitle:'子标题',
					    bottom:{
					        cancel:"cancel",
					        cancelEvent:actions.myDialogHide
					    }
					  }

+ isShow 是否显示，bool类型true/false

## Switcher开关

### 用法：

	import Switcher from '../components/vera/Switcher'
	...
	<Switcher isOn={stores.pub.mySwitcher.isOn} handleToggle={actions.toggleSwitcher}></Switcher>

### 参数：

	Switcher.propTypes = {
	    isOn:PropTypes.bool.isRequired,
	    handleToggle: PropTypes.func.isRequired
	}

+ isOn 是否开或关，bool类型true/false

+ handleToggle 开关点击事件





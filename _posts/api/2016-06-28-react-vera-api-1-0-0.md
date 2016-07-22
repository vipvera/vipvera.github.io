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

![header 图片示例](images/examples/react-header.gif)

### 用法：

	import Header from '../lib/vera/Header'
	....
	<Header 
		text="快捷支付" 
		isBack={true} 
		isClose={true}/>

### 参数:	

	Header.propTypes = {
	  	text: PropTypes.string.isRequired,
	  	isBack: PropTypes.bool.isRequired,
	  	isClose: PropTypes.bool.isRequired,
	  	closeText:PropTypes.string,
  		closeClick:PropTypes.func,
  		handleClick:PropTypes.func
	}

+ text 展示的文字

+ isBack 是否带返回箭头，bool类型true/false

+ isClose 是否带关闭按钮，bool类型true/false

+ closeText close按钮显示的文字

+ closeClick close按钮点击回调事件

+ handleClick 返回箭头点击回调事件

## Banner横幅

![banner 图片示例](images/examples/react-banner.gif)

### 用法：

	<div className="banner">这是一个默认的 banner 条</div>

### 参数：

    无

## MsgBannerHide定时隐藏横幅

![banner 图片示例](images/examples/react-hideBanner.gif)

### 用法：
	import MsgBannerHide from '../components/vera/MsgBannerHide'
	...
	<MsgBannerHide msgType="error" text={store.errorsBanner.text} isShow={store.errorsBanner.isShow} />

### 参数：

    Label.propTypes = {
	    msgType: PropTypes.string.isRequired,
	    text: PropTypes.string.isRequired,
	    isShow: PropTypes.bool.isRequired
	}

+ msgType 横幅类型，可选项有"error"和"info"

+ text 横幅显示文字

+ isShow 是否显示，bool类型true/false

## Button按钮

![btn 图片示例](images/examples/react-btn.gif)

### 用法：

	import Button from '../components/vera/Button'
	...
	<Button 
		text="确定" 
		isAble={stores.pub.mybtnBlock} 
		handleClick={actions.fetchUserName}/>

### 参数：
	
	Button.propTypes = {
	  	text: PropTypes.string.isRequired,
	  	isAble: PropTypes.bool.isRequired,
	  	handleClick: PropTypes.func
	}

+ text 按钮显示文字

+ isAble 是否可点击，bool类型true/false

+ handleClick 按钮点击事件

## Switcher开关

![switcher 图片示例](images/examples/react-switcher.gif)

### 用法：

	import Switcher from '../components/vera/Switcher'
	...
	<Switcher 
		isOn={stores.pub.mySwitcher.isOn} 
		handleToggle={actions.toggleSwitcher}>
	</Switcher>

### 参数：

	Switcher.propTypes = {
	    isOn:PropTypes.bool.isRequired,
	    handleToggle: PropTypes.func.isRequired
	}

+ isOn 是否开或关，bool类型true/false

+ handleToggle 开关点击事件

## Radio单选框

![radio 图片示例](images/examples/react-radio.gif)

### 用法：

	import Radio from '../components/vera/Radio'
	import RadioButton from '../components/vera/RadioButton'
	...
	<Radio handleToggle={actions.toggleRadioGroup}>
      	<RadioButton 
      		text={stores.pub.myRadioGroup.group[0].text} 
      		isDisabled={stores.pub.myRadioGroup.group[0].isDisabled} 
      		isChecked={stores.pub.myRadioGroup.group[0].isChecked} 
      		value={stores.pub.myRadioGroup.group[0].value} >
      	</RadioButton>
      	<RadioButton 
      		text={stores.pub.myRadioGroup.group[1].text} 
      		isDisabled={stores.pub.myRadioGroup.group[1].isDisabled} 
      		isChecked={stores.pub.myRadioGroup.group[1].isChecked} 
      		value={stores.pub.myRadioGroup.group[1].value}>
      	</RadioButton>
      	<RadioButton 
      		text={stores.pub.myRadioGroup.group[2].text} 
      		isDisabled={stores.pub.myRadioGroup.group[2].isDisabled} 
      		isChecked={stores.pub.myRadioGroup.group[2].isChecked} 
      		value={stores.pub.myRadioGroup.group[2].value} >
      	</RadioButton>
      	<RadioButton 
      		text={stores.pub.myRadioGroup.group[3].text} 
      		isDisabled={stores.pub.myRadioGroup.group[3].isDisabled} 
      		isChecked={stores.pub.myRadioGroup.group[3].isChecked} 
      		value={stores.pub.myRadioGroup.group[3].value} >
      	</RadioButton>
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

![checkbox 图片示例](images/examples/react-checkbox.gif)

### 用法：

	import Checkbox from '../components/vera/Checkbox'
	...
	<Checkbox 
	 	text={stores.pub.myCheckboxList[0].text} 
	 	isDisabled={stores.pub.myCheckboxList[0].isDisabled } 
	 	isChecked={stores.pub.myCheckboxList[0].isChecked} 
	 	handleToggle={actions.toggleCB1}>
	</Checkbox>

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

+ handleToggle 多选框点击事件，返回当前选项是否选中

## Select下拉框选项

![select 图片示例](images/examples/react-select.gif)

### 用法：

	import Select from '../components/vera/Select'
	...
	<Checkbox 
	 	text={stores.pub.myCheckboxList[0].text} 
	 	isDisabled={stores.pub.myCheckboxList[0].isDisabled } 
	 	isChecked={stores.pub.myCheckboxList[0].isChecked} 
	 	handleToggle={actions.toggleCB1}>
	</Checkbox>

### 参数：

	Select.propTypes = {
	    selected: PropTypes.string.isRequired,
	    placeholder: PropTypes.string.isRequired,
	    options: PropTypes.array.isRequired,
	    schemaLabel: PropTypes.string,
	    schemaValue: PropTypes.string,
	    onChange: PropTypes.func
	}

+ selected 下拉框选中value

+ placeholder 下拉框选项未选前占位文字

+ options 下拉框选项，array类型

+ schemaLabel 后选项label绑定字段，可缺省，则label和value同值

+ schemaValue 后选项value绑定字段，可缺省，则label和value同值

+ onChange 下拉框点选事件，返回选择项的value，可缺省

## Input输入框

![input 图片示例](images/examples/react-input.gif)
![input 图片示例](images/examples/react-input-pwd.gif)

### 用法：

	import Input from '../components/vera/Input'
	...
	<Input 
        id="myIpt" 
        type="text" 
        placeholder="用户名"
        isError={stores.pub.myIpt.isError} 
        writeValue={actions.myIptValue}
        blurFn={actions.blurIpt} />

### 参数：

	Input.propTypes = {
	  	id: PropTypes.string.isRequired,
	  	type: PropTypes.string.isRequired,
	  	placeholder: PropTypes.string.isRequired,
	  	isError: PropTypes.bool.isRequired,
	  	writeValue: PropTypes.func.isRequired,
	  	formatFn: PropTypes.func,
	  	blurFn: PropTypes.func,
	  	focusFn: PropTypes.func,
	  	inputFn: PropTypes.func
	}

+ id 输入框ID

+ type 输入框类型，同html input原生类型

+ placeholder 输入框未输入时默认显示文字

+ isError 输入框是否报错显示，bool类型true/false

+ writeValue 输入框值变化事件，返回输入框内容值

+ formatFn 输入框显示值经过格式化，例如手机号显示格式、身份证显示格式和，可缺省

+ blurFn 输入框失焦onBlur事件，返回输入框内容值，可缺省

+ focusFn 输入框聚焦onFocus事件，可缺省

+ inputFn 输入框onChange事件，返回输入框内容值，可缺省


## IdentifyingCodeInput获取验证码输入验证码

![identifyingCodeInput 图片示例](images/examples/react-identifyingCodeInput.gif)

### 用法：

	import IdentifyingCodeInput from '../components/vera/IdentifyingCodeInput'
	...
	<IdentifyingCodeInput
      	id="myIdentifying"
      	writeValue={actions.writeIdentifyCode}
      	getIdentifyCode={actions.fetchIdentifyCode}
      	isCounting={stores.pub.myIdentifyCode.countdown}
      	handleCount={actions.startIdentifyCodeCountdown}
      	handleDisCount={actions.stopIdentifyCodeCountdown}
      	isDisabled={stores.pub.myIdentifyCode.isDisabled}
      	handleAble={actions.identifyCodeBtnAbled}
      	handleDisable={actions.identifyCodeBtnDisabled}
      	isWithTitle={true}/>

### 参数：

	IdentifyingCodeInput.propTypes = {
	    id: PropTypes.string.isRequired,
	    writeValue: PropTypes.func.isRequired,
	    getIdentifyCode: PropTypes.func.isRequired,
	    isWithTitle: PropTypes.bool.isRequired,
	    isCounting: PropTypes.bool.isRequired,
	    handleDisCount: PropTypes.func.isRequired,
	    isDisabled: PropTypes.bool.isRequired,
	    handleAble: PropTypes.func.isRequired,
	    handleDisable: PropTypes.func.isRequired,
	    inputFn: PropTypes.func
	}

+ id 输入框ID

+ isWithTitle 是否显示左边“验证码”三个字，bool类型true/false

+ writeValue 输入框值变化事件，返回输入框内容！

+ getIdentifyCode 点击“获取验证码”按钮事件

+ isCounting 是否倒计时，bool类型true/false

+ handleDisCount 倒计时停止事件

+ isDisabled “获取验证码”按钮是否可点击，bool类型true/false

+ handleAble “获取验证码”按钮可点击事件

+ handleDisable “获取验证码”按钮不可点击事件

+ inputFn 输入框onChage事件，可缺省

## SmartInput带左边框的输入框

![input 图片示例](images/examples/react-smartinput-mobile.gif)
![input 图片示例](images/examples/react-smartinput-card.gif)
![input 图片示例](images/examples/react-smartinput-id.gif)

### 用法：

	import SmartInput from '../components/vera/SmartInput'
	...
	<SmartInput 
      value={store.myIpt.val} 
      placeholder="仅支持提现卡到储蓄卡"
      id="bankcard"
      isError={stores.pub.myIpt.isError}
      writeValue={actions.myIptValue}
      isWithTitle={true}
      title="卡号"
      type="card"
      blurFn={actions.blurBankcardIpt}
      inputType="tel"/>

### 参数：

	SmartInput.propTypes = {
	    title:PropTypes.string.isRequired,
	    value: PropTypes.string.isRequired,
	    id: PropTypes.string.isRequired,
	    placeholder: PropTypes.string.isRequired,
	    isError: PropTypes.bool.isRequired,
	    writeValue: PropTypes.func.isRequired,
	    isWithTitle: PropTypes.bool.isRequired,
	    type: PropTypes.string,
	    inputType: PropTypes.string,
	    blurFn: PropTypes.func,
	    inputFn: PropTypes.func,
	    focusFn: PropTypes.func
	}

+ id 输入框ID

+ title 输入框左侧栏文字

+ type 输入框类型，可有三种值可选"card"银行卡、"mobile"手机号和"id"身份证号，会对输入进行正则校验

+ placeholder 输入框未输入时默认显示文字

+ isError 输入框是否报错显示，bool类型true/false

+ writeValue 输入框值变化事件，返回输入框内容值

+ inputType 输入框类型，同原生input的type，可缺省，默认为text

+ blurFn 输入框失焦onBlur事件，返回输入框内容值，可缺省

+ focusFn 输入框聚焦onFocus事件，可缺省

+ inputFn 输入框onChange事件，返回输入框内容值，可缺省

## Tabs选项卡

![tab 图片示例](images/examples/react-tab.gif)

### 用法：

	import Tabs from '../components/vera/Tabs'
	import TabList from '../components/vera/TabList'
	import TabButton from '../components/vera/TabButton'
	import TabPanel from '../components/vera/TabPanel'
	...
	<Tabs onSelect={this.myTabsSelect}>
        <TabList>
          <TabButton>交易记录</TabButton>
          <TabButton>激活记录</TabButton>
        </TabList>
        <TabPanel>
          tab1 content
        </TabPanel>
        <TabPanel>
          tab2 content
        </TabPanel>
    </Tabs>

### 参数：

	Tabs.propTypes = {
	  	children: childrenPropType,
	  	onSelect: PropTypes.func
	}

+ children 选项卡下子内容必须为TabList（Tab按钮列表，其子dom必须放置TabButton）和TabPanel（Tab内容，可任意dom元素）

+ onSelect 选项卡切换事件，返回2个值（第一个是点击切换后的选中项index，第二个是点击切换前的选中项index），可缺省

## Trace提示框

![trace 图片示例](images/examples/react-trace.gif)

### 用法：

	import Trace from '../components/vera/Trace'
	...
	<Trace 
		isShow={stores.pub.myTrace.traceBlock} 
		text={stores.pub.myTrace.text} 
		handleHide={actions.myTraceHide} >
	</Trace>

### 参数：

	Trace.propTypes = {
	    text: PropTypes.string.isRequired,
	    isShow: PropTypes.bool.isRequired,
	    handleHide: PropTypes.func.isRequired
	}

+ text 提示框内显示文字

+ isShow 是否显示，bool类型true/false

+ handleHide Trace隐藏事件

## Toast对话框

![toast 图片示例](images/examples/react-toast.gif)

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

#### 例如：
	var toast = {
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

![dialoge 图片示例](images/examples/react-dialoge.gif)

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
		titleClass: PropTypes.string,
		closePositionRight: PropTypes.bool,
		isFixedHeight: PropTypes.bool
	}

+ contentData 对话框显示的内容，可以有title 对话框标题、subTitle 对话框副标题，必须有bottom 底部信息例如cancel提供相关显示信息和点击后的操作

#### 例如：
	var dialog = {
					title:"提示信息",
					subTitle:'子标题',
					bottom:{
						cancel:"cancel",
						cancelEvent:actions.myDialogHide
					}
				}

+ isShow 是否显示，bool类型true/false

+ titleClass 对话框title加className来控制样式，可缺省

+ closePositionRight 对话框close按钮位置是否为右侧，bool类型true/false，可缺省，默认值为false即按钮在左侧

+ isFixedHeight 对话框是否是固定高度，bool类型true/false，可缺省，默认值为false即未达到最大高度前非固定高

## Loading加载

![loading 图片示例](images/examples/react-loading.gif)

### 用法：
	
	import Loading from '../lib/vera/Loading'
	...
	<Loading text="安全加载中" isShow={stores.pub.loadingBlock}/>

### 参数：

	Loading.propTypes = {
	    text: PropTypes.string.isRequired,
	    isShow: PropTypes.bool.isRequired
	}

+ text 加载显示的文字

+ isShow 是否显示，bool类型true/false

## Modal模态框

![modal 图片示例](images/examples/react-modal.gif)

### 用法：

	import Modal from '../components/vera/Modal'
	...
	<Modal 
          isShow={stores.pub.modalBlock} 
          handleHide={actions.myModalHide} 
          title="模态框">
          <div className="list">
            <div>1</div>
            <div>2</div>
            <div>3</div>
            <div>4</div>
            <div>5</div>
          </div>
        </Modal>

### 参数：

	Modal.propTypes = {
	    title: PropTypes.string.isRequired,
	    isShow: PropTypes.bool.isRequired,
	    handleHide: PropTypes.func.isRequired
	}

+ title 模态框题目

+ isShow 模态框是否显示，bool类型true/false

+ handleHide 模态框隐藏事件

## Util公用方法

clearSpace清楚字符串内部空格

### 用法：
	
	import clearSpace from '../lib/vera/util/clearSpace'
	...
	var str = clearSpace(strWithSpace);

format格式化

### 用法：

	import format from '../lib/vera/util/format'
	...
	var str = format(str, type);

### 参数：

+ type 	三种："mobile_split"、"card_split"、"idcard_split"，分别格式化成手机号、银行卡号和身份证号

Validate校验

### 用法：

	import Validate from '../lib/vera/util/Validate'
	...
	var result = Validate.bankcardNo(val);
	var result = Validate.fullname(val);
	var result = Validate.iDCard(val);
	var result = Validate.cvv2(val);
	var result = Validate.exptime(val);
	var result = Validate.mobileNo(val);
	var result = Validate.authCode(val);
	var result = Validate.passport(val);
	var result = Validate.paypass(val);	
	var result = Validate.email(val);
	var result = Validate.lenMN(val, min, max);
	var result = Validate.notEmpty(val);

### 参数：
+ bankcardNo 银行卡号校验

+ fullname 用户名校验，2-20位中文格式

+ iDCard 身份证号校验

+ cvv2 银行卡号背面末尾3位数字校验

+ exptime 信用卡有效期校验

+ mobileNo 手机号校验

+ authCode 6位短信验证码校验

+ passport 密码长度校验，6到20位

+ paypass 支付密码校验，支持由6-20位字母、数字、特殊字符，至少包含其中2类以上字符组合；全特殊字符：`-=[]\;',./~!@#$%^&*()_+{}|:"<>? 空格

+ email 邮箱校验

+ lenMN 长度在min和manx之间校验

+ notEmpty 不为空校验

encrypt md5加密

### 用法：

	import {pass_encrypt} from '../lib/vera/util/encrypt'
	...
	var str = pass_encrypt(pwd,salt);

### 参数：

+ pass_encrypt 给密码做md5加密，第二个参数为盐值

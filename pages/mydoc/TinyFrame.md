/*
Title: 多窗口机制
Sort: 102
*/

<font size=2>
<font face="微软雅黑">

### 功能描述
在移动开发中，页面一般以多窗口的形式保存到窗口堆栈中，在页面来回切换时，可以减少页面加载时间，提高用户体验。比如在多窗口机制中，A页面跳转到B页面。在B页面返回A页面时，A页面直接从窗口堆栈中取出显示，减少了重新渲染A页面的时间，在切换过程中，也可以加载过渡动画，提高用户体验。<br/>
Tiny视图在一个窗口中展示，为了实现Tiny的多窗口切换效果，引入了TinyFrame框架。<br/>
TinyFrame提供针对Tiny视图的多窗口开发。在多窗口机制中，Page为一个窗口，包含了Tiny视图。通过navigator堆栈管理Page的生命周期。当页面创建时(goto)，页面进入堆栈。当页面back时，页面离开堆栈，同时，Tiny视图会被回收，释放占用的资源，包括Tiny中注册的通知、定时器等都会被释放。<br/>
通过XML、CSS、JavaScript封装原生框架，提供针对IOS、android平台的一套标准化开发流程。保持同原生一致的用户体验和效果。

### 目标
TinyFrame提供了一套针对多窗口的标准化开发流程，取代原生的页面开发。保持IOS、android平台一致的开发标准和效果。提供单页面窗口、TabBar窗口、抽屉窗口等常用的窗口视图。针对页面之间的跳转，提供堆栈机制，并提供常见的过渡动画。

### 标签说明

####  frame

##### 描述

 frame根节点标签，标识文档为xml规范的文档，xml文件中必须有的结构标签。`<frame>` 与 `</ frame >` 标签限定了文档的开始点和结束点，在它们之间是文档的头部和主体。正如您所了解的那样，文档的头部由 `<head>` 标签定义。#### head

##### 描述
`<head>` 标签用于定义文档的头部，它是所有头部元素的容器。`<head>` 中的元素可以引用脚本、样式表等。文档的头部描述了文档的各种属性和信息，绝大多数文档头部包含的数据都不会真正作为内容显示给读者。
####  style

##### 描述
`<style>` 标签定义文档与外部CSS样式表资源的关系。`<style>` 标签的用途是链接样式表。

##### 属性

<table class="table table-bordered table-striped table-condensed">   <tr>      <td>属性</td>      <td>取值</td>      <td>描述</td>      <td>缺省值</td>   </tr>   <tr>      <td>href</td>      <td></td>      <td>定义被链接文档的位置。</td>      <td></td>   </tr></table>
####  script 

##### 描述

`<script>` 标签定义文档与外部脚本资源的关系。`<script>` 标签的用途是链接脚本文件。

##### 属性

<table class="table table-bordered table-striped table-condensed">
   <tr>
      <td>属性</td>
      <td>取值</td>
      <td>描述</td>
      <td>缺省值</td>
   </tr>
   <tr>
      <td>src</td>
      <td></td>
      <td>定义被链接文档的位置。</td>
      <td></td>
   </tr>
</table>

####  page 

##### 描述
  `<page>`标签定义为整个页面，对应原生的ViewControler(activity)页面。一个page页面内置一个Tiny控件
##### 属性

<table class="table table-bordered table-striped table-condensed">
   <tr>
      <td>属性</td>
      <td>取值</td>
      <td>描述</td>
      <td>缺省值</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>url</td>
      <td></td>
      <td>页面对应的tinyview的请求地址</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>hidesStatusBar</td>
      <td>true/false</td>
      <td>显示和隐藏状态栏</td>
      <td>默认false</td>
      <td>只针对IOS平台。当statusBar显示时，tinyView的高度为屏幕高度-statusBar高度-tarBar高度</td>
   </tr>
   <tr>
      <td>navigator</td>
      <td></td>
      <td>navigator导航器</td>
      <td></td>
      <td>page.navigator</td>
   </tr>
   <tr>
      <td>tabBar</td>
      <td></td>
      <td>tabBar控制器</td>
      <td></td>
      <td>page.tabBar</td>
   </tr>
   <tr>
      <td>hidesTabBar</td>
      <td>true/false</td>
      <td>显示和隐藏底部栏</td>
      <td></td>
      <td>当存在tabBar栏时，默认显示</td>
   </tr>
</table>

`备注：style暂支持background-color、background-image、background9-image。      Page的宽度和高度无法设置。`
      
##### 函数
###### page.present(opts)
###### 描述
 打开指定的框架页面。

###### 参数

<table class="table table-bordered table-striped table-condensed">
   <tr>
      <td>属性</td>
      <td>取值</td>
      <td>描述</td>
      <td>缺省值</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>opts.url</td>
      <td></td>
      <td>必须。到打开的frame页面的地址</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>opts.animate</td>
      <td>default/none</td>
      <td>执行的动画类型</td>
      <td></td>
      <td></td>
   </tr>
</table>

###### 示例
	var opts = {"url":"file:///frame.xml", "animate":"default"}	window.page.present(opts)


###### page.dismiss(opts)
###### 描述

关闭当前的框架页面

###### 参数

<table class="table table-bordered table-striped table-condensed">
   <tr>
      <td>属性</td>
      <td>取值</td>
      <td>描述</td>
      <td>缺省值</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>opts.animate</td>
      <td>default/none</td>
      <td>执行的动画类型</td>
      <td></td>
      <td></td>
   </tr>
</table>

###### 示例
	var opts = {"animate":"default"}	page.dismiss (opts)##### 标签示例
	<frame>	        <page url="file:///test.tml"  hidesStatusBar ="false" id=”pageid”/>	</frame>
	
	
####  navigator  

##### 描述
  `<navigator>`为导航器标签，负责page页面之间的导航，内置栈功能。当push页面时，该页面进站栈。当pop页面时，该页面出栈。
  
##### 属性

<table class="table table-bordered table-striped table-condensed">
   <tr>
      <td>属性</td>
      <td>取值</td>
      <td>描述</td>
      <td>缺省值</td>
   </tr>
   <tr>
      <td>src</td>
      <td></td>
      <td>栈顶页面page的请求地址</td>
      <td></td>
   </tr>
</table>

##### 函数
###### navigator.push(opts)
###### 描述
 导航器push新的页面。功能同tiny中的goto函数一致。

###### 参数

<table class="table table-bordered table-striped table-condensed">   <tr>      <td>属性</td>      <td>取值</td>      <td>描述</td>      <td>缺省值</td>      <td>备注</td>   </tr>   <tr>      <td>opts.page</td>      <td></td>      <td>必须。要打开的page对象。</td>      <td></td>      <td></td>   </tr>   <tr>      <td>opts.animate</td>      <td>default/none</td>      <td>执行的动画类型</td>      <td></td>      <td></td>   </tr></table> 
###### navigator.popToTop(opts)
###### 描述
返回到导航器的第一个页面，同时，导航器弹出其他所有页面。
 
<table class="table table-bordered table-striped table-condensed">
   <tr>
      <td>属性</td>
      <td>取值</td>
      <td>描述</td>
      <td>缺省值</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>opts.animate</td>
      <td>default/none</td>
      <td>执行的动画类型</td>
      <td></td>
      <td></td>
   </tr>
</table>

###### navigator.popToPage(opts)
###### 描述
返回到指定页面，同时，弹出该页面之前的所有页面。功能同tiny中的back(‘id’)一致。

###### 参数

<table class="table table-bordered table-striped table-condensed">
   <tr>
      <td>属性</td>
      <td>取值</td>
      <td>描述</td>
      <td>缺省值</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>opts.id</td>
      <td></td>
      <td>页面的id。tml的id值</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>opts.animate</td>
      <td>default/none</td>
      <td>执行的动画类型</td>
      <td></td>
      <td></td>
   </tr>
</table>

##### 标签示例

	<frame>
	    <navigator id="nav1">
	        <page url="hello.xml"  />
	    </navigator>
	</frame>	
	
####  tabBar  

##### 描述
   `<tabBar>`为分页栏控制器标签。显示在屏幕的最下方，包含多个`<tab>`标签。通过点击，不同的`<tab>`标签，切换屏幕中显示的视图。
  
##### 属性

<table class="table table-bordered table-striped table-condensed">
   <tr>
      <td>属性</td>
      <td>取值</td>
      <td>描述</td>
      <td>缺省值</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>style</td>
      <td></td>
      <td>样式设置</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>visibility</td>
      <td>visible/hidden</td>
      <td>显示隐藏分页栏</td>
      <td></td>
      <td>默认显示visible</td>
   </tr>
</table>
	
`备注：tabBar宽度默认100%。tabBar中page视图的高度为屏幕内容高度－tabBar高度`


##### 函数
###### tabBar.selectIndex(index)
###### 描述
 根据索引，设置需要显示的tab页。

###### 参数

<table class="table table-bordered table-striped table-condensed">
   <tr>
      <td>属性</td>
      <td>取值</td>
      <td>描述</td>
      <td>缺省值</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>index</td>
      <td></td>
      <td>tab索引</td>
      <td></td>
      <td></td>
   </tr>
</table>

###### 示例
    
    //index值由点击事件等传入。
    var tabBar = $("tabBar")
	tabBar.selectIndex(index)


####  tab  

##### 描述
  `<tabBar>`的子标签，定义每个分页标签。`<tab>`标签必须包含一个子元素，子元素可以为`<page>`、`<navigator>`.
  
##### 属性

<table class="table table-bordered table-striped table-condensed">
   <tr>
      <td>属性</td>
      <td>取值</td>
      <td>描述</td>
      <td>缺省值</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>id</td>
      <td></td>
      <td>唯一id</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>title</td>
      <td></td>
      <td>显示标题</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>selected</td>
      <td>true／false</td>
      <td></td>
      <td></td>
      <td>是否选中</td>
   </tr>
   <tr>
      <td>class</td>
      <td></td>
      <td>样式</td>
      <td></td>
      <td></td>
   </tr>
</table>

`备注：bar宽度默认平均分配tabBar的宽度，高度默认100%.`

##### 事件

<table class="table table-bordered table-striped table-condensed">
   <tr>
      <td>事件</td>
      <td>描述</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>press</td>
      <td>点击事件</td>
      <td>点击tab时执行</td>
   </tr>
   <tr>
      <td>select</td>
      <td>选中回调事件，由js回调。参数含索引。</td>
      <td>由selectedIndex属性变化时触发</td>
   </tr>
</table>

##### 标签示例

	
	<frame>	<tabBar style=”height:49;”>	        <tab	id=”messageID”	title=”Message”	onPress=”tabBarSelect(‘message’)”	selected=”true”	style=”background-image:url(file:///message.png)”>	<navigator id=”nav1” url=”file:///1.tml”/>	        </tab>	        <tab	id = “friendID”	title=”Friend”	onPress=”tabBarSelect(‘friend’)”	selected=”false”	style=”background-image:url(file:///friend.png)”>	<navigator id=”nav2” url=”file:///2.tml”/>	        </tab>	        <tab	id=”settingID”	title=”setting”	onPress=”tabBarSelect(‘settings’)”	selected=”false”	style=”background-image:url(file:///setting.png)”>	<page url=”file:///test.tml”></page>	        </tab>	</tabBar>	</frame>		function tabBarSelect(tabName) {	    var message = $("messageID")	    var friend = $("friendID")	    var setting = $("settingID")	    var nav1 = $("nav1")	    var nav2 = $("nav2")	    var nav3 = $("nav3")	    if(tabName == "message") {	        nav1.popToTop();	        message.setStyle("background-color", "#ffaa00");	    }	}	

###	JS说明

####	TinyFrame js对象
##### 	document
######	描述
   当前上下文文档的树结构，提供访问和操作文档的标准方法。
   
######  方法
###### 	getElementById
###### 描述
   getElementById(id) 方法返回带有指定 ID 的元素
  ***
  
##### 	Element
   定义document对象中的每个元素。
###### page
`<page>` 标签对应的节点元素
###### navigator
`<navigator>` 标签对应的节点元素
###### tabBar
`<tabBar>` 标签对应的节点元素
###### tab
`<tab>` 标签对应的节点元素

#### Tiny新增JS方法
##### 	window.page
   page为TinyFrame中<page>标签的js对象，对应原生的ViewControler(activity)页面。
###### 	示例
	function goto(url) {	var page = new Page();	page.url = url	page.name=”首页”	page.hidesStatusBar= “false”	page.hidesTabBar = “false”	var opts = {“page”: page, “animate”:”default”}		window.page.navigator.push(opts)	}		function back(id) {	    if(id==undefined) {	    	var opts = {“animate”:”default”}		       window.page.navigator.pop(opts); 	   } else {	       var opts = {“id”:id,“animate”:”default”}		  	    window.page.navigator. popToPage(opts);	  }	}
##### 	tiny增加didAppear事件
tiny页面在每次展示完成后执行的事件，第一次会在onload之后执行。在每次页面back回来后也会执行。页面事件由TinyFrame发起执行###### 	示例 
	document.addEventListener("didAppear",function(){	})
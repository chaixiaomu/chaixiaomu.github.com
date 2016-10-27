---
title: Sample 1 Topic (Product 1)
keywords: sample
summary: "This is just a sample topic..."
sidebar: product1_sidebar
permalink: p1_sample1.html
folder: product1
---


本文档将带你一步步创建完成一个 Tiny demo，并可以在手机上体验该 demo 的实际效果，这个 demo 将会显示用户信息，绘制出用户的姓名、性别、身份证号以及手机号码等等。

古语云:工欲善其事，必先利其器，在正式开发之前，我们先要搭建一个良好的开发环境，以此来开展我们在 Tiny 平台的开发之旅。

### 环境搭建 ###

1. 开发环境 Tiny IDE 下载地址：<a href="http://www.mtiny.cn/%E8%B5%84%E6%BA%90%E4%B8%8B%E8%BD%BD/IDE" target="_blank">IDE 下载 </a>，Tiny IDE 的使用，请参考以下链接： <a href="http://www.mtiny.cn/tinyBuilder/IDE" target="_blank">IDE 使用指南 </a>

2. 调试工具 TinyLoader 下载地址： <a href="http://www.mtiny.cn/%E8%B5%84%E6%BA%90%E4%B8%8B%E8%BD%BD/TinyLoader" target="_blank">TinyLoader 下载 </a>。

3. 导入 Tiny 组件 demo，下载地址：[demo 下载](http://www.mtiny.cn/Tiny-demo.zip)，这份 demo 囊括了Tiny 平台大多数的功能，请详细阅读 demo 代码。
4. Tiny 组件还有 iOS 平台的 app，用来展示Tiny 丰富的功能，下载地址：<a href="https://www.pgyer.com/explorer" target="_blank">Tiny 组件 demo 下载 </a>。这是应用首图：


![](http://www.mtiny.cn/explorer.jpg)


5. 下载好 demo 之后，就可以开始导入到 Tiny IDE 中了，具体的导入流程如下图所示：<img src="%base_url%/jiaocheng .gif" />




### 案例示范 ###

通过IDE 使用指南的学习，你已经掌握了如何通过 TinyLoader 调试器来跟 PC 上的 TinyIDE 设计器联调来实时查看 UI 设计效果、调试代码了，接下来我们将通过一系列的 demo 开发教学让你很快掌握TinyBuilder 并且利用TinyBuilder 开发一个真正的 App。

接下来我们要展现一个用户信息的页面，绘制出用户的姓名、性别、身份证号以及手机号码等等信息，具体的 demo 效果图如下所示：

![](http://www.mtiny.cn/guide/guide01.png)

在上一节教程中想必大家已经学会了如何 在TinyIDE 中创建项目，我们也对项目包含的文件进行分析，一个完整的项目应该包含Js、CSS 和img 等文件或文件夹，之所以这样是因为我们的 TinyBuilder 是通过 tml 和 css 构建用户界面，使用 JavaScript 脚本进行交互和业务开发，整个开发过程基本都在 TinyIDE 中完成。简而言之：

* tml：包含了 App 的表现内容和结构。
* CSS：控制 App 的布局、外观和表现。
* JavaScript：控制页面的行为、进行用户交互以及业务开发。

我们即将要演示的个人信息界面包含的标签比较多，在学习过程中遇到不是很懂的希望勤翻文档中心的文档，都有详细说明，接下来我们进行演示这个 demo 书写的过程。

### 头部设计 ###

在创建好项目之后，我们新建一个tml 文档，新建的tml 文档包含了`<tml>`，`<head>`，`<body>`，`<script>`和`<style>`五大结构性标签。以后如果要进行界面优化、样式设计以及用户交互等，可以直接在`<head>` 标示的外部资源表里进行修改，App 主要呈现的内容和结构我们需要在tml 页面中的`<body>` 内进行书写修改。

`<label>` 标签可以用来展示简单的单行文本，所以这个界面中的一大部分的文本都可以用此标签来展示，我们在不涉及布局的情况下使用`<label>` 将这些栏目都展示出来，具体代码如下：
 
     <tml>
	    <head>
		    <style href="css/public.css"/>
		    <script src="commonJs/tools.js"/>
	    </head>
	    <body>
	        <label value="个人信息" class=""/>
	        <label value="用户名" class=""/>
	        <label value="姓名" class=""/>
	        <label value="身份证号 " class=""/>
	        <label value="手机号 " class=""/>
	        <label value="邮箱 " class=""/>
	        <label value="所属省市 " class=""/>
	        <label value="详细地址" class=""/>
	    </body>
    </tml>

写完以上代码之后，我们通过TinyLoader 进行预览，呈现出如下界面：

<img src="%base_url%/guide/guide02.png"  width = "350"  alt="Drawing" />

效果很糟糕，这是因为我们还没有为`<label>` 标签指定我们想要渲染的宽和高。下面让我们把它弄得更好看一些，让这些标签不要拥挤在一起，而是平分整个`<body>` 的高度，我们通过容器标签`<vbox>` 来实现，也就是将标签竖向嵌套在`<vbox>` 标签之中，效果如下：

<img src="%base_url%/guide/guide08.png"  width = "350"  alt="Drawing" />

和之前相比，文字分明了很多，我们需要借助CSS 样式表和Js 脚本来继续完成页面，在书写代码之前我们先分析如何实现。

在App 页面顶部，涉及到三个元素：

* 返回的图标，我们可以用`<img>` 标签来实现。
* 文字信息，简单的单行文字信息用`<label>` 实现。
* 所涉及的样式跟需要发生的事件。

一般的我们布局的规则是

* 从左到右，从上到下。
* 从左到右属于横向布局，是行内元素，行内元素一般用`<span>`、`<hbox>`和`<hpanel>`等三种容器标签。
* 从上到下属于竖向布局，是块级元素，块级元素一般用`<div>`、`<vbox>`、`<vpanel>`和`<group>`等四种容器标签。

对App 页面顶部涉及到的三个元素分析发现属于横向布局，从左到右依次是返回图标和文字信息，在点击这个图标或者图标所在区域之后，会发生返回事件，所以我们可以确定我们需要使用的标签：两个控件标签：`<img>`、`<label>`，两个容器标签：`<span>`、`<group>`。

>  `<group>`和`<div>`最大的不同是`<group>`具有点击事件，在本例中，用户点击返回图标之后，调动点击事件，返回到上一级页面，所以选用`<group>`标签。

我们重新书写设计代码，效果图如下：

<img src="%base_url%/guide/guide03.png" width = "350"  alt="Drawing" />

整体而言，App 界面是有些接近了实例 demo，具体代码如下。


**tml代码**

     <tml>
	    <head>
		    <style href="css/public.css"/>
		    <script src="commonJs/tools.js"/>
	    </head>
	    <body>
        <vbox> 
           <span class="header blue">
	           <group class="back blue" onclick="alert('返回')">
	               <img class="back_img" src="img/back.png"/>
	           </group>
	           <label value="个人信息" class="title"/>
	       </span>     

	        <label value="用户名" class=""/>
	        <label value="姓名" class=""/>
	        <label value="身份证号 " class=""/>
	        <label value="手机号 " class=""/>
	        <label value="邮箱 " class=""/>
	        <label value="所属省市 " class=""/>
	        <label value="详细地址" class=""/>
        </vbox>
	    </body>
    </tml>

**css代码**

    .header{
        height:48;  width:100%; 
    }

    .back_img{
       height:20;      
       width:13;      
       align:center;     
       vertical-align:middle; 
    }

    .back{
      height:48;  width:40;  position:absolute; 
    }

    .blue{
      background-color:#2599EA; 
    }

    .title{
      align:center;  text-align:center;  vertical-align:middle;  font-size:17; 
    }
​
### 主体设计 ###

与App 顶部不同，主体部分除了要展示一些简单的单行文本和图片之外，还需要用户输入信息，输入信息的实现是依靠`<input>` 标签。

我们先来完成用户名这一行行内元素的布局，这一行行内元素有两个标签：`<label>` 标签和`<input>` 标签。

具体代码如下所示：

**tml代码**
	       
	           <span class="spanPublic">
	               <label value="用户名" class="label_left"/>
	               <input class="input_right" value="莱昂纳多"  tip="输入用户名"/>
	           </span>

**CSS代码**
    
    .w100{
    	width:100%;
    }

    .fs_content{
	    font-size:14;
    }

    .spanPublic{
    	height:46;
    	padding:0 12 0 12;
    	background-color:#ffffff;
    	color:#666666;	
    	border-color:#d5d5d5;	
    	border-width:0 0 0.5 0;
    	width:100%;
    }    
    
    .label_left{
    	height:100%;
    	width:25%;
    }
    
    .input_right{
    	height:100%;
    	width:75%;
    }


打开TinyLoader 之后，我们发现UI 效果如下：

<img src="%base_url%/guide/guide04.png"  width = "350" alt="Drawing" />

这种效果基本已经接近了实例效果，所以我们只需要按照这个模式一直写下去下去即可。

tml 如下所示：

          <div class="w100 fs_content">
                <span class="spanPublic">
                    <label class="label_left" value="用户名:"/>
                    <input class="input_right" value="" tip="输入用户名"/>
                </span>

				<span class="spanPublic">
					<label class="label_left" value="姓名:"/>
					<input class="input_right" value="" tip="输入姓名"/>
				</span>

                <span class="spanPublic">
                    <label class="label_left" value="性别:"/>
                    <span class="selectSexSpan">
                        <label class="vcenter" value="男"/>
                        <label class="vcenter margin31" value="女"/>
                    </span>
                </span>

                <span class="spanPublic">
                    <label class="label_left" value="身份证号:"/>
                    <input class="input_right" value="" tip="输入身份证号"/>
                </span>

				<span class="spanPublic">
					<label class="label_left" value="手机号:"/>
					<input class="input_mid" value="" tip="输入手机号" type="digital"/>
				</span>

                <span class="spanPublic">
                    <label class="label_left" value="邮箱:"/>
                    <input class="input_right" value="" tip="输入身份证号"/>
                </span>
                
                <span class="block_height bg_white border_line w100 edge_distance">
                    <label class="vcenter fs_content fc_h_gray cLeft" value="所属省市:"/>
                    <select class="vcenter fs_content fc_gray ccRight" tip="请选择省市">
                        <option value="01" caption="浙江"/>
                        <option value="02" caption="江苏"/>
                        <option value="03" caption="上海"/>
                        <option value="04" caption="安徽"/>
                        <option value="05" caption="北京"/>
                        <option value="06" caption="天津"/>
                    </select>
                </span>

	            <span class="spanPublic">
                    <label class="label_left" value="详细地址:"/>
                    <input class="input_right" value="" tip="请填写详细地址"/>
                </span>
	        </div>

效果图如下所示：

<img src="%base_url%/guide/guide09.png"  width = "350" alt="Drawing" />

但也有两处不同的地方需要额外处理。

1.性别，

性别，在这里没有使用`<input>` 标签来处理信息的输入，而是通过单选框来决定，出现了男女两个单选框，具体原理会在下文中说明：

**tml代码**

    <span class="spanPublic">
	    <label value="性别" class="label_left"/>
	    <span class="selectSexSpan">
	        <label value="男" class="vcenter"/>
	        <button class="selectSexbtn_F vcenter" id="man" onclick="changeSex('man')"/>
	        <label value="女" class="vcenter"/>
	        <button class="selectSexbtn vcenter" id="woman" onclick="changeSex('woman')"/>
	    </span>
	</span>	

在上面的代码片段里，简单的文字信息我们依旧通过`<label>` 标签来实现，单选框以及样式我们通过`<button>` 按钮控件实现，但是在按钮控件上添加了点击事件`changeSex()`，当用户选中某个性别按钮时，该按钮的样式会发生变化，呈现出被选中的状态。

这个事件我们通过`if...else` 条件语句实现。具体Js 代码如下：

    function changeSex(id) {
        if (id == "man") {
            $('man').setAttribute('class', 'selectSexbtn_F vcenter');
            $('woman').setAttribute('class', 'selectSexbtn vcenter');
        } 
    
        else {
            $('man').setAttribute('class', 'selectSexbtn vcenter');
            $('woman').setAttribute('class', 'selectSexbtn_F vcenter');
        }
    }


在上面的代码中我们构建了一个带有`id `参数的函数 `changesex（id）`，这个函数由`If...else`  语句组成，当某一个语句为`true` 时，`id` 会返回具体的元素，并且改变该元素的属性值，实现的方法是`setAttribute`。

>`setAttribute` 会设置属性，具体语法:element.setAttribute(name, value)。

显而易见的，`selectSexbtn_F`样式是被选中时候的状态，`selectSexbtn` 是未被选择的样式。

css代码如下：
    
    .selectSexSpan
    {
        height:100%;
        align:right;
    }
    
    .selectSexbtn
    {
        height:19;
        width:19;
        background-image:url(img/radioBtn.png);
        margin:0 0 0 13;
    }
    
    .selectSexbtn_F
    {
        height:19;
        width:19;
        background-image:url(img/radioBtn_f.png);
        margin:0 0 0 13;
    }
    
2.所属省市

所属省市与其他的不同在于当点击该行之后，会创建一个包含全国省市的选项列表，这个效果的实现我们通过`select` 标签中嵌套`option` 标签来实现。

需要注意的是，`<option>` 标签可以在不带有任何属性的情况下使用，但是通常需要使用 `value` 属性，此属性会指示出被送往服务器的内容，`<option>` 标签呈现的文字信息由`caption` 属性来实现。 

所以所属省市实现的代码是：

    <select class="vcenter fs_content fc_gray ccRight" tip="请选择省市">
        <option value="01" caption="浙江"/>
        <option value="02" caption="江苏"/>
        <option value="03" caption="上海"/>
        <option value="04" caption="安徽"/>
        <option value="05" caption="北京"/>
        <option value="06" caption="天津"/>
    </select>

效果图如下：

<img src="%base_url%/guide/guide05.png"  width = "350" alt="Drawing" />

以上代码并没有涉及到Js 脚本，所以也比较简单，就是对于标签的应用和熟悉，所以希望大家认真学习官方文档。

### 底部设计 ###

到这里，呈现的效果图基本与要达到的效果图别无二致，最后需要处理的就是底部信息和导航栏，导航栏我们将在以后的教程里结合多窗口机制进行讲解，在本次课程中我们先将底部信息处理好。

在写代码之前我们依旧分析底部信息会有怎样的样式和事件：第一种情况是，当我们填写完整信息，系统默认我们是同意《xx金融消费贷款合同》，那么只需要点击保存按钮进行保存，保存完成后通过`alert` 提示保存完成。

第二种情况是，当我们填写完整信息之后，由于某些操作，没有同意该合同就直接进行保存信息设置不可行，此时应该会弹出“请先同意《xx金融消费贷款合同》”的信息提示我们同意该合同，一句通过`alert` 来实现。

难点是怎么样判断我们是否同意了该合同，判断的依据应该是是否选中了”同意《xx金融消费贷款合同》“
，当我们选中的时候是第一种情况，**这也是系统默认的情况**，当我们没有选中的事情应该是第二种情况。

所以我们依旧通过`if...else `语句实现。

**具体Js 代码如下**：

    var state = "true";
    function changeRadioBtnState() {
        if (state == "true") {
            $('radioBtn').setAttribute('src', 'img/orderDetail/orderDetail_11.png');
            $('btn_order').setAttribute('class', 'btn_gray');
            state = "false";
        } 
    
        else {
            $('radioBtn').setAttribute('src', 'img/orderDetail/orderDetail_13.png');
            $('btn_order').setAttribute('class', 'btn_blue');
            state = "true";
        }
    }


    function clickEvent() {
        if (state == "true") {
        alert('保存');
        } 
    
        else {
        alert('请先同意《XX金融消费贷款合同》');
        }
    }

以上代码片段中，我们定义了一个文本值为true 的变量state。当我们点击按钮之后，会调动`changeRadioBtnState() ` 函数和`clickEvent（）` 函数，该函数通过判断state 的值是否为时true 来执行`if...else `。

语句实现这样的效果：对变量state 进行判断之后，将会改变tml 文件中的`<img>`标签的属性值 和id为`btn_order` 的`<button>` 的属性值并重新给变量state 赋值。

思路：

1.设置一个变量state，默认值位true。

2.点击按钮之后，调动`changeRadioBtnState() ` 函数，执行`if...else ` 语句。

3.对`if...else ` 语句进行判断，条件语句`state == "true" `是true（默认的state=true），执行if语句块：
    
    $('radioBtn').setAttribute('src', 'img/orderDetail/orderDetail_11.png');
    $('btn_order').setAttribute('class', 'btn_gray');
    state = "false";

4.id为`radioBtn` 的 `<img>`标签属性值 和id为`btn_order` 的`<button>` 标签的样式改变，均为灰色，表示未被选中。

5.对state 重新赋值，`state="false"`。

底部信息的样式为灰色，表示未被选择，我们去选择他，依旧触发`changeRadioBtnState() ` 函数。

1.变量state被重新赋值，为`state="false"`。

2.点击按钮之后，调动`changeRadioBtnState() ` 函数，执行`if...else ` 语句。

3.对`if...else ` 语句进行判断，条件语句`state == "true" `为false（重新赋值之后，`state="false"`）。

4.执行else语句块，改变底部信息的样式。

     else {
        $('radioBtn').setAttribute('src', 'img/orderDetail/orderDetail_13.png');
        $('btn_order').setAttribute('class', 'btn_blue');
        state = "true";
    }

5.对state 重新赋值，`state="true"`。

最后，我们运行TinyLoader，整个App 呈现的效果图跟我们模板的效果图是一样的，但是缺乏底部的导航栏，导航栏的设计我们会在多窗口机制的教程中讲述到，目前未添加导航栏的效果图如下。

<img src="%base_url%/guide/guide07.png" width = "350"  alt="Drawing" />

### 结语 ###

到这里，一个能响应点击事件并输入信息的 demo 就完成了，是不是很简单易学呢？！我们可以从上一节教程中所学的手机和电脑联调代码的方法来赶快验证一下所学内容啦。

为了实现一个完整功能的应用，接下来还有大量工作要做，譬如：添加导航栏，搜索，加载更多，等等等等，在接下来的教程中，我们将会一步一步实现这些功能。


### 最终的demo下载 ###

[个人信息 demo 下载](%base_url%/template\myInfo\myInfo1\myInfo1.zip "点我下载")
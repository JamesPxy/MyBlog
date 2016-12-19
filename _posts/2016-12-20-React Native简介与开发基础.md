---
layout: default
title: 手把手教React Native实战之开山篇
---
#0、手把手教React Native实战之开山篇

##作者简介

  东方耀    Android开发
  RN技术   facebook
  github  
  android ios  原生开发
  react reactjs nodejs 前端  进入 移动互联网 
  js nodejs    大波
  app 
  个人角度   学习的必要性    全栈工程师的捷径

  公司角度    组件化  成本降低  热更新 

<font color=red size=5>加作者微信公众号（dongfangyao888）或扫描下面二维码</font>

<font color=red size=6>推送高清视频教程+语音解说+课堂笔记和源码</font>

![微信号：dongfangyao888二维码](http://image17-c.poco.cn/mypoco/myphoto/20160309/23/17351665220160309234005020.jpg?430x430_120) 


##技术背景
   
   app store 
   facebook   html5   native app 
   Hybrid app   native +  web   混合模式 
   

##视频课程简介

1.基础语法

2.API和组件

3.App更新 热更新上架

4.实战项目  3个  RN技术开发 

##0、配套视频(下载地址)：https://yunpan.cn/cY4JWzTtmVyNY  访问密码 7b60 或 http://vdisk.weibo.com/s/aLDC43gEH4wZV


#1、手把手教React Native实战之环境搭建
React Native 的宗旨是，学习一次，高效编写跨平台原生应用。

在Windows下搭建React Native Android开发环境

1.安装jdk

2.安装sdk
 
 在墙的环境下，为了速度我选择了使用http://androiddevtools.cn/

3.安装C++环境

择Windows SDK、cygwin或mingw等其他C++环境。编译node.js的C++模块时需要用到。

4.安装Node.js与Git

Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。Node.js 使用了一个事件驱动、非阻塞式 I/O 的模型，使其轻量又高效。Node.js 的包管理器 npm，是全球最大的开源库生态系统

 [点击下载msysgit](https://git-for-windows.github.io/)

建议设置npm镜像以加速后面的过程（或使用科学上网工具）。

设置全局使用指定的镜像

npm config set registry https://registry.npm.taobao.org

npm config set disturl https://npm.taobao.org/dist

5.安装React Native命令行工具


github下载

npm install -g react-native-cli

6.创建项目

react-native init DongFang

7.运行packager  进入工程目录

react-native start

可以用浏览器访问http://localhost:8081/index.android.bundle?platform=android看看是否可以看到打包后的脚本

8.准备模拟器或真机 运行android

react-native run-android

问题：找不到sdk  或者 无法正常化 sdk路径  解决办法：环境变量

问题：failed to find target with hash string 'android-23' in: F:\Android_SDK    解决版本：更新23版本的sdk

问题：build成功后是红色的：没有连接服务器js Server
解决方法：ip地址+8081端口  例子：192.168.1.100:8081

9.调试app
  菜单  reload js

##1、配套视频(下载地址)：https://yunpan.cn/cY4JtUGe5X5NW  访问密码 91a6 或 http://vdisk.weibo.com/s/aLDC43gEH4w_e

#2、手把手教React Native实战之从React到RN
###React简介
RN是基于React设计，了解React有助于我们开发RN应用；
React希望将功能分解化，让开发变得像搭积木一样，快速而且可维护

React主要有如下3个特点：

*作为UI（Just the UI）

*虚拟DOM（Virtual DOM）

这是亮点  是React最重要的一个特性  放进内存   最小更新的视图

差异部分更新 diff算法

*数据流（Date Flow）单向数据流

学习React需要掌握哪些知识？

*JSX语法   类似XML

*ES6相关知识

*前端基础  CSS+DIV  JS

举例说明React的用法，IDE工具：WebStorm(JavaScript 开发工具 Web前端开发神器  插件很丰富)

比如：ReactNative 代码智能提醒（webstorm）

`git clone https://github.com/virtoolswebplayer/ReactNative-LiveTemplate`

下载模板：https://github.com/wix/react-templates安装命令
`npm install react-templates -g`

[点击下载WebStorm](https://www.jetbrains.com/webstorm/download/)


[点击下载WebStorm破解版](http://www.cr173.com/soft/130969.html)

1.例子一（简单组件和数据传递）
使用this.props 指向自己的属性

从http://facebook.github.io/react/downloads.html下载react Kit

react.js react-dom.js：React的核心文件

JSXTransformer.js browser.min.js：讲JSX转译成js和html的工具

最新的react版本：react-0.14.7

>在react 0.14前，浏览器端实现对jsx的编译依赖jsxtransformer.js 
在react 0.14后，这个依赖的库改为browser.js，页面script标签的type也由text/jsx改为text/babel
但是以上只能用来测试学习react
生产环境需要借助编译工具事先将jsx编译成js 

例如可以使用Node.js做预编译，可以安装react-tools工具
npm install -g react-tools



2.例子二（通过this.state更新视图）


3.例子三（简单应用）

###React Native简介与代码分析

###为什么要使用React Native
如何在开发成本和用户体验做到更好的平衡？
很多时候，前端都有一种乐观的想法：H5可以替代原生应用
RN不仅可以使用前端开发的模式来开发应用，还能调用原生应用的UI组件和API

##2、配套视频(下载地址)：https://yunpan.cn/cY4JX8Aj5Vr9Y  访问密码 413d 或 http://vdisk.weibo.com/s/aLDC43gEHngfd

#3、手把手教React Native实战之flexbox布局(RN基础)
flexbox是Flexible Box的缩写，弹性盒子布局  主流的浏览器都支持

flexbox布局是伸缩容器(container)和伸缩项目(item)组成

Flexbox布局的主体思想是元素可以改变大小以适应可用空间，当可用空间变大，Flex元素将伸展大小以填充可用空间，当Flex元素超出可用空间时将自动缩小。总之，Flex元素是可以让你的布局根据浏览器的大小变化进行自动伸缩。

按照伸缩流的方向布局

伸缩容器有主轴和交叉轴组成！ 主轴既可以是水平轴，也可以是垂直轴

flexbox目前还处于草稿状态，所有在使用flexbox布局的时候，需要加上各个浏览器的私有前缀，即-webkit -moz -ms -o等

###伸缩容器的属性

1.display
  
  display:flex | inline-flex 

  块级伸缩容器   行内级伸缩容器

2.flex-direction
  
  指定主轴的方向 flex-direction:row（默认值）| row-reverse | column | column-reverse

3.flex-wrap

  伸缩容器在主轴线方向空间不足的情况下，是否换行以及该如何换行

  flex-wrap:nowrap（默认值） | wrap | wrap-reverse

4.flex-flow

是flex-direction和flex-wrap的缩写版本，它同时定义了伸缩容器的主轴和侧轴
，其默认值为 row nowrap

5.justify-content

用来定义伸缩项目在主轴线的对齐方式，语法为：
justify-content:flex-start（默认值） | flex-end | center | space-between | space-around

6.align-items

用来定义伸缩项目在交叉轴上的对齐方式，语法为：
align-items:flex-start（默认值） | flex-end | center | baseline | stretch

7.align-content

用来调整伸缩项目出现换行后在交叉轴上的对齐方式，语法为：
align-content:flex-start | flex-end | center | space-between | space-around | stretch（默认值）



##3、配套视频(下载地址)：https://yunpan.cn/cY4JGpecp5K7c  访问密码 b832 或 http://vdisk.weibo.com/s/aLDC43gEHnge_

#4、手把手教React Native实战之flexbox布局(伸缩属性)

###伸缩项目的属性

1.order

定义项目的排列顺序，数值越小，排列越靠前，默认值为0，语法为：order：整数值

2.flex-grow

定义伸缩项目的放大比例，默认值为0，即表示如果存在剩余空间，也不放大，语法为：flex-grow：整数值

3.flex-shrink

定义伸缩项目的收缩能力，默认值为1 ，其语法为：flex-shrink:整数值

4.flex-basis

用来设置伸缩项目的基准值，剩余的空间按比率进行伸缩，其语法为：flex-basis:length | auto，默认值为auto

5.flex

是flex-grow flex-shrink flex-basis这三个属性的缩写，其语法为：flex:none | flex-grow flex-shrink flex-basis，其中第二个和第三个参数为可选参数，默认值为：0 1 auto

6.align-self

用来设置单独的伸缩项目在交叉轴上的对齐方式，会覆盖默认的对齐方式，其语法为：align-self:auto | flex-start | flex-end | center | baseline | stretch(伸缩项目在交叉轴方向占满伸缩容器，如果交叉轴为垂直方向的话，只有在不设置高度的情况下才能看到效果)

###在React Native中使用flexbox

RN目前主要支持flexbox的如下6个属性：

1.alignItems

用来定义伸缩项目在交叉轴上的对齐方式，语法为：
alignItems:flex-start（默认值） | flex-end | center | stretch

2.alignSelf

用来设置单独的伸缩项目在交叉轴上的对齐方式，会覆盖默认的对齐方式，其语法为：alignSelf:auto | flex-start | flex-end | center | stretch(伸缩项目在交叉轴方向占满伸缩容器，如果交叉轴为垂直方向的话，只有在不设置高度的情况下才能看到效果)

3.flex

是flex-grow flex-shrink flex-basis这三个属性的缩写，其语法为：flex:none | flex-grow flex-shrink flex-basis，其中第二个和第三个参数为可选参数，默认值为：0 1 auto

4.flexDirection

指定主轴的方向 flex-direction:row| row-reverse | column（默认值） | column-reverse

5.flexWrap

6.justifyContent



##4、配套视频(下载地址)：https://yunpan.cn/cYIG6dCUNIRkB  访问密码 d6b6 或 http://vdisk.weibo.com/s/aLDC43gEHngf9

#5、手把手教React Native实战之盒子模型BoxApp

用HTML5和React Native分别实现盒子模型显示

写法不一样：

1.样式

![样式不同](http://image17-c.poco.cn/mypoco/myphoto/20160323/00/17351665220160323002240032.png?854x367_130)

2.元素

![元素不同](http://image17-c.poco.cn/mypoco/myphoto/20160323/00/17351665220160323002422011.png?1468x163_130)

3.书写格式

![书写格式1](http://image17-c.poco.cn/mypoco/myphoto/20160323/00/1735166522016032300253208.png?852x215_130)

![书写格式2](http://image17-c.poco.cn/mypoco/myphoto/20160323/00/17351665220160323002653079.png?898x374_130)



##5、配套视频(下载地址)：https://yunpan.cn/cYIGk4LBKw4y6  访问密码 fd93 或 http://vdisk.weibo.com/s/aLDC43gEHngeF



#6、手把手教React Native实战之JSX入门

React是由ReactJS与React Native组成，其中ReactJS是Facebook开源的一个前端框架，React Native是ReactJS思想在native上的体现！

JSX并不是一门新的语言，仅仅是个语法糖，允许开发者在JavaScript中书写HTML语法。，最后每个HTML标签都转化为JavaScript代码来运行

1.环境

2.载入方式

3.标签  HTML标签 与  ReactJS创建的组件类标签(首字母一定要大写)

4.转换 解析器

  `<h3>输入</h3>`  转换成：

React.createElement("h3",null,"输入") 返回一个ReactElement对象

5.执行JavaScript表达式

var msg="我是东方耀";

`<h1>{msg}</h1>`

React.createElement("h1",null,msg)

6.注释
   单行：//
   多行：/*注释文本*/

7.属性

  `var msg=<h1 width="10px">我是东方耀</h1>`

  React.createElement("h1",{width:"10px"},"我是东方耀")

8.延展属性
 
 使用ES6的语法

 var props={};
 props.foo="1";
 props.bar="1";

 `<h1 {...props} foo="2" >欢迎关注我的微信号</h1>` 转换成：

React.createElement("h1",React.__spread({},props,{foo:"2"}),"欢迎关注我的微信号")

9.自定义属性(HTML5给出了方案，凡是以data-开头的自定义属性，可渲染到页面)

10.显示HTML 显示一段HMTL字符串，而不是html节点

借助一个属性 _html

`<div>{{_html:'<h1>我是东方耀，欢迎关注我的微信号</h1>'}}</div>`

11.样式的使用

style属性   js对象  外层{}按照JSX语法  内层{}是JavaScript对象

12.事件绑定

 注意：onClick  调用bind方法（设定作用域，要传递的参数）


##6、配套视频(下载地址)：https://yunpan.cn/cYINUwNP6nj57  访问密码 6890 或 http://vdisk.weibo.com/s/aLDC43gEHnfPV

#7、手把手教React Native实战之ReactJS

ReactJS核心思想：组件化  维护自己的状态和UI  自动重新渲染  

多个组件组成了一个ReactJS应用

React是全局对象   顶层API与组件API

React.createClass创建组件类的方法

React.render渲染，将指定组件渲染到指定DOM节点

render:组件级API,返回组件的内部结构


React.render被ReactDOM.render替代

##7、配套视频(下载地址)：https://yunpan.cn/cYNfQsCXm3byY  访问密码 cf7f 或 http://vdisk.weibo.com/s/aLDC43gEHngyO


#8、手把手教React Native实战之ReactJS组件生命周期

1.创建阶段

getDefaultProps：处理props的默认值 在React.createClass调用


2.实例化阶段

React.render(<HelloMessage 启动之后

getInitialState、componentWillMount、render、componentDidMount

state：组件的属性，主要是用来存储组件自身需要的数据，每次数据的更新都是通过修改state属性的值，ReactJS内部会监听state属性的变化，一旦发生变化的话，就会主动触发组件的render方法来更新虚拟DOM结构

虚拟DOM：将真实的DOM结构映射成一个JSON数据结构


3.更新阶段

主要发生在用户操作之后或父组件有更新的时候，此时会根据用户的操作行为进行相应的页面结构的调整

componentWillReceiveProps、shouldComponentUpdate、componentWillUpdate、render、componentDidUpdate

4.销毁阶段

销毁时被调用，通常做一些取消事件绑定、移除虚拟DOM中对应的组件数据结构、销毁一些无效的定时器等工作

componentWillUnmount


##8、配套视频(下载地址)：https://yunpan.cn/cYid89wLX5w3c  访问密码 3f0d 或 http://vdisk.weibo.com/s/aLDC43gEHngyv


#9、手把手教React Native实战之ReactJS组件通信

ReactJS组件关系是一层套一层，DOM结构 组织结构比较清晰

父组件 子组件

1.子组件如何调用父组件
 
this.props

2.父组件如何调用子组件

首先用属性ref给子组件取个名字吧

this.refs.名字.getDOMNode().


##9、配套视频(下载地址)：https://yunpan.cn/cYCbUCrEAFIyy  访问密码 5dbf 或 http://vdisk.weibo.com/s/aLDC43gEHngyu


#10、手把手教React Native实战之JSX实战

React Native中没有DOM的概念，只有组件的概念，所以我们在ReactJS中使用的Html标签以及对DOM的操作是不起作用的，但是组件的生命周期、JSX的语法、事件绑定、自定义属性等，在RN和ReactJS中是一样的。


##10、配套视频(下载地址)：https://yunpan.cn/cYaddHwY52Jiz  访问密码 e877 或 http://vdisk.weibo.com/s/aLDC43gEHngr8


#11、手把手教React Native实战之调试与打包发布

http://localhost:8081/index.android.bundle?platform=android；当应用启动运行的时候，会自动拉取这个bundle文件，该文件里存放的是应用的全部逻辑代码，在目录中并不存在这个文件，事实上，这个地址只是一个请求地址，而非真正的静态资源文件，是通过包服务器packager通过动态分析index.android.js中的依赖，并对其进行合并得到的，而且该服务允许代码实时渲染。

1.生成一个签名密钥

`keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000`

最后它会生成一个叫做my-release-key.keystore的密钥库文件

2.找到路径/android/app/src/main，并在该目录下新建assets文件夹

3.在工程目录下将index.android.bundle下载并保存到assets资源文件夹中

`curl -k "http://localhost:8081/index.android.bundle" > android/app/src/main/assets/index.android.bundle`

这句命令是重点，如果assets目录中不存在该文件，则打包的apk在执行时显示空白。

Protocol 'http not supported or disabled in libcurl

Windows下安装使用curl命令:http://jingyan.baidu.com/article/a681b0dec4c67a3b1943467c.html

4.添加gradle的android keystore配置

打包的apk在未签名的情况下,在手机中（非root）是不允许安装的

在build.gradle文件中

  //签名
`signingConfigs{
    release {
        storeFile file("/my-release-key.keystore")
        storePassword "密码"
        keyAlias "keyAlias的名字"
        keyPassword "密码"
    }
}
 buildTypes {
    release {
        minifyEnabled false
        proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        signingConfig signingConfigs.release //添加这句话引用签名配置
    }
}`


5.启用Proguard代码混淆来缩小APK文件的大小

Proguard是一个Java字节码混淆压缩工具，它可以移除掉React Native Java（和它的依赖库中）中没有被使用到的部分，最终有效的减少APK的大小。

重要：启用Proguard之后，你必须再次全面地测试你的应用。Proguard有时候需要为你引入的每个原生库做一些额外的配置。参见app/proguard-rules.pro文件。

def enableProguardInReleaseBuilds = true


6.在/android/目录中执行gradle assembleRelease命令，打包后的文件在 android/app/build/outputs/apk目录中，例如app-release.apk。如果打包碰到问题可以先执行 gradle clean 清理一下。

安装gradle工具（版本与android\gradle\wrapper下的一致），并配置环境变量，配置GRADLE_HOME到你的gradle根目录当中，然后把%GRADLE_HOME%/bin（linux或mac的是$GRADLE_HOME/bin）加到PATH的环境变量。

配置完成之后，运行gradle -v，检查一下是否安装无误


7.将apk发布到各大应用市场（BUILD SUCCESSFUL）


##11、配套视频(下载地址)：https://yunpan.cn/cYaCjA9nINHx3  访问密码 05a4


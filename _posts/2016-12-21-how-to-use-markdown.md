---
layout: post
title:  如何使用LessOrMore这个Jekyll模版
date:   2016-12-21 11:44:00 +0800
categories: 技术栈
tag: 教程
---

* content
{:toc}
#MarkDown  常用语法(经测试最多支持六级标题)
-------------------------------------
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
####### 七级标题
------------------------------------

##无序列表
- 文本1
- 文本2
- 文本3

##有序列表
1. 有序文本1
2. 有序文本2
3. 有序文本3

注：- ，1.和文本之间要保留一个字符的空格。
----------------------------------------

##链接和图片

在 Markdown 中，插入链接不需要其他按钮，你只需要使用 [显示文本](链接地址) 这样的语法即可，例如：

[简书](http://www.jianshu.com)

在 Markdown 中，插入链接不需要其他按钮，你只需要使用 [显示文本](链接地址) 这样的语法即可，例如：

![](http://ww4.sinaimg.cn/bmiddle/aa397b7fjw1dzplsgpdw5j.jpg)


![](http://ww4.sinaimg.cn/large/a9dcb8f3gw1fayeaq8y04j20go0b3dgc.jpg)

注：插入图片的语法和链接的语法很像，只是前面多了一个 ！。


##引用
在我们写作的时候经常需要引用他人的文字，这个时候引用这个格式就很有必要了，在 Markdown 中，你只需要在你希望引用的文字前面加上 > 就好了，例如：

> 一盏灯， 一片昏黄； 一简书， 一杯淡茶。 守着那一份淡定， 品读属于自己的寂寞。 保持淡定， 才能欣赏到最美丽的风景！ 保持淡定， 人生从此不再寂寞。

注：> 和文本之间要保留一个字符的空格。

###诗的引用
> 朝辞白帝彩云间 
> 
> 千里江陵一日还 
> 
> 两岸猿声啼不住 
> 
> 轻舟已过万重山



##粗体和斜体
Markdown 的粗体和斜体也非常简单，用两个 * 包含一段文本就是粗体的语法，用一个 * 包含一段文本就是斜体的语法。例如：

 *一盏灯*， 一片昏黄；**一简书**， 一杯淡茶。 守着那一份淡定， 品读属于自己的寂寞。 保持淡定， 才能欣赏到最美丽的风景！ 保持淡定，人生从此不再寂寞。

 跟着我**左手右手一个慢动作**，这首歌给你快乐，**你会不会爱上我**！


##代码的应用

代码引用
需要引用代码时，如果引用的语句只有一段，不分行，可以用 ` 将语句包起来。
如果引用的语句为多行，可以将```置于这段代码的首行和末行。
代码引用的案例截图：

`this.setIndeterminateDrawable(context.getResources().getDrawable(R.drawable.loading)) ;`


<!--lang:java-->
		public MyProgressDialog(Context context) {
		super(context,R.style.progressDialog);
		this.context=context;
		}

	public MyProgressDialog(Context context, int theme) {
		super(context, theme);
		this.context=context;
		}


	    

##表格
	
	| Tables        | Are           | Cool  |
	| ------------- |:-------------:| -----:|
	| col 3 is      | right-aligned | $1600 |
	| col 2 is      | centered      |   $12 |
	| zebra stripes | are neat      |    $1 |
	
	
	
	dog | bird | cat
	----|------|----
	foo | foo  | foo
	bar | bar  | bar
	baz | baz  | baz

----------------------

##Markdown 支持以下这些符号前面加上反斜杠来帮助插入普通的符号：

当然，项目列表很可能会不小心产生，像是下面这样的写法：

1986. What a great season.
换句话说，也就是在行首出现数字-句点-空白，要避免这样的状况，你可以在句点前面加上反斜杠。

1986\. What a great season.

1.  \   反斜线
1.  `   反引号
1.  *   星号
1.  _   底线
1.  {}  花括号
1.  []  方括号
1.  ()  括弧
1.  #   井字号
1.  +   加号
1.   -  减号
1.  .   英文句点
1.  !   惊叹号

---------------------


### 列表项目可以包含多个段落，每个项目下的段落都必须缩进 4 个空格或是 1 个制表符：

 1.	This is a list item with two paragraphs. Lorem ipsum dolor
    sit amet, consectetuer adipiscing elit. Aliquam hendrerit
    mi posuere lectus.

	Vestibulum enim wisi, viverra nec, fringilla in, laoreet
    vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
    sit amet velit.

2.  Suspendisse id sem consectetuer libero luctus adipiscing.


*   This is a list item with two paragraphs.

    This is the second paragraph in the list item. You're
only required to indent the first line. Lorem ipsum dolor
sit amet, consectetuer adipiscing elit.

*   Another item in the same list.

#####如果你每行都有缩进，看起来会看好很多，当然，再次地，如果你很懒惰，Markdown 也允许(见上)：


##如果要放代码区块的话，该区块就需要缩进两次，也就是 8 个空格或是 2 个制表符：

*   一列表项包含一个列表区块：

        < this.setIndeterminateDrawable(context.getResources().getDrawable(R.drawable.loading)) ;  >

Here is an example of AppleScript:

    tell application "Foo"
        beep
    end tell

   <div class="footer">
        &copy; 2004 Foo Corporation
    </div>

	package com.eshore.wifibroadband.views;
	
	import android.app.ProgressDialog;
	import android.content.Context;
	import android.os.Bundle;
	import android.view.LayoutInflater;
	import android.view.View;
	import android.view.animation.Animation;
	import android.view.animation.AnimationUtils;
	import android.widget.ImageView;
	import android.widget.LinearLayout;
	import android.widget.TextView;
	
	import com.eshore.wifibroadband.R;
	
	public class MyProgressDialog extends ProgressDialog {
		
	private  Context  context;

	public MyProgressDialog(Context context) {
		super(context,R.style.progressDialog);
		this.context=context;
	}

	public MyProgressDialog(Context context, int theme) {
		super(context, theme);
		this.context=context;
	}

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		 this.setIndeterminateDrawable(context.getResources().getDrawable(R.drawable.loading)) ;  
	     this.setCanceledOnTouchOutside(false) ; 
	     
	        View  view=LayoutInflater.from(context).inflate(R.layout.item_progress_dialog_view, null);
	        // main.xml中的ImageView  
	        ImageView spaceshipImage = (ImageView) view.findViewById(R.id.image_loading);  
	        TextView tipTextView = (TextView) view.findViewById(R.id.tv_msg);// 提示文字  
	        // 加载动画  
            Animation hyperspaceJumpAnimation = AnimationUtils.loadAnimation(  
	        // 使用ImageView显示动画  
            spaceshipImage.startAnimation(hyperspaceJumpAnimation);  
	        tipTextView.setText("加载中...");// 设置加载信息  
	        
	        this.setContentView((LinearLayout)view, new LinearLayout.LayoutParams(  
	                LinearLayout.LayoutParams.MATCH_PARENT,  
	                LinearLayout.LayoutParams.MATCH_PARENT));// 设置布局  
	}
	
				@Override
				public void show() {
					// TODO Auto-generated method stub
					super.show();
				}

	}


未完待续，之后再补充...
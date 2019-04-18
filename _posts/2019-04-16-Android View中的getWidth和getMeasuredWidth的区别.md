---
layout: post
title: "View中的getWidth和getMeasuredWidth的区别"
date:   2019-3-15 15:46 +0800
categories: Android
tag: 经验
---

* content
{:toc}




- 先上一张图 View核心方法调用顺序应该是
-----------------------------------------

构造函数——->onMeasure——->onSizeChanged——->onLayout——->onDraw——-> onMeasure——->onLayout——->onDraw 

![View的核心方法调用顺序图](https://i.imgur.com/f3JwZGD.jpg)

 

- View getMeasuredWidth 源码剖析：
----------------------------------------

    public final int getMeasuredWidth() {
			 return mMeasuredWidth & MEASURED_SIZE_MASK;
	}

	public static final int MEASURED_SIZE_MASK = 0x00ffffff;

 换算成二进制是：111111111111111111111111，在与运算中，1 与任何数字进行与运算的结果都取决于对方。所以，mMeasuredWidth 变量值决定了 getMeasuredWidth() 方法的返回值。进一步查看，mMeasuredWidth 的赋值在这里：
    
    private void setMeasuredDimensionRaw(int measuredWidth, int measuredHeight) {
	    mMeasuredWidth = measuredWidth;
	    mMeasuredHeight = measuredHeight;
	    mPrivateFlags |= PFLAG_MEASURED_DIMENSION_SET;
    }

但这个方法是私有方法，在 View 类内部调用，在setMeasuredDimension()被调用：
    
    protected final void setMeasuredDimension(int measuredWidth, int measuredHeight) {
		 boolean optical = isLayoutModeOptical(this);
	    // 只展示核心代码
	    ...
		setMeasuredDimensionRaw(measuredWidth, measuredHeight);
    }

进一步看setMeasuredDimension()在onMeasure()方法中被调用：

     protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
    	setMeasuredDimension(getDefaultSize(getSuggestedMinimumWidth(), widthMeasureSpec),
    	getDefaultSize(getSuggestedMinimumHeight(), heightMeasureSpec));
    }

**可以看出，mMeasuredWidth 的赋值，即 getMeasuredWidth() 的取值最终来源于 setMeasuredDimension() 方法调用时传递的参数！在自定义 View 时测量并设置 View 宽高时经常用到。通常在 onMeasure() 方法中设置，可以翻看一下系统中的 TextView、LinearLayout 等方法，都是如此。**


- getWidth 源码剖析
-------------------------

    public final int getWidth() {
		return mRight - mLeft;
	}

    mRight、mLeft 变量分别表示 View 相对父容器的左右边缘位置，并且二者的赋值是通过 setFrame() 方法赋值：
    
    // Assign a size and position to this view.
     *
    //This is called from layout.
    
    protected boolean setFrame(int left, int top, int right, int bottom) {
    boolean changed = false;
    		// 只展示核心代码
    		...
    mLeft = left;
    mTop = top;
    mRight = right;
    mBottom = bottom;
    ...
    }
    
    从注释中可以看到该方法被layout()调用
    
    public void layout(int l, int t, int r, int b) {
       ... 
       boolean changed = isLayoutModeOptical(mParent) ?
    setOpticalFrame(l, t, r, b) : setFrame(l, t, r, b);
       ...
    }
    其中setOpticalFrame()内部也是调用setFrame()方法


**所以，getWidth() 的取值最终来源于 layout() 方法的调用。通常，layout() 方法在 parent 中被调用，来确定 child views 在父容器中的位置，一般在自定义 ViewGroup 的 onLayout() 方法中调用**

## 分析完源码，可以知道：
measuredWidth 值在 View 的 measure 阶段决定的，是通过 setMeasuredDimension() 方法赋值的；
width 值在 layout 阶段决定的，是由 layout() 方法决定的。
有一点需要注意，通常来讲，View 的 width 和 height 是由 View 本身和 parent 容器共同决定的。

getMeasuredWidth()获取的是view原始的大小，也就是这个view在XML文件中配置或者是代码中设置的大小。getWidth（）获取的是这个view最终显示的大小，这个大小有可能等于原始的大小也有可能不等于原始大小。
一般情况下，getWidth() 与 getMeasuredWidth() 的返回值是相同的。
** 注意在自定义View或者ViewGroup中，在 onLayout() **方法中通过 child.getMeasuredWidth() 方法获取 child views 的原始大小来设置其显示区域，不要用getWidth()，有可能获得值为0（诸如 LinearLayout 之类的系统中的 ViewGroup 都是这么做的；

除此之外，我们都可以通过 getWidth() 方法获取 View 的实际显示宽度。** ##

##或者简言之：
- getMeasuredWidth方法获得的值是setMeasuredDimension方法设置的值，它的值在measure方法运行后就会确定
- getWidth方法获得是layout方法中传递的四个参数中的mRight-mLeft，它的值是在layout方法运行后确定的 
- 一般情况下在onLayout方法中使用getMeasuredWidth方法，而在除onLayout方法之外的地方用getWidth方法。





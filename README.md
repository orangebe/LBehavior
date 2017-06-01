## LBehavior: Simple implementation of sliding animation of title bar, bottom bar and floatingActionButton.


[![](https://jitpack.io/v/Lauzy/LBehavior.svg)](https://jitpack.io/#Lauzy/LBehavior)

[中文文档](/README_CN.md)

# ScreenShoot


<img src="/screenshoots/screen1.gif" alt="screenshot" title="screenshot" width="270" height="460" /> <img src="/screenshoots/screen2.gif" alt="screenshot" title="screenshot" width="270" height="460" /> <img src="/screenshoots/screen3.gif" alt="screenshot" title="screenshot" width="270" height="460" />


# Blog Introduce

CSDN: [http://blog.csdn.net/freedompaladin/article/details/70253391]

JianShu: [http://www.jianshu.com/p/2974d8ffc3a5](http://www.jianshu.com/p/2974d8ffc3a5)

Personal WebSite: [http://lauzy.me/2017/04/14/Behavior/](http://lauzy.me/2017/04/14/Behavior/)

## Download
```java
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
	}

    dependencies {
        compile 'com.android.support:design:25.3.1'(latestVersion)
        compile 'com.github.Lauzy:LBehavior:VERSION_CODE'
	}
```
The version code of the latest release can be found [here](https://github.com/Lauzy/LBehavior/releases)

# Usage


Xml file：

The root layout must be CoordinatorLayout，which is similar to FrameLayout
```xml
    <android.support.design.widget.CoordinatorLayout
        ...>
		<FloatingActionButton
 			...
			app:layout_behavior="@string/fab_vertical_behavior/>
    </android.support.design.widget.CoordinatorLayout>
```


Set different layout_behavior in xml file according to different view.



Param     							|	Explanation
-----------------------------------|-----------------------
@string/title_view_behavior   		|   Title Layout
@string/bottom_view_behavior   	|   Bottom Layout
@string/fab_scale_behavior   		|   FloatingActionBar（scale anim）
@string/fab_vertical_behavior   	|   FloatingActionBar（slide anim）



Custom properties(All have default values)：


| Function           	 	|    Param           	| Explanation  			|
| ------------------------- |------------------ | --------------------- |
| setMinScrollY				| int y 			| Sets the minimum sliding distance for triggering the animation, default value is 5 pixels.|
| setScrollYDistance		| int y      	    | 设置触发动画的滑动距离，防止用户缓慢滑动时单次滑动距离一直小于setMinScrollY的最小滑动距离导致无法触发动画.如设置此值为100，则用户即便缓慢滑动，当滑动距离达到100时也可触发动画.默认为40.|
| setDuration				| int duration     	| 设置动画持续时间.默认为400ms.|
| setInterpolator			| Interpolator interpolator | 设置动画插补器，修饰动画效果.默认模式为LinearOutSlowInInterpolator. [Interpolator官方文档](https://developer.android.google.cn/reference/android/view/animation/Interpolator.html)|


```java

	CommonBehavior.from(mFloatingActionButton).show();//show the view
	CommonBehavior.from(mFloatingActionButton).hide();//hide

	CommonBehavior.from(mFloatingActionButton)
		.setMinScrollY(20)
		.setScrollYDistance(100)
		.setDuration(1000)
		.setInterpolator(new LinearOutSlowInInterpolator());
```

## Tips

1、因为根布局为CoordinatorLayout，所以使用时Toolbar可能会遮盖RecyclerView顶部的item，BottomBar也可能会遮盖底部item。
可以参考知乎首页设置顶部留白，具体可为RecyclerView添加一个占位的ItemDecoration，或者顶部加一个占位的View，若场景比较固定可简单设置Padding，Margin等，
详情可见Demo，简单处理了这种情况。


2、FloatingActionButton的elevation若大于BottomBar的elevation，则FloatingActionButton动画覆盖在BottomBar上层，反之则在下层，为gif的下部两个按钮的效果。


## Apk and More Info

For more usage, you can download or clone the demo. You can also [download the demo apk](https://github.com/Lauzy/LBehavior/raw/master/apk/demo.apk).









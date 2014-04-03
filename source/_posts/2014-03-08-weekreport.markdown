---
layout: post
title: "每周一记"
date: 2014-03-08 17:45
comments: true
categories: iOS,Objective-C,iOS开发工具
---
{% img /images/2014/03/08/week.jpg %}

由于上次的博文发现大家对工具还是蛮感兴趣的，所以今天也是由工具开头。之后说一些我这周工作中遇到的问题，可以给大家分享一下。
<!--more-->

##工具介绍

###<a href="https://github.com/dblock/fui" target="_blank">FUI</a>
可能我们应用中经常import了很多类，但是经过不停的修改后可能已经不需要导入这个类，可是我们没有删除#import，这样会导致我们编译速度变慢，这个工具就是帮你发现你导入但未使用的类。


###<a href="http://objclean.com/index.php" target="_blank">OBJECTIVE-CLEAN</a>
这个工具可以更好的约束团队中每个人代码规范，可以设置一个配置文件，之后团队中每个人如何不符合代码规范就会提示警告和错误。

###<a href="https://itunes.apple.com/cn/app/liya/id455484422?mt=12" target="_blank">Liya</a>
sqlite查看工具，可能大家都使用过MesaSQLite这个工具，但是我觉得这个工具更方便和友好，大家可以试试。

###<a href="http://luckymarmot.com/paw" target="_blank">Paw</a>
一款可以管理HTTP & REST API工具，界面非常漂亮，比chrome插件postman更友好，推荐给大家，可以更好的管理接口，定位问题。

##工作中遇到的问题

###UIButton居中图片和文字

我们都知道UIbutton可以中使用UIEdgeInsetsMake可以改变text和image来居中，但是网上大部分的例子都没有考虑到当字符长度很长出现省略号的时候就不会居中，下面这个UIButton的category可以实现无论字多长都会居中而且可以设置图片在文字上面还是下面。

``` objective-c button居中
- (void)centerImageAndButton:(CGFloat)gap imageOnTop:(BOOL)imageOnTop {
	NSInteger sign = imageOnTop ? 1 : -1;
	
	CGSize imageSize = self.imageView.frame.size;
	self.titleEdgeInsets = UIEdgeInsetsMake((imageSize.height+gap)*sign, -imageSize.width, 0, 0);
	
	CGSize titleSize = self.titleLabel.bounds.size;
	self.imageEdgeInsets = UIEdgeInsetsMake(-(titleSize.height+gap)*sign, 0, 0, -titleSize.width);  
}
```

{%ribbonp warning Xcode一打开就Crash重装无效%}
最终发现<a href="https://github.com/ricobeck/KFCocoaPodsPlugin" target="_blank">KFCocoaPodsPlugin</a>是这个插件的问题，可能是我系统升级到10.9.2了与这个插件不兼容导致的，但是有的人不会出现，我已经联系了作者，最后知道了原来xcode卸载重装，第三方插件是不会清除的。
{%endribbonp%}






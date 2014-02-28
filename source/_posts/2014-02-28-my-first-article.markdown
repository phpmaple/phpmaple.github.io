---
layout: post
title: "启程"
date: 2014-02-28 13:39
comments: true
categories: iOS生涯集
---
{% img /images/2014/02/28/start.jpg %}

引言：其实这个网站已经有了很长时间，但是一直都没有写下一篇博文，可能是没有时间，可能是偷懒，可以找出一大堆的理由，但是久而久之，发现学的越多，似乎知道的就越少了，所以还是决定记录点什么，哪怕只是一些憋足的字也好，坚信：坚持一些东西，总会获得一些回报。
<!--more-->

## 下面介绍一下我常用的iOS开发或者优化的小工具
由于很多工具大多数博客都已经介绍过了，我就列举一些我认为还不错但是大家不常列举的：
***

### <a href="https://github.com/krzysztofzablocki/crafter" target="_blank">Crafter</a>

你是否经常见一个Project之后你经常会建立一个Podfile，然后把自己一些几乎每个项目都要用的第三方库加进去或者，添加ignore文件等等重复的事情，Crafter 是一个可以自动化初始化你xcode工程的默认配置，是由Ruby语言写的。一个script即可以自动化帮你配置好你的项目。

### <a href="http://wasted.werk01.de/" target="_blank">Wasted</a>

你是否关心过一个问题，项目体积越来越大，然而图片的体积占了大部分，Wasted只要选取一个ipa文件就可以帮你分析出哪些可以优化，然后生成了一个文件夹是他帮你优化过的图片还有一个表格，你可以选择性的替换原项目的图片，肉眼几乎感觉不到优化前后的区别。

### <a href="https://github.com/jeffhodnett/Unused" target="_blank">Unused</a>

之前看到很多人已经说过可以用一个script来检测出项目中未使用过的图片然后用生成一个文件来告诉你哪些没有使用过，这个工具用可视化的界面来检测告诉你更亲切。

### <a href="https://itunes.apple.com/cn/app/linguan/id477163052?mt=12" target="_blank">Linguan</a>

是否遇到过一种情况项目起初只有一种语言，经过后续很多版本更新之后老板要求你出个多过语言版本，但是那么多的项目文件和xib，显然手动的去寻找是不科学的，这款工具就可以帮你找出项目里的所有string包括xib中的然后可以导出.Strings格式，然后交给你们翻译的就可以了。


## 然后在翻译一段iOS小文（水平有限）
***
### 声明Blocks内联
译自<a href="http://macoscope.com/blog/calling-blocks-inline/" target="_blank">Calling Blocks Inline</a>

我最新发现了一个在oc中使用Blocks非常有趣的的方法,它定义起来也许像in javascript里那样，样子是这样的：
```objective-c
const NSInteger value = (^NSInteger {
    switch (type) {
        case TypeOne:
            return 1;

        case TypeTwo:
            return 2;

        case TypeUnknown:
        case TypeUnspecified:
            return NSNotFound;

        default:
            return 0;
    }
}());
```

首选，它在定义这个Block的同时赋值给了我们的变量，然后指定了变量是`const`类型，Block内所有相关的代码都是为了计算出值赋值给变量，这样一来代码更容易阅读，而且这都可以被GCC code block extension所识别，这种方法实现的有点就是可以有`return`这个关键词，这使得我们可以是用`switch`并且循环里不使用`break`，缺点是不得不重复声明变量的类型，而且当我们遇到`UISwipeGestureRecognizerDirection`是非常讨厌的，例如：

```objective-c
const BOOL anyValueIsXyz = (^BOOL {
  for (QwertyValue *value in values) {
    if (value.isXyz) {
      return YES;
    }
  }

  return NO;
}());
```

大家认为呢？
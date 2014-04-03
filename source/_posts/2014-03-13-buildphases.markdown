---
layout: post
title: "Xcode之BuildPhases"
date: 2014-03-13 19:04
comments: true
categories: iOS,Objective-C
---
{% img /images/2014/03/13/build-phases.jpg %}

引言：Build Phases是Xcode在build的时候执行的一些任务，这次就关于代码优化和重构方面，来说说Build Phases可以帮助我们的一些Script，还请大家补充。
<!--more-->

##Build Phrases与Xcode插件

1.谈到重构，如果我们想在后期把我们的项目重构一下，这不仅可以让我们重新巩固一下用到的iOS知识，还可以提高我们对整个项目理解和代码水平，其中重构的最简单的一个方法就是从代码行数开始检查，从我了解和经验我们暂可以规定每行代码不超过80个字符，每个函数不超过限定在50-80行之间，这样对于我们开发者以后的维护来说，简洁的代码更容易进行修改和维护。每个类最好保持在400行以内，如果太多就可以考虑重构一下你的类了，我发现1000行代码看着真的头晕，下面一个Build Phrases就可以帮助你检查你所有m文件大于400行的类，warning提示你。

```objective-c
find "${SRCROOT}" \( -name "*.m" \) -and \( -path "${SRCROOT}/Pods/*" -prune -o -
print0 \) | xargs -0 wc -l | awk '$1 > 400 && $2 != "total" {for(i=2;i<NF;i++){printf "%s%s", $i, " "} print $NF ":1: warning: File more than 400 lines (" $1 "), consider refactoring." }'      
```

如果你需要更好的改善你的代码推荐<a href="http://oclint.org/" target="_blank">OCLint</a>可以更好的帮你改善代码质量，可以配合<a href="https://github.com/facebook/xctool" target="_blank">xctool</a>很强大。如果你约束能里不大好，那推荐你<a href="https://itunes.apple.com/us/app/objective-clean/id713910413?mt=12" target="_blank">Objective-Clean</a>，这样如果你不符合规则就等着不能Build吧。其实这样蛮好的O.O。当然你也可以使用<a href="http://www.jetbrains.com/objc/" target="_blank">AppCode</a>这个强大的编辑器来改善。

2.还有一个好的方法是经常在项目中使用TODO，FIXME等，这样可以帮助我们下次浏览项目快速定位和提醒你哪些代码需要继续改进，这段Build Phrases可以用warning的方式提醒你哪些需要处理，相比<a href="https://github.com/trawor/XToDo" target="_blank">XToDo</a>这个插件更为直观不需要你打开界面去寻找，直接提示，但是如果你要可视化界面也可以用XToDo这款插件，还是很不错的。

```objective-c
KEYWORDS="TODO|FIXME|\?\?\?:|\!\!\!:"
find "${SRCROOT}" \( -name "*.h" -or -name "*.m" \) -and \( -path "${SRCROOT}/Pods/*" -prune -o -print0 \) | xargs -0 egrep --with-filename --line-number --only-matching "($KEYWORDS).*\$" | perl -p -e "s/($KEYWORDS)/ warning: \$1/"
```

3.再推荐一个Xcode小技巧是Edit all in Scope 这个功能，这个功能就强大了，而且比较酷，适合进行大批量的修改变量和方法；选定一个想要修改的字符串，然后选择Edit－Edit all in Scope，然后在你输入的时候，所有该字符出现的地方都进行同步更改，看起来很cool的。

4.再推荐一个工具，你也许会遇到项目中使用自定义的外部字体，虽然导入项目中修改plist文件可以用代码来改变字体，但是在xib中选择字体是没有，你必须连接到代码中修改，很麻烦，所以推荐一款工具安装后添加一个Build Phrases就可以在xib中随意的选择外部字体了。工具叫<a href="http://pitaya.ch/moarfonts/" target="_blank">Moarfonts</a>，如果项目，可以考虑一下，还是不错的。

5.最后再推荐两款xcode插件，代码规范/美化工具<a href="https://github.com/benoitsan/BBUncrustifyPlugin-Xcode" target="_blank">BBUncrustifyPlugin-Xcode</a>,这边是配置文件<a href="https://github.com/bengardner/uncrustify/blob/master/etc/objc.cfg" target="_blank">关于objc语言的</a>。第二个插件是推荐给更新到xcode5.1的，由于改善了autolayout，可能这款插件可以更方便的布局<a href="https://github.com/RolandasRazma/RRConstraintsPlugin" target="_blank">RRConstraintsPlugin</a>

结语：如果大家需要Moarfonts，我可以共享一下<a href="https://www.dropbox.com/s/21cokfqw8gvgd0v/moarfonts-1.0.3.zip" target="_blank">Moarfonts</a>如果觉得可以可以支持一下作者，如果小伙伴有更好的实用的Build Phrases可以分享<a href="http://weibo.com/phpmaple" target="_blank">@Koofrank</a>



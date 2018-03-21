---
layout: default
title: Android Studio Logcat 设置不显示某些自定义匹配的文本的日志行
---

# Android Studio Logcat 设置不显示某些自定义匹配的文本的日志行

Logcat中经常会显示很多我们不需要的日志信息，常常有刷屏的感觉，我们可以把某些不需要的日志信息通过正则表达式匹配进行隐藏起来。

这是没有过滤的时候：
![image](/assets/android_logcat_verbose.png)

这是过滤之后的样子：
![image](/assets/android_logcat_regex.png)

用到的正则表达式如下：
```
[VIDWE]/(?!ViewRootImpl@)
```

简单解释一下，匹配不包含是利用正则表达式的`零宽度负预测先行断言`，上面的 `VIDWE` 是为了匹配 Android 日志的5个级别，后面的 `ViewRootImpl@` 就是我们不希望看到包含的日志行的内容。

关于正则表达式的介绍可以参考：[正则表达式30分钟入门教程](http://deerchao.net/tutorials/regex/regex.htm)。

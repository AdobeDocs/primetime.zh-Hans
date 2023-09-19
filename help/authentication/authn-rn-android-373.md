---
title: Authentication Android 3.7.3发行说明
description: Authentication Android 3.7.3发行说明
source-git-commit: fbc0e710d205532d268213ca0bdc81449e9c9835
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Authentication Android 3.7.3发行说明 {#android-sdk-370-release-notes}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权使用。

本页介绍了此版本的新增功能、更改和已知问题：

## 内部版本号 {#build-no-android-sdk-373}

Adobe Primetime身份验证： Android 3.7.3

发行日期： 2023年9月19日



## 发行版概述 {#overview-android-sdk-370}

* 更改了对Android 14和面向API级别34的应用程序的支持
   * 添加标记必填项 [Android 14运行时注册的广播接收器](https://developer.android.com/about/versions/14/behavior-changes-14#runtime-receivers-exported).
* 修复在模拟器API 32及更高版本上无法为MVPD登录打开的ChromeCustomTabs
   * 注意： SDK &lt;3.7.3上此问题的解决方法是：在模拟器上打开Chrome应用程序，并在尝试进行MVPD登录之前完成设置


## 发行包 {#rel=pkg-android373}

您可以从下载Android SDK v3.7.3 [此处](https://tve.zendesk.com/hc/en-us/articles/204963219-Android-Native-AccessEnabler-Library).

在升级到此版本之前，请查看此技术说明。
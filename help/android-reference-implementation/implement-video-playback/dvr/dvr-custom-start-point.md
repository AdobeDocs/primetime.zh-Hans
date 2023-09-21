---
description: 您可以选择自定义起点，确定何时输入DVR流，而不是默认行为，即开始使用ConfigProvider类输入DVR流。
title: 为DVR选择自定义起点
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# 为DVR选择自定义起点 {#choosing-a-custom-starting-point-for-dvr}

您可以选择自定义起点，确定何时输入DVR流，而不是默认行为，即开始使用ConfigProvider类输入DVR流。

要设置开始时间 [配置提供程序](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) class：

1. 启用 [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled()).
1. 设置开始时间 [retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref()).
1. 检查自定义起始位置是否已启用。

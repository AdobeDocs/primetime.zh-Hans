---
description: 您可以为何时输入DVR流选择自定义起始点，而不是使用ConfigProvider类在开始时输入DVR流的默认行为。
title: 为DVR选择自定义起点
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# 为DVR {#choosing-a-custom-starting-point-for-dvr}选择自定义起点

您可以为何时输入DVR流选择自定义起始点，而不是使用ConfigProvider类在开始时输入DVR流的默认行为。

要通过[ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html)类设置开始时间：

1. 启用[isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled())。
1. 在[retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref())中设置开始时间。
1. 检查自定义开始位置是否已启用。

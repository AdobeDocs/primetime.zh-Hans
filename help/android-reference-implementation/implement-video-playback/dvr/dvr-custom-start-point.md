---
description: 您可以选择何时输入DVR流的自定义起始点，而不是使用ConfigProvider类在开始时输入DVR流的默认行为。
seo-description: 您可以选择何时输入DVR流的自定义起始点，而不是使用ConfigProvider类在开始时输入DVR流的默认行为。
seo-title: 为DVR选择自定义起点
title: 为DVR选择自定义起点
uuid: a7e13865-2b86-4234-ac4c-9a5320b293db
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# 为DVR {#choosing-a-custom-starting-point-for-dvr}选择自定义起点

您可以选择何时输入DVR流的自定义起始点，而不是使用ConfigProvider类在开始时输入DVR流的默认行为。

通过[ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html)类设置开始时间：

1. 启用[isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled())。
1. 在[retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref())中设置开始时间。
1. 检查自定义开始位置是否已启用。

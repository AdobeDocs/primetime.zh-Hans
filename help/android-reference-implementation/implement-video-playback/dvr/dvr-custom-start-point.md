---
description: 您可以为何时输入DVR流选择自定义起始点，而不是使用ConfigProvider类在开始时输入DVR流的默认行为。
seo-description: 您可以为何时输入DVR流选择自定义起始点，而不是使用ConfigProvider类在开始时输入DVR流的默认行为。
seo-title: 为DVR选择自定义起点
title: 为DVR选择自定义起点
uuid: a7e13865-2b86-4234-ac4c-9a5320b293db
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 为DVR选择自定义起点 {#choosing-a-custom-starting-point-for-dvr}

您可以为何时输入DVR流选择自定义起始点，而不是使用ConfigProvider类在开始时输入DVR流的默认行为。

要通过 [ConfigProvider类设置开始时间](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) :

1. 启 [用isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled())。
1. 在retrieveStartTimePref() [中设置开始时间](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref())。
1. 检查自定义开始位置是否已启用。

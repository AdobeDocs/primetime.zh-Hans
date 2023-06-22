---
description: 您可以选择用于输入DVR流的自定义起始点，而不是默认行为，即在开始时使用ConfigProvider类输入DVR流。
title: 为DVR选择自定义起点
exl-id: 9813bf60-a91d-4376-a5fe-02311b73e8a0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# 为DVR选择自定义起点 {#choosing-a-custom-starting-point-for-dvr}

您可以选择用于输入DVR流的自定义起始点，而不是默认行为，即在开始时使用ConfigProvider类输入DVR流。

要设置开始时间，请执行以下操作： [配置提供程序](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) 类：

1. 启用 [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled()).
1. 设置开始时间 [retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref()).
1. 检查自定义起始位置是否已启用。

---
description: 当您不再需要MediaResource时，您应该发布MediaPlayer实例和资源。
seo-description: 当您不再需要MediaResource时，您应该发布MediaPlayer实例和资源。
seo-title: 发布MediaPlayer实例和资源
title: 发布MediaPlayer实例和资源
uuid: e7b2112e-8add-4789-9345-5f829d39d639
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# 释放MediaPlayer实例和资源{#release-a-mediaplayer-instance-and-resources}

当您不再需要MediaResource时，您应该发布MediaPlayer实例和资源。

释放`MediaPlayer`对象时，将取消分配与此`MediaPlayer`对象关联的基础硬件资源。

以下是释放`MediaPlayer`的一些原因：

* 保留不必要的资源可能会影响性能。
* 如果设备不支持同一视频编解码器的多个实例，则其他应用程序可能会出现播放失败。

1. 释放`MediaPlayer`。

   ```
   function release():void;
   ```

释放`MediaPlayer`实例后，您不能再使用它。 如果在释放`MediaPlayer`接口后调用其任何方法，则会引发`IllegalStateException`。
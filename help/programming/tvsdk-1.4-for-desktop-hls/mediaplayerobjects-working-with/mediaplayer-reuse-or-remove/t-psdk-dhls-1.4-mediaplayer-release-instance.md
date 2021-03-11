---
description: 当您不再需要MediaResource时，您应释放MediaPlayer实例和资源。
title: 发布MediaPlayer实例和资源
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# 释放MediaPlayer实例和资源{#release-a-mediaplayer-instance-and-resources}

当您不再需要MediaResource时，您应释放MediaPlayer实例和资源。

释放`MediaPlayer`对象时，将取消分配与此`MediaPlayer`对象关联的基础硬件资源。

以下是释放`MediaPlayer`的一些原因：

* 持有不必要的资源会影响性能。
* 如果设备上不支持同一视频编解码器的多个实例，则其他应用程序可能会出现播放失败。

1. 释放`MediaPlayer`。

   ```
   function release():void;
   ```

释放`MediaPlayer`实例后，您不能再使用它。 如果在释放`MediaPlayer`接口后调用其任何方法，则引发`IllegalStateException`。
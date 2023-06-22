---
description: 当您不再需要MediaResource时，应该发布MediaPlayer实例和资源。
title: 发布MediaPlayer实例和资源
exl-id: 2a802754-5c51-4e5f-8c36-843074b487b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# 发布MediaPlayer实例和资源{#release-a-mediaplayer-instance-and-resources}

当您不再需要MediaResource时，应该发布MediaPlayer实例和资源。

当您发布 `MediaPlayer` 对象，与此对象关联的底层硬件资源 `MediaPlayer` 对象被取消分配。

以下是发布的原因 `MediaPlayer`：

* 持有不必要的资源可能会影响性能。
* 如果同一设备不支持同一视频编解码器的多个实例，则其他应用程序可能会发生播放失败。

1. 发布 `MediaPlayer`.

   ```
   function release():void;
   ```

在 `MediaPlayer` 实例已发布，您无法再使用它。 如果使用的任何方法 `MediaPlayer` 界面在发布后调用，即 `IllegalStateException` 被抛出。

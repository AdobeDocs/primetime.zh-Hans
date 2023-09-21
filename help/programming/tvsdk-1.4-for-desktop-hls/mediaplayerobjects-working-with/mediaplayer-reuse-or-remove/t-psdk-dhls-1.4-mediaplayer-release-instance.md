---
description: 当您不再需要MediaResource时，应该发布MediaPlayer实例和资源。
title: 发布MediaPlayer实例和资源
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# 发布MediaPlayer实例和资源{#release-a-mediaplayer-instance-and-resources}

当您不再需要MediaResource时，应该发布MediaPlayer实例和资源。

当您发布 `MediaPlayer` 对象，与此对象关联的底层硬件资源 `MediaPlayer` 对象被取消分配。

以下是发布的原因 `MediaPlayer`：

* 保留不必要的资源可能会影响性能。
* 如果某个设备上不支持同一视频编解码器的多个实例，则其他应用程序可能会发生播放失败。

1. 发布 `MediaPlayer`.

   ```
   function release():void;
   ```

在 `MediaPlayer` 实例已发布，您无法再使用它。 如果使用的任何 `MediaPlayer` 在发布界面后调用，其中 `IllegalStateException` 被抛出。

---
description: 当您不再需要MediaResource时，您应该发布MediaPlayer实例和资源。
seo-description: 当您不再需要MediaResource时，您应该发布MediaPlayer实例和资源。
seo-title: 发布MediaPlayer实例和资源
title: 发布MediaPlayer实例和资源
uuid: e7b2112e-8add-4789-9345-5f829d39d639
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 发布MediaPlayer实例和资源{#release-a-mediaplayer-instance-and-resources}

当您不再需要MediaResource时，您应该发布MediaPlayer实例和资源。

释放对象时， `MediaPlayer` 将取消分配与此对象关联的底层硬件 `MediaPlayer` 资源。

以下是发布Adobe Cloud的一些理由 `MediaPlayer`:

* 保留不必要的资源可能会影响性能。
* 如果设备上不支持同一视频编解码器的多个实例，则其他应用程序可能会出现播放失败。

1. 释放 `MediaPlayer`。

   ```
   function release():void;
   ```

在发 `MediaPlayer` 布实例后，您不能再使用它。 如果在释放接口 `MediaPlayer` 的任何方法后调用它，则会引 `IllegalStateException` 发一个方法。
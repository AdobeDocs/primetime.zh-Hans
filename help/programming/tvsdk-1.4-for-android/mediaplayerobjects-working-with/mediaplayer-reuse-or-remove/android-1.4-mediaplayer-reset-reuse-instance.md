---
description: 重置MediaPlayer实例时，它将返回到其未初始化的IDLE状态，如MediaPlayerState中所定义。
seo-description: 重置MediaPlayer实例时，它将返回到其未初始化的IDLE状态，如MediaPlayerState中所定义。
seo-title: 重置或重用MediaPlayer实例
title: 重置或重用MediaPlayer实例
uuid: 72cc4511-8ab0-44e5-b93c-b36f0321bba8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 重置、重用或删除MediaPlayer实例 {#reset-or-reuse-a-mediaplayer-instance}

您可以重置、重用或释放您不再需要的MediaPlayer实例。

重置MediaPlayer实例时，它将返回到其未初始化的IDLE状态，如MediaPlayerState中所定义。

此操作在以下情况下很有用：

* 您希望重复使 `MediaPlayer` 用实例，但需要加载新(视 `MediaResource` 频内容)并替换以前的实例。

   重置允许您重复使用实 `MediaPlayer` 例，而无需释放资源、重新创建资源 `MediaPlayer`和重新分配资源。

* 当它处 `MediaPlayer` 于ERROR状态并且需要清除时。

   >[!IMPORTANT]
   >
   >这是从ERROR状态恢复的唯一方法。

1. 调用 `reset` 以将实例返 `MediaPlayer` 回到其未初始化状态：

   ```java
   void reset() throws IllegalStateException; 
   ```

1. 使用 `MediaPlayer.replaceCurrentResource` 加载其他 `MediaResource`。

   >[!TIP]
   >
   >要清除错误，请加载相同的错误 `MediaResource`。

1. 当您收到具有PREPARED `STATUS_CHANGED` 状态的事件回调时，开始播放。

## 发布MediaPlayer实例和资源{#release-a-mediaplayer-instance-and-resources}

当您不再需要MediaResource时，您应该发布MediaPlayer实例和资源。

释放对象时， `MediaPlayer` 将取消分配与此对象关联的底层硬件 `MediaPlayer` 资源。

以下是发布MediaPlayer的一些理由：

* 保留不必要的资源可能会影响性能。
* 留下不必要 `MediaPlayer` 的对象可导致移动设备的电池持续消耗。
* 如果设备上不支持同一视频编解码器的多个实例，则其他应用程序可能会出现播放失败。

1. 释放 `MediaPlayer`。

   ```java
   void release() throws IllegalStateException;
   ```

在发 `MediaPlayer` 布实例后，您不能再使用它。 如果在释放接口 `MediaPlayer` 的任何方法后调用它，则会引 `IllegalStateException` 发一个方法。
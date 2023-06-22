---
description: 重置MediaPlayer实例时，该实例将返回到MediaPlayerState中定义的未初始化的IDLE状态。
title: 重置或重用MediaPlayer实例
exl-id: db8264f7-2f33-4441-86db-bb985edf7c3c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# 重置、重用或删除MediaPlayer实例 {#reset-or-reuse-a-mediaplayer-instance}

您可以重置、重用或释放不再需要的MediaPlayer实例。

重置MediaPlayer实例时，该实例将返回到MediaPlayerState中定义的未初始化的IDLE状态。

此操作在以下情况下很有用：

* 您希望重用 `MediaPlayer` 实例，但需要加载新的 `MediaResource` （视频内容）并替换上一个实例。

   通过重置，您可以重复使用 `MediaPlayer` 实例无需释放资源，重新创建 `MediaPlayer`，并重新分配资源。

* 当 `MediaPlayer` 处于错误状态，需要清除。

   >[!IMPORTANT]
   >
   >这是从ERROR状态恢复的唯一方法。

1. 调用 `reset` 以返回 `MediaPlayer` 实例恢复到其未初始化状态：

   ```java
   void reset() throws IllegalStateException; 
   ```

1. 使用 `MediaPlayer.replaceCurrentResource` 加载另一个 `MediaResource`.

   >[!TIP]
   >
   >要清除错误，请加载相同的 `MediaResource`.

1. 当您收到 `STATUS_CHANGED` PREPARED状态的事件回调，开始播放。

## 发布MediaPlayer实例和资源{#release-a-mediaplayer-instance-and-resources}

当您不再需要MediaResource时，应该发布MediaPlayer实例和资源。

当您发布 `MediaPlayer` 对象，与此对象关联的底层硬件资源 `MediaPlayer` 对象被取消分配。

以下是发布MediaPlayer的一些原因：

* 持有不必要的资源可能会影响性能。
* 保留不必要的 `MediaPlayer` 对象会导致移动设备持续消耗电池。
* 如果同一设备不支持同一视频编解码器的多个实例，则其他应用程序可能会发生播放失败。

1. 发布 `MediaPlayer`.

   ```java
   void release() throws IllegalStateException;
   ```

在 `MediaPlayer` 实例已发布，您无法再使用它。 如果使用的任何方法 `MediaPlayer` 界面在发布后调用，即 `IllegalStateException` 被抛出。

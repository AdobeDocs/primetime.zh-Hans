---
description: 您可以重置、重用或释放不再需要的MediaPlayer实例。
title: 重用或删除MediaPlayer实例
exl-id: 8b84c7f1-713a-46b4-8eb7-d699a79e74b7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# 重用或删除MediaPlayer实例 {#reuse-or-remove-a-mediaplayer-instance}

您可以重置、重用或释放不再需要的MediaPlayer实例。

## 重置或重用MediaPlayer实例 {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

当您重置 `MediaPlayer` 实例时，会返回到其未初始化的IDLE状态，如中所定义 `MediaPlayerStatus`.

此操作在以下情况下很有用：

* 您希望重用 `MediaPlayer` 实例，但需要加载新的 `MediaResource` （视频内容）并替换上一个实例。

   通过重置，您可以重复使用 `MediaPlayer` 实例无需释放资源，重新创建 `MediaPlayer`，并重新分配资源。

* 当 `MediaPlayer` 处于错误状态，需要清除。

   >[!IMPORTANT]
   >
   >这是从ERROR状态恢复的唯一方法。

   1. 调用 `reset` 以返回 `MediaPlayer` 实例恢复到其未初始化状态：

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. 使用 `MediaPlayer.replaceCurrentResource()` 加载另一个 `MediaResource`.

      >[!NOTE]
      >
      >要清除错误，请加载相同的 `MediaResource`.

   1. 当您收到 `STATUS_CHANGED` 事件回调方式 `PREPARED` 状态，开始播放。

## 发布MediaPlayer实例和资源 {#section_13A0914AFF784943ABC343F7EB249C4E}

您应该发布 `MediaPlayer` 实例和资源 `MediaResource`.

当您发布 `MediaPlayer` 对象，与此对象关联的底层硬件资源 `MediaPlayer` 对象被取消分配。

以下是发布的原因 `MediaPlayer`：

* 持有不必要的资源可能会影响性能。
* 保留不必要的 `MediaPlayer` 实例化的对象可能导致移动设备持续的电池消耗。
* 如果某个设备上不支持同一视频编解码器的多个实例，则其他应用程序可能会发生播放失败。

* 发布 `MediaPlayer`.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >在 `MediaPlayer` 实例已发布，您无法再使用它。 如果使用的任何方法 `MediaPlayer` 界面在发布后调用，即 `MediaPlayerException` 被抛出。

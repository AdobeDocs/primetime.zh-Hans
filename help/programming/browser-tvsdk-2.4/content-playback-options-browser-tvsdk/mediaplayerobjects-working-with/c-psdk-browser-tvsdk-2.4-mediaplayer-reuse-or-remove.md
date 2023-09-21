---
description: 您可以重置、重用或释放不再需要的MediaPlayer实例。
title: 重用或删除MediaPlayer实例
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# 重用或删除MediaPlayer实例{#reuse-or-remove-a-mediaplayer-instance}

您可以重置、重用或释放不再需要的MediaPlayer实例。

## 重置或重用MediaPlayer实例 {#section_C183E6164C184C3CBC5321FC6A2528EA}

您可以重置 `MediaPlayer` 实例以将其返回到在中定义的未初始化空闲状态 `MediaPlayerStatus`. 也可以替换当前的媒体项目，或使用以前加载的媒体资源设置新的媒体项目。

此操作在以下情况下很有用：

* 您希望重用 `MediaPlayer` 实例，但需要加载新的 `MediaResource` （视频内容）并替换上一个实例。

  重置允许您重复使用 `MediaPlayer` 实例没有释放资源的开销，重新创建 `MediaPlayer`以及重新分配资源。 此 `replaceCurrentItem` 方法会自动为您执行这些步骤。

* 当 `MediaPlayer` 处于错误状态，需要清除。

  >[!IMPORTANT]
  >
  >这是从ERROR状态恢复的唯一方法。

1. 调用 `MediaPlayer.reset()` 以返回 `MediaPlayer` 实例处于未初始化状态：

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. 调用 `MediaPlayer.replaceCurrentItem()` 加载另一个 `MediaResource`

   >[!TIP]
   >
   >要清除错误，请加载相同的 `MediaResource`.

1. 调用 `prepareToPlay()` 方法。

   >[!NOTE]
   >
   >当您收到 `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` 事件处于“已准备”状态，可以开始播放。

## 发布MediaPlayer实例和资源 {#section_2D159975C82245098E7078FE0B1578CE}

您应该发布 `MediaPlayer` 实例和资源。

以下是发布的原因 `MediaPlayer`：

* 保留不必要的资源可能会影响性能。
* 留下不必要的 `MediaPlayer` 目标会导致移动设备持续消耗电池。
* 如果某个设备上不支持同一视频编解码器的多个实例，则其他应用程序可能会发生播放失败。

* 发布 `MediaPlayer`.

  ```js
  void release()
  ```

  >[!NOTE]
  >
  >在 `MediaPlayer` 实例已发布，您无法再使用它。 如果使用的任何 `MediaPlayer` 在发布界面后调用，其中 `IllegalStateException` 被抛出。

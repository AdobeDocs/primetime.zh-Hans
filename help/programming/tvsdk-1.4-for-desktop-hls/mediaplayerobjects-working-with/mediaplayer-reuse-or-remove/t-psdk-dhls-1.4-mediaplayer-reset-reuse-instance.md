---
description: 重置MediaPlayer实例时，该实例将返回到MediaPlayerStatus中定义的未初始化的IDLE状态。
title: 重置或重用MediaPlayer实例
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 重置或重用MediaPlayer实例{#reset-or-reuse-a-mediaplayer-instance}

您可以重置、重用或释放不再需要的MediaPlayer实例。

重置MediaPlayer实例时，该实例将返回到MediaPlayerStatus中定义的未初始化的IDLE状态。

此操作在以下情况下很有用：

* 您希望重用 `MediaPlayer` 实例，但需要加载新的 `MediaResource` （视频内容）并替换上一个实例。

  重置允许您重复使用 `MediaPlayer` 实例没有释放资源的开销，重新创建 `MediaPlayer`以及重新分配资源。 此 `replaceCurrentItem` 和 `replaceCurrentResource` 方法会自动为您执行这些步骤，而无需调用reset方法。

* 当 `MediaPlayer` 状态为“错误”，需要清除。

  >[!IMPORTANT]
  >
  >这是从ERROR状态恢复的唯一方法。

1. 调用 `reset` 以返回 `MediaPlayer` 实例处于未初始化状态：

   ```
   function reset():void; 
   ```

1. 使用 `MediaPlayer.replaceCurrentItem` 或 `MediaPlayer.replaceCurrentResource` 加载另一个 `MediaResource`.

   >[!TIP]
   >
   >要清除错误，请加载相同的 `MediaResource`.

1. 当您收到 `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` 使用 `PREPARED` 状态，开始播放。

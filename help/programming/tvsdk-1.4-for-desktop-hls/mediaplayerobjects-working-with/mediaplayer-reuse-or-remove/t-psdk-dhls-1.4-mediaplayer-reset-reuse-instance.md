---
description: 重置MediaPlayer实例时，它将返回到其未初始化的IDLE状态，如MediaPlayerStatus中所定义。
seo-description: 重置MediaPlayer实例时，它将返回到其未初始化的IDLE状态，如MediaPlayerStatus中所定义。
seo-title: 重置或重用MediaPlayer实例
title: 重置或重用MediaPlayer实例
uuid: b376096b-0aed-4ac2-96e5-e30a4eaf742e
translation-type: tm+mt
source-git-commit: c547002eb8946f8ccc5a79d0836f3f814e823b97

---


# 重置或重用MediaPlayer实例{#reset-or-reuse-a-mediaplayer-instance}

您可以重置、重用或释放您不再需要的MediaPlayer实例。

重置MediaPlayer实例时，它将返回到其未初始化的IDLE状态，如MediaPlayerStatus中所定义。

此操作在以下情况下很有用：

* 您希望重复使 `MediaPlayer` 用实例，但需要加载新(视 `MediaResource` 频内容)并替换以前的实例。

   重置允许您重复使用实 `MediaPlayer` 例，而无需释放资源、重新创建资源 `MediaPlayer`和重新分配资源。 这些 `replaceCurrentItem` 和方 `replaceCurrentResource` 法会自动为您执行这些步骤，而无需调用reset方法。

* 当ERROR `MediaPlayer` 状态为且需要清除时。

   >[!IMPORTANT]
   >
   >这是从ERROR状态中恢复的唯一方法。

1. 调用 `reset` 以将实例返 `MediaPlayer` 回到其未初始化状态：

   ```
   function reset():void; 
   ```

1. 使用 `MediaPlayer.replaceCurrentItem` 或 `MediaPlayer.replaceCurrentResource` 加载其他 `MediaResource`。

   >[!TIP]
   >
   >要清除错误，请加载相同的错误 `MediaResource`。

1. 当您收到具有状 `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` 态的 `PREPARED` 文件时，开始播放。

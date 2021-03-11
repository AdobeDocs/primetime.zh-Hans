---
description: 重置MediaPlayer实例时，它将返回到MediaPlayerStatus中定义的未初始化的IDLE状态。
title: 重置或重用MediaPlayer实例
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---


# 重置或重用MediaPlayer实例{#reset-or-reuse-a-mediaplayer-instance}

您可以重置、重用或释放不再需要的MediaPlayer实例。

重置MediaPlayer实例时，它将返回到MediaPlayerStatus中定义的未初始化的IDLE状态。

此操作在以下情况下很有用：

* 您希望重用`MediaPlayer`实例，但需要加载新的`MediaResource`（视频内容）并替换以前的实例。

   重置允许您重用`MediaPlayer`实例，而不会产生释放资源、重新创建`MediaPlayer`和重新分配资源的开销。 `replaceCurrentItem`和`replaceCurrentResource`方法会自动为您执行这些步骤，无需调用reset方法。

* 当`MediaPlayer`具有ERROR状态并需要清除时。

   >[!IMPORTANT]
   >
   >这是从ERROR状态恢复的唯一方法。

1. 调用`reset`将`MediaPlayer`实例返回到其未初始化状态：

   ```
   function reset():void; 
   ```

1. 使用`MediaPlayer.replaceCurrentItem`或`MediaPlayer.replaceCurrentResource`加载另一个`MediaResource`。

   >[!TIP]
   >
   >要清除错误，请加载相同的`MediaResource`。

1. 当您收到状态为`PREPARED`的`MediaPlaybackStatusChangeEvent.STATUS_CHANGED`时，请开始播放。

---
description: 重置MediaPlayer实例时，它将返回到MediaPlayerState中定义的未初始化的IDLE状态。
title: 重置或重用MediaPlayer实例
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---


# 重置、重用或删除MediaPlayer实例{#reset-or-reuse-a-mediaplayer-instance}

您可以重置、重用或释放不再需要的MediaPlayer实例。

重置MediaPlayer实例时，它将返回到MediaPlayerState中定义的未初始化的IDLE状态。

此操作在以下情况下很有用：

* 您希望重用`MediaPlayer`实例，但需要加载新的`MediaResource`（视频内容）并替换以前的实例。

   重置允许您重用`MediaPlayer`实例，而不会产生释放资源、重新创建`MediaPlayer`和重新分配资源的开销。

* 当`MediaPlayer`处于ERROR状态并需要清除时。

   >[!IMPORTANT]
   >
   >这是从ERROR状态恢复的唯一方法。

1. 调用`reset`将`MediaPlayer`实例返回到其未初始化状态：

   ```java
   void reset() throws IllegalStateException; 
   ```

1. 使用`MediaPlayer.replaceCurrentResource`加载另一个`MediaResource`。

   >[!TIP]
   >
   >要清除错误，请加载相同的`MediaResource`。

1. 当您收到具有PREPARED状态的`STATUS_CHANGED`事件回调时，请开始播放。

## 释放MediaPlayer实例和资源{#release-a-mediaplayer-instance-and-resources}

当您不再需要MediaResource时，您应释放MediaPlayer实例和资源。

释放`MediaPlayer`对象时，将取消分配与此`MediaPlayer`对象关联的基础硬件资源。

以下是发布MediaPlayer的一些原因：

* 持有不必要的资源会影响性能。
* 保留不必要的`MediaPlayer`对象可导致移动设备的电池持续消耗。
* 如果设备上不支持同一视频编解码器的多个实例，则其他应用程序可能会出现播放失败。

1. 释放`MediaPlayer`。

   ```java
   void release() throws IllegalStateException;
   ```

释放`MediaPlayer`实例后，您不能再使用它。 如果在释放`MediaPlayer`接口后调用其任何方法，则引发`IllegalStateException`。
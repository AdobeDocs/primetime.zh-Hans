---
description: 您可以重置、重用或释放不再需要的MediaPlayer实例。
title: 重用或删除MediaPlayer实例
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# 重用或删除MediaPlayer实例{#reuse-or-remove-a-mediaplayer-instance}

您可以重置、重用或释放不再需要的MediaPlayer实例。

## 重置或重用MediaPlayer实例{#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

重置`MediaPlayer`实例时，该实例将返回到其未初始化的IDLE状态，如`MediaPlayerStatus`中所定义

* 您希望重用`MediaPlayer`实例，但需要加载新的`MediaResource`（视频内容）并替换以前的实例。

   重置允许您重用`MediaPlayer`实例，而不会产生释放资源、重新创建`MediaPlayer`和重新分配资源的开销。

* 当`MediaPlayer`处于“ERROR（错误）”状态时，需要清除。

   >[!IMPORTANT]
   >
   >这是从ERROR状态恢复的唯一方法。

   1. 调用`reset`将`MediaPlayer`实例返回到其未初始化状态：

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. 使用`MediaPlayer.replaceCurrentResource()`加载另一个`MediaResource`。

      >[!NOTE]
      >
      >要清除错误，请加载相同的`MediaResource`。

   1. 当您收到状态为`PREPARED`的`STATUS_CHANGED`事件回调时，请开始播放。

## 释放MediaPlayer实例和资源{#section_13A0914AFF784943ABC343F7EB249C4E}

当不再需要`MediaResource`时，您应释放`MediaPlayer`实例和资源。

释放`MediaPlayer`对象时，将取消分配与此`MediaPlayer`对象关联的基础硬件资源。

以下是释放`MediaPlayer`的一些原因：

* 持有不必要的资源会影响性能。
* 如果不必要的实例化`MediaPlayer`对象，则会导致移动设备的电池持续消耗。
* 如果设备上不支持同一视频编解码器的多个实例，则其他应用程序可能会出现播放失败。

* 释放`MediaPlayer`。

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >释放`MediaPlayer`实例后，您不能再使用它。 如果在释放`MediaPlayer`接口后调用其任何方法，则引发`MediaPlayerException`。
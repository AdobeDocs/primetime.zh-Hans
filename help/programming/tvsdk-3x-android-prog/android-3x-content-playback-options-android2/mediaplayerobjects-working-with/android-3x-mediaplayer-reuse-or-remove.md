---
description: 您可以重置、重用或释放不再需要的MediaPlayer实例。
seo-description: 您可以重置、重用或释放不再需要的MediaPlayer实例。
seo-title: 重用或删除MediaPlayer实例
title: 重用或删除MediaPlayer实例
uuid: 74a46689-1708-4d26-9a4e-a4cdb0e55451
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# 重用或删除MediaPlayer实例{#reuse-or-remove-a-mediaplayer-instance}

您可以重置、重用或释放不再需要的MediaPlayer实例。

## 重置或重用MediaPlayer实例{#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

重置`MediaPlayer`实例时，它将返回到其未初始化的IDLE状态，如`MediaPlayerStatus`中所定义。

此操作在以下情况下很有用：

* 您希望重用`MediaPlayer`实例，但需要加载新的`MediaResource`（视频内容）并替换以前的实例。

   重置允许您重用`MediaPlayer`实例，而无需释放资源、重新创建`MediaPlayer`和重新分配资源。

* 当`MediaPlayer`处于“ERROR（错误）”状态并需要清除时。

   >[!IMPORTANT]
   >
   >这是从ERROR状态中恢复的唯一方法。

   1. 调用`reset`将`MediaPlayer`实例返回其未初始化状态：

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. 使用`MediaPlayer.replaceCurrentResource()`加载另一个`MediaResource`。

      >[!NOTE]
      >
      >要清除错误，请加载相同的`MediaResource`。

   1. 当您收到状态为`PREPARED`的`STATUS_CHANGED`事件回调时，请开始播放。

## 释放MediaPlayer实例和资源{#section_13A0914AFF784943ABC343F7EB249C4E}

当您不再需要`MediaResource`时，您应该释放`MediaPlayer`实例和资源。

释放`MediaPlayer`对象时，将取消分配与此`MediaPlayer`对象关联的基础硬件资源。

以下是释放`MediaPlayer`的一些原因：

* 保留不必要的资源可能会影响性能。
* 如果不必要的实例化`MediaPlayer`对象，则会导致移动设备的电池消耗持续。
* 如果有多个实例
设备上不支持同一视频编解码器，其他应用程序可能出现播放失败。

* 释放`MediaPlayer`。

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >释放`MediaPlayer`实例后，您不能再使用它。 如果在释放`MediaPlayer`接口后调用其任何方法，则会引发`MediaPlayerException`。
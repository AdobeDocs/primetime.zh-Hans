---
description: 您可以重置、重用或释放不再需要的MediaPlayer实例。
seo-description: 您可以重置、重用或释放不再需要的MediaPlayer实例。
seo-title: 重用或删除MediaPlayer实例
title: 重用或删除MediaPlayer实例
uuid: 0b9a06b0-ece7-4e18-9221-a4528bcbc141
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# 重用或删除MediaPlayer实例{#reuse-or-remove-a-mediaplayer-instance}

您可以重置、重用或释放不再需要的MediaPlayer实例。

## 重置或重用MediaPlayer实例{#section_C183E6164C184C3CBC5321FC6A2528EA}

可以重置`MediaPlayer`实例，使其返回到`MediaPlayerStatus`中定义的未初始化的IDLE状态。 您还可以替换当前媒体项目或使用先前加载的媒体资源设置新媒体项目。

此操作在以下情况下很有用：

* 您希望重用`MediaPlayer`实例，但需要加载新的`MediaResource`（视频内容）并替换以前的实例。

   重置允许您重用`MediaPlayer`实例，而无需释放资源、重新创建`MediaPlayer`和重新分配资源。 `replaceCurrentItem`方法会自动为您执行这些步骤。

* 当`MediaPlayer`处于ERROR状态并需要清除时。

   >[!IMPORTANT]
   >
   >这是从ERROR状态恢复的唯一方法。

1. 调用`MediaPlayer.reset()`将`MediaPlayer`实例返回到其未初始化状态：

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. 调用`MediaPlayer.replaceCurrentItem()`以加载另一个`MediaResource`

   >[!TIP]
   >
   >要清除错误，请加载相同的`MediaResource`。

1. 调用`prepareToPlay()`方法。

   >[!NOTE]
   >
   >当您收到具有PREPARED状态的`MediaPlaybackStatusChangeEvent.STATUS_CHANGED`事件时，您可以开始播放。

## 释放MediaPlayer实例和资源{#section_2D159975C82245098E7078FE0B1578CE}

当您不再需要MediaResource时，您应该释放`MediaPlayer`实例和资源。

以下是释放`MediaPlayer`的一些原因：

* 保留不必要的资源可能会影响性能。
* 保留不必要的`MediaPlayer`对象可导致移动设备的电池持续消耗。
* 如果设备不支持同一视频编解码器的多个实例，则其他应用程序可能会出现播放失败。

* 释放`MediaPlayer`。

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >释放`MediaPlayer`实例后，您不能再使用它。 如果在释放`MediaPlayer`接口后调用其任何方法，则会引发`IllegalStateException`。


---
description: 您可以重置、重用或释放您不再需要的MediaPlayer实例。
seo-description: 您可以重置、重用或释放您不再需要的MediaPlayer实例。
seo-title: 重用或删除MediaPlayer实例
title: 重用或删除MediaPlayer实例
uuid: 74a46689-1708-4d26-9a4e-a4cdb0e55451
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 重用或删除MediaPlayer实例 {#reuse-or-remove-a-mediaplayer-instance}

您可以重置、重用或释放您不再需要的MediaPlayer实例。

## 重置或重用MediaPlayer实例 {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

重置实例时， `MediaPlayer` 它将返回到其未初始化的IDLE状态，如中定义 `MediaPlayerStatus`。

此操作在以下情况下很有用：

* 您希望重复使 `MediaPlayer` 用实例，但需要加载新(视 `MediaResource` 频内容)并替换以前的实例。

   重置允许您重复使用实 `MediaPlayer` 例，而无需释放资源、重新创建资源 `MediaPlayer`和重新分配资源。

* 处于“ `MediaPlayer` ERROR”状态且需要清除时。

   >[!IMPORTANT]
   >
   >这是从ERROR状态中恢复的唯一方法。

   1. 调用 `reset` 以将实例返 `MediaPlayer` 回到其未初始化状态：

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. 使用 `MediaPlayer.replaceCurrentResource()` 加载其他 `MediaResource`。

      >[!NOTE]
      >
      >要清除错误，请加载相同的错误 `MediaResource`。

   1. 当您收到状态 `STATUS_CHANGED` 的事件回 `PREPARED` 调时，开始播放。

## 发布MediaPlayer实例和资源 {#section_13A0914AFF784943ABC343F7EB249C4E}

您应该在不 `MediaPlayer` 再需要时释放实例和资源 `MediaResource`。

释放对象时， `MediaPlayer` 将取消分配与此对象关联的底层硬件 `MediaPlayer` 资源。

以下是发布Adobe Cloud的一些理由 `MediaPlayer`:

* 保留不必要的资源可能会影响性能。
* 将不必要的对 `MediaPlayer` 象实例化会导致移动设备的电池持续消耗。
* 如果设备上不支持同一视频编解码器的多个实例，则其他应用程序可能会出现播放失败。

* 释放 `MediaPlayer`。

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >在发 `MediaPlayer` 布实例后，您不能再使用它。 如果在释放接口 `MediaPlayer` 的任何方法后调用它，则会引 `MediaPlayerException` 发一个方法。
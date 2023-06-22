---
description: 事件处理程序使您能够响应TVSDK事件。
title: 实施事件侦听器和回调
exl-id: c8825a6c-3d48-412f-81f5-542c7731a122
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# 实施事件侦听器和回调 {#implement-event-listeners-and-callbacks}

事件处理程序使您能够响应TVSDK事件。

发生事件时，TVSDK的事件机制会调用已注册的事件处理程序，向其传递事件信息。

TVSDK将侦听器定义为内的公共内部接口。 `MediaPlayer` 界面。

应用程序必须为影响应用程序的任何TVSDK事件实施事件侦听器。

1. 确定应用程序必须侦听的事件。

   * 必需事件：监听所有播放事件。

      >[!IMPORTANT]
      >
      >监听状态更改事件，当播放器的状态以您需要了解的方式更改时，会发生该事件。 它提供的信息包含可能会影响播放器后续操作的错误。

   * 有关其他事件，请根据您的应用程序参阅事件摘要。

1. 为每个事件实施并添加一个事件侦听器。

   >[!NOTE]
   >
   >对于大多数事件，TVSDK会将参数传递给事件侦听器。 此类值提供有关事件的信息，可帮助您决定下一步要做什么。 此 `MediaPlayerEvent` 明细列表列出了所有符合以下条件的事件： `MediaPlayer` 调度。 有关更多信息，请参阅事件摘要。

   例如，如果 `mPlayer` 的实例 `MediaPlayer`，下面是如何添加和构建事件侦听器的：

   ```java
   mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED, new StatusChangeEventListener() { 
       @Override 
       public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
           event.getMetadata(); 
           if (event.getMetadata() != null) {/* Do something */} 
           if (event.getStatus() == MediaPlayerStatus.IDLE) {/* Do something */} 
           else if (event.getStatus() == MediaPlayerStatus.INITIALIZED) {/* Do something */} 
           else if (event.getStatus() == MediaPlayerStatus.PREPARED) {/* Do something */} 
       } 
   }); 
   ```

## 播放事件的顺序 {#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK按通常预期的序列调度事件/通知。 您的播放器可以按照预期顺序基于事件实施操作。

以下示例显示在播放期间发生的一些事件的顺序。

通过成功加载媒体资源时 `MediaPlayer.replaceCurrentResource`，事件的顺序为：

1. `MediaPlayerEvent.STATUS_CHANGED` 状态 `MediaPlayerStatus.INITIALIZING`

1. `MediaPlayerEvent.STATUS_CHANGED` 状态 `MediaPlayerStatus.INITIALIZED`

>[!TIP]
>
>在主线程上加载媒体资源。 如果在后台线程上加载媒体资源，则此操作或后续操作可能会引发错误，例如 `MediaPlayerException`，并退出。

通过准备播放时 `MediaPlayer.prepareToPlay`，事件的顺序为：

1. `MediaPlayerEvent.STATUS_CHANGED` 状态 `MediaPlayerStatus.PREPARING`

1. `MediaPlayerEvent.TIMELINE_UPDATED` 是否插入了广告。
1. `MediaPlayerEvent.STATUS_CHANGED` 状态 `MediaPlayerStatus.PREPARED`

对于实时/线性流，在播放期间，当播放窗口前进并解决其他机会时，事件的顺序为：

1. `MediaPlayerEvent.ITEM_UPDATED`
1. `MediaPlayerEvent.TIMELINE_UPDATED` 如果插入了广告

## 广告事件的顺序 {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

当您的播放包含广告时，TVSDK会按通常预期的序列发送事件/通知。 您的播放器可以根据预期序列中的事件实施操作。

在播放广告时，事件的顺序为：

* `MediaPlayerEvent.AD_RESOLUTION_COMPLETE`

将为广告时间内的每个广告调度以下事件：

* `MediaPlayerEvent.AD_BREAK_START`
* `MediaPlayerEvent.AD_START`
* `MediaPlayerEvent.AD_PROGRESS (multiple times)`
* `MediaPlayerEvent.AD_CLICK (for each click)`
* `MediaPlayerEvent.AD_COMPLETE`
* `MediaPlayerEvent.AD_BREAK_COMPLETE`

以下示例显示了广告播放事件的典型进度：

```
mediaPlayer.addEventListener(MediaPlayerEvent.AD_RESOLUTION_COMPLETE, new AdResolutionCompleteEventListener() { 
        @Override 
        public void onAdResolutionComplete() { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_BREAK_START, new AdBreakStartedEventListener() { 
         @Override 
        public void onAdBreakStarted(AdBreakPlaybackEvent adBreakPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_START, new AdStartedEventListener() { 
         @Override 
        public void onAdStarted(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_PROGRESS, new AdProgressEventListener() { 
         @Override 
         public void onAdProgress(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_COMPLETE, new AdCompletedEventListener() { 
         @Override 
         public void onAdCompleted(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_BREAK_COMPLETE, new AdBreakCompletedEventListener() { 
         @Override 
         public void onAdBreakCompleted(AdBreakPlaybackEvent adBreakPlaybackEvent) { ... } 
    }); 
 
Below event is for tracking ad clicks. 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_CLICK, new AdClickedEventListener() { 
         @Override 
         public void onAdClicked(AdClickEvent adClickEvent) { ... } 
    });
```

## DRM事件的顺序 {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK调度数字版权管理(DRM)事件以响应DRM相关操作，例如当新的DRM元数据可用时。 您的播放器可以实施操作来响应这些事件。

要接收有关所有DRM相关事件的通知，请侦听 `MediaPlayerEvent.DRM_METADATA`. TVSDK通过 `DRMManager` 类。

## 加载器事件的顺序 {#section_5638F8EDACCE422A9425187484D39DCC}

TVSDK调度 `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` 发生加载程序事件时。

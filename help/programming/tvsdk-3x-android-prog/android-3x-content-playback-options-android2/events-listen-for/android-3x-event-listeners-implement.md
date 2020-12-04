---
description: 事件处理函数使您能够响应TVSDK事件。
seo-description: 事件处理函数使您能够响应TVSDK事件。
seo-title: 实现事件监听器和回呼
title: 实现事件监听器和回呼
uuid: f186b39e-e634-4f64-977d-279147d76c5c
translation-type: tm+mt
source-git-commit: 1034a0520590777cc0930d2f732741202bc3bc04
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# 实现事件监听器和回呼{#implement-event-listeners-and-callbacks}

事件处理函数使您能够响应TVSDK事件。

发生事件时，TVSDK的事件机制将调用注册的事件处理程序，并将事件信息传递给它。

TVSDK将监听器定义为`MediaPlayer`接口内的公共内部接口。

您的应用程序必须对影响您的应用程序的任何TVSDK事件事件实施监听器。

1. 确定您的应用程序必须侦听的事件。

   * 必需事件:聆听所有播放事件。

      >[!IMPORTANT]
      >
      >侦听状态更改事件，当玩家的状态以您需要了解的方式发生更改时发生。 它提供的信息包括可能影响播放器下一步操作的错误。

   * 有关其他事件，请参阅[Primetime播放器事件摘要](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md)。

1. 为每个事件实施并添加事件监听器。

   对于大多数事件,TVSDK将参数传递给事件监听器。 这些值提供有关事件的信息，可帮助您决定下一步的操作。 `MediaPlayerEvent`明细列表列表`MediaPlayer`调度的所有事件。 有关详细信息，请参阅[Primetime播放器事件摘要](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md)。

   例如，如果`mPlayer`是`MediaPlayer`的实例，则以下是如何添加和构建事件监听器：

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

## 播放事件的顺序{#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK按通常预期的序列发送事件/通知。 您的播放器可以根据预期序列中的事件执行操作。

以下示例显示了播放过程中发生的某些事件的顺序。

成功通过`MediaPlayer.replaceCurrentResource`加载媒体资源时，事件的顺序为：

1. `MediaPlayerEvent.STATUS_CHANGED` 状态  `MediaPlayerStatus.INITIALIZING`

1. `MediaPlayerEvent.STATUS_CHANGED` 状态  `MediaPlayerStatus.INITIALIZED`

>[!TIP]
>
>在主线程上加载媒体资源。 如果在后台线程上加载媒体资源，此操作或后续操作可能会引发错误，如`MediaPlayerException`，然后退出。

通过`MediaPlayer.prepareToPlay`准备回放时，事件的顺序为：

1. `MediaPlayerEvent.STATUS_CHANGED` 状态  `MediaPlayerStatus.PREPARING`

1. `MediaPlayerEvent.TIMELINE_UPDATED` 是否插入了广告。
1. `MediaPlayerEvent.STATUS_CHANGED` 状态  `MediaPlayerStatus.PREPARED`

对于实时／线性流，在播放期间，随着播放窗口的前进以及其他机会的解决，事件的顺序是：

1. `MediaPlayerEvent.ITEM_UPDATED`
1. `MediaPlayerEvent.TIMELINE_UPDATED` 是否插入广告

## 广告事件的顺序{#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

当您的播放包括广告时，TVSDK会按通常预期的序列发送事件/通知。 您的播放器可以根据预期序列中的事件实施操作。

播放广告时，事件的顺序是：

* `MediaPlayerEvent.AD_RESOLUTION_COMPLETE`

广告分时段内的每则广告将分派以下事件:

* `MediaPlayerEvent.AD_BREAK_START`
* `MediaPlayerEvent.AD_START`
* `MediaPlayerEvent.AD_PROGRESS (multiple times)`
* `MediaPlayerEvent.AD_CLICK (for each click)`
* `MediaPlayerEvent.AD_COMPLETE`
* `MediaPlayerEvent.AD_BREAK_COMPLETE`

以下示例展示了广告播放事件的典型进度：

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

## DRM事件的顺序{#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK响应DRM相关操作（如当新的DRM元数据可用时）发送数字版权管理(DRM)事件。 您的播放器可以实施响应这些事件的操作。

要获得所有与DRM相关的事件的通知，请侦听`MediaPlayerEvent.DRM_METADATA`。 TVSDK通过`DRMManager`类发送其他DRM事件。

## 加载器事件的顺序{#section_5638F8EDACCE422A9425187484D39DCC}

TVSDK在发生加载器事件时调度`MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE`。
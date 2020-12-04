---
description: 事件处理函数允许TVSDK对事件做出响应。
seo-description: 事件处理函数允许TVSDK对事件做出响应。
seo-title: 实现事件监听器和回呼
title: 实现事件监听器和回呼
uuid: 6b7859a4-55f9-48b1-b1f1-7b79bc92610a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---


# 实现事件监听器和回调{#implement-event-listeners-and-callbacks}

事件处理函数允许TVSDK对事件做出响应。

发生事件时，TVSDK的事件机制将调用注册的事件处理程序，并将事件信息传递给该处理程序。

TVSDK将监听器定义为`MediaPlayer`接口中的公共内部接口。

您的应用程序必须为影响您的应用程序的TVSDK事件事件实施监听器。

有关视频分析事件的完整列表，请参阅跟踪核心视频播放。

1. 确定您的应用程序必须监听哪些事件。

   * **必需事件**:聆听所有播放事件。

      >[!IMPORTANT]
      >
      >播放事件`onStateChanged`提供播放器状态，包括错误。 任何状态都可能影响玩家的下一步

   * **其他事件**:可选，具体取决于您的应用程序。

      例如，如果在播放中加入广告，则实施AdPlaybackEventListener回调。

1. 为每个事件实施事件监听器。

   TVSDK将参数值返回给事件监听器回调。 这些值提供有关事件的相关信息，您可以在监听器中使用这些信息来执行适当的操作。

   `MediaPlayer.EventListener` 列表所有回调接口。每个接口显示为每个事件返回的回调名称和参数。

   例如：

   ```
   MediaPlayer.PlaybackEventListener.onStateChanged( 
    MediaPlayer.PlayerState state, MediaPlayerNotification notification)
   ```

1. 使用`MediaPlayer.addEventListener`向`MediaPlayer`对象注册回调监听器。

   ```
   mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, 
    new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onStateChanged( 
    MediaPlayer.PlayerState state, 
    MediaPlayerNotification notification) {...} 
   }
   ```

## 播放事件的顺序{#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK按通常预期的序列发送事件/通知。 您的播放器可以根据预期序列中的事件执行操作。

以下示例显示了包含播放事件的某些事件的顺序。

* 成功通过`MediaPlayer.replaceCurrentResource`加载媒体资源时，事件的顺序为：

1. `MediaPlayer.PlaybackEventListener.onStateChanged` 状态  `MediaPlayer.PlayerState.INITIALIZING`

1. `MediaPlayer.PlaybackEventListener.onStateChanged` 状态  `MediaPlayer.PlayerState.INITIALIZED`

>[!TIP]
>
>在主线程上加载媒体资源。 如果在后台线程上加载媒体资源，则此操作或后续的TVSDK操作，或两者都可能会引发错误（例如`IllegalStateException`）并退出。

* 通过`MediaPlayer.prepareToPlay`准备回放时，事件的顺序为：

1. `MediaPlayer.PlaybackEventListener.onStateChanged` 状态  `MediaPlayerStatus.PREPARING`

1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` 是否插入了广告。
1. `MediaPlayer.PlaybackEventListener.onStateChanged` 状态  `MediaPlayerStatus.PREPARED`

* 对于实时／线性流，在播放期间，随着播放窗口的前进以及其他机会的解决，事件的顺序是：

1. `MediaPlayer.PlaybackEventListener.onUpdated`
1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` 是否插入广告
1. `MediaPlayerItemEvent.ITEM_UPDATED`
1. `TimelineEvent.TIMELINE_UPDATED` 是否插入广告

以下示例显示了事件的典型进度：

```java
mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK,  
  new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() {...} 
    @Override 
    public void onUpdated() {...} 
    @Override 
    public void onPlayStart() {...} 
    @Override 
    public void onPlayComplete() {...} 
    @Override 
    public void onSizeAvailable(long height, long width) {...} 
    @Override 
    public void onStateChanged(MediaPlayer.PlayerState state,  
      MediaPlayerNotification notification) {...} 
});
```

## 广告事件的顺序{#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

当您的播放包括广告时，TVSDK会按通常预期的序列发送事件/通知。 您的播放器可以根据预期序列中的事件执行操作。

播放广告时，事件的顺序是：

* `AdPlaybackEventListener.onAdBreakStart`
* 广告分时段中的每则广告都会派发以下内容：

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` （在广告播放过程中多次）
   * `AdPlaybackEventListener.onAdClick` （对于每次单击）
   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdBreakComplete`

以下示例展示了广告播放事件的典型进度：

```java
mediaPlayer.addEventListener(MediaPlayer.Event.AD_PLAYBACK,  
  new MediaPlayer.AdPlaybackEventListener() { 
    @Override  
    public void onAdBreakStart(AdBreak adBreak) { ... } 
    @Override 
    public void onAdStart(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdProgress(AdBreak adBreak, Ad ad, int percentage) { ... }  
    @Override 
    public void onAdComplete(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdBreakComplete(AdBreak adBreak) { ... } 
    @Override 
    public void onAdClick(AdBreak adBreak, Ad ad, AdClick adClick) { ... } 
});
```

播放广告时，事件的顺序是：

* `AdPlaybackEventListener.onAdBreakStart`
* 广告分时段中的每则广告都会派发以下内容：

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` （在广告播放过程中多次）
   * `AdPlaybackEventListener.onAdClick` （对于每次单击）
   * `AdPlaybackEventListener.onAdStart`

* `AdPlaybackEventListener.onAdBreakComplete`

以下示例展示了广告播放事件的典型进度：

```java
mediaPlayer.addEventListener(MediaPlayer.Event.AD_PLAYBACK,  
  new MediaPlayer.AdPlaybackEventListener() { 
    @Override  
    public void onAdBreakStart(AdBreak adBreak) { ... } 
    @Override 
    public void onAdStart(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdProgress(AdBreak adBreak, Ad ad, int percentage) { ... }  
    @Override 
    public void onAdComplete(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdBreakComplete(AdBreak adBreak) { ... } 
    @Override 
    public void onAdClick(AdBreak adBreak, Ad ad, AdClick adClick) { ... } 
});
```

## QoS事件{#section_9BFF3CD7AA1C4BD6960ACF6B9C0B25CC}

TVSDK调度服务质量(QoS)事件，以通知您的应用程序可能影响QoS统计数据计算的事件，如缓冲和搜索事件。

以下示例显示这些事件的典型进度：

```java
mediaPlayer.addEventListener(MediaPlayer.Event.QOS,  
  new MediaPlayer.QOSEventListener(){ 
    //For buffering activity 
    @Override 
    public void onBufferStart() 
    @Override 
    public void onBufferComplete() 
    // For seeking 
    @Override 
    public void onSeekStart() 
    @Override 
    public void onSeekComplete(long adjustedTime) 
    @Override 
    public void onLoadComplete (MediaPlayerItem mediaplayeritem) 
    @Override 
    public void onLoadInfo(LoadInfo loadInfo) 
    @Override 
    public void onOperationFailed(MediaPlayerNotification.Warning warning) 
});
```

## DRM事件{#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK响应DRM相关操作（如当新的DRM元数据可用时）发送数字版权管理(DRM)事件。 您的播放器可以实施响应这些事件的操作。

要获得所有与DRM相关的事件的通知，请侦听`onDRMMetadata(DRMMetadataInfo drmMetadataInfo)`。 TVSDK通过`DRMManager`类发送其他DRM事件。

以下示例显示了典型的进度：

```
mediaPlayer.addEventListener(MediaPlayer.Event.DRM, 
 new MediaPlayer.DRMEventListener() { 
 @Override 
 public void onDRMMetadata(byte[] data, int length, long timestamp) {...} 
}); 
```

## 加载器事件{#section_5638F8EDACCE422A9425187484D39DCC}

您的播放器可以基于以下事件实施操作：

| 事件 | 意义 |
|---|---|
| `onLoadComplete (mediaPlayerItem playerItem)` | 媒体资源加载已成功完成。 |
| `onError` | 加载媒体资源时出现问题。 |


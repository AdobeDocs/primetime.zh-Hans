---
description: 事件处理程序允许TVSDK响应事件。
title: 实施事件侦听器和回调
exl-id: eda5cd4e-4ee8-4b37-a179-242e8697f61f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# 实施事件侦听器和回调{#implement-event-listeners-and-callbacks}

事件处理程序允许TVSDK响应事件。

发生事件时，TVSDK的事件机制会调用已注册的事件处理程序，并将事件信息传递给处理程序。

TVSDK将侦听器定义为中的公共内部接口 `MediaPlayer` 界面。

应用程序必须为影响应用程序的TVSDK事件实施事件侦听器。

有关视频分析的事件完整列表，请参阅跟踪核心视频播放。

1. 确定应用程序必须侦听的事件。

   * **必需事件**：监听所有播放事件。

      >[!IMPORTANT]
      >
      >播放事件 `onStateChanged` 提供播放器状态，包括错误。 任何状态都可能影响播放器的下一步

   * **其他事件**：可选，具体取决于您的应用程序。

      例如，如果在播放中合并广告，则实施AdPlaybackEventListener回调。

1. 为每个事件实施事件侦听器。

   TVSDK会向事件侦听器回调返回参数值。 这些值提供有关事件的相关信息，您可以在监听器中使用该信息执行相应的操作。

   `MediaPlayer.EventListener` 列出了所有回调接口。 每个界面都会显示针对每个事件返回的回调名称和参数。

   例如：

   ```
   MediaPlayer.PlaybackEventListener.onStateChanged( 
    MediaPlayer.PlayerState state, MediaPlayerNotification notification)
   ```

1. 使用注册回调侦听器 `MediaPlayer` 对象，使用 `MediaPlayer.addEventListener`.

   ```
   mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, 
    new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onStateChanged( 
    MediaPlayer.PlayerState state, 
    MediaPlayerNotification notification) {...} 
   }
   ```

## 播放事件的顺序 {#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK按通常预期的序列调度事件/通知。 您的播放器可以按照预期顺序基于事件实施操作。

以下示例显示了一些包括播放事件的事件的顺序。

* 通过成功加载媒体资源时 `MediaPlayer.replaceCurrentResource`，事件的顺序为：

1. `MediaPlayer.PlaybackEventListener.onStateChanged` 带有状态 `MediaPlayer.PlayerState.INITIALIZING`

1. `MediaPlayer.PlaybackEventListener.onStateChanged` 带有状态 `MediaPlayer.PlayerState.INITIALIZED`

>[!TIP]
>
>在主线程上加载媒体资源。 如果在后台线程中加载媒体资源，则此操作或后续TVSDK操作（或两者）可能会引发错误(例如， `IllegalStateException`)并退出。

* 通过准备播放时 `MediaPlayer.prepareToPlay`，事件的顺序为：

1. `MediaPlayer.PlaybackEventListener.onStateChanged` 带有状态 `MediaPlayerStatus.PREPARING`

1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` 是否插入了广告。
1. `MediaPlayer.PlaybackEventListener.onStateChanged` 带有状态 `MediaPlayerStatus.PREPARED`

* 对于实时/线性流，在播放期间，当播放窗口前进并解决其他机会时，事件的顺序为：

1. `MediaPlayer.PlaybackEventListener.onUpdated`
1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` 如果插入了广告
1. `MediaPlayerItemEvent.ITEM_UPDATED`
1. `TimelineEvent.TIMELINE_UPDATED` 如果插入了广告

以下示例显示了事件的典型进展：

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

## 广告事件的顺序 {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

当您的播放包含广告时，TVSDK会按通常预期的序列发送事件/通知。 您的播放器可以按照预期顺序基于事件实施操作。

在播放广告时，事件的顺序为：

* `AdPlaybackEventListener.onAdBreakStart`
* 将为广告时间中的每个广告调度以下内容：

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` （在广告播放期间多次）
   * `AdPlaybackEventListener.onAdClick` （对于每次点击）
   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdBreakComplete`

以下示例显示了广告播放事件的典型进度：

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

在播放广告时，事件的顺序为：

* `AdPlaybackEventListener.onAdBreakStart`
* 将为广告时间中的每个广告调度以下内容：

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` （在广告播放期间多次）
   * `AdPlaybackEventListener.onAdClick` （对于每次点击）
   * `AdPlaybackEventListener.onAdStart`

* `AdPlaybackEventListener.onAdBreakComplete`

以下示例显示了广告播放事件的典型进度：

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

## QoS事件 {#section_9BFF3CD7AA1C4BD6960ACF6B9C0B25CC}

TVSDK调度服务质量(QoS)事件，以通知应用程序有关可能会影响QoS统计信息计算的事件，例如缓冲和搜寻事件。

以下示例显示了这些事件的典型过程：

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

## DRM事件 {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK调度数字版权管理(DRM)事件以响应DRM相关操作，例如当新的DRM元数据可用时。 您的播放器可以实施操作来响应这些事件。

要接收有关所有DRM相关事件的通知，请侦听 `onDRMMetadata(DRMMetadataInfo drmMetadataInfo)`. TVSDK通过 `DRMManager` 类。

以下示例显示了一个典型的行进：

```
mediaPlayer.addEventListener(MediaPlayer.Event.DRM, 
 new MediaPlayer.DRMEventListener() { 
 @Override 
 public void onDRMMetadata(byte[] data, int length, long timestamp) {...} 
}); 
```

## 加载器事件 {#section_5638F8EDACCE422A9425187484D39DCC}

您的播放器可以实施基于以下事件的操作：

| 事件 | 含义 |
|---|---|
| `onLoadComplete (mediaPlayerItem playerItem)` | 媒体资源加载已成功完成。 |
| `onError` | 加载媒体资源时出现问题。 |

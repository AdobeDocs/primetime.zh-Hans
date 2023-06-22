---
description: 通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的方法之一。
title: 在媒体播放器中加载媒体资源
exl-id: ee11876b-c752-46cc-8e65-8c1608a41362
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# 在媒体播放器中加载媒体资源 {#load-a-media-resource-in-the-media-player}

通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的方法之一。

1. 设置媒体播放器以播放新资源。

   通过调用替换当前可播放的项目 `MediaPlayer.replaceCurrentResource()` 并传递现有 `MediaResource` 实例。

   这将启动资源加载过程。

1. 注册 `MediaPlayerEvent.STATUS_CHANGED` 事件与 `MediaPlayer` 实例。 在回调中，至少检查以下状态值：

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`

   通过这些事件， `MediaPlayer` 对象会在应用程序成功加载媒体资源后通知应用程序。
1. 当媒体播放器的状态更改为 `INITIALIZED`，您可以调用 `MediaPlayer.prepareToPlay()`.

   此状态表示媒体已成功加载。 新 `MediaPlayerItem` 已准备好播放。 呼叫 `prepareToPlay()` 启动广告解析和投放流程（如果有）。

如果失败，媒体播放器将切换到 `ERROR` 状态。

以下简化的示例代码说明了加载媒体资源的过程：

```java
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register a PlaybackEventListener implementation with the MediaPlayer instance 
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatus status) { 
        if(event.getStatus() == MediaPlayerStatus.PREPARED) { 
            // The resource is successfully loaded and available. The  
            // MediaPlayer is ready to start the playback and can 
            // provide a reference to the current playable item 
            MediaPlayerItem playerItem = mediaPlayer.getCurrentItem(); 
            if (playerItem != null) { 
                // We can look at the properties of the loaded stream 
            } 
        } 
        else if (event.getStatus() == MediaPlayerStatus.ERROR) { 
            //Something bad happened - the resource cannot be loaded. 
            // The Metadata object in the event provides details. 
        } 
        else if (status == MediaPlayerStatus.INITIALIZED) { 
            mediaPlayer.prepareToPlay(); 
        } 
    } 
} 
```

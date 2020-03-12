---
description: 通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的一种方式。
seo-description: 通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的一种方式。
seo-title: 在媒体播放器中加载媒体资源
title: 在媒体播放器中加载媒体资源
uuid: 1a27b83b-afa6-48c7-a701-e11b2d280810
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 在媒体播放器中加载媒体资源 {#load-a-media-resource-in-the-media-player}

通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的一种方式。

1. 设置媒体播放器以播放新资源。

   通过调用并传递现有实例来替 `MediaPlayer.replaceCurrentResource()` 换当前可播放的 `MediaResource` 项。

   这将启动资源加载过程。

1. 向实 `MediaPlayerEvent.STATUS_CHANGED` 例注册事 `MediaPlayer` 件。 在回调中，至少检查以下状态值：

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`
   通过这些事件，对 `MediaPlayer` 象会在成功加载媒体资源时通知您的应用程序。
1. 当媒体播放器的状态更改为时， `INITIALIZED`您可以调用 `MediaPlayer.prepareToPlay()`。

   此状态表示媒体已成功加载。 新的播 `MediaPlayerItem` 放已准备就绪。 呼叫 `prepareToPlay()` 启动广告解决和投放流程（如果有）。

如果出现故障，媒体播放器会切换到状 `ERROR` 态。

以下简化的示例代码说明了加载媒体资源的过程：

```java>
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

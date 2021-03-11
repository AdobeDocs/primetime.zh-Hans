---
description: 通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的一种方式。
title: 在媒体播放器中加载媒体资源
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# 在媒体播放器{#load-a-media-resource-in-the-media-player}中加载媒体资源

通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的一种方式。

1. 设置媒体播放器以播放新资源。

   通过调用`MediaPlayer.replaceCurrentResource()`并传递现有`MediaResource`实例来替换当前可播放项。

   这将开始资源加载过程。

1. 向`MediaPlayer`实例注册`MediaPlayerEvent.STATUS_CHANGED`事件。 在回调中，至少检查以下状态值：

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`

   通过这些事件,`MediaPlayer`对象在成功加载媒体资源后通知您的应用程序。
1. 当媒体播放器的状态变为`INITIALIZED`时，您可以调用`MediaPlayer.prepareToPlay()`。

   此状态表示媒体已成功加载。 新`MediaPlayerItem`已准备好播放。 调用`prepareToPlay()`将开始广告分辨率和投放过程（如果有）。

如果发生故障，媒体播放器会切换到`ERROR`状态。

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

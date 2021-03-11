---
description: 通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的一种方式。
title: 在MediaPlayer中加载媒体资源
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# 在MediaPlayer中加载媒体资源{#load-a-media-resource-in-the-mediaplayer}

通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的一种方式。

1. 使用要播放的新资源设置MediaPlayer的可播放项。

   通过调用`MediaPlayer.replaceCurrentItem`并传递现有`MediaResource`实例，替换现有MediaPlayer的当前可播放项。

1. 使用`MediaPlayer`实例注册`MediaPlayer.PlaybackEventListener`接口的实现。

   * `onPrepared`
   * `onStateChanged`，并检查INITIALIZED和ERROR。

1. 当媒体播放器的状态更改为INITIALIZED时，您可以调用`MediaPlayer.prepareToPlay`

   INITIALIZED状态表示媒体已成功加载。 调用`prepareToPlay`将开始广告分辨率和投放过程（如果有）。

1. 当TVSDK调用`onPrepared`回调时，媒体流已成功加载并准备好回放。

   加载媒体流时，将创建`MediaPlayerItem`。

>如果发生故障，`MediaPlayer`将切换到“ERROR”状态。 它还会通过调用`PlaybackEventListener.onStateChanged`回调来通知您的应用程序。
>
>这传递了几个参数：
>* `MediaPlayer.PlayerState.ERROR`值为`MediaPlayer.PlayerState`类型的`state`参数。
   >
   >
* 类型`MediaPlayerNotification`的`notification`参数，包含有关错误事件的诊断信息。


以下简化的示例代码说明了加载媒体资源的过程：

```java
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register a PlaybackEventListener implementation with the MediaPlayer  
instancemediaPlayer.addEventListener( 
  MediaPlayer.Event.PLAYBACK, 
  new MediaPlayer.PlaybackEventListener()) { 
    @Overridepublic void onPrepared() { 
        // at this point, the resource is successfully loaded and available 
        // and the MediaPlayer is ready to start the playback 
        // once the resource is loaded, the MediaPlayer is able to 
        // provide a reference to the current "playable item" 
 
        MediaPlayerItem playerItem = mediaPlayer.CurrentItem(); 
 
        if (playerItem != null) {     
            // here we can take a look at the properties of the     
            // loaded stream 
        } 
    } @Overridepublic void onStateChanged( 
        MediaPlayer.PlayerState state,  
        MediaPlayerNotification notification) { 
        if (state == MediaPlayer.PlayerState.ERROR) { 
            // something bad happened - the resource cannot be loaded    
            // details about the problem are provided via the  
            // MediaPlayerNotification instance 
        }  
        elseif (state == MediaPlayer.PlayerState.INITIALIZED) {     
            mediaPlayer.prepareToPlay(); 
        } 
    } 
    // implementation of the other methods in the PlaybackEventListener interface... 
} 
```

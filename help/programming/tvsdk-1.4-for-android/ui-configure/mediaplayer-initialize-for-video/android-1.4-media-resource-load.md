---
description: 通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的一种方式。
seo-description: 通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的一种方式。
seo-title: 在MediaPlayer中加载媒体资源
title: 在MediaPlayer中加载媒体资源
uuid: 6ee8032f-0728-423f-a1d2-5030aa7db14f
translation-type: tm+mt
source-git-commit: 4ef05be045334a2e723da4c7c6a7ee22fb0f776c

---


# 在MediaPlayer中加载媒体资源 {#load-a-media-resource-in-the-mediaplayer}

通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的一种方式。

1. 使用要播放的新资源设置MediaPlayer的可播放项。

   通过调用并传递现有实例，替换现有MediaPlayer `MediaPlayer.replaceCurrentItem` 的当前可播放 `MediaResource` 项。

1. 使用实例注册接 `MediaPlayer.PlaybackEventListener` 口的一个实 `MediaPlayer` 现。

   * `onPrepared`
   * `onStateChanged`，并检查INITIALIZED和ERROR。

1. 当媒体播放器的状态更改为“已初始化”时，您可以调用 `MediaPlayer.prepareToPlay`

   INITIALIZED状态表示媒体已成功加载。 致电 `prepareToPlay` 开始解决广告问题和投放流程（如果有）。

1. 当TVSDK调用回 `onPrepared` 调时，媒体流已成功加载并准备好回放。

   加载媒体流时，会创 `MediaPlayerItem` 建一个。

>如果出现故障，则切 `MediaPlayer` 换到“ERROR”状态。 它还通过调用回调来通知您的应用 `PlaybackEventListener.onStateChanged`程序。
>
>这传递了几个参数：
>* 具 `state` 有值的 `MediaPlayer.PlayerState` 类型参数 `MediaPlayer.PlayerState.ERROR`。
   >
   >
* 包含 `notification` 错误事件 `MediaPlayerNotification` 诊断信息的类型参数。


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

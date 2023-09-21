---
description: 通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的方法之一。
title: 在MediaPlayer中加载媒体资源
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 在MediaPlayer中加载媒体资源 {#load-a-media-resource-in-the-mediaplayer}

通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的方法之一。

1. 将MediaPlayer的可播放项目设置为要播放的新资源。

   通过调用替换您现有的MediaPlayer当前可播放的项目 `MediaPlayer.replaceCurrentItem` 并传递现有 `MediaResource` 实例。

1. 注册 `MediaPlayer.PlaybackEventListener` 与的接口 `MediaPlayer` 实例。

   * `onPrepared`
   * `onStateChanged`，并检查是否存在初始化和错误。

1. 当媒体播放器的状态变为“已初始化”时，您可以调用 `MediaPlayer.prepareToPlay`

   INITIALIZED状态表示媒体已成功加载。 呼叫 `prepareToPlay` 开始广告解析和投放流程（如果有）。

1. 当TVSDK调用 `onPrepared` 回调时，媒体流已成功加载并准备好进行播放。

   加载媒体流时， `MediaPlayerItem` 创建。

>如果发生故障， `MediaPlayer` 将切换到ERROR状态。 此外，它还会通过调用 `PlaybackEventListener.onStateChanged`回调。
>
>这传递了多个参数：
>* A `state` 类型参数 `MediaPlayer.PlayerState` 值为 `MediaPlayer.PlayerState.ERROR`.
>
>* A `notification` 类型参数 `MediaPlayerNotification` 其中包含有关错误事件的诊断信息。

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

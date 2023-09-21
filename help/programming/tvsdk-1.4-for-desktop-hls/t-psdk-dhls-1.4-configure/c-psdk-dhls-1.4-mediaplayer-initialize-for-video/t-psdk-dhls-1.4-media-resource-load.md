---
description: 通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的方法之一。
title: 在MediaPlayer中加载媒体资源
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# 在MediaPlayer中加载媒体资源{#load-a-media-resource-in-the-mediaplayer}

通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的方法之一。

1. 设置您的 `MediaPlayer` 包含要播放的新资源的对象可播放项目。

   通过调用替换您现有的MediaPlayer当前可播放的项目 `MediaPlayer.replaceCurrentResource` 并传递现有 `MediaResource` 实例。

1. 至少检查以下更改：

   * 已初始化
   * 已准备
   * 错误

     通过这些事件， `MediaPlayer` 当媒体资源成功加载时，对象可以通知您的应用程序。

1. 当媒体播放器的状态变为“已初始化”时，您可以调用 `MediaPlayer.prepareToPlay`

   INITIALIZED状态表示媒体已成功加载。 呼叫 `prepareToPlay` 开始广告解析和投放流程（如果有）。

1. 当媒体播放器状态变为“已准备”时，媒体流已成功加载并准备播放。

   加载媒体流时， `MediaPlayerItem` 创建。

如果发生故障，MediaPlayer将切换到ERROR状态。 它还会通过发送 `STATUS_CHANGED` 事件 `MediaPlayerStatusChangeEvent` 回调。

这传递了多个参数：
* A `type` 字符串类型的参数值 `ERROR`.

* A `MediaError` 用于获取包含有关错误事件的诊断信息的通知的参数。


<!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

以下简化的示例代码说明了加载媒体资源的过程：

```
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register an event listener with the MediaPlayer instance 
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
private function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
   switch(event.status) { 
      case MediaPlayerStatus.INITIALIZED: 
          // at this point, the resource is successfully loaded 
          // the media player will provide a reference to the current 
          // "playable item" ( is guarantee to be valid and not-null). 
          var playerItem: MediaPlayerItem = mediaPlayer.currentItem; 
          // we can take a look at the media item characteristics like 
          // alternate audio tracks, profile information, if is a live stream 
          // if is drm protected 
          mediaPlayer.prepareToPlay(); 
          break; 
    case MediaPlayerStatus.PREPARED: 
         // at this point, the resource is successfully processed all  
         // advertisement placements have been executed and the the  
         // MediaPlayer is ready to start the playback 
        if (autoPlay) { 
            mediaPlayer.play(); 
        } 
        break; 
    case MediaPlayerStatus.ERROR: 
        // something bad happened - the resource cannot be loaded 
        // details about the problem are provided via the event.error property 
        break; 
        // implementation of the other methods in the PlaybackEventListener interface 
        ... 
    } 
}
```

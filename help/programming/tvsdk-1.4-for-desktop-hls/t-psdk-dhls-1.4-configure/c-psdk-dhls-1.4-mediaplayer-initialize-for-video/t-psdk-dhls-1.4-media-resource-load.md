---
description: 通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的一种方式。
seo-description: 通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的一种方式。
seo-title: 在MediaPlayer中加载媒体资源
title: 在MediaPlayer中加载媒体资源
uuid: 8af3e8d1-359d-483c-b394-b95054f7265a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 在MediaPlayer中加载媒体资源{#load-a-media-resource-in-the-mediaplayer}

通过直接实例化MediaResource并加载要播放的视频内容来加载资源。 这是加载媒体资源的一种方式。

1. 将对 `MediaPlayer` 象的可播放项目与要播放的新资源一起设置。

   通过调用并传递现有实例，替换现有MediaPlayer `MediaPlayer.replaceCurrentResource` 的当前可播放 `MediaResource` 项。

1. 请至少检查以下更改：

   * 已初始化
   * 准备好
   * 错误

      通过这些事件， `MediaPlayer` 对象可以在媒体资源成功加载时通知您的应用程序。

1. 当媒体播放器的状态更改为“已初始化”时，您可以调用 `MediaPlayer.prepareToPlay`

   INITIALIZED状态表示媒体已成功加载。 呼叫 `prepareToPlay` 启动广告解决和投放流程（如果有）。

1. 当媒体播放器状态更改为“PREPARED”时，媒体流已成功加载并准备好回放。

   加载媒体流时，会创 `MediaPlayerItem` 建一个。

如果出现故障，MediaPlayer将切换到“ERROR”状态。 它还会通过将事件调度到回调来通 `STATUS_CHANGED` 知应用程 `MediaPlayerStatusChangeEvent` 序。

这传递了几个参数：>
* 带 `type` 有值的字符串类型的参数 `ERROR`。

* 可用 `MediaError` 于获取包含错误事件诊断信息的通知的参数。


><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->


以下简化的示例代码说明了加载媒体资源的过程：
>```>
>>// mediaResource is a properly configured MediaResource instance 
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
```>
>

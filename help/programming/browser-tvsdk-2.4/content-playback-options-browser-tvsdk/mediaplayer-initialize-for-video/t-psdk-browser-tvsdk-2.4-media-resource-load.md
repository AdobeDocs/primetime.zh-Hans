---
description: 通过直接实例化MediaResource并加载要播放的视频内容来加载资源。
title: 在MediaPlayer中加载媒体资源
exl-id: b775c33e-399c-4a03-a132-407944f07706
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# 在MediaPlayer中加载媒体资源 {#load-a-media-resource-in-the-mediaplayer}

通过直接实例化MediaResource并加载要播放的视频内容来加载资源。

1. 设置您的 `MediaPlayer` 包含要播放的新资源的对象可播放项目。

   替换现有 `MediaPlayer` 通过调用对象的当前可播放项目 `replaceCurrentResource` 并传递现有 `MediaResource` 实例。

1. 等待浏览器TVSDK调度 `AdobePSDK.MediaPlayerStatusChangeEvent` 替换为 `event.status` 等于以下任意值：

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

      通过这些事件，MediaPlayer对象会通知您的应用程序媒体资源是否已成功加载。

1. 当媒体播放器的状态更改为 `MediaPlayerStatus.INITIALIZED`，您可以调用 `MediaPlayer.prepareToPlay`.

   INITIALIZED状态表示媒体已成功加载。 呼叫 `prepareToPlay` 启动广告解析和投放流程（如果有）。
1. 当浏览器TVSDK调度 `MediaPlayerStatus.PREPARED` 媒体流已成功加载的事件（已创建MediaPlayerItem）并准备好进行播放。

如果发生故障， `MediaPlayer` 切换到 `MediaPlayerStatus.ERROR`.

它还会通过调度 `MediaPlayerStatus.ERROR` 事件。

><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

以下简化的示例代码说明了加载媒体资源的过程：

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                        onStatusChange); 
 
onStatusChange = function (event) { 
    var msg = ""; 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            msg = "Player Status: INITIALIZED"; 
            console.log(msg); 
            player.prepareToPlay(AdobePSDK.MediaPlayer.LIVE_POINT); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARED: 
        // The resource is successfully loaded and available 
        // and the MediaPlayer is ready to start the playback. 
        // Once the resource is loaded, the MediaPlayer can 
        // provide a reference to the current "playable item" 
           MediaPlayerItem playerItem = player.currentItem; 
           if (playerItem != null) {  
              // here we can look at the properties of the  
              // loadedstream 
           } 
           break; 
    } 
}
```

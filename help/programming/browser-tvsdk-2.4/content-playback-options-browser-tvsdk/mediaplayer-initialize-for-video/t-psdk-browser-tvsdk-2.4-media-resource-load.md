---
description: 通过直接实例化MediaResource并加载要播放的视频内容来加载资源。
seo-description: 通过直接实例化MediaResource并加载要播放的视频内容来加载资源。
seo-title: 在MediaPlayer中加载媒体资源
title: 在MediaPlayer中加载媒体资源
uuid: ac31ccfe-161d-41a2-9a6e-38fae11ceab5
translation-type: tm+mt
source-git-commit: 7d61a6cd8cb2c381f85a19d9ccac3d235ffceaf1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# 在MediaPlayer中加载媒体资源{#load-a-media-resource-in-the-mediaplayer}

通过直接实例化MediaResource并加载要播放的视频内容来加载资源。

1. 使用要播放的新资源设置`MediaPlayer`对象的可播放项。

   通过调用`replaceCurrentResource`并传递现有`MediaResource`实例，替换现有`MediaPlayer`对象的当前可播放项。

1. 等待浏览器TVSDK将`AdobePSDK.MediaPlayerStatusChangeEvent`调度为等于以下任一项的`event.status`:

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

      通过这些事件,MediaPlayer对象将通知您的应用程序媒体资源是否已成功加载。

1. 当媒体播放器的状态变为`MediaPlayerStatus.INITIALIZED`时，您可以调用`MediaPlayer.prepareToPlay`。

   INITIALIZED状态表示媒体已成功加载。 调用`prepareToPlay`将开始广告解决和投放过程（如果有）。
1. 当浏览器TVSDK发送`MediaPlayerStatus.PREPARED`事件时，媒体流已成功加载（已创建MediaPlayerItem）并准备好回放。

如果出现故障，`MediaPlayer`将切换到`MediaPlayerStatus.ERROR`。

它还通过调度`MediaPlayerStatus.ERROR`事件通知您的应用程序。

><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->


以下简化的示例代码说明加载媒体资源的过程：

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

---
description: 创建一个PlaybackManager，它处理HLS流设置和播放操作。 无需任何其他配置。
seo-description: 创建一个PlaybackManager，它处理HLS流设置和播放操作。 无需任何其他配置。
seo-title: 启用视频回放
title: 启用视频回放
uuid: ddc0defa-c40f-4ee6-a69f-d5eeca6c2fce
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# 启用视频播放{#enable-video-playback}

创建一个PlaybackManager，它处理HLS流设置和播放操作。 无需任何其他配置。

1. 通过确保[!DNL PlayerFragment.java]中存在以下代码，创建媒体播放器对象：

   ```java
   private MediaPlayer createMediaPlayer() { 
           MediaPlayer mediaPlayer = DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
           return mediaPlayer;
   ```

   <!-- I've duplicated this information. It also exists in the PlayerFragment section, just before the Feature manager section. I figured that I should have it here as well, in case they jump directly to this section.-->

1. 通过`ManagerFactory`创建播放管理器：

   ```java
   playbackManager = ManagerFactory.getPlaybackManager(config, mediaPlayer);
   ```

1. 在`PlayerFragment`中实现`PlaybackManagerEventListener`以处理播放事件:

   ```java
   private final PlaybackManagerEventListener playbackManagerEventListener =  
     new PlaybackManagerEventListener() 
   ```

1. 在`PlayerFragment`中注册事件监听器：

   ```
   playbackManager.addEventListener(playbackManagerEventListener);
   ```

1. 设置视频资源：

   ```
   playbackManager.setupVideo(url, adsManager); 
   ```

1. 在`PlayerFragment`中设置控制栏操作：

   ```
   controlBar.pressPlay() { 
       playbackManager.play();  
   }
   ```

## 相关API文档{#related-api-documentation}

* [类PlaybackManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.html)
* [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)
* [mediacore.utils.TimeRange](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/utils/TimeRange.html)
* [mediacore.BufferControlParameters](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/BufferControlParameters.html)
* [mediacore.MediaPlayer.PlayerState](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/MediaPlayer.PlayerState.html)
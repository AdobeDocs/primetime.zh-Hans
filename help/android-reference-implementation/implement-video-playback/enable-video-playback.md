---
description: 创建一个PlaybackManager，它处理HLS流设置和播放操作。 不需要任何其他配置。
title: 启用视频播放
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# 启用视频播放{#enable-video-playback}

创建一个PlaybackManager，它处理HLS流设置和播放操作。 不需要任何其他配置。

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

1. 在`PlayerFragment`中注册事件侦听器：

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
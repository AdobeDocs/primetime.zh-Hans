---
description: 创建可处理HLS流设置和播放操作的PlaybackManager。 无需其他配置。
title: 启用视频播放
exl-id: b53f602b-5752-4471-9905-2e4351dfc8d3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 启用视频播放 {#enable-video-playback}

创建可处理HLS流设置和播放操作的PlaybackManager。 无需其他配置。

1. 创建媒体播放器对象，确保中存在以下代码 [!DNL PlayerFragment.java]：

   ```java
   private MediaPlayer createMediaPlayer() { 
           MediaPlayer mediaPlayer = DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
           return mediaPlayer;
   ```

   <!-- I've duplicated this information. It also exists in the PlayerFragment section, just before the Feature manager section. I figured that I should have it here as well, in case they jump directly to this section.-->

1. 通过创建播放管理器 `ManagerFactory`：

   ```java
   playbackManager = ManagerFactory.getPlaybackManager(config, mediaPlayer);
   ```

1. 实施 `PlaybackManagerEventListener` 在 `PlayerFragment` 要处理播放事件：

   ```java
   private final PlaybackManagerEventListener playbackManagerEventListener =  
     new PlaybackManagerEventListener() 
   ```

1. 在中注册事件侦听器 `PlayerFragment`：

   ```
   playbackManager.addEventListener(playbackManagerEventListener);
   ```

1. 设置视频资源：

   ```
   playbackManager.setupVideo(url, adsManager); 
   ```

1. 在中设置控制栏操作 `PlayerFragment`：

   ```
   controlBar.pressPlay() { 
       playbackManager.play();  
   }
   ```

## 相关API文档 {#related-api-documentation}

* [类播放管理器](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.html)
* [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)
* [mediacore.utils.TimeRange](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/utils/TimeRange.html)
* [mediacore.BufferControlParameters](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/BufferControlParameters.html)
* [mediacore.MediaPlayer.PlayerState](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/MediaPlayer.PlayerState.html)

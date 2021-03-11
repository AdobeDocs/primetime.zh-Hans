---
title: 视频播放的基本操作
description: PlaybackManager提供HLS流的基本操作
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# 视频播放的基本操作{#essential-operations-of-video-playback}

PlaybackManager提供HLS流的基本操作：

* 调用能够对视频事件做出相应响应的[PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)。
* 提供播放操作，如播放、暂停和搜索。
* 返回有关播放器的信息，如播放器状态、播放范围和视频直播流。
* 确定是否启用了ABR，并根据提供的配置数据设置ABR和缓冲区控制参数。
* 确定是否启用缓冲区控制，并根据提供的配置数据设置缓冲区控制参数。
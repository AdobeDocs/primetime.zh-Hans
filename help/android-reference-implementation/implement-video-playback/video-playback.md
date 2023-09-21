---
title: 视频播放的基本操作
description: PlaybackManager提供HLS流的基本操作
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# 视频播放的基本操作 {#essential-operations-of-video-playback}

PlaybackManager提供HLS流的基本操作：

* 调用 [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)，能够正确响应视频事件。
* 提供播放、暂停和搜寻等播放操作。
* 返回有关播放器的信息，例如播放器状态、播放范围和视频实时流。
* 确定是否启用ABR，并根据提供的配置数据设置ABR和缓冲区控制参数。
* 确定是否启用缓冲区控制，并根据提供的配置数据设置缓冲区控制参数。

---
seo-title: 视频播放的基本操作
title: 视频播放的基本操作
description: PlaybackManager提供HLS流的基本操作
seo-description: PlaybackManager提供HLS流的基本操作
uuid: 7ac93f1f-9233-4462-a4be-528d1aa524a9
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# 视频播放的基本操作{#essential-operations-of-video-playback}

PlaybackManager提供HLS流的基本操作：

* 调用[PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)，它可以对视频事件做出适当响应。
* 提供播放、暂停和搜索等播放操作。
* 返回有关播放器的信息，如播放器状态、播放范围和视频实时流。
* 确定是否启用ABR，并根据提供的配置数据设置ABR和缓冲区控制参数。
* 确定是否启用缓冲区控制，并根据提供的配置数据设置缓冲区控制参数。
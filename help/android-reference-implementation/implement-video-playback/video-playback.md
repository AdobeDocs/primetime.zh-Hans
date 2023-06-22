---
title: 视频播放的基本操作
description: PlaybackManager提供HLS流的基本操作
exl-id: b4d1b41a-7a16-47f5-be88-6b52f0451813
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# 视频播放的基本操作 {#essential-operations-of-video-playback}

PlaybackManager提供HLS流的基本操作：

* 调用 [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)，可以对视频事件做出适当响应。
* 提供播放、暂停和搜寻等播放操作。
* 返回有关播放器的信息，例如播放器状态、播放范围和视频实时流。
* 确定是否启用了ABR，并根据提供的配置数据设置ABR和缓冲区控制参数。
* 确定是否启用缓冲区控制，并根据提供的配置数据设置缓冲区控制参数。

---
description: MediaPlayer对象表示您的媒体播放器。 MediaPlayerItem表示播放器上的音频或视频。
seo-description: MediaPlayer对象表示您的媒体播放器。 MediaPlayerItem表示播放器上的音频或视频。
seo-title: 关于MediaPlayerItem类
title: 关于MediaPlayerItem类
uuid: d7f65edf-4693-4b1e-bae0-46fadce98751
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 关于MediaPlayerItem类{#about-the-mediaplayeritem-class}

MediaPlayer对象表示您的媒体播放器。 MediaPlayerItem表示播放器上的音频或视频。

成功加载媒体资源后，TVSDK将创建类的一个实例， `MediaPlayerItem` 以提供对该资源的访问。

该 `MediaResource` 表示应用程序层向实例发出的用于加载内 `MediaPlayer` 容的请求。

解 `MediaPlayer` 析媒体资源，加载关联的清单文件，并分析清单。 这是资源加载过程的异步部分。 该实 `MediaPlayerItem` 例是在资源解析后生成的，并且该实例是的已解析版本 `MediaResource`。 TVSDK允许访问新创建的 `MediaPlayerItem` 实例 `MediaPlayer.CurrentItem`

>[!TIP]
>
>您必须等待资源成功加载后，才能访问媒体播放器项。


---
description: MediaPlayer对象表示您的媒体播放器。 MediaPlayerItem表示播放器上的音频或视频。
seo-description: MediaPlayer对象表示您的媒体播放器。 MediaPlayerItem表示播放器上的音频或视频。
seo-title: 关于MediaPlayerItem类
title: 关于MediaPlayerItem类
uuid: 531dd1a6-d72c-4ae3-9c3f-2f1d854245c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 关于MediaPlayerItem类{#about-the-mediaplayeritem-class}

MediaPlayer对象表示您的媒体播放器。 MediaPlayerItem表示播放器上的音频或视频。

<!--<a id="section_01BC89E5C5A94D0A95EF9D29FBCE758A"></a>-->

成功加载媒体资源后，TVSDK将创建类的一个实例， `MediaPlayerItem` 以提供对该资源的访问。

该 `MediaResource` 表示应用程序层向实例发出的用于加载内 `MediaPlayer` 容的请求。

解 `MediaPlayer` 析媒体资源，加载关联的清单文件，并分析清单。 这是资源加载过程的异步部分。 该实 `MediaPlayerItem` 例是在资源解析后生成的，并且该实例是的已解析版本 `MediaResource`。 TVSDK提供对新创建实例的访 `MediaPlayerItem` 问权限 `MediaPlayer.currentItem`。

>[!TIP]
>
>您必须等待资源成功加载后，才能访问媒体播放器项。


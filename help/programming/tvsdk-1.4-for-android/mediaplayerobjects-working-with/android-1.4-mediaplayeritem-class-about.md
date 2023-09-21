---
description: MediaPlayer对象表示您的媒体播放器。 MediaPlayerItem表示播放器上的音频或视频。
title: 关于MediaPlayerItem类
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# 关于MediaPlayerItem类{#about-the-mediaplayeritem-class}

MediaPlayer对象表示您的媒体播放器。 MediaPlayerItem表示播放器上的音频或视频。

成功加载媒体资源后，TVSDK会为创建一个实例 `MediaPlayerItem` 类以提供对该资源的访问权限。

此 `MediaResource` 表示由应用层向 `MediaPlayer` 实例来加载内容。

此 `MediaPlayer` 解析媒体资源，加载关联的清单文件，并解析清单。 这是资源加载过程的异步部分。 此 `MediaPlayerItem` 实例在资源解析后生成，此实例是的解析版本 `MediaResource`. TVSDK提供对新创建的的访问权限 `MediaPlayerItem` 实例到 `MediaPlayer.CurrentItem`

>[!TIP]
>
>在访问媒体播放器项目之前，必须等待资源成功加载。

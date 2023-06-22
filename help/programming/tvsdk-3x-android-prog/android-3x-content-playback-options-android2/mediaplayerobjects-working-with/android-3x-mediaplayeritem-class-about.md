---
description: 成功加载MediaResource对象后，TVSDK将创建一个MediaPlayerItem类的实例，以提供对该资源的访问权限。
title: 关于MediaPlayerItem类
exl-id: 372c4766-440a-4e69-b86d-e1a0a2232a9a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# 关于MediaPlayerItem类 {#about-the-mediaplayeritem-class}

MediaPlayer对象表示您的媒体播放器。 MediaPlayerItem表示播放器上的音频或视频。

成功加载MediaResource对象后，TVSDK将创建一个MediaPlayerItem类的实例，以提供对该资源的访问权限。

此 `MediaResource` 表示由应用层向 `MediaPlayer` 加载内容的实例。

此 `MediaPlayer` 解析媒体资源，加载关联的清单文件，并解析清单。 这是资源加载过程的异步部分。 此 `MediaPlayerItem` 实例在资源解析后生成，并且该实例是的解析版本 `MediaResource`. TVSDK提供对新创建的的访问权限 `MediaPlayerItem` 实例到 `MediaPlayer.CurrentItem`.

>[!TIP]
>
>在访问媒体播放器项目之前，必须等待资源成功加载。

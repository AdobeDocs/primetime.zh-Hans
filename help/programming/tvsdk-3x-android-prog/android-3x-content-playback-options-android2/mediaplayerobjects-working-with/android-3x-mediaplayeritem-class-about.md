---
description: 在您成功加载MediaResource对象后，TVSDK将创建MediaPlayerItem类的一个实例以提供对该资源的访问。
seo-description: 在您成功加载MediaResource对象后，TVSDK将创建MediaPlayerItem类的一个实例以提供对该资源的访问。
seo-title: 关于MediaPlayerItem类
title: 关于MediaPlayerItem类
uuid: fc79c442-2e38-48c4-8ef9-6dce9ad6790a
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 关于MediaPlayerItem类 {#about-the-mediaplayeritem-class}

MediaPlayer对象表示您的媒体播放器。 MediaPlayerItem表示播放器上的音频或视频。

在您成功加载MediaResource对象后，TVSDK将创建MediaPlayerItem类的一个实例以提供对该资源的访问。

该 `MediaResource` 表示应用程序层向实例发出的用于加载内 `MediaPlayer` 容的请求。

解 `MediaPlayer` 析媒体资源，加载关联的清单文件，并分析清单。 这是资源加载过程的异步部分。 该实 `MediaPlayerItem` 例是在资源解析后生成的，并且该实例是的已解析版本 `MediaResource`。 TVSDK提供对新创建实例的访 `MediaPlayerItem` 问权限 `MediaPlayer.CurrentItem`。

>[!TIP]
>
>您必须等待资源成功加载后，才能访问媒体播放器项。
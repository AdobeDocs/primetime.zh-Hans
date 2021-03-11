---
description: MediaPlayer对象表示您的媒体播放器。 MediaPlayerItem表示播放器上的音频或视频。
title: 关于MediaPlayerItem类
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# 关于MediaPlayerItem类{#about-the-mediaplayeritem-class}

MediaPlayer对象表示您的媒体播放器。 MediaPlayerItem表示播放器上的音频或视频。

成功加载媒体资源后，TVSDK会创建`MediaPlayerItem`类的实例，以提供对该资源的访问。

`MediaResource`表示应用程序层向`MediaPlayer`实例发出的用于加载内容的请求。

`MediaPlayer`将解析媒体资源，加载关联的清单文件，并解析清单。 这是资源加载过程的异步部分。 `MediaPlayerItem`实例在资源解析后生成，此实例是`MediaResource`的已解析版本。 TVSDK提供通过`MediaPlayer.CurrentItem`访问新创建的`MediaPlayerItem`实例

>[!TIP]
>
>您必须等待资源成功加载，然后才能访问媒体播放器项。


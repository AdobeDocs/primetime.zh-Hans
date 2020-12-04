---
description: MediaPlayer对象表示您的媒体播放器。 MediaPlayerItem表示播放器上的音频或视频。
seo-description: MediaPlayer对象表示您的媒体播放器。 MediaPlayerItem表示播放器上的音频或视频。
seo-title: 关于MediaPlayerItem类
title: 关于MediaPlayerItem类
uuid: 531dd1a6-d72c-4ae3-9c3f-2f1d854245c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# 关于MediaPlayerItem类{#about-the-mediaplayeritem-class}

MediaPlayer对象表示您的媒体播放器。 MediaPlayerItem表示播放器上的音频或视频。

<!--<a id="section_01BC89E5C5A94D0A95EF9D29FBCE758A"></a>-->

成功加载媒体资源后，TVSDK将创建`MediaPlayerItem`类的一个实例以提供对该资源的访问。

`MediaResource`表示应用程序层向`MediaPlayer`实例发出的加载内容的请求。

`MediaPlayer`解析媒体资源，加载关联的清单文件，并解析清单。 这是资源加载过程的异步部分。 `MediaPlayerItem`实例在资源解析后生成，此实例是`MediaResource`的已解析版本。 TVSDK通过`MediaPlayer.currentItem`提供对新创建的`MediaPlayerItem`实例的访问。

>[!TIP]
>
>您必须等待资源成功加载，然后才能访问媒体播放器项。


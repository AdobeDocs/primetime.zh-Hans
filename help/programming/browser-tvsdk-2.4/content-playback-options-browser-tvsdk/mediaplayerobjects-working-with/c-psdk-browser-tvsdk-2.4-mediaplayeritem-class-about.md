---
description: 成功加载MediaResource后，浏览器TVSDK将创建MediaPlayerItem类的一个实例，以提供对该资源的访问。
seo-description: 成功加载MediaResource后，浏览器TVSDK将创建MediaPlayerItem类的一个实例，以提供对该资源的访问。
seo-title: 关于MediaPlayerItem类
title: 关于MediaPlayerItem类
uuid: 5226d3ad-2438-44fe-a8ef-bcc0da8331b8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 关于MediaPlayerItem类{#about-the-mediaplayeritem-class}

成功加载MediaResource后，浏览器TVSDK将创建MediaPlayerItem类的一个实例，以提供对该资源的访问。

该 `MediaResource` 表示应用程序层向实例发出的用于加载内 `MediaPlayer` 容的请求。

解 `MediaPlayer` 析媒体资源，加载关联的清单文件，并分析清单。 这是资源加载过程的异步部分。 该实 `MediaPlayerItem` 例是在资源解析后生成的，并且该实例是的已解析版本 `MediaResource`。 浏览器TVSDK允许访问新创建的实 `MediaPlayerItem` 例(通过 `MediaPlayer.CurrentItem`)。

>[!TIP]
>
>您必须等待资源成功加载后，才能访问媒体播放器项。


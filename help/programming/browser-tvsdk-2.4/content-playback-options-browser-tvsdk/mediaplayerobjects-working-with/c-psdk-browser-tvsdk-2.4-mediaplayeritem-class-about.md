---
description: 成功加载MediaResource后，浏览器TVSDK会创建MediaPlayerItem类的一个实例以提供对该资源的访问。
seo-description: 成功加载MediaResource后，浏览器TVSDK会创建MediaPlayerItem类的一个实例以提供对该资源的访问。
seo-title: 关于MediaPlayerItem类
title: 关于MediaPlayerItem类
uuid: 5226d3ad-2438-44fe-a8ef-bcc0da8331b8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# 关于MediaPlayerItem类{#about-the-mediaplayeritem-class}

成功加载MediaResource后，浏览器TVSDK会创建MediaPlayerItem类的一个实例以提供对该资源的访问。

`MediaResource`表示应用程序层向`MediaPlayer`实例发出的加载内容的请求。

`MediaPlayer`解析媒体资源，加载关联的清单文件，并解析清单。 这是资源加载过程的异步部分。 `MediaPlayerItem`实例在资源解析后生成，此实例是`MediaResource`的已解析版本。 浏览器TVSDK提供通过`MediaPlayer.CurrentItem`访问新创建的`MediaPlayerItem`实例的权限。

>[!TIP]
>
>您必须等待资源成功加载，然后才能访问媒体播放器项。


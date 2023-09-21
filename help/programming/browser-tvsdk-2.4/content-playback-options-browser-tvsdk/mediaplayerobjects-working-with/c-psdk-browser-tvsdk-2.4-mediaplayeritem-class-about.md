---
description: 成功加载MediaResource后，浏览器TVSDK将创建MediaPlayerItem类的实例，以提供对该资源的访问权限。
title: 关于MediaPlayerItem类
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# 关于MediaPlayerItem类{#about-the-mediaplayeritem-class}

成功加载MediaResource后，浏览器TVSDK将创建MediaPlayerItem类的实例，以提供对该资源的访问权限。

此 `MediaResource` 表示由应用层向 `MediaPlayer` 实例来加载内容。

此 `MediaPlayer` 解析媒体资源，加载关联的清单文件，并解析清单。 这是资源加载过程的异步部分。 此 `MediaPlayerItem` 实例在资源解析后生成，此实例是的解析版本 `MediaResource`. 浏览器TVSDK提供对新创建的的访问权限 `MediaPlayerItem` 实例到 `MediaPlayer.CurrentItem`.

>[!TIP]
>
>在访问媒体播放器项目之前，必须等待资源成功加载。

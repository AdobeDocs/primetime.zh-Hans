---
description: 成功加载MediaResource后，浏览器TVSDK会创建MediaPlayerItem类的实例以提供对该资源的访问权限。
title: 关于MediaPlayerItem类
exl-id: 6e47914c-3d46-4aaf-9144-1a00d886e5bf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# 关于MediaPlayerItem类{#about-the-mediaplayeritem-class}

成功加载MediaResource后，浏览器TVSDK会创建MediaPlayerItem类的实例以提供对该资源的访问权限。

此 `MediaResource` 表示由应用层向 `MediaPlayer` 加载内容的实例。

此 `MediaPlayer` 解析媒体资源，加载关联的清单文件，并解析清单。 这是资源加载过程的异步部分。 此 `MediaPlayerItem` 实例在资源解析后生成，并且该实例是的解析版本 `MediaResource`. 通过浏览器TVSDK，可访问新创建的 `MediaPlayerItem` 实例到 `MediaPlayer.CurrentItem`.

>[!TIP]
>
>在访问媒体播放器项目之前，必须等待资源成功加载。

---
description: MediaResource表示将由MediaPlayer实例加载的内容。
title: MediaPlayer和MediaResource类
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# MediaPlayer和MediaResource类 {#mediaplayer-and-mediaresource-classes}

MediaResource表示将由MediaPlayer实例加载的内容。

<!--<a id="section_431AB7221E0249BF949EC72EEB9B428A"></a>-->

TVSDK通过使用提供了加载和准备内容以进行播放的方法 `replaceCurrentResource` 中的方法 `MediaPlayer`. 此方法采用两个参数，一个实例 `MediaPlayerResource` 以及（可选）的实例 `MediaPlayerItemConfig`，可用于传递应用程序定义的自定义参数。

* 有关更多详细信息，请参阅mediaplayer-reuse-or-remove 。
* 详细信息 `MediaPlayerResource`，请参阅media-resource-create

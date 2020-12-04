---
description: 即时加载在一个或多个渠道上预载部分媒体。 在用户选择或切换渠道后，内容开始会更早，因为某些缓冲已经完成。
seo-description: 即时加载在一个或多个渠道上预载部分媒体。 在用户选择或切换渠道后，内容开始会更早，因为某些缓冲已经完成。
seo-title: 即时
title: 即时
uuid: 23864919-9045-4223-9e47-464e38ebe5ef
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# 即时启动{#instant-on}

即时加载在一个或多个渠道上预载部分媒体。 在用户选择或切换渠道后，内容开始会更早，因为某些缓冲已经完成。

当播放器处于`PTMediaPlayerStatusReady`状态时，调用`prepareToPlay`预加载并处理部分内容以供以后回放。

>[!TIP]
>
>如果不调用`prepareToPlay`，调用`play`会先自动调用`prepareToPlay`。 此时已完成预加载和处理。

TVSDK为`prepareToPlay`完成以下部分或全部任务:

* 如果元数据密钥`kSyncCookiesWithAVAsset`已设置，则TVSDK会向原始M3U8文件发出一个请求，以同步cookie。
* 加载DRM元数据密钥。
* 创建并准备播放内容所需的一些结构、元素或资源。

>[!TIP]
>
>`PTMediaPlayer`和`PTMediaPlayerItem` `prepareToPlay`方法相等。 要避免为每个资产创建单独的`PTMediaPlayer`实例，请使用`PTMediaPlayerItem`方法。

即时启动可帮助您启动多个媒体播放器实例或媒体播放器项目加载器实例，同时在后台启动并缓冲所有这些实例中的视频流。 当用户更改渠道，且流已正确缓冲时，调用新渠道开始上的`play`会更快地播放。

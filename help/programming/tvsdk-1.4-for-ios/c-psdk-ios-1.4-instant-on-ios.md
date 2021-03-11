---
description: 即时加载将部分媒体预加载到一个或多个渠道。 在用户选择或切换渠道后，内容开始会更早，因为某些缓冲已经完成。
title: 即时
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# 即时启动{#instant-on}

即时加载将部分媒体预加载到一个或多个渠道。 在用户选择或切换渠道后，内容开始会更早，因为某些缓冲已经完成。

当您的播放器处于`PTMediaPlayerStatusReady`状态时，请调用`prepareToPlay`以预加载并处理某些内容以供以后播放。

>[!TIP]
>
>如果不调用`prepareToPlay`，调用`play`会先自动调用`prepareToPlay`。 此时已完成预加载和处理。

TVSDK为`prepareToPlay`完成以下部分或全部任务:

* 如果设置了元数据密钥`kSyncCookiesWithAVAsset`，则TVSDK向原始M3U8文件发出一个请求以同步Cookie。
* 加载DRM元数据键。
* 创建并准备播放内容所需的一些结构、元素或资源。

>[!TIP]
>
>`PTMediaPlayer`和`PTMediaPlayerItem` `prepareToPlay`方法相等。 要避免为每个资产创建单独的`PTMediaPlayer`实例，请使用`PTMediaPlayerItem`方法。

即时启动可帮助您同时在后台启动多个媒体播放器实例或媒体播放器项目加载器实例，并缓冲所有这些实例中的视频流。 当用户更改渠道，且流已正确缓冲时，对新渠道调用`play`会更快地开始播放。

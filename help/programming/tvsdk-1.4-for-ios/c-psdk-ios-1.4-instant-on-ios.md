---
description: 即时开启在一个或多个通道上预先加载部分介质。 用户选择或切换渠道后，由于某些缓冲已完成，因此内容会更快地开始。
title: 即时
exl-id: 3a1b2172-8036-40f1-86b6-8304ef771aa9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 即时{#instant-on}

即时开启在一个或多个通道上预先加载部分介质。 用户选择或切换渠道后，由于某些缓冲已完成，因此内容会更快地开始。

当您的播放器在 `PTMediaPlayerStatusReady` 状态，调用 `prepareToPlay` 以预加载和处理某些内容以供以后播放。

>[!TIP]
>
>如果你不打电话 `prepareToPlay`，调用 `play` 自动调用 `prepareToPlay` 首先。 预加载和处理在此时完成。

TVSDK完成以下部分或全部任务 `prepareToPlay`：

* 如果元数据键 `kSyncCookiesWithAVAsset` 设置，TVSDK会向原始M3U8文件发出一个请求来同步Cookie。
* 加载DRM元数据键。
* 创建并准备播放内容所需的一些结构、元素或资产。

>[!TIP]
>
>此 `PTMediaPlayer` 和 `PTMediaPlayerItem` `prepareToPlay` 方法相同。 以避免创建单独的 `PTMediaPlayer` 对于每个资源，使用 `PTMediaPlayerItem` 方法。

Instant-on可帮助您在后台和缓冲视频流中同时启动多个媒体播放器实例或媒体播放器项目加载器实例。 当用户更改频道，并且流已正确缓冲时，调用 `play` 可以更早地开始播放。

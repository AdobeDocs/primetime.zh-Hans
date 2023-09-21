---
description: 即时打开在一个或多个通道上预加载部分介质。 用户选择或切换渠道后，由于某些缓冲已完成，内容会更快地开始。
title: 即时
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 即时 {#instant-on}

即时打开在一个或多个通道上预加载部分介质。 用户选择或切换渠道后，由于某些缓冲已完成，内容会更快地开始。

当您的播放器在 `PTMediaPlayerStatusReady` 状态，呼叫 `prepareToPlay` 以预加载和处理某些内容以供将来播放。

>[!TIP]
>
>如果您不致电 `prepareToPlay`，呼叫 `play` 自动调用 `prepareToPlay` 首先。 预加载和处理在此时完成。

TVSDK将为完成以下部分或全部任务 `prepareToPlay`：

* 如果元数据键 `kSyncCookiesWithAVAsset` 设置，TVSDK会对原始M3U8文件发出一个请求以同步Cookie。
* 加载DRM元数据键。
* 创建并准备播放内容所需的一些结构、元素或资产。

>[!TIP]
>
>此 `PTMediaPlayer` 和 `PTMediaPlayerItem` `prepareToPlay` 方法相同。 要避免创建单独的 `PTMediaPlayer` 对于每个资产，使用 `PTMediaPlayerItem` 方法。

Instant-on可帮助您在后台同时启动多个媒体播放器实例，或启动媒体播放器项目加载器实例，并在所有这些实例中缓冲视频流。 当用户更改频道，并且流已正确缓冲时，调用 `play` 在新的频道上更快地开始播放。

---
description: 即时加载将部分媒体预加载到一个或多个渠道上。 在用户选择或切换频道后，由于某些缓冲已经完成，内容会更早开始。
seo-description: 即时加载将部分媒体预加载到一个或多个渠道上。 在用户选择或切换频道后，由于某些缓冲已经完成，内容会更早开始。
seo-title: 即时启动
title: 即时启动
uuid: 23864919-9045-4223-9e47-464e38ebe5ef
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 即时启动{#instant-on}

即时加载将部分媒体预加载到一个或多个渠道上。 在用户选择或切换频道后，由于某些缓冲已经完成，内容会更早开始。

当播放器处于状态时， `PTMediaPlayerStatusReady` 调用以预加 `prepareToPlay` 载并处理某些内容以供以后回放。

>[!TIP]
>
>如果不拨叫， `prepareToPlay`先自动 `play` 拨叫 `prepareToPlay` 电话。 此时已完成预加载和处理。

TVSDK完成以下部分或所有任务 `prepareToPlay`:

* 如果设置了元 `kSyncCookiesWithAVAsset` 数据密钥，则TVSDK向原始M3U8文件发出一个请求以同步cookie。
* 加载DRM元数据键。
* 创建和准备播放内容所需的一些结构、元素或资源。

>[!TIP]
>
>该方法 `PTMediaPlayer` 和方 `PTMediaPlayerItem``prepareToPlay` 法是相等的。 要避免为每个资产 `PTMediaPlayer` 创建单独的实例，请使用该 `PTMediaPlayerItem` 方法。

即时启动可帮助您同时在后台启动多个媒体播放器实例或媒体播放器项目加载器实例，并在所有这些实例中缓冲视频流。 当用户更改频道且流已正确缓冲时，对新频道 `play` 的调用会更快地开始播放。

---
description: TVSDK引入了通过HTTPS的安全投放。
seo-description: TVSDK引入了通过HTTPS的安全投放。
seo-title: 通过HTTPS安全投放
title: 通过HTTPS安全投放
translation-type: tm+mt
source-git-commit: 4a2271fc481b37bb0a437091de6efe98fcb348d9
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---


# 通过HTTPS{#secure-delivery-https}安全投放

Adobe PrimetimeTVSDK为来自TVSDK的所有呼叫提供HTTPS投放支持，这些呼叫包括

* Auditude Ad Server调用
* CRS请求
* DRM许可呼叫
* 视频分析Ping
* 计费Ping

为了使用此功能，请确保为提供上述请求而配置的服务器支持HTTPS。

默认情况下不启用此新行为。 在调用`MediaPlayer.replaceCurrentResource()`之前，请使用以下内容启用安全投放

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```

---
description: TVSDK引入了通过HTTPS的安全交付。
seo-description: TVSDK引入了通过HTTPS的安全交付。
seo-title: 通过HTTPS安全交付
title: 通过HTTPS安全交付
translation-type: tm+mt
source-git-commit: 4a2271fc481b37bb0a437091de6efe98fcb348d9

---


# 通过HTTPS安全交付 {#secure-delivery-https}

Adobe Primetime TVSDK为来自TVSDK的所有调用提供HTTPS交付支持，包括

* Auditude广告服务器调用
* CRS请求
* DRM许可呼叫
* 视频分析Ping
* 计费Ping

为了使用此功能，请确保为提供上述请求而配置的服务器支持HTTPS。

默认情况下不启用此新行为。 在呼叫之前，请使用以下工具启用安全交付 `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```

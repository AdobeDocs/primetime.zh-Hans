---
description: TVSDK引入了通过HTTPS的安全交付。
title: 通过HTTPS的安全交付
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---

# 通过HTTPS的安全交付 {#secure-delivery-https}

Adobe Primetime TVSDK为源自TVSDK的所有调用支持HTTPS交付，其中包括

* Auditude广告服务器调用
* CRS请求
* DRM许可证调用
* 视频分析Ping
* 计费Ping

要使用此功能，请确保配置为提供上述请求的服务器支持HTTPS。

默认情况下，不启用此新行为。 使用以下内容在调用之前启用安全交付 `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```

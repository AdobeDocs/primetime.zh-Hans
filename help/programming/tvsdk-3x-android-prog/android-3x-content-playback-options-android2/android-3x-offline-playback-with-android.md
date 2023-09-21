---
description: 引入了新API，它将指示TVSDK在下载清单时忽略网络连接状态。
title: 使用Android脱机播放
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# 使用Android脱机播放 {#offline-playback-with-android}

已引入以下API，它们将指示TVSDK在下载清单时忽略网络连接状态。 网络连接状态通常在自适应比特率流(ABR)期间使用，以确定是尝试回退还是等待网络恢复。

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

您可以启用此设置并忽略网络连接。

设置 `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` 为真。 布尔值的默认值为false。

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```

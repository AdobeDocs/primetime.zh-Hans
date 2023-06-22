---
description: 引入新API，指示TVSDK在下载清单时忽略网络连接状态。
title: 使用Android脱机播放
exl-id: 9ac50d3e-5839-4eb9-8811-efde56cfe375
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# 使用Android脱机播放 {#offline-playback-with-android}

引入了以下API，指示TVSDK在下载清单时忽略网络连接状态。 网络连接状态通常在自适应比特率流(ABR)期间使用，以确定是尝试回退还是等待网络恢复。

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

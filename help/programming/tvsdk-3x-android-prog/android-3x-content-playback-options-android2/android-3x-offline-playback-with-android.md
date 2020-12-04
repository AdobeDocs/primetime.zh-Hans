---
description: '已引入新的API，它将指示TVSDK在下载清单时忽略网络连接状态。 '
seo-description: '已引入新的API，它将指示TVSDK在下载清单时忽略网络连接状态。 '
seo-title: 使用Android脱机播放
title: 使用Android脱机播放
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Android {#offline-playback-with-android}脱机回放

已引入以下API，它们将指示TVSDK在下载清单时忽略网络连接状态。 在自适应比特率流播放(ABR)期间，通常使用网络连接状态来确定是尝试回退还是等待网络恢复。

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

您可以启用此设置并忽略网络连接。

将`com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback`设置为true。 布尔值的默认值为false。

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```

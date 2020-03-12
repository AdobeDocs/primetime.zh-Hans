---
description: 当变体播放列表具有多个相同比特率的演绎版，并且其中一个演绎版停止工作时，将发生故障转移处理。 TVSDK在再现之间切换。
seo-description: 当变体播放列表具有多个相同比特率的演绎版，并且其中一个演绎版停止工作时，将发生故障转移处理。 TVSDK在再现之间切换。
seo-title: 故障转移
title: 故障转移
uuid: 064886ab-afa2-4afc-b795-d094b31934b8
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 故障转移 {#failover}

当变体播放列表具有多个相同比特率的演绎版，并且其中一个演绎版停止工作时，将发生故障转移处理。 TVSDK在再现之间切换。

以下示例显示了具有相同比特率的故障转移URL的变体播放列表：

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

当TVSDK加载变体播放列表时，它会创建一个队列，该队列以相同比特率保存内容的所有再现的URL。 当URL请求失败时，TVSDK使用故障转移队列中相同位速率的下一个URL。 在任何特定的故障时间，TVSDK都会循环使用所有可用的URL，直到它找到正确的URL或尝试所有可用的URL为止。 如果TVSDK已尝试使用所有可用的URL，且这些URL均无效，则TVSDK将停止尝试播放内容。

故障转移仅在M3U8级别发生，这意味着：

* 对于VOD，仅当它开始尝试播放时才会发生故障转移，而在它开始播放后不会发生故障转移。
* 对于实时流，故障转移可以在流的中间发生。

>[!TIP]
>
>TVSDK（而非Apple AV Foundation播放器）提供故障转移处理。
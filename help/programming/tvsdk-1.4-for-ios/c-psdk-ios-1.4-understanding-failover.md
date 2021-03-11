---
description: 当变量播放列表具有多个位速率相同的演绎版，并且其中一个演绎版停止工作时，将发生故障转移处理。 TVSDK在再现之间切换。
title: 故障转移
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# 故障转移{#failover}

当变量播放列表具有多个位速率相同的演绎版，并且其中一个演绎版停止工作时，将发生故障转移处理。 TVSDK在再现之间切换。

以下示例显示了具有相同比特率的故障转移URL的变体播放列表：

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

当TVSDK加载变体播放列表时，它会创建一个队列，该队列保存相同比特率的内容所有再现的URL。 当URL请求失败时，TVSDK使用故障转移队列中相同比特率的下一个URL。 在任何特定的故障时间，TVSDK循环一次访问所有可用的URL，直到它找到一个正常工作的URL，或直到它尝试了所有可用的URL。 如果TVSDK已尝试使用所有可用的URL，而且这些URL都不起作用，则TVSDK将停止尝试播放内容。

故障转移仅在M3U8级别发生，这意味着：

* 对于VOD，仅当开始尝试播放时才能进行故障转移，而在开始播放后不能进行故障转移。
* 对于实时流，故障转移可能发生在流的中间。

>[!TIP]
>
>TVSDK（而非Apple AV Foundation播放器）提供故障转移处理。


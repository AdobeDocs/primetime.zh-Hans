---
description: 当变体播放列表具有具有相同比特率的多个演绎版，并且其中一个演绎版停止工作时，会发生故障转移处理。 TVSDK在呈现版本之间切换。
title: 故障转移
exl-id: 8c215e2b-e601-4991-a66f-0e810176a511
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# 故障转移{#failover}

当变体播放列表具有具有相同比特率的多个演绎版，并且其中一个演绎版停止工作时，会发生故障转移处理。 TVSDK在呈现版本之间切换。

以下示例显示具有相同比特率的故障转移URL的变体播放列表：

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

当TVSDK加载变体播放列表时，它将创建一个队列，该队列会以相同的比特率保存内容的所有演绎版的URL。 当URL请求失败时，TVSDK将使用故障转移队列中具有相同比特率的下一个URL。 在任何特定的故障时间，TVSDK都会循环浏览所有可用的URL，直到找到正确工作的URL或尝试了所有可用的URL为止。 如果TVSDK尝试了所有可用的URL，但所有URL都无法正常工作，则TVSDK将停止尝试播放内容。

故障转移仅在M3U8级别进行，这意味着：

* 对于VOD，仅当开始尝试播放时才能进行故障切换，而不是在开始播放后进行故障切换。
* 对于实时流，故障转移可以在流中间发生。

>[!TIP]
>
>TVSDK(而不是Apple AV Foundation播放器)提供故障转移处理。

---
description: 通过Internet进行流式传输需要持续稳定的连接才能从远程服务器播放流。 但是，查看者的Internet连接或流播放的可变性意味着远程播放可能没有本地播放的媒体质量。
title: 播放和故障切换
exl-id: ba8326ba-4ff1-46ad-bd18-9c83147ab619
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# 概述 {#playback-and-failover-overview}

通过Internet进行流式传输需要持续稳定的连接才能从远程服务器播放流。 但是，查看者的Internet连接或流播放的可变性意味着远程播放可能没有本地播放的媒体质量。

>[!IMPORTANT]
>
>Primetime无法针对ISP中断或电缆断开等故障提供保护。

Primetime流提供故障转移保护，可保护播放免受某些远程服务器故障或操作故障的影响，从而提供更好的观看体验。 尽管存在传输问题，TVSDK仍实施了故障转移保护，以最大程度地减少播放中断并实现无缝播放。 当整个演绎版或片段不可用时，视频播放器会自动切换到备份媒体集。

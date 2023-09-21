---
description: 通过Internet进行流式传输需要持续稳定的连接才能从远程服务器播放流。 但是，观看者的Internet连接或流播放的可变性意味着远程播放可能没有在本地播放的媒体质量。
title: 播放和故障转移
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# 概述 {#playback-and-failover-overview}

通过Internet进行流式传输需要持续稳定的连接才能从远程服务器播放流。 但是，观看者的Internet连接或流播放的可变性意味着远程播放可能没有在本地播放的媒体质量。

Primetime无法防止ISP中断或电缆断开等故障。 但是，Primetime流提供故障转移保护，可保护播放免受某些远程服务器故障或操作故障的影响，从而为观看者提供更好的体验。 TVSDK实施了故障转移保护，以最大程度地减少播放中断，并在存在传输问题的情况下实现无缝播放。 当整个演绎版或片段不可用时，视频播放器会自动切换到备份媒体集。

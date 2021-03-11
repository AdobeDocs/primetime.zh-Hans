---
description: 通过Internet进行流播放需要一个持续稳定的连接才能从远程服务器播放流。 但是，查看器的Internet连接或流播放的可变性意味着远程播放可能无法在本地播放媒体的质量。
title: 播放和故障转移
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---


# 概述{#playback-and-failover-overview}

通过Internet进行流播放需要一个持续稳定的连接才能从远程服务器播放流。 但是，查看器的Internet连接或流播放的可变性意味着远程播放可能无法在本地播放媒体的质量。

Primetime无法避免ISP中断或电缆断开等故障。 但是，Primetime流提供故障转移保护，可保护回放免受某些远程服务器故障或操作故障的影响，为观看者提供更好的体验。 TVSDK实施故障转移保护以最大程度地减少播放中断，尽管存在传输问题，仍可实现无缝播放。 当整个再现或片段不可用时，视频播放器会自动切换到备份媒体集。

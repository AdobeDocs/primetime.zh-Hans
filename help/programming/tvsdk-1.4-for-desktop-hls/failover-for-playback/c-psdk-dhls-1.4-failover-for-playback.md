---
description: 通过Internet进行流播放需要一个持续稳定的连接才能从远程服务器播放流。 但是，查看器的Internet连接或流播放的可变性意味着远程播放可能不具有本地播放的媒体质量。
seo-description: 通过Internet进行流播放需要一个持续稳定的连接才能从远程服务器播放流。 但是，查看器的Internet连接或流播放的可变性意味着远程播放可能不具有本地播放的媒体质量。
seo-title: 播放和故障转移
title: 播放和故障转移
uuid: 731c087d-9e14-4c7a-a856-c3962b9d7608
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# 概述{#playback-and-failover-overview}

通过Internet进行流播放需要一个持续稳定的连接才能从远程服务器播放流。 但是，查看器的Internet连接或流播放的可变性意味着远程播放可能不具有本地播放的媒体质量。

Primetime无法避免ISP中断或电缆断开等故障。 但是，Primetime流提供故障转移保护，以保护回放免受某些远程服务器故障或操作故障的影响，为观看者提供更好的体验。 TVSDK实施故障转移保护以最大限度地减少播放中断，尽管存在传输问题，仍可实现无缝播放。 当整个再现或片段不可用时，视频播放器会自动切换到备份媒体集。

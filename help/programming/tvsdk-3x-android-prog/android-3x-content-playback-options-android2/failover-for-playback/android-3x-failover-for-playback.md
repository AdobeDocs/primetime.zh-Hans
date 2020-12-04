---
description: 通过Internet进行流播放需要一个持续稳定的连接才能从远程服务器播放流。 但是，查看器的Internet连接或流播放的可变性意味着远程播放可能不具有本地播放的媒体质量。
seo-description: 通过Internet进行流播放需要一个持续稳定的连接才能从远程服务器播放流。 但是，查看器的Internet连接或流播放的可变性意味着远程播放可能不具有本地播放的媒体质量。
seo-title: 播放和故障转移
title: 播放和故障转移
uuid: 511f16b9-2b86-42c1-8d89-09b26534200b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# 概述{#playback-and-failover-overview}

通过Internet进行流播放需要一个持续稳定的连接才能从远程服务器播放流。 但是，查看器的Internet连接或流播放的可变性意味着远程播放可能不具有本地播放的媒体质量。

>[!IMPORTANT]
>
>Primetime无法防止ISP中断或电缆断开等故障。

Primetime流提供故障转移保护，以保护回放免受某些远程服务器故障或操作故障的影响，从而提供更好的观看体验。 尽管存在传输问题，TVSDK仍实施故障转移保护以最大限度地减少播放中断并实现无缝播放。 当整个再现或片段不可用时，视频播放器会自动切换到备份媒体集。
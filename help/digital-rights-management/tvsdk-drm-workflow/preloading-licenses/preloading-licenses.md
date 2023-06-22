---
title: 离线播放的预加载许可证概述
description: 离线播放的预加载许可证概述
copied-description: true
exl-id: 0d49c0e4-821b-4354-b92d-bbe2c07e467b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# 为离线播放预先加载许可证 {#pre-loading-licenses-for-offline-playback}

您可以预载播放受Primetime DRM保护的内容所需的许可证。 预加载的许可证允许用户查看内容，无论他们是否有活动的Internet连接。

预加载过程本身 *是* 需要互联网连接。 您可以使用 `DRMManager.loadVoucher()` 提前预载许可证。 之后，当客户希望播放所需的内容时，DRM系统已经预先准备好，可以立即播放受保护的内容。

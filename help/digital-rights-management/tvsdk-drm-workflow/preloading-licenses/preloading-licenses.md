---
title: 离线播放的预加载许可证概述
description: 离线播放的预加载许可证概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# 为离线播放预加载许可证 {#pre-loading-licenses-for-offline-playback}

您可以预加载播放受Primetime DRM保护的内容所需的许可证。 预加载的许可证允许用户查看内容，无论他们是否有活动的Internet连接。

预加载过程本身 *是* 需要互联网连接。 您可以使用 `DRMManager.loadVoucher()` 提前预载许可证。 之后，当客户希望播放期望的内容时，DRM系统已经预先准备好，可以立即播放受保护的内容。

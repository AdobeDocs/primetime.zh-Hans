---
seo-title: 脱机回放的预加载许可证概述
title: 脱机回放的预加载许可证概述
uuid: 71e5169b-7f70-4723-9f9b-fdff822c5876
translation-type: tm+mt
source-git-commit: 9bbcb228d3367fbf53de811bf2941ca653ce3b0e

---


# 为脱机回放预加载许可证 {#pre-loading-licenses-for-offline-playback}

您可以预加载播放Primetime DRM保护的内容所需的许可证。 预加载的许可证允许用户查看内容，无论他们是否具有活动的Internet连接。

预载过程本身 *需要* Internet连接。 您可以提 `DRMManager.loadVoucher()` 前使用来预载许可证。 之后，当客户希望播放所需内容时，DRM系统已预先准备好并可立即播放受保护的内容。

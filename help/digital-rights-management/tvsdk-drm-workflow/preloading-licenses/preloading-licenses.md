---
seo-title: 预加载许可证脱机播放概述
title: 预加载许可证脱机播放概述
uuid: 71e5169b-7f70-4723-9f9b-fdff822c5876
translation-type: tm+mt
source-git-commit: 9bbcb228d3367fbf53de811bf2941ca653ce3b0e
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# 用于脱机播放的预加载许可证{#pre-loading-licenses-for-offline-playback}

您可以预载播放Primetime DRM保护的内容所需的许可证。 预加载的许可证允许用户视图内容，无论他们是否具有活动的Internet连接。

预载过程本身&#x200B;*需要Internet连接。*&#x200B;您可以提前使用`DRMManager.loadVoucher()`预载许可证。 之后，当客户希望播放所需内容时，DRM系统已预先准备，并且可以立即播放受保护的内容。

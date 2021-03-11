---
description: 如果您的Adobe Primetime DRM实施使用要求客户端保持状态（例如，播放窗口间隔）的业务规则，Adobe建议服务器保持回滚计数器的跟踪并使用AIR或SWF允许列表。
title: 回滚检测
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# 回滚检测{#rollback-detection}

如果您的Adobe Primetime DRM实施使用要求客户端保持状态（例如，播放窗口间隔）的业务规则，Adobe建议服务器保持回滚计数器的跟踪并使用AIR或SWF允许列表。

回滚计数器在客户端发出的大多数请求中发送到服务器。 如果您实施Primetime DRM时不需要回滚计数器，则可以忽略它。 否则，Adobe建议服务器存储随机计算机ID(使用[MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())获取)以及数据库中的当前计数器值。

有关如何增加和跟踪回滚计数器的详细信息，请参阅[ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html)和回滚检测。
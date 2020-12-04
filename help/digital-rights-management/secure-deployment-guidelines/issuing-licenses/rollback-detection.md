---
description: 如果您的Adobe PrimetimeDRM实施使用要求客户端保持状态（例如，播放窗口间隔）的业务规则，则Adobe建议服务器跟踪回滚计数器，并使用AIR或SWF允许列表。
seo-description: 如果您的Adobe PrimetimeDRM实施使用要求客户端保持状态（例如，播放窗口间隔）的业务规则，则Adobe建议服务器跟踪回滚计数器，并使用AIR或SWF允许列表。
seo-title: 回滚检测
title: 回滚检测
uuid: f161ed41-488a-478a-b6a8-468cf6d11e89
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# 回滚检测{#rollback-detection}

如果您的Adobe PrimetimeDRM实施使用要求客户端保持状态（例如，播放窗口间隔）的业务规则，则Adobe建议服务器跟踪回滚计数器，并使用AIR或SWF允许列表。

回滚计数器在客户端发出的大多数请求中都发送到服务器。 如果您的Primetime DRM实施不需要回滚计数器，则可忽略它。 否则，Adobe建议服务器存储随机计算机ID(使用[MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())获取)以及数据库中的当前计数器值。

有关如何增加和跟踪回滚计数器的详细信息，请参阅[ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html)和回滚检测。
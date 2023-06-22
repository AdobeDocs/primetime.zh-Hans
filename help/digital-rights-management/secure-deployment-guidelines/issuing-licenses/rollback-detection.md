---
description: 如果您的Adobe Primetime DRM实施使用要求客户端保持状态的业务规则（例如，播放窗口间隔），Adobe建议服务器跟踪回滚计数器并使用AIR或SWF允许列表。
title: 回滚检测
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# 回滚检测 {#rollback-detection}

如果您的Adobe Primetime DRM实施使用要求客户端保持状态的业务规则（例如，播放窗口间隔），Adobe建议服务器跟踪回滚计数器并使用AIR或SWF允许列表。

回滚计数器在来自客户端的大多数请求中发送到服务器。 如果您的Primetime DRM实施不需要回滚计数器，则可以忽略。 否则，Adobe建议服务器存储随机计算机ID，该ID是使用获取的 [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())，以及数据库中的当前计数器值。

有关如何递增和跟踪回滚计数器的详细信息，请参见 [客户端状态](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) 和回滚检测。
---
description: 如果您实施Adobe Primetime DRM时使用要求客户端保持状态（例如，播放窗口间隔）的业务规则，Adobe建议服务器跟踪回滚计数器并使用AIR或SWF白名单。
seo-description: 如果您实施Adobe Primetime DRM时使用要求客户端保持状态（例如，播放窗口间隔）的业务规则，Adobe建议服务器跟踪回滚计数器并使用AIR或SWF白名单。
seo-title: 回滚检测
title: 回滚检测
uuid: f161ed41-488a-478a-b6a8-468cf6d11e89
translation-type: tm+mt
source-git-commit: 3fdef12b717bb6f70ca27d9278de61d709f8349c

---


# 回滚检测 {#rollback-detection}

如果您实施Adobe Primetime DRM时使用要求客户端保持状态（例如，播放窗口间隔）的业务规则，Adobe建议服务器跟踪回滚计数器并使用AIR或SWF白名单。

回滚计数器在来自客户端的大多数请求中发送到服务器。 如果您实施Primetime DRM时不需要回滚计数器，则可以忽略它。 否则，Adobe建议服务器存储随机计算机ID(使用 [MachineToken.getUniqueId()获取)](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())，以及数据库中的当前计数器值。

有关如何增加和跟踪回滚计数器的详细信息，请参 [阅ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) 和Rollback detection。
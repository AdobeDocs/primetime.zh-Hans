---
seo-title: 回滚检测
title: 回滚检测
uuid: fc80c98f-7ee5-414b-87fe-0dbb8d4f6019
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# 回滚检测{#rollback-detection}

如果Adobe Access的实施使用要求客户端保持状态（例如，播放窗口间隔）的业务规则，Adobe强烈建议服务器跟踪回滚计数器并使用AIR或SWF允许列表。

回滚计数器在客户端发出的大多数请求中都发送到服务器。 如果Adobe Access的实施不需要回滚计数器，则可忽略它。 否则，Adobe建议服务器将随机计算机ID（使用获取的） `MachineToken.getMachineId().getUniqueId()`和当前计数器值存储在数据库中。 有关增加和跟踪回滚计数器的详细信息，请参阅 *使用Adobe Access SDK保护内* 容中的 *Adobe Access* API Reference *and* Rollback detection中的ClientState。

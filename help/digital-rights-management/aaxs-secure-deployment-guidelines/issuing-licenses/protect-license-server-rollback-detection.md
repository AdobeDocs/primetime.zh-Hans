---
seo-title: 回滚检测
title: 回滚检测
uuid: fc80c98f-7ee5-414b-87fe-0dbb8d4f6019
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# 回滚检测{#rollback-detection}

如果您的Adobe访问实施使用要求客户端保持状态（例如，播放窗口间隔）的业务规则，Adobe强烈建议服务器跟踪回滚计数器并使用AIR或SWF允许列表。

回滚计数器在客户端发出的大多数请求中都发送到服务器。 如果Adobe访问的实施不需要回滚计数器，则可以忽略它。 否则，Adobe建议服务器将随机计算机ID（使用`MachineToken.getMachineId().getUniqueId()`获取）和当前计数器值存储在数据库中。 有关增加和跟踪回滚计数器的详细信息，请参阅&#x200B;*Adobe访问API参考*&#x200B;和&#x200B;*回滚检测*&#x200B;中的ClientState(使用Adobe访问SDK保护内容)*。*

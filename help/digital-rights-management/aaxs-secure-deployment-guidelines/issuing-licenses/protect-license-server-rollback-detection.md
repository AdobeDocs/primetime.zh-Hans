---
title: 回滚检测
description: 回滚检测
copied-description: true
exl-id: 054d3634-5ce9-4a51-ac91-e6ae60a1fd6e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# 回滚检测 {#rollback-detection}

如果您的Adobe访问实施使用要求客户端保持状态的业务规则（例如，播放窗口间隔），Adobe强烈建议服务器跟踪回滚计数器，并使用AIR或SWF允许列表。

回滚计数器在来自客户端的大多数请求中发送到服务器。 如果您实施的Adobe访问不需要回滚计数器，则可以忽略该计数器。 否则，Adobe建议服务器存储随机计算机ID，该ID是使用获取的 `MachineToken.getMachineId().getUniqueId()` — 和数据库中的当前计数器值。 有关递增和跟踪回滚计数器的更多信息，请参阅中的ClientState *Adobe访问API参考* 和 *回滚检测* 在 *使用Adobe访问SDK保护内容*.

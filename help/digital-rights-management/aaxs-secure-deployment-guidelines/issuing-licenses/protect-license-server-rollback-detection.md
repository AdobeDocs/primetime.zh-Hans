---
seo-title: 回滚检测
title: 回滚检测
uuid: fc80c98f-7ee5-414b-87fe-0dbb8d4f6019
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 回滚检测{#rollback-detection}

如果Adobe Access的实施使用要求客户端保持状态（例如，播放窗口间隔）的业务规则，Adobe强烈建议服务器跟踪回滚计数器并使用AIR或SWF白名单。

回滚计数器在来自客户端的大多数请求中发送到服务器。 如果Adobe Access的实施不需要回滚计数器，则可以忽略它。 否则，Adobe建议服务器将随机计算机ID（使用获取的） `MachineToken.getMachineId().getUniqueId()`和当前计数器值存储在数据库中。 有关增加和跟踪回滚计数器的详细信息，请参阅《使用Adobe Access SDK for Protecting Content *》(* Adobe Access API Reference *and* Rollback detection)中的ClientState **。

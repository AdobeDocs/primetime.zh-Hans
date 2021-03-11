---
title: 同步要求
description: 同步要求
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# 同步要求{#requirements-for-synchronization}

指定客户端将与服务器同步其状态的频率。 如果客户端已经颁发带外许可证（未联系许可证服务器），使用规则可指定客户端必须向服务器发送同步消息以同步客户端的安全时间并向服务器报告客户端状态。

同步行为是使用以下参数定义的：

* 开始间隔 — 指定在上次成功同步后等待多长时间以开始另一个同步请求。
* 硬停止间隔 — （可选）。 如果在指定的时间内未成功同步，则禁止播放。
* 强制同步概率 — （可选）。 客户端在下一个开始间隔之前发送同步消息的概率。

>[!NOTE]
>
>Adobe Access客户端版本3.0及更高版本支持此使用规则。 旧客户端上的行为取决于许可证服务器支持的最低客户端版本。 请参阅[最低客户端版本](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md)。


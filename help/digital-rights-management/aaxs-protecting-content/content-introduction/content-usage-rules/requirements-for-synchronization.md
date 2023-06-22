---
title: 同步要求
description: 同步要求
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# 同步要求{#requirements-for-synchronization}

指定客户端将其状态与服务器同步的频率。 如果客户机已经获得带外许可证（未联系许可证服务器），则使用规则可指定客户机必须向服务器发送同步消息，以便同步客户机的安全时间并向服务器报告客户机状态。

使用以下参数定义同步行为：

* 开始时间间隔 — 指定在上次成功同步之后等待多长时间以启动另一个同步请求。
* 硬停止间隔 — （可选）。 如果在指定的时间内未成功进行同步，则不允许播放。
* 强制同步概率 — （可选）。 客户端在下一次启动间隔之前发送同步消息的概率。

>[!NOTE]
>
>Adobe访问客户端3.0及更高版本支持此使用规则。 旧版客户端的行为取决于许可证服务器支持的最低客户端版本。 参见， [最低客户端版本](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).


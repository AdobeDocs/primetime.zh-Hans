---
title: 概述
description: 概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 概述{#overview}

您可能需要撤销客户端的凭据，或检查给定的凭据集是否已在某些情况下被撤销。 如果凭据受到威胁，可能会吊销凭据。 出现这些问题时，将不再向受到威胁的客户端颁发许可证。

Adobe维护证书吊销列表(CRL)，用于吊销受到威胁的客户端。 这些CRL由SDK自动实施。 许可证服务器可能通过禁止特定计算机凭据或DRM和运行时凭据的特定版本来进一步限制客户端。 A `RevocationList` 可以创建并传递到SDK以撤销计算机凭据。 可以在DRM策略级别撤销特定的DRM/运行时版本，方法是在播放权限中设置模块限制，或者通过在播放权限中设置模块限制来全局撤销特定的DRM/运行时版本。 `HandlerConfiguration`.

讨论的重点是撤销客户凭证。

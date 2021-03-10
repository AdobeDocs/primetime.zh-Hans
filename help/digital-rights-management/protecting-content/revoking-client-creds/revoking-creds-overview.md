---
title: 概述
description: 概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# 概述{#overview}

您可能需要撤销客户端的凭据，或检查给定的一组凭据是否已在某些条件下被吊销。 如果凭据已泄露，则可撤销凭据。 出现这些问题时，许可证不再发给受损的客户。

Adobe保留用于撤销受损客户端的证书吊销列表(CRL)。 这些CRL由SDK自动强制执行。 许可服务器可以通过禁止特定机器凭证或特定版本的DRM和运行时凭证进一步限制客户端。 可以创建`RevocationList`并将其传递到SDK以撤销计算机凭据。 可以通过在播放权中设置模块限制在DRM策略级别撤销特定DRM/运行时版本，也可以通过在`HandlerConfiguration`中设置模块限制在全局级别撤销特定DRM/运行时版本。

讨论的中心是撤销客户端凭据。

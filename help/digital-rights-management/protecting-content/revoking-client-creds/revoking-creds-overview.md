---
title: 概述
description: 概述
copied-description: true
exl-id: 332343ce-ac22-41a5-801a-3597476f0eaf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 概述{#overview}

您可能需要撤销客户端的凭据，或检查给定的凭据集是否已在某些情况下被撤销。 如果凭据受到危害，可能会吊销凭据。 当出现这些问题时，将不再向受到威胁的客户端颁发许可证。

Adobe维护用于撤销受威胁客户端的证书撤销列表(CRL)。 这些CRL由SDK自动实施。 许可证服务器可以通过禁止特定计算机凭证或DRM和运行时凭证的特定版本来进一步限制客户端。 A `RevocationList` 可以创建并传递到SDK以撤销计算机凭据。 可以通过在播放权限中设置模块限制来在DRM策略级别撤销特定DRM/运行时版本，或者通过在播放权限中设置模块限制来全局撤销特定DRM/运行时版本。 `HandlerConfiguration`.

讨论的重点是撤销客户凭证。

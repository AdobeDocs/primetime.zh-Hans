---
title: 撤销客户端凭据
description: 撤销客户端凭据
copied-description: true
exl-id: 583dff28-c34a-4759-81a6-0471feab309f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 撤销客户端凭据{#revoking-client-credentials}

在某些情况下，需要撤销客户端的凭据或检查给定的凭据集是否已撤销。 如果凭据受损，凭据可能会被撤销。 发生这种情况时，将不再向受到威胁的客户端颁发许可证。

Adobe维护用于撤销受威胁客户端的证书撤销列表(CRL)。 这些CRL由SDK自动实施。 许可证服务器可以通过禁止特定计算机凭证或DRM和运行时凭证的特定版本来进一步限制客户端。 A `RevocationList` 可以创建并传递到SDK以撤销计算机凭据。 特定DRM/运行时版本可以在策略级别（通过在播放权限中设置模块限制）或全局(通过在 `HandlerConfiguration`)。

本章的讨论将着重于撤销客户端凭据。

---
title: 撤销客户端凭据
description: 撤销客户端凭据
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 撤销客户端凭据{#revoking-client-credentials}

在某些情况下，需要撤销客户端的凭据或检查给定的凭据集是否已撤销。 如果凭据被泄漏，凭据可能会被撤销。 发生这种情况时，将不再向受到威胁的客户端颁发许可证。

Adobe维护证书吊销列表(CRL)，用于吊销受到威胁的客户端。 这些CRL由SDK自动实施。 许可证服务器可能通过禁止特定计算机凭据或DRM和运行时凭据的特定版本来进一步限制客户端。 A `RevocationList` 可以创建并传递到SDK以撤销计算机凭据。 特定DRM/运行时版本可以在策略级别（通过在播放权限中设置模块限制）或全局(通过在 `HandlerConfiguration`)。

本章的讨论将围绕撤销客户端凭据展开。

---
seo-title: 撤销客户端凭据
title: 撤销客户端凭据
uuid: 47f1ec1a-bd8f-4f8c-bee3-bfbf6d9902e7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# 撤销客户端凭据{#revoking-client-credentials}

在某些情况下，必须撤销客户端的凭据或检查给定的一组凭据是否已被撤销。 如果凭据被破坏，则可撤销凭据。 发生这种情况时，许可证将不再颁发给受损客户。

Adobe保留用于撤销被破坏的客户端的证书吊销列表(CRL)。 这些CRL由SDK自动强制执行。 许可证服务器可以通过禁止特定计算机凭据或特定版本的DRM和运行时凭据进一步限制客户端。 可以创建`RevocationList`并将其传递到SDK以撤销计算机凭据。 特定DRM/运行时版本可以在策略级别撤销（通过在播放权中设置模块限制）或全局撤销（通过在`HandlerConfiguration`中设置模块限制）。

本章中的讨论将集中于撤销客户端凭据。

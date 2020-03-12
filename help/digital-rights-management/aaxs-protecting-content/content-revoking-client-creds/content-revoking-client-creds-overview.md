---
seo-title: 撤销客户端凭据
title: 撤销客户端凭据
uuid: 47f1ec1a-bd8f-4f8c-bee3-bfbf6d9902e7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 撤销客户端凭据{#revoking-client-credentials}

在某些情况下，必须撤销客户端的凭据或检查给定的一组凭据是否已被撤销。 如果凭据被破坏，则可撤销凭据。 发生这种情况时，许可证将不再发给受损客户。

Adobe为撤销受损的客户端维护证书撤销列表(CRL)。 这些CRL由SDK自动强制执行。 许可服务器可以通过禁止特定计算机凭据或特定版本的DRM和运行时凭据进一步限制客户端。 可 `RevocationList` 以创建并传递到SDK以撤销计算机凭据。 特定DRM/运行时版本可在策略级别（通过在播放权限中设置模块限制）或全局(通过在中设置模块限制 `HandlerConfiguration`)撤销。

本章中的讨论将集中于撤销客户端凭据。

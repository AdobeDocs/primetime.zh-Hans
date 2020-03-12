---
seo-title: 概述
title: 概述
uuid: c6f54867-d0a3-43fd-9493-6496f1b7831a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 概述{#overview}

您可能需要撤销客户端的凭据，或检查给定的一组凭据是否已在某些条件下被撤销。 如果凭据被破坏，则可撤销凭据。 发生这些问题时，许可证不再发给受损的客户。

Adobe为撤销受损的客户端维护证书撤销列表(CRL)。 这些CRL由SDK自动强制执行。 许可服务器可以通过禁止特定计算机凭据或特定版本的DRM和运行时凭据进一步限制客户端。 可 `RevocationList` 以创建并传递到SDK以撤销计算机凭据。 通过在播放权限中设置模块限制或通过在中设置模块限制，可以在DRM策略级别撤销特定DRM/运行时版本 `HandlerConfiguration`。

讨论的中心是撤销客户端凭据。

---
seo-title: 使用DRMErrorEvent类概述
title: 使用DRMErrorEvent类概述
uuid: cbb9c1a7-3c50-479d-b7e5-63010a696dfa
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# 使用DRMErrorEvent类概述 {#using-the-drmerrorevent-class-overview}

当Primetime对 `DRMErrorEvent` 象尝试播放受保护的内容时遇到与DRM相 [关的错误时，Primetime将调度对象](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)。 如果用户凭据无效，则对象会 `DRMAuthenticateEvent` 重复进行调度，直到用户输入有效凭据或应用程序拒绝进一步尝试为止。 应用程序负责侦听任何其他DRM错误事件，以检测、识别和处理与DRM [相关的错误](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)。

即使使用有效的用户凭据，内容的许可证条款仍可能阻止用户查看加密内容。 例如，用户可能因尝试视图未授权应用程序中的内容而被拒绝访问（例如“应用程序允许列表”）。 未授权的应用程序是未使用列出的允许应用程序签名证书进行签名的应用程序。 在这种情况下，将调 `DRMErrorEvent` 度对象。

如果内容已损坏或应用程序的版本与许可指定的版本不匹配，也可以触发错误事件。 应用程序必须提供相应的错误处理机制。

---
title: 使用DRMErrorEvent类概述
description: 使用DRMErrorEvent类概述
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# 使用DRMErrorEvent类概述 {#using-the-drmerrorevent-class-overview}

Primetime调度 `DRMErrorEvent` 对象，当Primetime对象尝试播放受保护的内容遇到 [DRM相关错误](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages). 如果用户凭据无效，则 `DRMAuthenticateEvent` 对象会重复调度，直到用户输入有效凭据或应用程序拒绝进一步尝试为止。 该应用程序负责侦听任何其他DRM错误事件，以检测、识别并处理 [DRM相关错误](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages).

即使使用有效的用户凭据，内容许可证的条款仍会阻止用户查看加密的内容。 例如，可以拒绝用户访问尝试在未经授权的应用程序中查看内容（例如，应用程序允许列表）。 未经授权的应用程序是指尚未使用允许列出的应用程序签名证书进行签名的应用程序。 在本例中， `DRMErrorEvent` 对象已调度。

如果内容已损坏或应用程序的版本与许可证指定的版本不匹配，也可以触发错误事件。 应用程序必须提供适当的错误处理机制。

---
title: 使用DRMErrorEvent类概述
description: 使用DRMErrorEvent类概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# 使用DRMErrorEvent类概述{#using-the-drmerrorevent-class-overview}

当Primetime对象尝试播放受保护的内容时遇到与DRM相关的错误](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)时，Primetime会调度`DRMErrorEvent`对象。 [如果用户凭据无效，则`DRMAuthenticateEvent`对象会重复调度，直到用户输入有效凭据或应用程序拒绝进一步尝试为止。 应用程序负责侦听任何其他DRM错误事件，以检测、识别和处理与DRM相关的[错误](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)。

即使使用有效的用户凭据，内容的许可证条款仍可能阻止用户查看加密内容。 例如，用户可能因尝试在未经授权的应用程序中视图内容而被拒绝访问（例如，“应用程序允许”列表）。 未授权的应用程序是尚未使用允许列出的应用程序签名证书进行签名的应用程序。 在这种情况下，将调度`DRMErrorEvent`对象。

如果内容已损坏或应用程序的版本与许可指定的版本不匹配，也可触发错误事件。 应用程序必须提供相应的机制来处理错误。

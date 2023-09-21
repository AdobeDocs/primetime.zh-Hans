---
description: 适用于受保护流的Adobe Primetime DRM Server是基于Primetime DRM SDK的许可证服务器实施。 此服务器向Primetime DRM客户端颁发受保护内容的许可证。
title: 关于用于受保护流的Adobe Primetime DRM Server
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# 关于用于受保护流的Adobe Primetime DRM Server{#about-adobe-primetime-drm-server-for-protected-streaming}

适用于受保护流的Adobe Primetime DRM Server是基于Primetime DRM SDK的许可证服务器实施。 此服务器向Primetime DRM客户端颁发受保护内容的许可证。

Primetime DRM Server for Protected Streaming支持多个租户。 您可以代表多个内容发布者托管单个服务器，每个发布者都有自己的配置设置。 此外，服务器支持自定义授权组件，因此您可以在颁发许可证之前执行自定义逻辑。

此服务器旨在用于HTTP流。 因此，此服务器实施不支持Primetime DRM中的所有可用功能。 例如，它不支持用户身份验证请求、多个策略、域绑定许可证、许可证链接或同步消息。

>[!NOTE]
>
>Adobe Primetime DRM以前称为Adobe访问，在此之前称为Flash Access。

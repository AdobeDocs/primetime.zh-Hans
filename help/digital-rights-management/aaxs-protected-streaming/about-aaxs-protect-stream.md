---
title: 关于Adobe Access Server的受保护流
description: 关于Adobe Access Server的受保护流
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# 关于Adobe Access Server for Protected Streaming{#about-adobe-access-server-for-protected-streaming}

Adobe® Access™ Server for Protected Streaming是基于Adobe Access SDK的许可证服务器实现。 此服务器向Adobe Access客户端发放受保护内容的许可证。

Adobe Access Server for Protected Streaming支持多个租户，这意味着可以代表多个内容发布者托管单个服务器，每个发布者都具有自己的配置设置。 此外，服务器支持自定义授权组件，因此可以在颁发许可证之前执行自定义逻辑。

此服务器专门用于HTTP流。 因此，此服务器实现不支持Adobe Access中提供的所有功能。 例如，Adobe Access Server for Protected Streaming不支持用户身份验证请求、多个策略、域绑定许可证、许可证链接或同步消息。

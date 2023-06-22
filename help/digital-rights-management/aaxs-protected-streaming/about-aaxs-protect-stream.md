---
title: 关于适用于受保护流的Adobe Access Server
description: 关于适用于受保护流的Adobe Access Server
copied-description: true
exl-id: 69fbc99d-ee1a-4066-ae01-d61838db32a3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# 关于适用于受保护流的Adobe Access Server{#about-adobe-access-server-for-protected-streaming}

Adobe® Access™ Server for Protected Streaming是基于Adobe访问SDK的许可证服务器实施。 此服务器向Adobe访问客户端颁发受保护内容的许可证。

适用于受保护流媒体的Adobe Access Server支持多个租户，这意味着可以代表多个内容发布者托管单个服务器，而每个发布者具有自己的配置设置。 此外，服务器支持自定义授权组件，因此可以在颁发许可证之前执行自定义逻辑。

此服务器旨在用于HTTP流。 因此，此服务器实现不支持Adobe访问中的所有可用功能。 例如， Adobe Access Server for Protected Streaming不支持用户身份验证请求、多个策略、域绑定许可证、许可证链接或同步消息。

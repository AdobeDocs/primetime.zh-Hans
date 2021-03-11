---
title: 防火墙规则
description: 防火墙规则
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# 防火墙规则{#firewall-rules}

要确保对个性化服务器的访问安全，只需公开某些应用程序路径。 个性化服务器必须接受来自客户端对以下路径的请求：

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

服务路径(如[!DNL /flashaccess/admin/*]（即状态和管理页）)只能从防火墙内访问。 密钥生成服务器的任何部分都不应从防火墙外部访问。

---
title: 防火墙规则
description: 防火墙规则
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# 防火墙规则{#firewall-rules}

要保护对个性化服务器的访问，只需要公开某些应用程序路径。 个性化服务器必须接受客户端向以下路径发出的请求：

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

服务路径，例如 [!DNL /flashaccess/admin/*] 必须只能在防火墙内访问（即状态和管理员页面）。 不应从防火墙外部访问密钥生成服务器的任何部分。

---
title: 防火墙规则
description: 防火墙规则
copied-description: true
exl-id: 1a40822a-893d-43ec-9c3e-8e0b4ebe6d01
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# 防火墙规则{#firewall-rules}

要保护对个性化服务器的访问，只需公开某些应用程序路径。 个性化服务器必须接受来自客户端的以下路径请求：

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

服务路径，例如 [!DNL /flashaccess/admin/*] 只能从防火墙内访问（即状态页面和管理页面）。 不应从防火墙外部访问密钥生成服务器的任何部分。

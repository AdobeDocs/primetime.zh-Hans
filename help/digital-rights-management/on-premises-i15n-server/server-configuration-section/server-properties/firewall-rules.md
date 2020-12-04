---
seo-title: 防火墙规则
title: 防火墙规则
uuid: f1629ceb-22de-4bb5-b73f-9b874d97ea8b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# 防火墙规则{#firewall-rules}

要确保对个性化服务器的访问安全，只需公开某些应用程序路径。 个性化服务器必须接受客户端对以下路径的请求：

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

服务路径(如[!DNL /flashaccess/admin/*]（即状态和管理页面）只能从防火墙内访问。 密钥生成服务器的任何部分都不应从防火墙外部进行访问。

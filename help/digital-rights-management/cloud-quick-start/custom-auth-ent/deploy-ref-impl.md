---
title: 部署BEES参考实施
description: 部署BEES参考实施
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---

# 部署BEES参考实施 {#deploy-the-bees-reference-implementation}

1. 设置Tomcat应用程序服务器。 （请参阅Tomcat文档。）
1. 复制 `[!DNL bees.war]` 归档到Tomcat的 [!DNL webapps/] 文件夹。
1. 发送请求到 `https://localhost:8080/bees`.

   如果看到“BEES正在运行”消息，则表示部署已成功完成。
1. 在您的服务器上启用SSL。

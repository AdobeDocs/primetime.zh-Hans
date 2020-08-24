---
seo-title: 部署BEES参考实施
title: 部署BEES参考实施
uuid: 5ee7b066-8ae8-48ba-a3f0-8cc14b19d5c5
translation-type: tm+mt
source-git-commit: 4f196bbd079edeb1a423afee6b4b7e249d380f40
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---


# 部署BEES参考实施 {#deploy-the-bees-reference-implementation}

1. 设置Tomcat应用程序服务器。 （请参阅Tomcat文档。）
1. 将文 `[!DNL bees.war]` 件复制到Tomcat的文 [!DNL webapps/] 件夹。
1. 向发送请求 `https://localhost:8080/bees`。

   如果看到“BEES is operational”消息，则部署已成功完成。
1. 在服务器上启用SSL。

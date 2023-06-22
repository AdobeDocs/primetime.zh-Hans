---
title: 部署BEES参考实施
description: 部署BEES参考实施
copied-description: true
exl-id: 87f3f879-66b4-4b8c-a0c4-e15551f9b727
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---

# 部署BEES参考实施 {#deploy-the-bees-reference-implementation}

1. 设置Tomcat应用程序服务器。 （请参阅您的Tomcat文档。）
1. 复制 `[!DNL bees.war]` 文件进入Tomcat [!DNL webapps/] 文件夹。
1. 发送请求至 `https://localhost:8080/bees`.

   如果您看到“BEES正在运行”消息，则表示部署已成功完成。
1. 在您的服务器上启用SSL。

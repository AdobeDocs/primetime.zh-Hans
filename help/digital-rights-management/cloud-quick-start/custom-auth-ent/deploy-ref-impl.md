---
title: 部署BEES参考实施
description: 部署BEES参考实施
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---


# 部署BEES引用实现{#deploy-the-bees-reference-implementation}

1. 设置Tomcat应用程序服务器。 （请参阅Tomcat文档。）
1. 将`[!DNL bees.war]`文件复制到Tomcat的[!DNL webapps/]文件夹中。
1. 向`https://localhost:8080/bees`发送请求。

   如果您看到“蜜蜂是可操作的”消息，则部署已成功完成。
1. 在服务器上启用SSL。

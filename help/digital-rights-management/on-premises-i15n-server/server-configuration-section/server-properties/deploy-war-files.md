---
seo-title: 部署WAR文件
title: 部署WAR文件
uuid: 435a6a6e-c981-46fb-bca9-7f5f34eecd6a
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# 部署WAR文件{#deploy-the-war-files}

1. 将WAR文件复制到Tomcat的[!DNL webapps]目录。

   * 个性化服务器：[!DNL flashaccess.war]
   * 密钥生成服务器：[!DNL flashaccess-kgs.war]

1. 将[!DNL ROOT]文件夹从Adobe提供的包复制到[!DNL webapps]目录。

   个性化服务器还需要承载[!DNL crossdomain.xml]文件。 ([!DNL ROOT]文件夹包含[!DNL crossdomain.xml]文件；[!DNL ROOT]必须位于所有大写中。) 密钥生成服务器不需要此文件。


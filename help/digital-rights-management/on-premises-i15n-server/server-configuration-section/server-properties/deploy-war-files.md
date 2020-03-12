---
seo-title: 部署WAR文件
title: 部署WAR文件
uuid: 435a6a6e-c981-46fb-bca9-7f5f34eecd6a
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 部署WAR文件{#deploy-the-war-files}

1. 将WAR文件复制到Tomcat的目 [!DNL webapps] 录。

   * 个性化服务器： [!DNL flashaccess.war]
   * 密钥生成服务器： [!DNL flashaccess-kgs.war]

1. 将Adobe [!DNL ROOT] 提供的包中的文件夹复制到目 [!DNL webapps] 录中。

   个性化服务器还需要托管该 [!DNL crossdomain.xml] 文件。 (文 [!DNL ROOT] 件夹包含文 [!DNL crossdomain.xml] 件；必 [!DNL ROOT] 须是全部大写。)密钥生成服务器不需要此文件。


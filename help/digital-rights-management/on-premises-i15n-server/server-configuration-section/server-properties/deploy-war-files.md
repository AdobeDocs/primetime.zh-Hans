---
title: 部署WAR文件
description: 部署WAR文件
copied-description: true
exl-id: 9f491596-2a02-4a55-9baa-86407e389d20
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---

# 部署WAR文件{#deploy-the-war-files}

1. 将WAR文件复制到Tomcat的 [!DNL webapps] 目录。

   * 个性化服务器： [!DNL flashaccess.war]
   * 密钥生成服务器： [!DNL flashaccess-kgs.war]

1. 复制 [!DNL ROOT] Adobe提供的包中的文件夹到 [!DNL webapps] 目录。

   个性化服务器还需要托管 [!DNL crossdomain.xml] 文件。 (此 [!DNL ROOT] 文件夹包含 [!DNL crossdomain.xml] 文件； [!DNL ROOT] 必须全部大写。) 密钥生成服务器不需要此文件。

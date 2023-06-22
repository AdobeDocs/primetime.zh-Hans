---
title: 安装Tomcat
description: 安装Tomcat
copied-description: true
exl-id: aed8fc1c-0d75-47ca-bbd4-c0934a66e284
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 安装Tomcat {#install-tomcat}

您必须在两个服务器上安装Tomcat。
1. 从安装Tomcat [!DNL \Third Party\Tomcat\6.0.18\] 目录。

   >[!NOTE]
   >
   >确保将Tomcat安装在路径中没有空格的位置。 您可以输入 `C:\Program Files\Tomcat`，但不匹配 `C:\Tomcat\`.

1. 要启动Tomcat，请输入 `TomcatInstallDir>\bin\catalina.bat run`.
1. 要验证安装，请通过输入以下命令转到Tomcat登录页面 `https://<Hostname>:8080/`.
1. 创建 `crossdomain.xml` 文件并将文件放入 `<TomcatInstallDir>\webapps\ROOT\` 目录。

   您还可以从以下位置复制文件： `https://drmtest2.adobe.com/crossdomain.xml` 目录。

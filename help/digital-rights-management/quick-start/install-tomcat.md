---
title: 安装Tomcat
description: 安装Tomcat
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 安装Tomcat {#install-tomcat}

您必须在两台服务器上安装Tomcat。
1. 从安装Tomcat [!DNL \Third Party\Tomcat\6.0.18\] 目录下。

   >[!NOTE]
   >
   >确保将Tomcat安装在路径中没有空格的位置。 您可以输入 `C:\Program Files\Tomcat`，但不匹配 `C:\Tomcat\`.

1. 要启动Tomcat，请输入 `TomcatInstallDir>\bin\catalina.bat run`.
1. 要验证安装，请转到Tomcat登陆页面，方法是输入 `https://<Hostname>:8080/`.
1. 创建 `crossdomain.xml` 文件并将文件放入 `<TomcatInstallDir>\webapps\ROOT\` 目录。

   您还可以从以下位置复制文件： `https://drmtest2.adobe.com/crossdomain.xml` 目录。

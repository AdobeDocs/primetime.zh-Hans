---
title: 安装Tomcat
description: 安装Tomcat
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# 安装Tomcat {#install-tomcat}

必须在两台服务器上安装Tomcat。
1. 从安装DVD上的 [!DNL \Third Party\Tomcat\6.0.18\] 目录安装Tomcat。

   >[!NOTE]
   >
   >确保Tomcat安装在路径中没有空格的位置。 可以输入`C:\Program Files\Tomcat`，但不能输入`C:\Tomcat\`。

1. 要开始Tomcat，请输入`TomcatInstallDir>\bin\catalina.bat run`。
1. 要验证安装，请输入`https://<Hostname>:8080/`，转到Tomcat登陆页。
1. 创建一个`crossdomain.xml`文件，并将该文件放在`<TomcatInstallDir>\webapps\ROOT\`目录中。

   还可以从`https://drmtest2.adobe.com/crossdomain.xml`目录中复制文件。

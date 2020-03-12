---
seo-title: 安装Tomcat
title: 安装Tomcat
uuid: f7663eda-ad18-4a6e-bb9f-01c74721b047
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c

---


# 安装Tomcat {#install-tomcat}

必须在两台服务器上安装Tomcat。
1. 从安装DVD上的[!DNL \Third Party\Tomcat\6.0.18\]目录安装Tomcat。

   >[!NOTE]
   >
   >确保Tomcat安装在路径中没有空格的位置。 您可以进 `C:\Program Files\Tomcat`入，但不能进 `C:\Tomcat\`入。

1. 要启动Tomcat，请输入 `TomcatInstallDir>\bin\catalina.bat run`。
1. 要验证安装，请通过输入转到Tomcat登录页 `https://<Hostname>:8080/`。
1. 创建一 `crossdomain.xml` 个文件，然后将文件放在目 `<TomcatInstallDir>\webapps\ROOT\` 录中。

   您还可以从目录中复制文 `https://drmtest2.adobe.com/crossdomain.xml` 件。

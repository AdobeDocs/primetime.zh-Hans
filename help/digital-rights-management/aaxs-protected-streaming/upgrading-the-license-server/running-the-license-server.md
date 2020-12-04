---
description: 要升级运行Adobe Access Server的受保护流服务器，请将部署在应用程序服务器上的flashaccessserver.war文件替换为最新Adobe访问中包含的文件。 如果您希望使用上述新配置选项，请更新服务器的flashaccess-tenant.xml。 您还需要将jsafe.dll或libjsafe.so更新到最新Adobe访问附带的版本。
seo-description: 要升级运行Adobe Access Server的受保护流服务器，请将部署在应用程序服务器上的flashaccessserver.war文件替换为最新Adobe访问中包含的文件。 如果您希望使用上述新配置选项，请更新服务器的flashaccess-tenant.xml。 您还需要将jsafe.dll或libjsafe.so更新到最新Adobe访问附带的版本。
seo-title: 运行Adobe Access Server以实现受保护的流
title: 运行Adobe Access Server以实现受保护的流
uuid: 3819500d-ad2f-49eb-8aa4-e50a55461608
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# 为受保护的流运行Adobe Access Server{#running-the-adobe-access-server-for-protected-streaming}

要升级运行Adobe Access Server的受保护流服务器，请将部署在应用程序服务器上的flashaccessserver.war文件替换为最新Adobe访问中包含的文件。 如果您希望使用上述新配置选项，请更新服务器的flashaccess-tenant.xml。 您还需要将jsafe.dll或libjsafe.so更新到最新Adobe访问附带的版本。

在运行受保护流的Adobe Access Server之前，Adobe建议您使用随许可证服务器提供的实用程序验证配置文件是否有效。 有关详细信息，请参阅“[配置验证程序](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)”。

要开始Tomcat和许可证服务器，请从Tomcat的bin目录运行“catalina.bat开始”或“catalina.sh开始”。

服务器启动后，请通过在浏览器窗口中打开&#x200B;*https:// license-server-host:port/flashaccessserver/tenant-name/flashaccess/license/v1*&#x200B;验证是否正确配置了该服务器。 如果租户配置成功加载，则显示确认消息。

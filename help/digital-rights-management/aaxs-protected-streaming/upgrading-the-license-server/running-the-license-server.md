---
description: 要升级运行Adobe Access Server的受保护流服务器，请将部署在应用程序服务器上的flashaccessserver.war文件替换为最新Adobe Access附带的文件。 如果要使用上述新配置选项，请更新服务器的flashaccess-tenant.xml。 您还需要将jsafe.dll或libjsafe.so更新到最新Adobe Access附带的版本。
seo-description: 要升级运行Adobe Access Server的受保护流服务器，请将部署在应用程序服务器上的flashaccessserver.war文件替换为最新Adobe Access附带的文件。 如果要使用上述新配置选项，请更新服务器的flashaccess-tenant.xml。 您还需要将jsafe.dll或libjsafe.so更新到最新Adobe Access附带的版本。
seo-title: 运行Adobe Access Server以实现受保护的流
title: 运行Adobe Access Server以实现受保护的流
uuid: 3819500d-ad2f-49eb-8aa4-e50a55461608
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 运行Adobe Access Server以实现受保护的流{#running-the-adobe-access-server-for-protected-streaming}

要升级运行Adobe Access Server的受保护流服务器，请将部署在应用程序服务器上的flashaccessserver.war文件替换为最新Adobe Access附带的文件。 如果要使用上述新配置选项，请更新服务器的flashaccess-tenant.xml。 您还需要将jsafe.dll或libjsafe.so更新到最新Adobe Access附带的版本。

在运行Adobe Access Server for Protected Streaming之前，Adobe建议您使用随许可证服务器提供的实用程序验证配置文件是否有效。 有关详细信息，请参[阅“Configuration Validator](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)”。

要启动Tomcat和许可证服务器，请从Tomcat的bin目录运行“catalina.bat start”或“catalina.sh start”。

启动服务器后，在浏览器窗口中打开https:// *license-server-host:port/flashaccessserver/tenant-name/flashaccess/license/v1* ，验证是否正确配置。 如果租户配置成功加载，则显示确认消息。

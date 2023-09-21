---
description: 要升级运行Adobe Access Server for Protected Streaming的服务器，请将应用程序服务器上部署的flashaccessserver.war文件替换为包含最新Adobe访问的文件。 如果要使用上述新配置选项，请更新服务器的flashaccess-tenant.xml。 您还需要将jsafe.dll或libjsafe.so更新到包含最新Adobe访问权限的版本。
title: 运行适用于受保护流的Adobe Access Server
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 运行适用于受保护流的Adobe Access Server{#running-the-adobe-access-server-for-protected-streaming}

要升级运行Adobe Access Server for Protected Streaming的服务器，请将应用程序服务器上部署的flashaccessserver.war文件替换为包含最新Adobe访问的文件。 如果要使用上述新配置选项，请更新服务器的flashaccess-tenant.xml。 您还需要将jsafe.dll或libjsafe.so更新到包含最新Adobe访问权限的版本。

在运行Adobe Access Server for Protected Streaming之前，Adobe建议您使用许可证服务器提供的实用程序验证配置文件是否有效。 有关更多详细信息，请参阅“[配置验证器](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)“。

要启动Tomcat和许可证服务器，请从Tomcat的bin目录中运行“catalina.bat start”或“catalina.sh start”。

服务器启动后，通过打开 *https:// license-server-host：port/flashaccessserver/tenant-name/flashaccess/license/v1* 在浏览器窗口中。 如果已成功加载租户配置，则会显示确认消息。

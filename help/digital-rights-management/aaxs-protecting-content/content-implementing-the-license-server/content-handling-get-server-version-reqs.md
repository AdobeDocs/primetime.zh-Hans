---
title: 处理Get Server版本请求
description: 处理Get Server版本请求
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 处理Get Server版本请求{#handling-get-server-version-requests}

Adobe访问客户端3.0及更高版本发送Get Server Version请求，以确定服务器的功能。 所有使用Adobe访问SDK 3.0及更高版本的服务器都必须实施对“获取服务器版本”请求的支持。

* 请求处理程序类为 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 请求URL必须是“元数据中的许可证服务器URL”+“/flashaccess/getServerVersion/v3”

对于Adobe访问SDK 4.0及更高版本，对Get Server Version请求的响应会向客户端指示，服务器支持Adobe访问协议版本3和版本4。

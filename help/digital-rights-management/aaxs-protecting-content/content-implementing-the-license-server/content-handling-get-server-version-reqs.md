---
title: 处理获取服务器版本请求
description: 处理获取服务器版本请求
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# 正在处理获取服务器版本请求{#handling-get-server-version-requests}

Adobe Access客户端3.0及更高版本会发送Get Server版本请求，以确定服务器的功能。 所有使用Adobe Access SDK 3.0及更高版本的服务器都必须实现对获取服务器版本请求的支持。

* 请求处理程序类为`com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 请求消息类为`com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 请求URL必须是“元数据中的许可证服务器URL”+“/flashaccess/getServerVersion/v3”

对于Adobe Access SDK 4.0及更高版本，对“获取服务器版本”请求的响应向客户端指示服务器支持Adobe Access协议的版本3和4。

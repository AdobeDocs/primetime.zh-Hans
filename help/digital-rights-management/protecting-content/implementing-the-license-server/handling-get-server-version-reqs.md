---
title: 处理获取服务器版本请求
description: 处理获取服务器版本请求
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 处理获取服务器版本请求{#handle-get-server-version-requests}

Adobe Primetime DRM客户端3.0或更高版本会发送“获取服务器版本”请求，以确定服务器的功能。 所有使用Primetime DRM SDK 3.0或更高版本的服务器都必须实现“获取服务器版本”请求支持。

* 请求处理程序类为`com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 请求消息类为`com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 请求URL必须是&quot;元数据中的许可证服务器URL&quot; + &quot; [!DNL /flashaccess/getServerVersion/v3]&quot;

对于Primetime DRM SDK 4.0或更高版本，对“获取服务器版本”请求的响应向客户表明服务器支持Primetime DRM协议的版本3和4。

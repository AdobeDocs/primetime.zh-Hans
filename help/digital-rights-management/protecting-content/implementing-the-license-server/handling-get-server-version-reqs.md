---
title: 处理获取服务器版本请求
description: 处理获取服务器版本请求
copied-description: true
exl-id: 86a1bbe3-2ae4-4d4e-be51-fbbeb32147c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 处理获取服务器版本请求 {#handle-get-server-version-requests}

Adobe Primetime DRM客户端3.0或更高版本发送一个Get Server Version请求，以确定服务器的功能。 所有使用Primetime DRM SDK 3.0或更高版本的服务器都必须实施对获取服务器版本请求的支持。

* 请求处理程序类为 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 请求URL必须是“元数据中的许可证服务器URL”+“ [!DNL /flashaccess/getServerVersion/v3]”

对于Primetime DRM SDK 4.0或更高版本，对Get Server Version请求的响应会向客户端指示服务器支持Primetime DRM协议版本3和4。

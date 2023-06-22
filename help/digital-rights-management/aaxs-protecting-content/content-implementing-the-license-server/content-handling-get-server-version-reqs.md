---
title: 处理Get Server版本请求
description: 处理Get Server版本请求
copied-description: true
exl-id: 125b0111-17e9-4f6f-954b-6975048cd2fa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 处理Get Server版本请求{#handling-get-server-version-requests}

Adobe访问客户端3.0及更高版本发送Get Server Version请求，以确定服务器的功能。 所有使用Adobe访问SDK 3.0及更高版本的服务器都必须实施对Get Server Version请求的支持。

* 请求处理程序类为 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 请求URL必须为“元数据中的许可证服务器URL”+“/flashaccess/getServerVersion/v3”

对于Adobe访问SDK 4.0及更高版本，对Get Server Version请求的响应会向客户端指示服务器支持Adobe访问协议版本3和版本4。

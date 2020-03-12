---
seo-title: 处理获取服务器版本请求
title: 处理获取服务器版本请求
uuid: a3084faa-cf3d-45cc-a244-298308c4cf15
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 处理获取服务器版本请求{#handling-get-server-version-requests}

Adobe Access客户端3.0及更高版本会发送Get Server版本请求，以确定服务器的功能。 所有使用Adobe Access SDK 3.0及更高版本的服务器都必须实现对获取服务器版本请求的支持。

* 请求处理函数类为 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 请求URL必须是“元数据中的许可证服务器URL” +“/flashaccess/getServerVersion/v3”

对于Adobe Access SDK 4.0及更高版本，对“获取服务器版本”请求的响应会向客户端指示服务器支持Adobe Access协议的版本3和版本4。

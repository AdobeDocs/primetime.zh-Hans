---
seo-title: 处理获取服务器版本请求
title: 处理获取服务器版本请求
uuid: 6e287f58-2ad2-428a-a76a-6847d06b0fd8
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 处理获取服务器版本请求 {#handle-get-server-version-requests}

Adobe Primetime DRM客户端3.0或更高版本会发送Get Server版本请求，以确定服务器的功能。 所有使用Primetime DRM SDK 3.0或更高版本的服务器都必须实现“获取服务器版本”请求支持。

* 请求处理函数类为 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 请求URL必须是“元数据中的许可证服务器URL”+“ [!DNL /flashaccess/getServerVersion/v3]”

对于Primetime DRM SDK 4.0或更高版本，对“获取服务器版本”请求的响应向客户指示服务器支持Primetime DRM协议的版本3和4。

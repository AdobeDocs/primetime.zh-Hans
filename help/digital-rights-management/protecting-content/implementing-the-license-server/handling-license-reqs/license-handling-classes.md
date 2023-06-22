---
title: 概述
description: 概述
copied-description: true
exl-id: 267188d0-83f8-42dc-88e3-78b52945cb6c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# 概述 {#overview}

要获取许可证，客户端从嵌入在打包内容中的元数据形成请求，然后将该请求提交到许可证服务器。 许可证服务器使用从内容元数据提取的信息来生成许可证。

如果客户端和服务器都支持协议版本5，则请求URL为“元数据中的许可证服务器URL”+ &quot; [!DNL /flashaccess/license/v4]“。 如果协议版本3是客户端或服务器支持的最大版本，则Primetime DRM客户端将身份验证请求发送到“元数据中的许可证服务器URL”+ [!DNL /flashaccess/license/v3]“。 否则，身份验证请求将发送到“元数据中的许可证服务器URL”+“ [!DNL /flashaccess/license/v1]”

一个设备可以有多个许可证用于相同内容（相同的许可证ID），但只能有一个许可证用于特定许可证ID和DRM策略ID。 如果收到具有重复LicenseID/PolicyID的许可证，则只有在新许可证的颁发日期晚于现有许可证的颁发日期时，新许可证才会替换旧许可证。 此逻辑用于处理嵌入到内容中的许可证。 因此，建议不要在一个内容块中嵌入多个具有相同DRM策略ID的许可证。 相同的逻辑适用于通过 `DRMManager.storeVoucher()` ActionScript3 API；如果客户端已拥有许可证，且许可证的颁发日期较晚，则可以忽略所提供的许可证。

## 许可证请求处理类 {#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`  — 这是许可证请求处理程序类。 它读取并解析许可证请求。 Its `getRequests()` 方法返回列表 `LicenseRequestMessage` 对象。
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`  — 这是请求消息类。 调用方应通过 `LicenseRequestMessage` 列表返回者 `getRequests()`，并为每个请求生成许可证或设置错误代码。 调用 `LicenseRequestMessage.getContentInfo()` 获取从内容元数据提取的信息，包括内容ID、许可ID和DRM策略。

许可证和错误会同时发送，如果 `LicenseHandler.close()` 方法名为。

请参阅 [DRM服务器API参考文档](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html) 了解详细信息。

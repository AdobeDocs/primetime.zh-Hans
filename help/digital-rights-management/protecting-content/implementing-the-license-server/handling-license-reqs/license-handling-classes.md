---
title: 概述
description: 概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# 概述{#overview}

要获取许可证，客户端从打包内容中嵌入的元数据中生成请求，然后将该请求提交到许可证服务器。 许可证服务器使用从内容元数据中提取的信息来生成许可证。

如果客户端和服务器都支持协议版本5，则请求URL为“元数据中的许可证服务器URL”+“ [!DNL /flashaccess/license/v4]”。 如果客户端或服务器支持的协议版本3是最大版本，则Primetime DRM客户端会向“元数据中的许可证服务器URL”+“ [!DNL /flashaccess/license/v3]”发送身份验证请求。 否则，身份验证请求将发送到“元数据中的许可证服务器URL”+“ [!DNL /flashaccess/license/v1]”

设备可能具有同一内容的多个许可证（同一许可证ID），但对于特定许可证ID和DRM策略ID只能具有一个许可证。 如果它收到具有重复LicenseID/PolicyID的许可证，则只有新许可证的发布日期晚于现有许可证的发布日期，新许可证才会替换旧许可证。 此逻辑用于处理嵌入到内容中的许可证。 因此，不建议在内容块中嵌入多个具有相同DRM策略ID的许可证。 同样的逻辑适用于通过`DRMManager.storeVoucher()` ActionScript3 API传递给客户端的许可证；如果客户端已经拥有一个许可证，并且该许可证的发布日期在以后，则可能会忽略提供的许可证。

## 许可证请求处理类{#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`  — 这是许可证请求处理程序类。它读取并解析许可证请求。 其`getRequests()`方法返回`LicenseRequestMessage`对象的列表。
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`  — 这是请求消息类。调用方应遍历由`getRequests()`返回的`LicenseRequestMessage`列表，并为每个请求生成许可证或设置错误代码。 调用`LicenseRequestMessage.getContentInfo()`以获取从内容元数据中提取的信息，包括内容ID、许可证ID和DRM策略。

调用`LicenseHandler.close()`方法时，将同时发送许可证和错误。

有关详细信息，请参阅[DRM服务器API参考文档](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html)。

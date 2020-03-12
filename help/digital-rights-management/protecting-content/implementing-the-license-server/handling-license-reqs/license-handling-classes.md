---
seo-title: 概述
title: 概述
uuid: 2bbf0aa1-df35-429d-84df-db357fa53e47
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 概述 {#overview}

要获得许可证，客户端从嵌入在打包内容中的元数据中提出请求，然后将该请求提交到许可证服务器。 许可证服务器使用从内容元数据中提取的信息来生成许可证。

如果客户端和服务器都支持协议版本5，则请求URL为“元数据中的许可证服务器URL”+“ [!DNL /flashaccess/license/v4]”。 如果协议版本3是客户端或服务器支持的最大版本，则Primetime DRM客户端会向“元数据中的许可证服务器URL”+“”发送身份验证请 [!DNL /flashaccess/license/v3]求。 否则，身份验证请求将发送到“元数据中的许可证服务器URL”+“ [!DNL /flashaccess/license/v1]”

设备可能具有同一内容的多个许可证（同一许可证ID），但特定许可证ID和DRM策略ID只能有一个许可证。 如果收到的许可证具有重复的LicenseID/PolicyID，则新许可证将替换旧许可证，但前提是新许可证的发布日期晚于现有许可证的发布日期。 此逻辑用于处理嵌入到内容中的许可证。 因此，不建议在内容块中嵌入多个具有相同DRM策略ID的许可证。 同样的逻辑适用于通过 `DRMManager.storeVoucher()` ActionScript3 API传递给客户端的许可证；如果客户端已经拥有稍后发布日期的许可证，则可能会忽略提供的许可证。

## 许可证请求处理类 {#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler` -这是许可证请求处理程序类。 它读取并解析许可证请求。 其方 `getRequests()` 法返回对象列 `LicenseRequestMessage` 表。
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage` -这是请求消息类。 调用者应遍历由返回 `LicenseRequestMessage` 的列表 `getRequests()`，并且对于每个请求都应生成许可证或设置错误代码。 调 `LicenseRequestMessage.getContentInfo()` 用以获取从内容元数据中提取的信息，包括内容ID、许可证ID和DRM策略。

调用方法时，会同时发送许 `LicenseHandler.close()` 可证和错误。

有关详细信息， [请参阅DRM Server API参考文档](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html) 。

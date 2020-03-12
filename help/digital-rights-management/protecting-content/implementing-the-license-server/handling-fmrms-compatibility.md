---
description: 处理FMRMS兼容性
seo-description: 处理FMRMS兼容性
seo-title: 升级客户端
title: 升级客户端
uuid: c32ee087-2edf-4d11-be36-e2b31f3769de
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 处理FMRMS兼容性 {#handling-fmrms-compatibility}

有两种类型的请求与Flash Media Rights Management Server 1.x兼容性相关。 一种请求类型用于提示1.x客户端升级到支持Adobe Primetime DRM 2.0或更高版本的运行时。 另一个用于在请求许可证之前将1.x元数据更新为Primetime DRM格式。 仅当您之前部署了使用FMRMS 1.0或1.5的任何内容时，才需要支持这些请求。

## 升级客户端 {#upgrading-clients}

如果FMRMS 1.x客户端与Adobe Primetime DRM服务器联系，则服务器需要提示客户端进行升级。

* 请求处理程序类是 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`。
* 请求URL为“*1.x内容的基本URL*” + &quot; [!DNL /edcws/services/urn:EDCLicenseService]&quot;

   与其他Adobe Primetime请求处理程序不同，此处理程序不提供对任何请求信息的访问，也不要求设置任何响应数据。 创建实例 `FMRMSv1RequestHandler`，然后调用 `close()`

## 升级元数据 {#upgrading-metadata}

如果Adobe Access客户端遇到与Flash Media Rights Management Server 1.x打包的内容，它将从内容中提取加密元数据并将其发送到服务器。 服务器将FMRMS 1.x元数据转换为Adobe Access格式，并将其发送回客户端。 然后，客户端在标准Adobe Access许可证请求中发送更新的元数据。

* 请求处理程序类是 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`。
* 请求URL是“*1.x内容的基本URL*” +&quot;/flashaccess/headerconversion/v1&quot;。

当服务器从客户端接收旧元数据时，可以立即执行元数据转换。 或者，服务器可以对旧内容进行预处理，并存储转换后的元数据；在这种情况下，当客户端请求新元数据时，服务器只需获取与旧元数据的许可证标识符相匹配的新元数据。

要转换元数据，服务器必须执行以下步骤：

* 获取 `LiveCycleKeyMetaData`。 要预转换元数据，可 `LiveCycleKeyMetaData` 以使用从1.x打包文件获取元数据 `MediaEncrypter.examineEncryptedContent()`。 元数据也包含在元数据转换请求( `FMRMSv1MetadataHandler.getOriginalMetadata()`)中。
* 从旧的元数据中获取许可证标识符，并找到加密密钥和策略（这些信息最初位于Adobe LiveCycle ES数据库中）。 LiveCycle ES策略必须转换为Adobe Access 2.0策略。)参考实施包括用于转换策略和从LiveCycle ES导出许可证信息的脚本和示例代码。
* 填充对 `V2KeyParameters` 象(可通过调用检索 `MediaEncrypter.getKeyParameters()`)。
* 加载 `SigningCredential`Adobe用于签署加密元数据的打包程序凭据。 通过调 `SignatureParameters` 用并填写签 `MediaEncrypter.getSignatureParameters()` 名凭证来获取对象。
* 调用 `MetaDataConverter.convertMetadata()` 以获取 `V2ContentMetaData`。
* 呼叫 `V2ContentMetaData.getBytes()` 和商店供将来使用，或呼叫 `FMRMSv1MetadataHandler.setUpdatedMetadata()`。
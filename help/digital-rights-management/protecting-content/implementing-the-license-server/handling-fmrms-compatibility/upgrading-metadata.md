---
seo-title: 升级元数据
title: 升级元数据
uuid: 769483e6-a2d1-46cb-afcf-557aa807037c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 升级元数据{#upgrading-metadata}

如果Adobe Primetime DRM客户端遇到与Flash Media Rights Management Server 1.x打包的内容，则会从内容中提取加密元数据并将其发送到服务器。 然后，服务器将FMRMS 1.x元数据转换为Primetime DRM格式，并将其发送到客户端。 然后，客户端在标准Primetime DRM许可证请求中发送更新的元数据。

* 请求处理程序类是 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`。
* 请求URL是“*1.x内容的基本URL*” +” [!DNL /flashaccess/headerconversion/v1]。

当服务器从客户端接收旧元数据时，可以立即执行元数据转换。 或者，服务器可以对旧内容进行预处理，并存储转换后的元数据；在这种情况下，当客户端请求新元数据时，服务器只需获取与旧元数据的许可证标识符相匹配的新元数据。

要转换元数据，服务器必须执行以下步骤：

* 获取 `LiveCycleKeyMetaData`。 要预转换元数据，可 `LiveCycleKeyMetaData` 以使用从1.x打包文件获取元数据 `MediaEncrypter.examineEncryptedContent()`。 元数据也包含在元数据转换请求( `FMRMSv1MetadataHandler.getOriginalMetadata()`)中。

* 从旧元数据中获取许可证标识符，并找到加密密钥和DRM策略（这些信息最初位于Adobe LiveCycle ES数据库中）。 LiveCycle ES DRM策略必须转换为Primetime DRM 2.0 DRM策略。)参考实施包括用于转换DRM策略和从LiveCycle ES导出许可证信息的脚本和示例代码。
* 填充对 `V2KeyParameters` 象(可通过调用检索 `MediaEncrypter.getKeyParameters()`)。

* 加载 `SigningCredential`Adobe用于签署加密元数据的打包程序凭据。 通过调 `SignatureParameters` 用并填写签 `MediaEncrypter.getSignatureParameters()` 名凭证来获取对象。

* 调用 `MetaDataConverter.convertMetadata()` 以获取 `V2ContentMetaData`。

* 呼叫 `V2ContentMetaData.getBytes()` 和商店供将来使用，或呼叫 `FMRMSv1MetadataHandler.setUpdatedMetadata()`。


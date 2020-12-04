---
seo-title: 升级元数据
title: 升级元数据
uuid: 769483e6-a2d1-46cb-afcf-557aa807037c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# 升级元数据{#upgrading-metadata}

如果Adobe PrimetimeDRM客户端遇到与Flash媒体Rights Management服务器1.x打包的内容，则会从该内容中提取加密元数据并将其发送到服务器。 然后，服务器将FMRMS 1.x元数据转换为Primetime DRM格式，并将其发送给客户端。 然后，客户端在标准Primetime DRM许可证请求中发送更新的元数据。

* 请求处理函数类为`com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`。
* 请求URL为&quot;*来自1.x内容*&quot; +&quot; [!DNL /flashaccess/headerconversion/v1]的基本URL&quot;。

当服务器从客户端接收旧元数据时，可以立即进行元数据转换。 或者，服务器可以对旧内容进行预处理并存储转换后的元数据；在这种情况下，当客户端请求新元数据时，服务器只需获取与旧元数据的许可证标识符匹配的新元数据。

要转换元数据，服务器必须执行以下步骤：

* 获取`LiveCycleKeyMetaData`。 要预转换元数据，可以使用`MediaEncrypter.examineEncryptedContent()`从1.x打包文件中获取`LiveCycleKeyMetaData`。 元数据也包含在元数据转换请求中(`FMRMSv1MetadataHandler.getOriginalMetadata()`)。

* 从旧的元数据中获取许可证标识符，并查找加密密钥和DRM策略(此信息最初位于AdobeLiveCycleES数据库中。 LiveCycleES DRM策略必须转换为Primetime DRM 2.0 DRM策略。) 参考实施包括用于转换DRM策略和从LiveCycleES导出许可证信息的脚本和示例代码。
* 填写`V2KeyParameters`对象（通过调用`MediaEncrypter.getKeyParameters()`来检索该对象）。

* 加载`SigningCredential`，它是由用于签署加密元数据的Adobe颁发的打包程序凭据。 通过调用`MediaEncrypter.getSignatureParameters()`获取`SignatureParameters`对象并填写签名凭据。

* 调用`MetaDataConverter.convertMetadata()`获取`V2ContentMetaData`。

* 调用`V2ContentMetaData.getBytes()`并存储以供将来使用，或调用`FMRMSv1MetadataHandler.setUpdatedMetadata()`。


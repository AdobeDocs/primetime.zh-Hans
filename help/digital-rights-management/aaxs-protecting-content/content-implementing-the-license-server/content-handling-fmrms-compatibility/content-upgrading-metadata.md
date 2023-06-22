---
title: 升级元数据
description: 升级元数据
copied-description: true
exl-id: 04b3fb22-489e-41bb-95d0-99375f92fbae
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# 升级元数据{#upgrading-metadata}

如果Adobe访问客户端遇到与FlashMediaRights Management服务器1.x打包的内容，它将从内容中提取加密元数据并将其发送到服务器。 服务器会将FMRMS 1.x元数据转换为Adobe访问格式，并将其发送回客户端。 然后，客户端在标准Adobe访问许可证请求中发送更新的元数据。

* 请求处理程序类为 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* 请求URL为&#39;&#39;*来自1.x内容的基本URL*“ +”/flashaccess/headerconversion/v1”。

当服务器从客户端接收旧元数据时，可以动态完成元数据转换。 或者，服务器可以预处理旧内容并存储转换后的元数据；在这种情况下，当客户端请求新元数据时，服务器只需要获取与旧元数据的许可证标识符匹配的新元数据。

要转换元数据，服务器必须执行以下步骤：

* Get `LiveCycleKeyMetaData`. 要预转换元数据，请执行以下操作 `LiveCycleKeyMetaData` 可从1.x打包文件中获取，使用 `MediaEncrypter.examineEncryptedContent()`. 元数据也包含在元数据转换请求中( `FMRMSv1MetadataHandler.getOriginalMetadata()`)。
* 从旧元数据中获取许可证标识符，并查找加密密钥和策略(此信息最初位于AdobeLiveCycleES数据库中)。 LiveCycleES策略必须转换为Adobe访问2.0策略。) 参考实施包括用于转换策略和从LiveCycleES导出许可证信息的脚本和示例代码。
* 填写 `V2KeyParameters` 对象（通过调用检索对象） `MediaEncrypter.getKeyParameters()`)。
* 加载 `SigningCredential`，这是由用于对加密元数据签名的Adobe颁发的打包员凭据。 获取 `SignatureParameters` 对象（通过调用） `MediaEncrypter.getSignatureParameters()` 并填写签名凭据。
* 调用 `MetaDataConverter.convertMetadata()` 以获取 `V2ContentMetaData`.
* 调用 `V2ContentMetaData.getBytes()` 并存储以供将来使用，或调用 `FMRMSv1MetadataHandler.setUpdatedMetadata()`.

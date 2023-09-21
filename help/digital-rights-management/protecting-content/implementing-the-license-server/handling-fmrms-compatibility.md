---
description: 处理FMRMS兼容性
title: 升级客户端
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# 处理FMRMS兼容性 {#handling-fmrms-compatibility}

有两种类型的请求与Flash MediaRights Management服务器1.x兼容性相关。 有一种类型的请求用于提示1.x客户端升级到支持Adobe Primetime DRM 2.0或更高版本的运行时。 另一个用于在请求许可证之前将1.x元数据更新为Primetime DRM格式。 仅当您之前部署了使用FMRMS 1.0或1.5的任何内容时，才需要支持这些请求。

## 升级客户端 {#upgrading-clients}

如果FMRMS 1.x客户端与Adobe Primetime DRM服务器联系，则服务器需要提示客户端进行升级。

* 请求处理程序类为 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* 请求URL为&#39;&#39;*来自1.x内容的基本URL*“ + ” [!DNL /edcws/services/urn:EDCLicenseService]&quot;

  与其他Adobe Primetime请求处理程序不同，此处理程序不提供对任何请求信息的访问权限，也不要求设置任何响应数据。 创建实例 `FMRMSv1RequestHandler`，然后调用 `close()`

## 升级元数据 {#upgrading-metadata}

如果Adobe访问客户端遇到与FlashMediaRights Management服务器1.x打包的内容，它将从内容中提取加密元数据并将其发送到服务器。 服务器会将FMRMS 1.x元数据转换为Adobe访问格式，并将其发送回客户端。 然后，客户端在标准Adobe访问许可证请求中发送更新的元数据。

* 请求处理程序类为 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* 请求URL为&#39;&#39;*来自1.x内容的基本URL*“ +”/flashaccess/headerconversion/v1”。

当服务器从客户端接收旧元数据时，可以动态完成元数据转换。 或者，服务器可以预处理旧内容并存储转换后的元数据；在这种情况下，当客户端请求新元数据时，服务器只需要获取与旧元数据的许可证标识符匹配的新元数据。

要转换元数据，服务器必须执行以下步骤：

* Get `LiveCycleKeyMetaData`. 要预转换元数据，请执行以下操作 `LiveCycleKeyMetaData` 可从1.x打包文件中获取，使用 `MediaEncrypter.examineEncryptedContent()`. 元数据也包含在元数据转换请求中( `FMRMSv1MetadataHandler.getOriginalMetadata()`)。
* 从旧元数据中获取许可证标识符，并查找加密密钥和策略(此信息最初位于AdobeLiveCycleES数据库中)。 LiveCycleES策略必须转换为AdobeAccess 2.0策略。) 参考实现包括用于转换策略和从LiveCycleES导出许可证信息的脚本和示例代码。
* 填写 `V2KeyParameters` 对象(通过调用 `MediaEncrypter.getKeyParameters()`)。
* 加载 `SigningCredential`，这是由Adobe颁发的用于签署加密元数据的打包程序凭据。 获取 `SignatureParameters` 通过调用对象 `MediaEncrypter.getSignatureParameters()` 并填写签名凭据。
* 调用 `MetaDataConverter.convertMetadata()` 以获取 `V2ContentMetaData`.
* 调用 `V2ContentMetaData.getBytes()` 并存储以供将来使用，或调用 `FMRMSv1MetadataHandler.setUpdatedMetadata()`.

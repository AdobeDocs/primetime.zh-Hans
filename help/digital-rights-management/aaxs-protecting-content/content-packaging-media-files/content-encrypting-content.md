---
title: 加密内容
description: 加密内容
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# 加密内容{#encrypting-content}

加密FLV和F4V内容涉及使用 `MediaEncrypter` 对象。 您还可以打包仅包含音频轨道的FLV和F4V文件。 在为低端设备加密H.264内容时，可以只应用部分加密以提高性能。 在这种情况下，可以使用部分加密F4V文件 `F4VDRMParameters.setVideoEncryptionLevel`方法。

要使用Java API加密FLV或F4V文件，请执行以下步骤：

1. 设置开发环境，并将设置开发环境中所述的所有JAR文件包含在项目中。
1. 创建 `ServerCredential` 用于加载签名所需的凭据的实例。
1. 创建 `MediaEncrypter` 实例。 使用 `MediaEncryperFactory` 如果您不知道您拥有的文件类型， 否则，您可以创建 `FLVEncrypter` 或 `F4VEncrypter` 直接。
1. 使用 `DRMParameters` 对象。
1. 使用设置签名选项 `SignatureParameters` 对象并传递 `ServerCredential` 实例到其 `setServerCredentials` 方法。
1. 使用设置密钥和许可证信息 `V2KeyParameters` 对象。 使用设置策略 `setPolicies` 方法。 通过调用 `setLicenseServerUrl` 和 `setLicenseServerTransportCertificate` 方法。 使用设置CEK加密选项 `setKeyProtectionOptions` 方法，以及使用 `setCustomProperties` 方法。 最后，根据使用的加密类型，强制转换 `DRMKeyParameters` 对象到以下对象之一 `VideoDRMParameters`， `AudioDRMParameters`， `FLVDRMParameters`，或 `F4VDRMParameters`，并设置加密选项。
1. 通过将输入和输出文件以及加密选项传递到 `MediaEncrypter.encryptContent` 方法。

有关演示如何加密内容的示例代码，请参阅 `com.adobe.flashaccess.samples.mediapackager.EncryptContent` 在参考实施命令行工具“samples”目录中。

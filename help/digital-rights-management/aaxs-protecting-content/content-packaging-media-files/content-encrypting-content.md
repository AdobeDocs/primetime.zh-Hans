---
seo-title: 加密内容
title: 加密内容
uuid: ea71154e-557b-447e-bc14-208232f00be1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 加密内容{#encrypting-content}

加密FLV和F4V内容涉及对象的使 `MediaEncrypter` 用。 还可以打包仅包含音轨的FLV和F4V文件。 在为低端设备加密H.264内容时，仅应用部分加密可以提高性能。 在这种情况下，可以使用该方法部分地加密F4V `F4VDRMParameters.setVideoEncryptionLevel`文件。

要使用Java API加密FLV或F4V文件，请执行以下步骤：

1. 设置开发环境并包含项目中设置开发环境中提到的所有JAR文件。
1. 创建一 `ServerCredential` 个实例以加载签名所需的凭据。
1. 创建实 `MediaEncrypter` 例。 如果 `MediaEncryperFactory` 您不知道您拥有的文件类型，请使用。 否则，您可以创建或 `FLVEncrypter` 直接 `F4VEncrypter` 创建。
1. 使用对象指定加密选 `DRMParameters` 项。
1. 使用对象设置签名选 `SignatureParameters` 项，并将实 `ServerCredential` 例传递给其方 `setServerCredentials` 法。
1. 使用对象设置密钥和许可证 `V2KeyParameters` 信息。 使用方法设置策 `setPolicies` 略。 通过调用和方法设置客户端联系许可证服务器所需 `setLicenseServerUrl` 的信 `setLicenseServerTransportCertificate` 息。 使用方法设置CEK加密选 `setKeyProtectionOptions` 项，使用方法设置其自定义 `setCustomProperties` 属性。 最后，根据所使用的加密类型，将对象转 `DRMKeyParameters` 换为一个、、、 `VideoDRMParameters`或 `AudioDRMParameters``FLVDRMParameters``F4VDRMParameters`，并设置加密选项。
1. 通过将输入和输出文件以及加密选项传递给方法来加密 `MediaEncrypter.encryptContent` 内容。

有关演示如何加密内容的示例代码，请参 `com.adobe.flashaccess.samples.mediapackager.EncryptContent` 阅Reference Implementation命令行工具“samples”目录。

---
seo-title: 加密内容
title: 加密内容
uuid: 03f33473-bcd4-4e06-a823-e944897cb28e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 加密内容{#encrypting-content}

您使用对象加密视频 `MediaEncrypter` 内容。 可以加密仅包含音轨的媒体文件。 您还可以仅应用部分加密；例如，在为低端设备加密H.264内容时，要提高性能。

要使用Java API加密媒体文件，请执行以下操作：

1. 设置开发环境，并将“设置开发环境”中提 *及的所有JAR文件包含在项目中* 。
1. 创建一 `ServerCredential` 个实例以加载签名所需的凭据。
1. 创建实 `MediaEncrypter` 例。 如果 `MediaEncryperFactory` 您不知道您拥有的文件类型，请使用。

1. 使用对象指定加密选 `DRMParameters` 项。
1. 使用对象设置签名选 `SignatureParameters` 项，并将实 `ServerCredential` 例传递给其方 `setServerCredentials` 法。

1. 使用对象设置密钥和许可证 `V2KeyParameters` 信息。 使用方法设置DRM策 `setPolicies` 略。 通过调用和方法设置客户端联系许可证服务器所需 `setLicenseServerUrl` 的信 `setLicenseServerTransportCertificate` 息。 使用方法设置CEK加密选 `setKeyProtectionOptions` 项，使用方法设置其自定义 `setCustomProperties` 属性。 最后，根据所使用的加密类型，将对 `DRMKeyParameters` 象转换为相应的类型( `VideoDRMParameters`, `AudioDRMParameters`)并设置加密选项。

1. 通过将输入和输出文件以及加密选项传递给方法来加密 `MediaEncrypter.encryptContent` 内容。

有关显示如何加密内容的示例代码，请参 `com.adobe.flashaccess.samples.mediapackager.EncryptContent` 阅Reference Implementation Command Line Tools目录中的 [!DNL samples/] 代码。

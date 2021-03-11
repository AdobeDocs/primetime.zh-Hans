---
title: 加密内容
description: 加密内容
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# 正在加密内容{#encrypting-content}

加密FLV和F4V内容涉及使用`MediaEncrypter`对象。 还可以打包仅包含音轨的FLV和F4V文件。 在为下端设备加密H.264内容时，仅应用部分加密可以提高性能。 在这种情况下，可以使用`F4VDRMParameters.setVideoEncryptionLevel`方法部分加密F4V文件。

要使用Java API加密FLV或F4V文件，请执行以下步骤：

1. 设置开发环境，并包含项目中设置开发环境中提到的所有JAR文件。
1. 创建一个`ServerCredential`实例以加载签名所需的凭据。
1. 创建`MediaEncrypter`实例。 如果您不知道您拥有的文件类型，请使用`MediaEncryperFactory`。 否则，您可以直接创建`FLVEncrypter`或`F4VEncrypter`。
1. 使用`DRMParameters`对象指定加密选项。
1. 使用`SignatureParameters`对象设置签名选项，并将`ServerCredential`实例传递给其`setServerCredentials`方法。
1. 使用`V2KeyParameters`对象设置密钥和许可证信息。 使用`setPolicies`方法设置策略。 通过调用`setLicenseServerUrl`和`setLicenseServerTransportCertificate`方法，设置客户端联系许可证服务器所需的信息。 使用`setKeyProtectionOptions`方法设置CEK加密选项，使用`setCustomProperties`方法设置其自定义属性。 最后，根据所使用的加密类型，将`DRMKeyParameters`对象转换为`VideoDRMParameters`、`AudioDRMParameters`、`FLVDRMParameters`或`F4VDRMParameters`中的一个对象，并设置加密选项。
1. 通过将输入和输出文件以及加密选项传递到`MediaEncrypter.encryptContent`方法来加密内容。

有关说明如何加密内容的示例代码，请参阅Reference Implementation Command Line Tools &quot;samples&quot;目录中的`com.adobe.flashaccess.samples.mediapackager.EncryptContent`。

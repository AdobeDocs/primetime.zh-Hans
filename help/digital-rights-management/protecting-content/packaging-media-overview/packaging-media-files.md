---
title: 打包媒体文件概述
description: 打包媒体文件概述
copied-description: true
exl-id: 88c593a7-33b5-4773-b283-2ab16f9e8c3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---

# 概述 {#packaging-media-files-overview}

打包是指将DRM策略加密并应用于视频内容的过程。 您可以使用媒体打包API来打包文件。 Primetime DRM Java SDK只能打包渐进式下载内容，如MP4。

>[!NOTE]
>
>请务必联系Primetime DRM代表，了解如何为您的媒体格式和用例选择最合适的打包选项。

封装从许可证服务器分离。 打包程序无需连接到许可证服务器来交换任何有关内容的信息。 许可证服务器颁发许可证所需了解的所有信息都包含在内容元数据中。

文件加密后，如果没有适当的许可证，将无法解析其内容。 可以使用Primetime DRM选择要加密的文件部分。 由于Primetime DRM可以解析视频内容的文件格式，因此它可以智能地加密文件的选择性部分，而不是整个文件。 数据（如元数据和提示点）可以保持未加密状态，以便搜索引擎仍可以搜索文件。

一个指定的内容可以有多个DRM策略。 例如，您可以根据不同的业务模型许可内容，而无需多次打包内容。 此外，您可以允许短期匿名访问，然后允许客户购买内容以获得无限的访问权限。 如果内容是使用多个DRM策略打包的，则许可证服务器必须实施逻辑来选择必须使用哪个DRM策略来颁发许可证。

>[!NOTE]
>
>该体系结构允许当内容被打包时指定使用DRM策略并将其绑定到内容。 在客户端可以播放内容之前，客户端必须获取指定计算机的许可证。 许可证指定了强制使用的使用规则，并提供了解密内容时必须使用的密钥。 DRM策略表示用于生成许可证的模板。 但是，当许可证服务器发出许可证时，它可能会覆盖使用规则。 许可证可能会因此类约束（如过期时间或播放窗口）而呈现无效。

Primetime DRM提供了一个用于在CEK中传递的API。 如果未指定CEK，则SDK会随机生成它。 通常，内容的每个部分都需要不同的CEK。 但是，在Dynamic Streaming中，您可能会对构成该内容的所有文件使用相同的CEK。 因此，用户只需要一个许可证就可以从一个比特率无缝地转换到另一个比特率。 如果要为多个内容段使用相同的密钥和许可证，则需要传递相同的 `DRMParameters` 对象对象 `MediaEncrypter.encryptContent()`，或使用在CEK中传递 `V2KeyParameters.setContentEncryptionKey()`. 如果要为内容的每个部分使用不同的密钥和许可证，则需要创建一个新的 `DRMParameters` 每个文件的实例。

使用密钥轮换打包内容时，您可以控制使用的轮换密钥以及密钥更改的频率。 `F4VDRMParameters` 和 `FLVDRMParameters` 实施 `KeyRotationParameters` 界面。 通过此界面，您可以启用密钥轮换。 您还需要指定 `RotatingContentEncryptionKeyProvider`. 对于每个加密的示例，此类确定要使用的轮换密钥。 您可以实施自己的提供商，也可以使用 `TimeBasedKeyProvider` 包含在SDK中。 此实施会在指定的秒数后随机生成新密钥。

在某些情况下，您可能需要将内容元数据存储为单独的文件，并使其可供客户端使用而不依赖于内容。 在这种情况下，您需要调用 `MediaEncrypter.encryptContent()`，返回 `MediaEncrypterResult` 对象。 调用 `MediaEncrypterResult.getKeyInfo()` 并将结果转换为 `V2KeyStatus`. 然后，检索内容元数据并将其存储在文件中。

所有这些任务都可以使用Java API来完成。

参见 *Adobe Primetime DRM API参考* 以了解有关Java API的详细信息。

参见 *使用Adobe Primetime DRM参考实施* 有关Media Packager参考实施的信息。

---
seo-title: 打包媒体文件概述
title: 打包媒体文件概述
uuid: 9509bcdc-ee4d-4025-9bb6-9b8ac439b926
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---


# 概述 {#packaging-media-files-overview}

打包是指对视频内容加密和应用DRM策略的过程。 您可以使用媒体打包API打包文件。 Primetime DRM Java SDK只能打包渐进式下载的内容，如MP4。

>[!NOTE]
>
>请务必联系您的Primetime DRM代表，了解如何为您的媒体格式和使用案例选择最合适的打包选项。

打包从许可证服务器中解除耦合。 包装程序无需连接到许可证服务器来交换有关内容的任何信息。 内容元数据包含许可证服务器发布许可证所需了解的一切。

加密文件后，如果没有相应的许可证，则无法分析其内容。 您可以使用Primetime DRM选择要加密的文件部分。 由于Primetime DRM可以解析视频内容的文件格式，因此它可以智能加密文件的选择性部分而不是整个文件。 数据（如元数据和提示点）可保持未加密状态，以便搜索引擎仍可搜索文件。

指定的内容片段可能具有多个DRM策略。 例如，您可以在不同业务模式下许可内容，而无需多次打包内容。 此外，您还可以在短时间内允许匿名访问，然后允许客户购买内容以拥有无限访问权限。 如果内容是通过使用多个DRM策略进行打包的，则许可证服务器必须实现逻辑，用于选择必须使用哪个DRM策略才能颁发许可证。

>[!NOTE]
>
>该体系结构允许在打包内容时指定使用DRM策略并将其绑定到内容。 在客户端可以播放内容之前，客户端必须获得指定计算机的许可证。 该许可证指定实施的使用规则，并提供必须用于解密内容的密钥。 DRM策略表示用于生成许可证的模板。 但是，许可证服务器在发出许可证时可能会覆盖使用规则。 许可证可能因此类限制（如过期时间或播放窗口）而变得无效。

Primetime DRM为在CEK中传递提供API。 如果未指定CEK，则SDK会随机生成它。 通常，您需要为每个内容部分提供不同的CEK。 但是，在动态流中，您可能对构成该内容的所有文件使用相同的CEK。 因此，用户只需一个许可证即可从一个比特率无缝过渡到另一个比特率。 如果要对多个内容使用相同的密钥和许可证，您需要将同一对象传递 `DRMParameters` 给 `MediaEncrypter.encryptContent()`，或使用传入CEK `V2KeyParameters.setContentEncryptionKey()`。 如果要对每个内容部分使用不同的密钥和许可证，您需要为每个文件创建 `DRMParameters` 一个新实例。

使用键旋转打包内容时，您可以控制使用的旋转键以及键更改的频率。 `F4VDRMParameters` 并实 `FLVDRMParameters` 现接 `KeyRotationParameters` 口。 通过此界面，您可以启用密钥旋转。 您还需要指定 `RotatingContentEncryptionKeyProvider`。 对于每个已加密的样本，此类确定要使用的旋转密钥。 您可以实施自己的提供商，或使 `TimeBasedKeyProvider` 用SDK附带的。 此实现在指定的秒数后随机生成新密钥。

在某些情况下，您可能需要将内容元数据存储为单独的文件，并使其与内容分开地提供给客户端。 在这种情况下，您需要调 `MediaEncrypter.encryptContent()`用，它返回一 `MediaEncrypterResult` 个对象。 调 `MediaEncrypterResult.getKeyInfo()` 用结果并将其转换为 `V2KeyStatus`。 然后检索内容元数据并将其存储在文件中。

所有这些任务都可以通过Java API实现。

有 *关Java API的详细信息* ，请参阅Adobe PrimetimeDRM API参考。

有 *关Media Packager参考实现的信息* ，请参阅使用Adobe PrimetimeDRM参考实现。

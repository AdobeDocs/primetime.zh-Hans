---
title: 打包媒体文件概述
description: 打包媒体文件概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---


# 概述{#packaging-media-files-overview}

打包是指对视频内容加密和应用DRM策略的过程。 您可以使用媒体打包API打包文件。 Primetime DRM Java SDK只能打包渐进式下载的内容，如MP4。

>[!NOTE]
>
>请务必联系您的Primetime DRM代表，了解如何为您的媒体格式和使用案例选择最合适的打包选项。

打包从许可证服务器中解耦。 包装程序无需连接到许可证服务器来交换有关内容的任何信息。 内容元数据包含许可证服务器发布许可证所需的一切信息。

加密文件后，如果没有相应的许可证，则无法分析其内容。 您可以使用Primetime DRM选择要加密的文件部分。 由于Primetime DRM可以分析视频内容的文件格式，因此它可以智能加密文件的选择性部分而不是整个文件。 数据（如元数据和提示点）可以保持未加密状态，以便搜索引擎仍可以搜索文件。

指定的内容片段可能有多个DRM策略。 例如，您可以在不同业务模式下许可内容，而无需多次打包内容。 此外，您还可以在短时间内允许匿名访问，然后允许客户购买内容以拥有无限的访问权限。 如果使用多个DRM策略对内容进行打包，则许可证服务器必须实现逻辑，用于选择必须使用哪个DRM策略才能颁发许可证。

>[!NOTE]
>
>该体系结构允许在打包内容时指定使用DRM策略并将其绑定到内容。 在客户端可以播放内容之前，客户端必须获得指定计算机的许可证。 许可证指定强制使用的使用规则，并提供必须用于解密内容的密钥。 DRM策略表示用于生成许可证的模板。 但是，许可证服务器在发布许可证时可能会覆盖使用规则。 许可证可能会因此类限制（如过期时间或播放窗口）而变得无效。

Primetime DRM为传递CEK提供API。 如果未指定CEK，则SDK会随机生成它。 通常，您需要为每个内容部分使用不同的CEK。 但是，在动态流中，您可能会对构成该内容的所有文件使用相同的CEK。 因此，用户只需一个许可证即可将一个比特率无缝地过渡到另一个比特率。 如果要对多个内容使用相同的密钥和许可证，您需要将相同的`DRMParameters`对象传递给`MediaEncrypter.encryptContent()`，或使用`V2KeyParameters.setContentEncryptionKey()`传入CEK。 如果要对内容的每个部分使用不同的密钥和许可证，则需要为每个文件创建一个新的`DRMParameters`实例。

使用键旋转打包内容时，您可以控制使用的旋转键以及键更改的频率。 `F4VDRMParameters` 并 `FLVDRMParameters` 实现 `KeyRotationParameters` 接口。通过此界面，您可以启用键旋转。 您还需要指定`RotatingContentEncryptionKeyProvider`。 对于加密的每个样本，此类确定要使用的旋转密钥。 您可以实施自己的提供程序，或使用SDK附带的`TimeBasedKeyProvider`。 此实现在指定秒数后随机生成新密钥。

在某些情况下，您可能需要将内容元数据存储为单独的文件，并使其与内容分开提供给客户端。 在这种情况下，您需要调用`MediaEncrypter.encryptContent()`，它返回一个`MediaEncrypterResult`对象。 调用`MediaEncrypterResult.getKeyInfo()`并将结果转换为`V2KeyStatus`。 然后检索内容元数据并将其存储在文件中。

所有这些任务都可以通过Java API实现。

有关Java API的详细信息，请参阅&#x200B;*Adobe Primetime DRM API参考*。

有关Media Packager参考实现的信息，请参阅&#x200B;*使用Adobe Primetime DRM参考实现*。

---
seo-title: 打包媒体文件概述
title: 打包媒体文件概述
uuid: 9509bcdc-ee4d-4025-9bb6-9b8ac439b926
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 概述 {#packaging-media-files-overview}

打包是指对视频内容加密和应用DRM策略的过程。 您可以使用媒体打包API打包文件。 Primetime DRM Java SDK只能打包渐进式下载的内容，如MP4。

>[!NOTE]
>
>请务必联系您的Primetime DRM代表，了解如何为您的媒体格式和使用案例选择最合适的打包选项。

打包与许可证服务器解耦。 包装程序无需连接到许可证服务器来交换有关内容的任何信息。 许可服务器在发布许可证时需要了解的所有信息都包含在内容元数据中。

当文件被加密时，如果没有相应的许可证，则无法分析其内容。 您可以使用Primetime DRM选择要加密的文件部分。 由于Primetime DRM可以解析视频内容的文件格式，因此它可以智能加密文件的选择部分而不是整个文件。 数据（如元数据和提示点）可以保持未加密，这样搜索引擎仍可以搜索文件。

指定的内容片段可具有多个DRM策略。 例如，您可以在不同业务模式下许可内容，而无需多次打包内容。 此外，您还可以允许在短时间内匿名访问，然后允许客户购买内容以无限制访问。 如果内容是通过使用多个DRM策略进行打包的，则许可证服务器必须实现用于选择必须使用哪个DRM策略才能发布许可证的逻辑。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>该架构允许指定使用DRM策略，并在内容打包时将其绑定到内容。 在客户端播放内容之前，客户端必须获得指定计算机的许可证。 该许可证指定实施的使用规则，并提供必须用于解密内容的密钥。 DRM策略表示用于生成许可证的模板。 但是，许可证服务器在发出许可证时可能会覆盖使用规则。 许可证可能因此类限制（如到期时间或播放窗口）而无效。

Primetime DRM为在CEK中传递提供了API。 如果未指定CEK，则SDK会随机生成它。 通常，您需要为每个内容部分使用不同的CEK。 但是，在动态流中，您可能会对构成该内容的所有文件使用相同的CEK。 因此，用户只需一个许可证即可从一个比特率无缝地过渡到另一个比特率。 如果要对多个内容使用相同的密钥和许可证，则需要将同一对象传递 `DRMParameters` 到 `MediaEncrypter.encryptContent()`CEK，或使用传递到CEK `V2KeyParameters.setContentEncryptionKey()`。 如果要对每个内容部分使用不同的密钥和许可证，您需要为每个文件创建 `DRMParameters` 一个新实例。

使用键旋转打包内容时，您可以控制使用的旋转键以及键更改的频率。 `F4VDRMParameters` 并实 `FLVDRMParameters` 现该 `KeyRotationParameters` 接口。 通过此界面，您可以启用键旋转。 您还需要指定 `RotatingContentEncryptionKeyProvider`。 对于加密的每个范例，此类确定要使用的旋转密钥。 您可以实施您自己的提供商，或使用 `TimeBasedKeyProvider` SDK附带的内容。 此实现在指定的秒数后随机生成新密钥。

在某些情况下，您可能需要将内容元数据存储为单独的文件，并使其与内容分开提供给客户端。 在这种情况下，您需要调用 `MediaEncrypter.encryptContent()`，它返回一个对 `MediaEncrypterResult` 象。 调 `MediaEncrypterResult.getKeyInfo()` 用结果并将其转换为 `V2KeyStatus`。 然后检索内容元数据并将其存储在文件中。

所有这些任务都可以通过Java API完成。

有关 *Java API的详细信息* ，请参阅Adobe Primetime DRM API参考。

有关 *Media Packager参考实施的信息，请参阅使用Adobe Primetime DRM参考实施* 。

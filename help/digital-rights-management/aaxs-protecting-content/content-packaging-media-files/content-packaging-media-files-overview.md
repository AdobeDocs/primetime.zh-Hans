---
seo-title: 概述
title: 概述
uuid: 11cf1f1f-a4b2-4ac2-aae7-e925d96729d2
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---


# 概述{#overview}

*打* 包是指对FLV或F4V文件加密和应用策略的过程。使用媒体打包API打包文件。 Adobe访问Java SDK只能打包渐进式下载的Flash和AIR内容，如FLV、F4V和MP4。 要使用Adobe访问DRM对其他内容格式(如AdobeHTTP Dynamic Streaming(HDS)或Apple HTTP Live Streaming(HLS))打包内容，您必须使用其他工具，如Adobe媒体服务器([https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html))或实现Adobe广播SDK的编码器([https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf)))。 或者，客户可以选择使用Adobe的Java Primetime Packager工具集，该工具集可以打包各种目标格式的内容，如HDS、HLS和DASH。

打包从许可证服务器中解除耦合。 包装程序无需连接到许可证服务器来交换有关内容的任何信息。 许可证服务器发布许可证所需了解的一切都包含在内容元数据中。

加密文件后，如果没有相应的许可证，则无法分析其内容。 Adobe访问允许您选择要加密的文件的哪些部分。 由于Adobe® Access™可以分析FLV和F4V内容的文件格式，因此它可以智能加密文件的选择性部分而不是整个文件。 元数据和提示点等数据可保持未加密状态，这样搜索引擎仍可以搜索文件。

给定内容可能具有多个策略。 这可能很有用，例如，如果您希望在不同业务模式下许可内容，而无需多次打包内容。 例如，您可以在短时间内允许匿名访问，然后允许客户购买内容并拥有无限的访问权限。 如果内容使用多个策略进行打包，则许可证服务器必须实现逻辑，以便选择用于发布许可证的策略。

>[!NOTE]
>
>该体系结构允许在打包内容时指定使用策略并将其绑定到内容。 在客户端可以播放内容之前，客户端必须获得该计算机的许可证。 该许可证指定实施的使用规则，并提供用于解密内容的密钥。 策略是用于生成许可证的模板，但许可证服务器在发出许可证时可以选择覆盖使用规则。 请注意，许可证可能会因过期时间或播放窗口等限制而失效。

打包内容时有许多选项可用。 这些属性在`DRMParameters`接口和实现该接口的类中指定，这些类是`F4VDRMParameters`和`FLVDRMParameters`。 通过这些类，您可以设置签名和密钥参数，并指示是加密音频内容、视频内容还是脚本数据。 要了解如何在引用实现中实现这些功能，请参阅&#x200B;*使用Adobe访问引用实现*&#x200B;中讨论的Media Packager命令行选项说明。 这些选项基于Java API，因此可用于程序化使用。

打包选项包括：

* 加密选项（音频、视频、部分加密）。
* 许可证服务器URL（客户端将此URL用作发送到许可证服务器的所有请求的基本URL）
* 许可证服务器传输证书
* 用于加密CEK的许可证服务器证书。
* 用于对元数据进行签名的打包程序凭据

Adobe访问提供了用于在CEK中传递的API。 如果未指定CEK，则SDK会随机生成它。 通常，您需要对每段内容使用不同的CEK。 但是，在动态流中，您可能对该内容的所有文件使用相同的CEK，因此用户只需要一个许可证，并可以无缝地从一个比特率过渡到另一个比特率。 要对多个内容使用相同的密钥和许可证，请将相同的`DRMParameters`对象传递给`MediaEncrypter.encryptContent()`，或使用`V2KeyParameters.setContentEncryptionKey()`在CEK中传递。 要对每个内容使用不同的密钥和许可证，请为每个文件新建一个`DRMParameters`实例。

使用密钥轮替打包内容时，您可以控制使用的旋转密钥以及密钥更改的频率。 `F4VDRMParameters` 并实 `FLVDRMParameters` 现接 `KeyRotationParameters` 口。通过此界面，您可以启用密钥旋转。 您还需要指定`RotatingContentEncryptionKeyProvider`。 对于每个已加密的样本，此类确定要使用的旋转密钥。 您可以实施您自己的提供程序，或使用SDK附带的`TimeBasedKeyProvider`。 此实现在指定的秒数后随机生成新密钥。

在某些情况下，您可能需要将内容元数据存储为单独的文件，并使其与内容分开地提供给客户端。 为此，请调用`MediaEncrypter.encryptContent()`，它返回`MediaEncrypterResult`对象。 调用`MediaEncrypterResult.getKeyInfo()`并将结果转换为`V2KeyStatus`。 然后检索内容元数据并将其存储在文件中。

所有这些任务都可以使用Java API完成。 有关本章中讨论的Java API的详细信息，请参阅&#x200B;*Adobe访问API参考*。

有关Media Packager参考实现的信息，请参见&#x200B;*使用Adobe访问参考实现*。

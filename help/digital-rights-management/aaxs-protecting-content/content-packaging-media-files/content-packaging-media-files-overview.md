---
title: 概述
description: 概述
copied-description: true
exl-id: 67c3d98f-8c17-4b5a-8abb-00f6f0f1e823
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# 概述 {#overview}

*包装* 是指将策略加密并应用于FLV或F4V文件的过程。 使用媒体打包API来打包文件。 Adobe访问Java SDK只能打包渐进式下载Flash和AIR内容，例如FLV、F4V和MP4。 要使用Adobe访问DRM打包内容以用于其他内容格式，例如AdobeHTTP Dynamic Streaming(HDS)或Apple HTTP实时流(HLS)，您必须使用其他工具，例如Adobe Medium服务器( [https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html))或实施Adobe广播SDK的编码器( [https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf))。 或者，客户可以选择使用Adobe的Java Primetime Packager工具集，该工具集可以为各种目标格式（如HDS、HLS和DASH）打包内容。

封装从许可证服务器分离。 打包程序无需连接到许可证服务器来交换任何有关内容的信息。 许可证服务器发出许可证所需了解的所有信息都包含在内容元数据中。

文件加密后，如果没有适当的许可证，将无法解析其内容。 Adobe访问允许您选择要加密的文件部分。 由于Adobe® Access™可以解析FLV和F4V内容的文件格式，因此可以智能地加密文件的选择性部分，而不是整个文件。 元数据和提示点等数据可以保持未加密，以便搜索引擎仍可以搜索文件。

给定内容块可能具有多个策略。 例如，如果您希望在不同业务模型下许可内容，而无需多次打包内容，则此功能会很有用。 例如，您可以允许匿名访问较短的时间，之后客户可以购买内容并拥有无限的访问权限。 如果使用多个策略对内容进行打包，则License Server必须实施逻辑以选择要使用哪个策略来颁发许可证。

>[!NOTE]
>
>该架构允许在打包内容时指定使用策略并将其绑定到内容。 在客户端可以播放内容之前，客户端必须获取该计算机的许可证。 许可证指定强制使用的使用规则，并提供用于解密内容的密钥。 该策略是用于生成许可证的模板，但是许可证服务器可以在颁发许可证时选择覆盖使用规则。 请注意，许可证可能会因过期时间或播放窗口等限制而呈现无效。

打包内容时，有多种选项可用。 这些在 `DRMParameters` 接口和实现该接口的类，即 `F4VDRMParameters` 和 `FLVDRMParameters`. 使用这些类，您可以设置签名和密钥参数，以及指示是加密音频内容、视频内容还是脚本数据。 要了解如何在参考实施中实施这些选项，请参阅中讨论的“媒体打包程序”命令行选项的说明。 *使用Adobe访问引用实施*. 这些选项基于Java API，因此可用于编程使用。

打包选项包括：

* 加密选项（音频、视频、部分加密）。
* 许可证服务器URL（客户端使用它作为发送到许可证服务器的所有请求的基本URL）
* 许可证服务器传输证书
* 许可证服务器证书，用于加密CEK。
* 用于签名元数据的打包程序凭据

Adobe访问提供了一个用于在CEK中传递的API。 如果未指定CEK，则SDK会随机生成它。 通常，每段内容需要不同的CEK。 但是，在Dynamic Streaming中，您可能会对该内容的所有文件使用相同的CEK，因此用户只需要一个许可证，并且可以从一个比特率无缝转换到另一个比特率。 要对多个内容使用相同的密钥和许可证，请传递相同的 `DRMParameters` 对象对象 `MediaEncrypter.encryptContent()`，或使用在CEK中传递 `V2KeyParameters.setContentEncryptionKey()`. 要对每段内容使用不同的密钥和许可证，请创建新的 `DRMParameters` 每个文件的实例。

使用轮换键打包内容时，您可以控制使用的轮换键以及键的更改频率。 `F4VDRMParameters` 和 `FLVDRMParameters` 实施 `KeyRotationParameters` 界面。 通过此界面，您可以启用密钥轮换。 您还需要指定 `RotatingContentEncryptionKeyProvider`. 对于每个加密的示例，此类确定要使用的轮换密钥。 您可以实施自己的提供商，也可以使用 `TimeBasedKeyProvider` 包含在SDK中。 此实施会在指定的秒数后随机生成新密钥。

在某些情况下，您可能需要将内容元数据存储为单独的文件，并使其可供客户端使用而不依赖于内容。 为此，调用 `MediaEncrypter.encryptContent()`，返回 `MediaEncrypterResult` 对象。 调用 `MediaEncrypterResult.getKeyInfo()` 并将结果转换为 `V2KeyStatus`. 然后，检索内容元数据并将其存储在文件中。

所有这些任务都可以使用Java API来完成。 有关本章讨论的Java API的详细信息，请参阅 *Adobe访问API参考*.

有关Media Packager参考实施的信息，请参阅 *使用Adobe访问引用实施*.

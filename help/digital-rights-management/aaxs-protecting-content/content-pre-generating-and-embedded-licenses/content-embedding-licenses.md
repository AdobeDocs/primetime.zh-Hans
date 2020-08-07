---
seo-title: 嵌入许可证
title: 嵌入许可证
uuid: b8d8ee9b-7430-4899-9caf-47d6b64021b8
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# 嵌入许可证 {#embedding-licenses}

一旦内容被加密并且许可证被预先生成，许可证就可以嵌入到加密的内容中。

要嵌入许可证，请获取的实例 `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`。 如果您知道加密内容的类型，请使用构造函数 `FLVKeyMetaDataUpdater` 或 `F4VKeyMetaDataUpdater`;否则，请 `MediaProcessorFactory.getMediaProcessor()` 使用根据检测到的文件类型返回实例。 构建并 `KeyMetaDataCallback` 调用 `modifyKeyMetaData()`。 当DRM元数据位于加密内容中时，将调用回调实现。 根据找到的元数据，您可以选择要嵌入的许可证并使用设置许可证 `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`。

有关演示嵌入式许可证的示例代 `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` 码，请参阅Reference Implementation命令行工具“示例”目录。

>[!NOTE]
>
>Adobe访问2.0客户端将忽略内容中嵌入的所有许可证，并尝试从元数据中指定的许可证服务器获取许可证。 但是，如果元数据指示没有可用的许可证服务器，则AdobeAccess 2.0客户端将需要升级才能视图内容。

请参 [阅带外许可证](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md)。

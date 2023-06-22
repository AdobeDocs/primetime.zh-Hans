---
title: 嵌入许可证
description: 嵌入许可证
copied-description: true
exl-id: 63b1bf18-b93d-4305-885a-3a9eee783a03
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 嵌入许可证 {#embedding-licenses}

一旦内容已经加密并且已经预先生成许可证，该许可证可以嵌入到加密内容中。

要嵌入许可证，请获取 `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. 如果您知道加密内容的类型，请使用构造函数 `FLVKeyMetaDataUpdater` 或 `F4VKeyMetaDataUpdater`；否则，使用 `MediaProcessorFactory.getMediaProcessor()` 以根据检测到的文件类型返回实例。 构建 `KeyMetaDataCallback` 和调用 `modifyKeyMetaData()`. 当DRM元数据位于加密内容中时，将调用您的回调实施。 根据找到的元数据，您可以选择要嵌入的许可证，并使用设置许可证 `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

有关演示嵌入式许可证的示例代码，请参阅 `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` 在参考实施命令行工具“Samples”目录中。

>[!NOTE]
>
>Adobe访问2.0客户端将忽略内容中嵌入的任何许可证，并将尝试从元数据中指定的许可证服务器获取许可证。 但是，如果元数据指示没有许可证服务器可用，则AdobeAccess 2.0客户端需要升级才能查看内容。

参见 [带外许可证](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md).

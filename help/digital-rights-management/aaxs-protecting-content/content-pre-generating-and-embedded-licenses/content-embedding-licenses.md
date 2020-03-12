---
seo-title: 嵌入许可证
title: 嵌入许可证
uuid: b8d8ee9b-7430-4899-9caf-47d6b64021b8
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 嵌入许可证 {#embedding-licenses}

一旦内容被加密并且已预生成许可证，许可证就可以嵌入到加密内容中。

要嵌入许可证，请获取的实例 `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`。 如果您知道加密内容的类型，请使用或的构造 `FLVKeyMetaDataUpdater` 函数 `F4VKeyMetaDataUpdater`;否则，请 `MediaProcessorFactory.getMediaProcessor()` 使用根据检测到的文件类型返回实例。 构建并 `KeyMetaDataCallback` 调用 `modifyKeyMetaData()`。 当DRM元数据位于加密内容中时，将调用回调实现。 根据找到的元数据，您可以选择要嵌入的许可证并使用设置该许可证 `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`。

有关演示嵌入式许可证的示例代 `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` 码，请参阅参考实施命令行工具“示例”目录。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Adobe Access 2.0客户端将忽略内容中嵌入的任何许可证，并将尝试从元数据中指定的许可证服务器获取许可证。 但是，如果元数据指示没有可用的许可证服务器，则Adobe Access 2.0客户端需要升级才能查看内容。

请参 [阅带外许可证](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md)。

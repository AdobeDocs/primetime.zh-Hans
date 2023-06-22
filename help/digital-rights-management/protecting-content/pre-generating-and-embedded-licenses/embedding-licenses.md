---
title: 嵌入许可证
description: 嵌入许可证
copied-description: true
exl-id: 8cd58808-73fb-4635-9a75-0520430f6b3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 嵌入许可证 {#embedding-licenses}

一旦内容已经加密并且已经预先生成许可证，该许可证可以嵌入到加密内容中。

如果要嵌入许可证，则需要获取一个实例 `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. 如果您知道加密内容的类型，请使用构造函数 `FLVKeyMetaDataUpdater` 或 `F4VKeyMetaDataUpdater`；否则，使用 `MediaProcessorFactory.getMediaProcessor()` 以根据检测到的文件类型返回实例。 那么您需要构建一个 `KeyMetaDataCallback` 和调用 `modifyKeyMetaData()`. 然后，当DRM元数据位于加密内容中时，将调用回调实施。 根据找到的元数据，您可以选择要嵌入的许可证，并使用设置许可证 `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

参见 `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` 在参考实施命令行工具中 [!DNL Samples] 用于演示嵌入式许可证的示例代码的目录。

>[!NOTE]
>
>Adobe Primetime DRM 2.0客户端忽略嵌入在内容中的任何许可证，然后尝试从元数据中指定的许可证服务器获取许可证。 但是，如果元数据指示没有许可证服务器可用，则需要升级Primetime DRM 2.0客户端，然后才能查看内容。

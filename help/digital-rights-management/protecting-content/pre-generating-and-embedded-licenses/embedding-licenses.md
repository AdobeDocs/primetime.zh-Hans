---
title: 嵌入许可证
description: 嵌入许可证
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# 嵌入许可证{#embedding-licenses}

一旦内容被加密并且许可证被预生成，许可证就可以嵌入到加密内容中。

如果要嵌入许可证，则需要获取`com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`的实例。 如果您知道加密内容的类型，请使用`FLVKeyMetaDataUpdater`或`F4VKeyMetaDataUpdater`的构造函数；否则，使用`MediaProcessorFactory.getMediaProcessor()`根据检测到的文件类型返回实例。 然后，您需要构造`KeyMetaDataCallback`并调用`modifyKeyMetaData()`。 然后，当DRM元数据位于加密内容中时，将调用回调实现。 根据找到的元数据，您可以选择要嵌入的许可证并使用`EmbedLicenseKeyMetaData.setEmbeddedLicenses()`设置许可证。

有关演示嵌入式许可证的示例代码，请参见Reference Implementation命令行工具[!DNL Samples]目录中的`com.adobe.flashaccess.samples.licenseembedder.EmbedLicense`。

>[!NOTE]
>
>Adobe Primetime DRM 2.0客户端会忽略嵌入到内容中的所有许可证，然后尝试从元数据中指定的许可证服务器获取许可证。 但是，如果元数据指示没有可用的许可证服务器，则需要升级Primetime DRM 2.0客户端，然后才能视图内容。


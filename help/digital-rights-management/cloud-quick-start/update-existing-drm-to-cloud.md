---
seo-title: 更新现有DRM内容以使用Cloud DRM（可选）
title: 更新现有DRM内容以使用Cloud DRM（可选）
uuid: cfabeb06-210f-45af-b8a6-8e0b03a76103
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 更新现有DRM内容以使用Cloud DRM（可选） {#update-existing-drm-content-to-use-cloud-drm-optional}

如果您有受Primetime DRM保护的现有内容库，则可以“重新标题”现有内容以使用Primetime Cloud DRM服务，而不必重新打包／加密原始源文件。 重新设置内容标题只会更新HLS清单中内容的DRM元数据。 它不会对原始资产执行任何非加密／重新加密。 如果原始源内容不可用，或者担心重新打包大型库所需的资源量，则此选项可能很有用。

可以使用Primetime DRM Java SDK以编程方式更新元数据。 此外，此保护 [!DNL OfflinePackager.jar] 工具包中附带的命令行工具也可以使用此选项完成此 `-drm_refresh` 任务。

## 重新标题详细信息 {#section_3F3980D8E775450588C64E02A8448189}

重定向必须更新以下字段才能使用CloudDRM:

* 许可证服务器URL(至 [!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod])
* 许可证服务器证书（至CloudDRM许可证服务器证书）
* 传输证书（到CloudDRM传输证书）
* Packager Credential（至已激活以用于CloudDRM的Packager凭据）

## 查找DRM元数据 {#section_28721CB7966F40708AEC8637F2E9BB72}

使用HTTP技术（如HDS或HLS）的内容使用引用Adobe Access DRM元数据的清单。 在HDS中，元数据由标记引 `<drmmeta>` 用，在HLS中，元数据由标记引 `#EXT-X-FAXS-CM` 用。 在任一情况下，元数据都可以作为基64编码的Blob包含在清单中，或作为二进制文件在外部引用。 如果元数据嵌入／内嵌在清单中，则可能首先必须将元数据基64解码为二进制数据，然后才能使用该数据来实例化DRM元数据。

## 使用包含的OfflinePacakger.jar {#section_37C2091856E44AA380D742C72B4DD1A7}

将命令 `-drm_refresh option` 行提供给该命令行。 将使用更新的DRM元数据创建新的清单文件，而内容将不会重新加密。

## 使用Primetime DRM Java SDK重新标题 {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2}

更新现有DRM元数据可通过使用Primetime DRM（以前称为Adobe Access DRM）Java SDK实现编程方法。 有关详细信息，请参 [!DNL RegenerateMetadata.java] 阅SDK包中的 [!DNL /Reference Implmentation/Command Line Tools/samples/] 代码示例。 Adobe Access Java SDK不是此CloudDRM保护工具包的一部分，必须直接从Adobe获取。 有关更多详细信息，请与您的Adobe业务联系人联系。
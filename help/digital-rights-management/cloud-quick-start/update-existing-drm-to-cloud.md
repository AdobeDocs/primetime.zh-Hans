---
title: 更新现有DRM内容以使用云DRM（可选）
description: 更新现有DRM内容以使用云DRM（可选）
copied-description: true
exl-id: 89b1e99a-cb28-4524-9c47-f71f92d3753d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# 更新现有DRM内容以使用云DRM（可选） {#update-existing-drm-content-to-use-cloud-drm-optional}

如果您有一个受Primetime DRM保护的现有内容库，则可以“重新标头”现有内容以使用Primetime Cloud DRM服务，而不必重新封装/加密原始源文件。 重新标题化内容只会更新HLS清单中内容的DRM元数据。 它不对原始资产执行任何解密/重新加密。 如果原始源内容不可用，或者担心重新打包大型库所需的资源量，则此选项可能很有用。

可以使用Primetime DRM Java SDK以编程方式更新元数据。 此外， [!DNL OfflinePackager.jar] 此保护套件随附的命令行工具也可以使用 `-drm_refresh` 选项。

## 重新标头详细信息 {#section_3F3980D8E775450588C64E02A8448189}

重新调整标题必须更新以下字段才能使用CloudDRM：

* 许可证服务器URL（至） [!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod])
* 许可证服务器证书（到CloudDRM许可证服务器证书）
* 传输证书（到CloudDRM传输证书）
* Packager凭据（已激活以用于CloudDRM的Packager凭据）

## 查找DRM元数据 {#section_28721CB7966F40708AEC8637F2E9BB72}

使用HTTP技术（例如HDS或HLS）的内容利用引用Adobe访问DRM元数据的清单。 在HDS中，元数据由 `<drmmeta>` 标签之间，而在HLS中，它由 `#EXT-X-FAXS-CM` 标记之前。 在任一方案中，元数据都可作为base-64编码的blob内联包含在清单中，也可作为二进制文件从外部引用。 如果元数据被嵌入/内联在清单中，则可能必须先将元数据进行base64解码为二进制数据，然后才能使用该数据实例化DRM元数据。

## 使用包含的OfflinePackger.jar {#section_37C2091856E44AA380D742C72B4DD1A7}

提供 `-drm_refresh option` 到命令行。 将使用更新后的DRM元数据创建新的清单文件，但不会重新加密内容。

## 使用Primetime DRM Java SDK重新生成标头 {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2}

更新现有DRM元数据可通过使用Primetime DRM(以前称为Adobe访问DRM) Java SDK以编程方法实现。 欲知更多详情，请参阅 [!DNL RegenerateMetadata.java] 中的代码示例 [!DNL /Reference Implmentation/Command Line Tools/samples/] sdk的包。 Adobe访问Java SDK不是此CloudDRM保护套件的一部分，必须直接从Adobe中获取。 请联系您的Adobe业务联系人以获取更多详细信息。

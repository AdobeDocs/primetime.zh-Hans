---
description: Primetime数字版权管理(DRM)系统的关键客户端元素是DRM管理器。
title: Primetime DRM界面概述
exl-id: dee420cf-8aad-42e8-965d-9fd9395f2c45
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# Primetime DRM界面概述 {#primetime-drm-interface-overview}

您可以使用PrimetimeDigital Rights Management(DRM)系统的功能来提供对视频内容的安全访问。 或者，您可以使用第三方DRM解决方案作为Adobe的集成Primetime DRM解决方案的替代方案。

有关第三方DRM解决方案可用性的最新信息，请咨询您的Adobe代表。

Primetime数字版权管理(DRM)系统的关键客户端元素是DRM管理器。

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM提供了一个可扩展的高效工作流，用于在TVSDK应用程序中实施内容保护。 通过为每个数字媒体文件创建许可证，您可以保护和管理视频内容的权限。

TVSDK支持将Primetime DRM集成作为自定义DRM工作流。 这意味着您的应用程序必须先实施DRM验证工作流，然后才能使用FlashDRMManager播放流。 要启用此功能，MediaPlayer将为您提供用于身份验证的DRM管理器。

请参阅TVSDK包中包含的DRM示例播放器代码。

以下是使用DRM时最重要的API元素：

* 媒体播放器中对实现DRM子系统的DRM管理器对象的引用：

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

TVSDK问题 `PTMediaPlayerItemDRMMetadataChanged` DRM元数据更改时通知。 此元数据用作的几乎所有函数的输入 `DRMManager` 类。

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

如果受DRM保护的流是多比特率(MBR)编码的，则用于变体播放列表的DRM元数据应当与用于所有比特率流中的元数据相同。

>[!TIP]
>
>在iOS应用程序中引用受DRM保护的资源URL时，查询字符串参数 `?faxs=1` 必须附加到(MBR)设置级别的M3U8 URL。 例如：
>
>
```
>https://your.domain.com/hls/[...]/index.m3u8?faxs=1
>```
>
>此 `faxs=1` 查询字符串参数指示内容受DRM保护，并在iOS TVSDK中相应地触发DRM解密工作流。 您还可以附加 `faxs=1` 标记位于受DRM保护的HLS资产URL上，且这些URL将发往其他平台；在iOS上会根据需要观察该标记，或者在其他平台上的播放器中将其视为非操作。

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

有关DRM的详细信息，请参见 [Adobe Primetime DRM文档](https://help.adobe.com/en_US/primetime/drm).

## 在TSVDK应用程序中实施Primetime DRM {#implement-primetime-drm-in-a-tsvdk-application}

Primetime DRM集成到TVSDK中，这简化了TVSDK应用程序中内容保护的实施。

有关使用Primetime DRM在TVSDK应用程序中实施内容保护的概述和详细信息，请参阅：

* [Adobe Primetime TVSDK-DRM工作流(PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)

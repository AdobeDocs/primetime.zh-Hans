---
description: Primetime数字版权管理(DRM)系统的关键客户端元素是DRM管理器。
seo-description: Primetime数字版权管理(DRM)系统的关键客户端元素是DRM管理器。
seo-title: Primetime DRM界面概述
title: Primetime DRM界面概述
uuid: 3aae7c7a-fd0c-430e-9018-fd72801ab778
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---


# Primetime DRM接口概述{#primetime-drm-interface-overview}

您可以使用PrimetimeDigital Rights Management(DRM)系统的功能提供对视频内容的安全访问。 或者，您也可以将第三方DRM解决方案用作Adobe集成Primetime DRM解决方案的替代方案。

请咨询您的Adobe代表，了解有关第三方DRM解决方案可用性的最新信息。

Primetime数字版权管理(DRM)系统的关键客户端元素是DRM管理器。

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM提供一个可伸缩、高效的工作流程，用于在TVSDK应用程序中实施内容保护。 通过为每个数字媒体文件创建许可证，您可以保护和管理视频内容的权利。

TVSDK支持Primetime DRM集成作为自定义DRM工作流。 这意味着您的应用程序必须在使用FlashDRMManager播放流之前实施DRM身份验证工作流。 要启用此功能，MediaPlayer将为您提供DRM管理器以进行身份验证。

请参阅TVSDK包中包含的DRM示例播放器代码。

以下是使用DRM时最重要的API元素：

* 媒体播放器中对实现DRM子系统的DRM管理器对象的引用：

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

TVSDK在DRM元数据更改时发出`PTMediaPlayerItemDRMMetadataChanged`通知。 此元数据用作`DRMManager`类几乎所有函数的输入。

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

如果受DRM保护的流是多比特率(MBR)编码的，则用于变型播放列表的DRM元数据应与在所有比特率流中使用的元数据相同。

>[!TIP]
>
>在iOS应用程序中引用受DRM保护的资产URL时，查询字符串参数`?faxs=1`必须附加到(MBR)设置级别M3U8 URL中。 例如：
>
>
```
>https://your.domain.com/hls/[...]/index.m3u8?faxs=1
>```
>
>`faxs=1`查询字符串参数指示内容受DRM保护，并在iOS TVSDK中相应地触发DRM解密工作流。 您还可以在受DRM保护的HLS资产URL上附加`faxs=1`标记，这些资产URL用于其他平台；在iOS上按要求进行观察，或在其他平台上的播放器中被视为非操作。

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

有关DRM的详细信息，请参阅[Adobe PrimetimeDRM文档](https://help.adobe.com/en_US/primetime/drm)。

## 在TSVDK应用程序{#implement-primetime-drm-in-a-tsvdk-application}中实施Primetime DRM

Primetime DRM已集成到TVSDK中，这简化了在TVSDK应用程序中实施内容保护。

有关使用Primetime DRM在TVSDK应用程序中实施内容保护的概述和详细信息，请参阅：

* [Adobe PrimetimeTVSDK-DRM工作流程(PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)
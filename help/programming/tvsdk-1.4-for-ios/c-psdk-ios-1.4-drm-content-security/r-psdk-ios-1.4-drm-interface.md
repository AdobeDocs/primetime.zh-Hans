---
description: Primetime数字版权管理(DRM)系统的关键客户端元素是DRM管理器。
seo-description: Primetime数字版权管理(DRM)系统的关键客户端元素是DRM管理器。
seo-title: Primetime DRM界面概述
title: Primetime DRM界面概述
uuid: 3aae7c7a-fd0c-430e-9018-fd72801ab778
translation-type: tm+mt
source-git-commit: 25a0dfef12ecf10ba939500c4ba539468c41ee1b

---


# Primetime DRM界面概述 {#primetime-drm-interface-overview}

您可以使用Primetime数字版权管理(DRM)系统的功能来提供对视频内容的安全访问。 或者，您也可以使用第三方DRM解决方案作为Adobe集成Primetime DRM解决方案的替代方案。

有关第三方DRM解决方案的可用性，请咨询Adobe代表。

Primetime数字版权管理(DRM)系统的关键客户端元素是DRM管理器。

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM提供了一个可伸缩、高效的工作流，用于在TVSDK应用程序中实施内容保护。 通过为每个数字媒体文件创建许可证，您可以保护和管理视频内容的权限。

TVSDK支持Primetime DRM集成作为自定义DRM工作流程。 这意味着您的应用程序必须在使用Flash DRManager播放流之前实现DRM身份验证工作流。 要启用此功能，MediaPlayer将为您提供DRM管理器以进行身份验证。

请参阅TVSDK包中包含的DRM示例播放器代码。

以下是使用DRM时最重要的API元素：

* 媒体播放器中对实现DRM子系统的DRM管理器对象的引用：

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

TVSDK在DRM元 `PTMediaPlayerItemDRMMetadataChanged` 数据更改时发出通知。 此元数据用作类几乎所有函数的输 `DRMManager` 入。

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

如果受DRM保护的流是多比特率(MBR)编码的，则用于变体播放列表的DRM元数据应与在所有比特率流中使用的元数据相同。

>[!TIP] {importance=&quot;high&quot;}
>
>在iOS应用程序中引用受DRM保护的资产URL时，查询字符串参 `?faxs=1` 数必须附加到(MBR)设置级M3U8 URL中。 例如：>
>
```>
>https://your.domain.com/hls/[...]/index.m3u8?faxs=1
>```>
>The `faxs=1` query string parameter signals that the content is DRM protected, and triggers the DRM decryption workflow accordingly in the iOS TVSDK. You can also append the `faxs=1` tag on DRM-protected HLS asset URLs that are destined for other platforms; it is observed as required on iOS or treated as a non-op in players on other platforms.



<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

有关DRM的详细信息，请参阅 [Adobe Primetime DRM文档](https://help.adobe.com/en_US/primetime/drm)。

## 在TSVDK应用程序中实施Primetime DRM {#implement-primetime-drm-in-a-tsvdk-application}

Primetime DRM已集成到TVSDK中，这简化了在TVSDK应用程序中实施内容保护的过程。

有关使用Primetime DRM在TVSDK应用程序中实施内容保护的概述和详细信息，请参阅：

* [Adobe Primetime TVSDK-DRM工作流程(PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)
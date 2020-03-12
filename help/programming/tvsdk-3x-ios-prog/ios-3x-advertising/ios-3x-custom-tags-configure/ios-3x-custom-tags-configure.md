---
description: 媒体流可以在播放列表／清单文件中以标记的形式携带其他元数据，并且此文件指示广告的放置。 您可以指定自定义标记名称，并在清单文件中出现某些标记时通知您。
seo-description: 媒体流可以在播放列表／清单文件中以标记的形式携带其他元数据，并且此文件指示广告的放置。 您可以指定自定义标记名称，并在清单文件中出现某些标记时通知您。
seo-title: 自定义标记
title: 自定义标记
uuid: 103f4fff-2218-4d44-90bc-b80da467f282
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 概述 {#custom-tags-overview}

媒体流可以在播放列表／清单文件中以标记的形式携带其他元数据，并且此文件指示广告的放置。 您可以指定自定义标记名称，并在清单文件中出现某些标记时通知您。

## HLS内容标记 {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>此功能不适用于Apple计算机上的Safari，因为TVSDK使用视频标记而不是Flash或MSE播放HLS内容。

TVSDK为特定#EXT广告标记提供开箱即用的支持。 您的应用程序可以使用自定义标记来增强广告工作流程或支持封锁场景。 为支持高级工作流程，TVSDK允许您在清单中指定和订阅其他标记。 当清单文件中出现这些标记时，您会收到通知。

>[!TIP]
>
>您可以订阅VOD和实时／线性流的自定义标记。

>[!NOTE] {othertype=&quot;Limitation&quot;}
>
>在Safari中使用视频标记播放HLS时，而不是使用Flash回退，此功能在Safari中将不可用。

## 使用自定义HLS标记 {#section_AD032318AEF5418393D2B1DF36B0BABB}

以下是自定义VOD资产的示例：

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:7
 
#EXT-X-ASSET:AID=10
 
#EXTINF:9.9766,
seg1.ts
 
#EXTINF:9.9766,
seg2.ts
 
#EXTINF:9.9766,
seg3.ts
 
#EXT-X-AD:DURATION=10
#EXTINF:9.9766,
seg4.ts
 
#EXTINF:9.9766,
seg5.ts
 
#EXT-X-ENDLIST
```

您的应用程序可以设置以下场景：

* 文件中存 `#EXT-X-ASSET` 在标记或您订阅的任何其他自定义标记名称集时的通知。
* 在流中找到标 `#EXT-X-AD` 记或任何其他自定义标记名称时插入广告。

您可以订阅以下任意标记作为自定义标记： `EXT-PROGRAM-DATE-TIME`, `EXT-X-START`, `EXT-X-AD`, `EXT-X-CUE`, `EXT-X-ENDLIST`. 在分析清单文件 `TimedMetadata` 时，系统会通知您一个事件。

您已经订阅了某些广 `EXT-X-CUE`告标签，例如。 这些广告标记也由默认的业务机会生成器使用。 您可以通过设置属性来指定默认业务机会生成器使用的广告 `adTags` 标记。
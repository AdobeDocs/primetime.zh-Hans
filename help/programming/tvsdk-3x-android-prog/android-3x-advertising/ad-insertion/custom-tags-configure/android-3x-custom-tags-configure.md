---
description: 媒体流可以播放列表/清单文件中的标记形式携带其他元数据，并且此文件指示广告的放置。 您可以指定自定义标记名称，并在清单文件中出现某些标记时收到通知。
title: 自定义标记
exl-id: 5c1ba637-5113-455c-977b-d190a554396a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 概述 {#custom-tags-overview}

媒体流可以播放列表/清单文件中的标记形式携带其他元数据，并且此文件指示广告的放置。 您可以指定自定义标记名称，并在清单文件中出现某些标记时收到通知。

## HLS内容标记 {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>此功能不适用于Apple计算机上的Safari，因为TVSDK使用视频标记(而不是Flash或MSE)播放HLS内容。

TVSDK为特定的提供现成支持 `#EXT` 广告标签。 您的应用程序可以使用自定义标记来增强广告工作流或支持封锁场景。 为了支持高级工作流，TVSDK允许您指定并订阅清单中的其他标记。 当这些标记出现在清单文件中时，您会收到通知。

>[!TIP]
>
>您可以为VOD和实时/线性流订阅自定义标记。

>[!NOTE]
>
>**限制**
>
>当HLS通过Safari中的视频标记而不是通过Flash回退来播放时，此功能在Safari中将不可用。

## 使用自定义HLS标记 {#section_AD032318AEF5418393D2B1DF36B0BABB}

以下是自定义VOD资源的示例：

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

您的应用程序可以设置以下方案：

* 通知时间 `#EXT-X-ASSET` 标记或您订阅的任何其他自定义标记名称集都存在于文件中。
* 插入广告时 `#EXT-X-AD` 标记或任何其他自定义标记名称。

您可以将以下任意标记订阅为自定义标记：

* `EXT-PROGRAM-DATE-TIME`
* `EXT-X-START`
* `EXT-X-AD`
* `EXT-X-CUE`
* `EXT-X-ENDLIST`

您将会收到通知 `TimedMetadata` 分析清单文件期间的事件。

有一些广告标记，例如 `EXT-X-CUE`，您已订阅该服务。 这些广告标记还由默认机会生成器使用。 您可以通过设置 `adTags` 属性。

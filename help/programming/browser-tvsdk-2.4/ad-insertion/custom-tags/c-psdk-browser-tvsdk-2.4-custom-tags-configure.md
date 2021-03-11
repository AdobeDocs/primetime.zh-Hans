---
description: 媒体流可以在媒体演示文稿描述(MPD)文件中以标记形式携带其他元数据，并且此文件指示广告的放置。 您可以指定自定义标记名称，并在清单文件中出现某些标记时通知您。
title: 自定义标记
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---


# 概述{#custom-tags-overview}

媒体流可以在媒体演示文稿描述(MPD)文件中以标记形式携带其他元数据，并且此文件指示广告的放置。 您可以指定自定义标记名称，并在清单文件中出现某些标记时通知您。

## HLS内容标记{#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>此功能在Apple计算机上不可用，因为浏览器TVSDK使用视频标记而不是Flash或MSE来播放HLS内容。

浏览器TVSDK为特定广告标#EXT提供开箱即用支持。 您的应用程序可以使用自定义标记来增强广告工作流程或支持封锁场景。 为支持高级工作流,Browser TVSDK允许您指定和订阅清单中的其他标记。 当清单文件中出现这些标签时，您会收到通知。

>[!TIP]
>
>您可以订阅VOD和实时/线性流的自定义标签。

>[!NOTE]
>
>在Safari中使用视频标记播放HLS时，而不是使用Flash回退，此功能在Safari中将不可用。

## 使用自定义HLS标记{#section_AD032318AEF5418393D2B1DF36B0BABB}

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

* 当`#EXT-X-ASSET`标记或您订阅的任何其他自定义标记名称集存在于文件中时的通知。
* 在流中找到`#EXT-X-AD`标记或任何其他自定义标记名称时插入广告。

您可以订阅以下任意标记作为自定义标记：`EXT-PROGRAM-DATE-TIME`、`EXT-X-START`、`EXT-X-AD`、`EXT-X-CUE`、`EXT-X-ENDLIST`。 解析清单文件时，系统会通过`TimedMetadata`事件通知您。

您已经订阅了某些广告标记，如`EXT-X-CUE`。 这些广告标记也由默认机会生成器使用。 您可以通过设置`adTags`属性来指定默认机会生成器使用的广告标签。

## 短划线内容标签{#section_967A952319BE4048B4C6612FFF7ADA6E}

DASH有两种信号事件:

* 在MPD文件中。

   此文件与HLS内容中的M3U8文件类似，MPD事件存在于.mpd文件中。
* 在表示中

   通过将事件消息作为段的一部分添加，带内事件用表示复用。 表示法是按顺序播放的视频和音频段的列表。 带内事件数据嵌入这些区段中。

这些事件一经浏览器TVSDK分析，即作为`TimedMetadata`事件通知应用程序。 一旦通知事件，将不再通知它。

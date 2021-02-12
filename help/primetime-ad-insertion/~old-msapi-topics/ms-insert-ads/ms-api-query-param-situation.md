---
description: 除了基本的查询参数之外，可选的查询参数还使清单服务器能够与不同的客户端和情况一起使用。
seo-description: 除了基本的查询参数之外，可选的查询参数还使清单服务器能够与不同的客户端和情况一起使用。
seo-title: 按客户端和情况选择的查询参数
title: 按客户端和情况选择的查询参数
uuid: e3fae41e-9f7d-4f01-9a01-52a1d5f5dad5
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# 按客户端和情况{#optional-query-parameters-by-client-and-situation}选择的查询参数

除了基本的查询参数之外，可选的查询参数还使清单服务器能够与不同的客户端和情况一起使用。

## 使用Akamai Ad Scaler{#section_120FEC75C34D4F4587B77D842166D68A}插入广告

在Akamai内容投放网络(CDN)上，Akamai Edge服务器充当客户端与清单服务器之间的中介。 如果还使用Ad Scaler,`ptassetid`和`live`查询参数会向Akamai Edge提供所需信息。

`ptassetid`参数是其资产的发布者ID。 Akamai使用此播放列表（而非作为请求URL的一部分提供的base64编码URL）来标识要提供给清单服务器以进行广告插入的播放列表。

`live`参数可区分实时内容和视频点播(VOD)。 清单服务器需要此信息来支持其与Akamai的简化界面。

以下是显示与Akamai相关的参数的示例URL:

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## 从Xbox {#section_5DB405F4647240A0B83E72DE35D5EC80}上的TVSDK插入广告

基于Xbox上的Primetime TVSDK的播放器不需要提供除基本参数之外的其他查询参数。

## 在iOS上使用Safari {#section_250E493A125E4F82940D19C7DA2AAB2E}从TVSDK插入广告

基于iOS上的Primetime TVSDK的播放器使用Safari浏览器，除了基本的查询参数外，还必须指定`ptplayer`和`live`参数。

清单服务器识别`ptplayer`值`ios-mobileweb`，并从它返回的广告拼接清单中消除预卷。

`live`参数告诉清单服务器是返回实时内容还是VOD内容。

以下是一个示例URL，它显示与Safari的iOS相关的参数：

```URL
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## 使用自定义广告提示格式{#section_82AF880AAABE4BD4B593D906434D4D89}进行广告插入

Adobe为Primetime包中不直接支持的广告提示格式提供名称。 要使用此格式，请提供其Adobe提供的名称作为`ptcueformat`参数的值。

以下是指定自定义广告提示格式的示例URL:

```URL
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## 使用广告提示为VOD {#section_E0D830F5EEE24639819B975B90F6999F}创建FreeWheel时间轴的广告插入

对于包含要分析并包含在FreeWheel广告请求中的广告提示的VOD内容，请将`ptcueformat`参数的值设置为`DPIsimple`。

以下是一个示例URL，它指定对VOD使用FreeWheel时间轴：

```URL
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## 使用VOD {#section_F398F7659164463FA886A4CC787C7B5A}的自定义时间轴进行广告插入

要要求清单服务器根据您提供的时间轴将广告插入VOD内容，请将`pttimeline`参数的值设置为指定时间轴的字符串。 请参阅[VOD时间线格式](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)。

以下是使用自定义时间轴进行VOD的示例URL:

```URL
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

它指定初始分段，最多包含两则广告，然后是两分钟内的内容段，最后是最多包含两则广告的30秒分段，最后是五分钟内容段。

VOD内容的自定义内容时间轴的广告拼接如下所示：

* 广告出现在广告服务器指定的广告投放时间之后最接近的中断边界。

* 区段至少长两秒。

## 对TS区段{#section_BF855A4399DC42CB8C0586113A416BBC}授权

Adobe仅支持Akamai CDN的此功能。 HTTP实时流(HLS)使用流级M3U8播放列表交付传输流(TS)段。 在变型M3U8播放列表中向客户端提供多个流级播放列表。 客户端从变型列表选择一个播放列表流，然后逐个下载该流级播放列表中的TS段。 在正常操作中，请求的内容可能需要Cookie授权，清单服务器在后台以不可见方式处理该授权。 它从原始内容中提取cookie，并向URL附加适当的令牌以用于请求所选播放列表流。

当BootstrapURL查询参数包括`pttoken=true`时，发布者需要使用cookie来请求每个TS段，而不是整个流只使用一次。 清单服务器将此cookie作为查询参数附加到它发回的流播放列表中的每个TS段URL。
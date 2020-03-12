---
description: 除了基本查询参数之外，可选的查询参数使清单服务器能够与不同的客户端和情况一起使用。
seo-description: 除了基本查询参数之外，可选的查询参数使清单服务器能够与不同的客户端和情况一起使用。
seo-title: 按客户端和情况选择的查询参数
title: 按客户端和情况选择的查询参数
uuid: e3fae41e-9f7d-4f01-9a01-52a1d5f5dad5
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# 按客户端和情况选择的查询参数 {#optional-query-parameters-by-client-and-situation}

除了基本查询参数之外，可选的查询参数使清单服务器能够与不同的客户端和情况一起使用。

## 使用Akamai Ad Scaler插入广告 {#section_120FEC75C34D4F4587B77D842166D68A}

在Akamai内容交付网络(CDN)上，Akamai Edge服务器充当客户端与清单服务器之间的中间人。 如果还使用Ad Scaler，则和查 `ptassetid` 询参数 `live` 会向Akamai Edge提供所需信息。

该 `ptassetid` 参数是其资产的发布者ID。 Akamai使用此URL（而不是作为请求URL的一部分提供的基本64编码URL）来标识要提供给清单服务器以进行广告插入的播放列表。

该参 `live` 数可区分实时内容和视频点播(VOD)。 清单服务器需要此信息来支持其与Akamai的简化界面。

以下是显示与Akamai相关的参数的示例URL:

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## Xbox上TVSDK的广告插入 {#section_5DB405F4647240A0B83E72DE35D5EC80}

基于Primetime TVSDK、Xbox的播放器不需要提供基本的查询参数以外的其他查询参数。

## 在iOS上使用Safari从TVSDK插入广告 {#section_250E493A125E4F82940D19C7DA2AAB2E}

基于iOS上的Primetime TVSDK的播放器（使用Safari浏览器）除了基本的查询参数 `ptplayer` 外， `live` 还必须指定和参数。

清单服务器识别 `ptplayer` 该 `ios-mobileweb` 值并从其返回的广告拼接清单中消除预卷。

该参 `live` 数告知清单服务器是返回实时内容还是VOD内容。

以下是一个示例URL，它显示与Safari的iOS相关的参数：

```
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## 使用自定义广告提示格式的广告插入 {#section_82AF880AAABE4BD4B593D906434D4D89}

Adobe为广告提示格式提供名称，它不直接在Primetime包中支持这些格式。 要使用此格式，请提供其Adobe提供的名称作为参数的 `ptcueformat` 值。

以下是指定自定义提示格式的示例URL:

```
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## 使用广告提示为VOD创建FreeWheel时间轴的广告插入 {#section_E0D830F5EEE24639819B975B90F6999F}

对于包含要分析并包含在FreeWheel广告请求中的广告提示的VOD内容，请将参数的值 `ptcueformat` 设置为 `DPIsimple`。

以下是一个URL示例，它指定对VOD使用FreeWheel时间轴：

```
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## 使用自定义时间轴进行VOD广告插入 {#section_F398F7659164463FA886A4CC787C7B5A}

要请求清单服务器根据您提供的时间轴将广告插入VOD内容，请将参数的值设置为指定时 `pttimeline` 间轴的字符串。 查看 [VOD时间轴格式](../../msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)

以下是使用自定义时间轴进行VOD的示例URL:

```
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

它指定最多包含两则广告的初始间隔为一分钟，然后是两分钟内容段，最后是最多包含两则广告的30秒间隔，最后是五分钟内容段。

VOD内容的自定义内容时间线的广告拼接如下所示：

* 广告显示在广告服务器指定的广告投放时间后最接近的中断边界处。
* 区段至少有2秒长。

## 授权TS细分 {#section_BF855A4399DC42CB8C0586113A416BBC}

Adobe仅支持Akamai CDN的此功能。 HTTP实时流(HLS)使用流级M3U8播放列表交付传输流(TS)段。 在变型M3U8播放列表中向客户端提供多个流级播放列表。 客户端从变体列表中选择一个播放列表流，然后逐个下载该流级播放列表中的TS段。 在正常操作中，所请求的内容可能需要cookie授权，清单服务器在后台以不可见方式处理。 它从原始内容中提取cookie，并向URL附加一个适当的令牌，以用于请求所选播放列表流。

当Bootstrap URL查询参数包含时 `pttoken=true`，发布者需要使用cookie来请求每个TS区段，而不是整个流只使用一次。 清单服务器将此cookie作为查询参数附加到它发送回的流播放列表中的每个TS段URL。

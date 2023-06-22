---
description: 除了基本查询参数之外，可选查询参数还使清单服务器能够与不同的客户端和情况配合使用。
title: 按客户端和情况的可选查询参数
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---


# 按客户端和情况的可选查询参数 {#optional-query-parameters-by-client-and-situation}

除了基本查询参数之外，可选查询参数还使清单服务器能够与不同的客户端和情况配合使用。

## 使用Akamai Ad Scaler插入广告 {#section_120FEC75C34D4F4587B77D842166D68A}

在Akamai内容分发网络(CDN)上，Akamai Edge Server充当客户端和清单服务器之间的中介。 如果您还使用Ad Scaler， `ptassetid` 和 `live` 查询参数可向Akamai Edge提供所需信息。

此 `ptassetid` parameter是发布者的资产ID。 Akamai使用此URL（而不是作为请求URL的一部分提供的base64编码URL）来标识要提供给清单服务器以供广告插入的播放列表。

此 `live` 参数区分实时内容和视频点播(VOD)。 清单服务器需要此信息来支持其与Akamai的简化界面。

以下是一个显示与Akamai相关的参数的示例URL：

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## 从Xbox上的TVSDK插入广告 {#section_5DB405F4647240A0B83E72DE35D5EC80}

基于Xbox上的Primetime TVSDK的播放器无需提供基本参数以外的其他查询参数。

## 使用Safari在iOS上从TVSDK插入广告 {#section_250E493A125E4F82940D19C7DA2AAB2E}

使用Safari浏览器且基于iOS上Primetime TVSDK的播放器必须指定 `ptplayer` 和 `live` 参数以及基本查询参数。

清单服务器识别 `ptplayer` 值 `ios-mobileweb` 并从返回的广告拼接清单中去除前置广告。

此 `live` 参数告知清单服务器是返回实时内容还是VOD内容。

以下是一个示例URL，其中显示了与使用Safari的iOS相关的参数：

```URL
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## 使用自定义广告提示格式的广告插入 {#section_82AF880AAABE4BD4B593D906434D4D89}

Adobe提供它在Primetime包中不直接支持的广告提示格式的名称。 要使用这种格式，请提供其Adobe提供的名称作为 `ptcueformat` 参数。

以下是一个指定自定义广告提示格式的URL示例：

```URL
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## 使用广告提示为VOD创建FreeWheel时间线的广告插入 {#section_E0D830F5EEE24639819B975B90F6999F}

对于包含要解析的广告提示并包含在FreeWheel广告请求中的VOD内容，请将 `ptcueformat` 参数至 `DPIsimple`.

以下是一个URL示例，它指定使用FreeWheel时间轴进行VOD：

```URL
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## 使用自定义VOD时间轴进行广告插入 {#section_F398F7659164463FA886A4CC787C7B5A}

要要求清单服务器根据您提供的时间轴将广告插入VOD内容，请将 `pttimeline` 指定时间线的字符串的参数。 参见 [VOD时间线格式](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md).

以下是一个使用自定义时间轴进行VOD的示例URL：

```URL
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

它指定一段时间的初始中断，这段时间最多包含两个广告，随后是两分钟的内容区段，随后是最多包含两个广告的30秒中断，最后是五分钟的内容区段。

VOD内容的自定义内容时间轴的广告拼接行为如下：

* 广告会显示在广告服务器指定的广告投放时间后最接近的广告时间边界处。

* 区段的长度至少为两秒。

## 授权TS段 {#section_BF855A4399DC42CB8C0586113A416BBC}

Adobe仅对Akamai CDN支持此功能。 HTTP实时流(HLS)使用流级别的M3U8播放列表提供传输流(TS)区段。 在变体M3U8播放列表中向客户端提供了多个流级播放列表。 客户端从变体列表中选择一个播放列表流，然后逐一下载该流级别播放列表中的TS区段。 在正常操作中，请求的内容可能需要Cookie授权，清单服务器会在后台以不可见方式处理该授权。 它从原始内容中提取Cookie，并将适当的令牌附加到URL中，以用于请求选定的播放列表流。

当BootstrapURL查询参数包括 `pttoken=true`，发布者要求在请求每个TS区段时都使用一个Cookie，而不是只为整个流使用一次。 清单服务器将此Cookie作为查询参数附加到它发送回的流播放列表中的每个TS区段URL。

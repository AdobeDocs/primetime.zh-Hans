---
description: 查询参数告诉清单服务器发送请求的客户端类型以及客户端希望清单服务器执行的操作。 有些是必需的，有些具有特定的可接受格式或值。
seo-description: 查询参数告诉清单服务器发送请求的客户端类型以及客户端希望清单服务器执行的操作。 有些是必需的，有些具有特定的可接受格式或值。
seo-title: 清单服务器查询参数
title: 清单服务器查询参数
uuid: 03632da3-ae20-427c-bd24-4794ab627cc8
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 0%

---


# 清单服务器查询参数 {#manifest-server-query-parameters}

查询参数告诉清单服务器发送请求的客户端类型以及客户端希望清单服务器执行的操作。 有些是必需的，有些具有特定的可接受格式或值。

完整的URL由基URL后跟问号和参数组成， `parameterName=value` 以和号分隔： `Base URL?name1=value1&name2=value2& . . .&name n=value n`

## 可识别的参数 {#section_072845B7FA94468C8068E9092983C9E6}

清单服务器识别以下参数。 它处理它们或将它们连同所有无法识别的参数一起传递到广告服务器。

| 密钥 | 说明 | 必需 | 有效值 |
|--- |--- |--- |--- |
| `__sid__` | 清单服务器用于生成会话ID的唯一ID。 | 是 | 字母数字 |
| g | 客户端设备类型 | 当定位规则取决于设备类型时 | 查看客户端 [类型的列表](https://adobeprimetime.zendesk.com) （需要Zendesk访问） |
| k | 自定义广告定位的关键字 | 否 | 格式为key1=value1;key2=value2；的URL安全字符串。.. |
| u | Primetime广告插入资产ID。 | 是 | MD5哈希值 |
| z | 资产的Primetime广告插入区域ID。 | 是 | 整数 |
| enableC3 | 客户端位于C3窗口中。 如果为true，则仅替换本地可用内容；否则，替换所有可用内容。 | 否 | 布尔值 |
| live | 指示内容是实时流还是VOD（视频点播）流。 | Akamai Ad Scaler或iOS Safari客户端 | 布尔值 |
| pabimode | [启用部分广告分段插入](../../msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) 支持如果为true则启用，如果为false则禁用开始 | 否（默认为禁用） | 开始、true或false |
| ptadwindow | 广告拼接窗口的持续时间（秒）:当DVR用户加入流时，查找广告的距离会有多远？ | 否（默认值= 1800） | 0至1800 |
| ptassetid | 由发布者分配和维护的内容的唯一ID。 | Akamai Ad Scaler | URL安全字符串 |
| ptcdn | 列表一个或多个CDN以托管转码资源。 请参 [阅多CDN支持](../../creative-repackaging-service/multi-cdn-supportt.md)。 | 否（默认=Akamai） | 示例：Akamai、Level3、Limelight、Comcast |
| ptcuformat | M3U8中存在的自定义广告提示格式的名称。 | 否 | DPISimple、DPIScte35、Elemental、NBC、NFL或Turner |
| ptfailover | 指示清单服务器识别在主控播放列表中指定的主流和故障转移流，并将它们视为不相交集。 这便于故障转移并防止时间错误。 （仅适用于Apple HLS设备。） 请参 [阅促进HLS播放器切换](../../msapi-topics/ms-insert-ads/hls-switching-to-failover.md) 。 | 否 | 真 |
| ptmulticall | 如果设置为true，则为FER发出多个Auditude广告调用；每个广告休息一次。  如果缺失或设置为false，则向FER的auditude发出一个广告呼叫。 | 否 | 布尔注： 以下要求： <ul><li>ptcueformat参数必须设置为nbc</li><li>将忽略pttimeline参数。</li></ul> |
| ptplayer | 请求的玩家。 | iOS/Safari | ios-mobileweb |
| ptrendition | 由广告插入自动生成并由Akamai使用。 请勿添加或删除。 | Akamai Ad Scaler |  |
| pttagds | 启 [用EXT-X-不连续——序列标签](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) | 否 | true —— 清单服务器在其发送的每个m3u8文件中的内容之前都包含序列标签；如果参数不存在或不为true，则清单服务器不包括序列标签。 |
| pttimeline | 包含广告放置和内容所需时间线的字符串，它覆盖内容流中的广告分段。 | 否 | VOD时间轴(请参 [阅VOD时间轴格式](../../msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)) |
| pttoken | 启用TS段授权令牌注意： 仅支持Akamai CDN令牌 | 对于TS段授权令牌 | 布尔值 |
| pttrackingmode | 启用广告跟踪；自定义客户端(simple)、服务器端(sstm)或混合(simplestm)。 | 否 | simple 、 sstm或simplesstm注释： 如果未包含此参数，则#EX-X-MARKER将注入清单中。 请参 [阅EXT-X-MARKER指令](../../msapi-topics/ms-at-effectiveness/ms-api-playlists.md)。 |
| pttrackposition | 指示清单服务器仅返回广告跟踪信息。 请勿在引导请求中指定此参数。 | 客户端跟踪 | 字母数字注释： 清单服务器忽略所有传递的值。 但是，如果传递空字符串或空字符串，清单服务器将返回M3U8而不是跟踪信息。 |
| pttrackversion | 客户端跟踪信息的格式版本。 | 客户端跟踪 | v1、v2、v3或vmap |
| scteTracking | 获取M3U8，然后在JSON V2附加项中获取SCTE跟踪信息。  <br/>此参数向清单服务器指示获取M3U8的播放器需要检索SCTE标记信息。 | 否(默认值： false) | true或false注释： 在JSON附加项中，SCTE-35数据会使用以下查询参数值组合返回： <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35` </li><li>pttrackingversion=v2 </li><li>scteTracking=true</li></ul> |
| vetargetmultiplier | 起始点的段数预卷偏移使用以下方式进行配置：  `(  vetargetmultiplier  *  targetduration ) +  vebufferlength`  <br/><br/>**注意**: 仅实时／线性 | 否(默认值： 3.0) | 浮动 |
| vebufferLength | 从实时点开始的秒数备注： 仅实时／线性 | 否(默认值： 3.0) | 浮动 |

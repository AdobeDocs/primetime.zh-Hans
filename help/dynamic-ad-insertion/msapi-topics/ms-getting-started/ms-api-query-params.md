---
description: 查询参数告知清单服务器发送请求的客户机类型以及客户机希望清单服务器执行的操作。 有些是必需的，有些具有特定的可接受格式或值。
seo-description: 查询参数告知清单服务器发送请求的客户机类型以及客户机希望清单服务器执行的操作。 有些是必需的，有些具有特定的可接受格式或值。
seo-title: 清单服务器查询参数
title: 清单服务器查询参数
uuid: 03632da3-ae20-427c-bd24-4794ab627cc8
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# 清单服务器查询参数 {#manifest-server-query-parameters}

查询参数告知清单服务器发送请求的客户机类型以及客户机希望清单服务器执行的操作。 有些是必需的，有些具有特定的可接受格式或值。

完整的URL由基本URL和问号组成，后跟参数， `parameterName=value` 以&amp;符分隔： `Base URL?name1=value1&name2=value2& . . .&name n=value n`

## 可识别的参数 {#section_072845B7FA94468C8068E9092983C9E6}

清单服务器可识别以下参数。 它会处理它们或将它们连同所有无法识别的参数一起传递给广告服务器。

| 密钥 | 说明 | 必需 | 有效值 |
|--- |--- |--- |--- |
| `__sid__` | 清单服务器用于生成会话ID的唯一ID。 | 是 | 字母数字 |
| g | 客户端设备类型 | 当定位规则取决于设备类型时 | 查看客户端类 [型列表](https://adobeprimetime.zendesk.com) （需要Zendesk访问） |
| k | 自定义广告定位的关键字 | 否 | 格式为key1=value1;key2=value2；的URL安全字符串。.. |
| u | Primetime广告插入资产ID。 | 是 | MD5哈希值 |
| z | 资产的Primetime广告插入区域ID。 | 是 | 整数 |
| enableC3 | 客户端位于C3窗口中。 如果为true，则仅替换本地可用内容；否则，替换所有可用内容。 | 否 | Boolean |
| live | 指示内容是实时流还是VOD（视频点播）流。 | Akamai Ad Scaler或iOS Safari客户端 | Boolean |
| pabimode | [启用部分广告插入支持](../../msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) “如果为true则启用”或“如果为false则启动禁用” | 否（默认为禁用） | start 、 true或false |
| ptadwindow | 广告拼接窗口的持续时间（秒）:DVR用户加入流时查找广告的距离。 | 否（默认值= 1800） | 0至1800 |
| ptassetid | 由发布者分配和维护的内容的唯一ID。 | Akamai Ad Scaler | URL安全字符串 |
| ptcdn | 用于托管转码资源的一个或多个CDN的列表。 请参阅 [多CDN支持](../../creative-repackaging-service/multi-cdn-supportt.md)。 | 否(default=Akamai) | 示例：Akamai、Level3、Limelight、Comcast |
| ptcuformat | M3U8中存在的自定义广告提示格式的名称。 | 否 | DPISimple、DPIScte35、Elemental、NBC、NFL或Turner |
| ptfailover | 向清单服务器发出信号，以标识主播放列表中指定的主流和故障转移流，并将它们视为不相交集。 这便于故障转移并防止定时错误。 （仅适用于Apple HLS设备。）请参阅 [促进HLS播放器切换](../../msapi-topics/ms-insert-ads/hls-switching-to-failover.md) 。 | 否 | true |
| ptmulticall | 如果设置为true，则多次向FER发出Auditude广告调用；每个广告中断一个。  如果缺席或设置为false，则向FER的auditude发出一个广告呼叫。 | 否 | 布尔注释： 以下要求： <ul><li>ptcueformat参数必须设置为nbc</li><li>将忽略pttimeline参数。</li></ul> |
| ptplayer | 播放器发出请求。 | iOS/Safari | ios-mobileweb |
| ptrendition | 由广告插入自动生成并由Akamai使用。 请勿添加或删除。 | Akamai Ad Scaler |  |
| pttagds | 启 [用EXT-X-不连续序列标签](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) | 否 | true - manifest服务器在其发送的每个m3u8文件中的内容之前都包含一个序列标签；如果参数不存在或不为true，则清单服务器不包括序列标签。 |
| pttimeline | 包含广告放置和内容所需时间线的字符串，该字符串会覆盖内容流中的广告分段。 | 否 | VOD时间轴(请参阅 [VOD时间轴格式](../../msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)]) |
| pttoken | 启用TS区段授权令牌注意： 仅支持Akamai CDN令牌 | 对于TS段授权令牌 | Boolean |
| pttrackingmode | 启用广告跟踪；自定义客户端（简单）、服务器端(sstm)或混合（简单）。 | 否 | simple、sstm或simplesstm注意： 如果未包含此参数，则#EX-X-MARKER将注入清单中。 请参 [阅EXT-X-MARKER指令](../../msapi-topics/ms-at-effectiveness/ms-api-playlists.md)。 |
| pttrackposition | 指示清单服务器仅返回广告跟踪信息。 请勿在引导请求中指定此参数。 | 客户端跟踪 | 字母数字注意事项： 清单服务器忽略所有传递的值。 但是，如果传递空字符串或空字符串，则清单服务器返回M3U8而不是跟踪信息。 |
| pttrackingversion | 客户端跟踪信息的格式版本。 | 客户端跟踪 | v1、v2、v3或vmap |
| scteTracking | 获取M3U8，然后在JSON V2附加项中获取SCTE跟踪信息。  <br/>此参数向清单服务器指示获取M3U8的播放器需要检索SCTE标签信息。 | 否(默认： false) | true或false注释： SCTE-35数据在JSON附加项中返回，并包含以下查询参数值组合： <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35` </li><li>pttrackingversion=v2 </li><li>scteTracking=true</li></ul> |
| vetargetmultiplier | 起始点的段数预卷偏移是使用以下方式配置的：  `(  vetargetmultiplier  *  targetduration ) +  vebufferlength` 注 <br/><br/>**意&#x200B;**: 仅实时／线性 | 否(默认： 3.0) | 浮动 |
| vebufferLength | 从实时点开始的秒数注意： 仅实时／线性 | 否(默认： 3.0) | 浮动 |

---
title: 清单服务器查询参数
description: 查询参数告诉清单服务器客户端发送请求的类型以及客户端希望清单服务器执行的操作。 有些是必需的，有些具有特定的可接受格式或值。
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---


# 清单服务器查询参数{#ms-query-params}

查询参数告诉清单服务器客户端发送请求的类型以及客户端希望清单服务器执行的操作。 有些是必需的，有些具有特定的可接受格式或值。

完整的URL由基URL后跟问号、`parameterName=value`参数组成，以&amp;符号分隔：`Base URL?name1=value1&name2=value2& . . .&name n=value n`。

## 可识别的参数{#section_072845B7FA94468C8068E9092983C9E6}

清单服务器可识别以下参数。 它处理它们或将它们以及所有无法识别的参数传递给广告服务器。

| 键 | 说明 | 必需 | 有效值 |
|---|---|---|---|
| `__sid__` | 清单服务器用于生成会话ID的唯一ID。 | 是 | 字母数字 |
| g | 客户端设备类型 | 当定位规则取决于设备类型时 | 请参阅[客户端类型](https://adobeprimetime.zendesk.com)中的列表。 需要Zendesk访问。 |
| k | 自定义广告定位的关键字 | 否 | 格式为`key1=value1;key2=value2;. . .`的URL安全字符串 |
| u | Primetime广告插入资产ID。 | 是 | MD5哈希值 |
| z | 资产的Primetime广告插入区域ID。 | 是 | 整数 |
| enableC3 | 客户端位于C3窗口中。 如果为true，则仅替换本地可用；否则，替换所有可用。 | 否 | 布尔值 |
| live | 指示内容是实时流还是VOD（视频点播）流。 | Akamai Ad Scaler或iOS Safari客户端。 | 布尔值 |
| `pabimode` | [启用部分广告中断插](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) 入支持。<br> 如果为true或开始，则启用。<br> 如果为false则禁用。 | 否（默认为禁用） | 开始、true或false |
| `ptadwindow` | 广告拼接窗口的持续时间（秒）：当DVR用户加入流时，要查找广告的时间。 | 否（默认值= 1800） | 0至1800 |
| `ptassetid` | 由发布者分配和维护的内容的唯一ID。 | 阿卡迈阿德斯卡勒 | URL安全字符串 |
| `ptcdn` | 列表一个或多个CDN以托管转码资源。 请参阅[多CDN支持](/help/primetime-ad-insertion/~old-creative-repackaging-service/multi-cdn-supportt.md)。 | 否（默认值=Akamai） | 示例：Akamai、Level3、Limelight、Comcast |
| `ptcueformat` | M3U8中存在的自定义广告提示格式的名称。 | 否 | DPISimple、DPIScte35、Elemental、NBC、NFL或Turner |
| `ptfailover` | 指示清单服务器识别在主控播放列表中指定的主流和故障转移流，并将它们视为不相交集。 这便于故障转移并防止计时错误。 （仅限Apple HLS设备）。 请参阅[促进HLS播放器切换](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/hls-switching-to-failover.md)。 | 否 | true |
| `ptmulticall` | 如果设置为true，则对FER发出多个Auditude广告调用；每个广告时段各一个。 如果缺席或设置为false，则向FER的auditude发出一个广告呼叫。 | 否 | 布尔值<br> **注意**:以下要求： <ul><li>`ptcueformat` 参数必须设置为nbc</li><li>将忽略pttimeline参数。</li></ul> |
| `ptplayer` | 发出请求的玩家。 | iOS/Safari | ios-mobileweb |
| `ptrendition` | 由广告插入自动生成并由Akamai使用。 请勿添加或删除。 | 阿卡迈阿德斯卡勒 |  |
| `pttagds` | 启用[EXT-X-DINSTRUCTION- SEQUENCE](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3)标签 | 否 | true — 清单服务器在其发送的每个m3u8文件中的内容前包含序列标签；如果参数不存在或不为true，则manifest server不包含序列标签。 |
| `pttimeline` | 包含广告投放和内容所需时间轴的字符串，它覆盖内容流中的广告分页。 | 否 | [VOD时间轴](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md) |
| `pttoken` | 启用TS区段授权令牌。<br> **注意**:仅支持Akamai CDN令牌 | 对于TS区段授权令牌 | 布尔值 |
| `pttrackingmode` | 启用广告跟踪；自定义客户端(simple)、服务器端(sstm)或混合(simplesstm)。 | 否 | simple、sstm或simplesstm.<br> **注意**:如果未包含此参数，则#EX-X-MARKER将注入清单中。请参阅[EXT-X-MARKER指令](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md)。 |
| `pttrackingposition` | 指示清单服务器仅返回广告跟踪信息。 请勿在引导请求中指定此参数。 | 客户端跟踪 | 字母数字注释： 清单服务器忽略所有传递的值。 但是，如果传递空字符串或空字符串，则清单服务器返回M3U8而不是跟踪信息。 |
| `pttrackingversion` | 客户端跟踪信息的格式版本。 | 客户端跟踪 | v1、v2、v3或vmap |
| `scteTracking` | 在JSON V2附加项中获取SCTE跟踪信息之前，获取M3U8。 <br>此参数向清单服务器指示获取M3U8的播放器需要检索SCTE标记信息。 | 否(默认：false) | 真或假。<br> **注意**:SCTE-35数据在JSON附加项中返回，并包含以下查询参数值组合： <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35`</li><li>`pttrackingversion=v2`</li><li>`scteTracking=true`</li></ul> |
| `vetargetmultiplier` | 起始点的段数预卷偏移是使用以下方式配置的：`(vetargetmultiplier * targetduration + vebufferlength`<br/><br/>**注意**: 仅实时/线性 | 否(默认： 3.0) | 浮动 |
| `vebufferLength` | 从实时点开始的秒数。 **注意**:仅限实时/线性。 | 否(默认：3.0) | 浮动 |

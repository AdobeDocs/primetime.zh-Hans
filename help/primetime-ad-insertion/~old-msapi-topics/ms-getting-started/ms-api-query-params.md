---
title: 清单服务器查询参数
description: 查询参数告知清单服务器发送请求的客户端的类型以及该客户端希望清单服务器执行的操作。 有些是必需的，有些具有特定的可接受格式或值。
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---


# 清单服务器查询参数 {#ms-query-params}

查询参数告知清单服务器发送请求的客户端的类型以及该客户端希望清单服务器执行的操作。 有些是必需的，有些具有特定的可接受格式或值。

完整的URL由基本URL和问号组成，然后 `parameterName=value` 参数，以&amp;号分隔： `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

## 已识别的参数 {#section_072845B7FA94468C8068E9092983C9E6}

清单服务器可识别以下参数。 它会处理这些参数，或将它们以及所有无法识别的参数传递给广告服务器。

| 键 | 描述 | 必需 | 有效值 |
|---|---|---|---|
| `__sid__` | 清单服务器用于生成会话ID的唯一ID。 | 是 | 字母数字 |
| g | 客户端设备类型 | 当定位规则取决于设备类型时 | 查看列表位置 [客户端类型](https://adobeprimetime.zendesk.com). 需要Zendesk访问权限。 |
| k | 自定义广告定位的关键字 | 否 | 格式中的URL安全字符串 `key1=value1;key2=value2;. . .` |
| u | Primetime广告插入资产ID。 | 是 | MD5哈希值 |
| z | 资源的Primetime广告插入区域ID。 | 是 | 整数 |
| enableC3 | 客户端位于C3窗口中。 如果为true，则仅替换本地可用；否则，替换所有可用。 | 否 | 布尔型 |
| 实时 | 指示内容是实时流还是VOD（视频点播）流。 | Akamai Ad Scaler或iOS Safari客户端。 | 布尔型 |
| `pabimode` | [启用部分广告时间插入](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) 支持。 <br> 如果为true或开始，则启用。<br> 如果为false，则禁用。 | 否（默认处于禁用状态） | start、true或false |
| `ptadwindow` | 广告拼接窗口的持续时间（秒）：当DVR用户加入流时，要回溯多久才能查找广告。 | 否（默认值= 1800） | 0至1800 |
| `ptassetid` | 发布者分配和维护的内容的唯一ID。 | Akamai Ad Scaler | URL安全字符串 |
| `ptcdn` | 托管转码资产的一个或多个CDN的列表。 参见 [多CDN支持](/help/primetime-ad-insertion/~old-creative-repackaging-service/multi-cdn-supportt.md). | 否（默认=Akamai） | 示例： Akamai、Level3、Limelight、Comcast |
| `ptcueformat` | M3U8中存在的自定义广告提示格式的名称。 | 否 | DPISimple、DPIScte35、Elemental、NBC、NFL或Turner |
| `ptfailover` | 指示清单服务器识别主控播放列表中指定的主流和故障转移流，并将其视为不相交集。 这有助于故障切换并防止计时错误。 (仅适用于Apple HLS设备)。 参见  [促进HLS播放器切换](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/hls-switching-to-failover.md). | 否 | true |
| `ptmulticall` | 如果设置为true，则会对FER进行多次auditude广告调用；每次广告时间各调用一次。 如果不存在或设置为false，则会发起一个广告调用以审核FER。 | 否 | 布尔型 <br> **注释**：以下要求： <ul><li>`ptcueformat` 参数必须设置为nbc</li><li>pttimeline参数将被忽略。</li></ul> |
| `ptplayer` | 发出请求的播放器。 | iOS/Safari | ios-mobileweb |
| `ptrendition` | 由广告插入自动生成，供Akamai使用。 请勿添加或删除。 | Akamai Ad Scaler |  |
| `pttagds` | 启用 [EXT-X — 间断 — 序列](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) 标记 | 否 | true — 清单服务器在其发送的每个m3u8文件中的内容之前包含一个序列标记；如果参数不存在或不为true，则清单服务器不包含序列标记。 |
| `pttimeline` | 一个字符串，其中包含广告投放和内容的所需时间轴，可覆盖内容流中的广告时间。 | 否 | [VOD时间线](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md) |
| `pttoken` | 启用TS区段授权令牌。<br> **注释**：仅支持Akamai CDN令牌 | 对于TS区段授权令牌 | 布尔型 |
| `pttrackingmode` | 启用广告跟踪；自定义客户端（简单）、服务器端(sstm)或混合（简单）。 | 否 | simple、sstm或simplesstm。<br> **注释**：如果未包含此参数，则将#EX-X-MARKER插入到清单中。 参见 [EXT-X-MARKER指令](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md). |
| `pttrackingposition` | 指示清单服务器仅返回广告跟踪信息。 请勿在引导请求中指定此参数。 | 客户端跟踪 | 字母数字注意：清单服务器会忽略所有传递的值。 但是，如果传递null或空字符串，清单服务器将返回M3U8，而不是跟踪信息。 |
| `pttrackingversion` | 客户端跟踪信息的格式版本。 | 客户端跟踪 | v1、v2、v3或vmap |
| `scteTracking` | 先获取M3U8 ，然后才能在JSON V2侧栏中获取SCTE跟踪信息。 <br>此参数向清单服务器指示获取M3U8的播放器需要检索SCTE标记信息。 | 否（默认值： false） | true或false。 <br> **注释**：SCTE-35数据使用以下查询参数值组合在JSON侧边栏中返回： <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35`</li><li>`pttrackingversion=v2`</li><li>`scteTracking=true`</li></ul> |
| `vetargetmultiplier` | 实时点中的区段数使用以下方式配置前置式偏移： `(vetargetmultiplier * targetduration + vebufferlength`<br/><br/>**注释**：仅限实时/线性 | 否（默认值： 3.0） | 浮点数 |
| `vebufferLength` | 从实时点开始的秒数。 **注释**：仅限实时/线性。 | 否（默认值： 3.0） | 浮点数 |

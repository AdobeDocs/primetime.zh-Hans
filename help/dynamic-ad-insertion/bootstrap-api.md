---
title: BootstrapAPI
description: null
translation-type: tm+mt
source-git-commit: aa43834fea161c537c448b7616c9bd8f779d1a74
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---


# BootstrapAPI {#bootstrap-api}

必需参数生成引导

## 参数描述 {#parameter-description}

| 参数 | 描述 | 格式 |
|---|---|---|
| pabimode | 支持 [实时流的部分广告](ad-insertion-live-linear-stream.md#partial-ad-break-support) 中断插入。 可能的值：true to enable忽略禁用（默认为禁用） | HLS/DASH |
| ptadwindow | 回顾广告决策窗口的持续时间（以秒为单位）- PrimetimeAd Insertion在DVR用户加入流时将查找广告提示的时长。 值为零将禁用初始清单中的中间广告决策，并且决策仅在第一次更新后恢复。 此参数可用于禁用广告插入只能持续几秒钟的会话(又称渠道翻转)。 可能的值：数字字符串0-1800（默认值1800） | 仅HLS |
| ptassetid | 由发布者分配和维护的内容的唯一ID。  与Akamai Ad Scaler一起使用时需要。 | HLS/DASH |
| ptcdn | 列表一个或多个CDN以托管转码资源。 有关详细信息，请参 [阅多CDN支持](multi-cdn-support.md)。 可能的值：akamai、level3、lnw(limelight networks)、comcast默认情况下，使用PrimetimeAd InsertionCDN | HLS/DASH |
| ptcuformat | 要执行广告决策的指定标记格式（例如，scte35）。 可能的值：dpisimple, dpiscte35, elemental对于自定义提示格式，请联系您的技术帐户代表以获取用于您的用例的值。 | HLS/DASH |
| ptfailover | 指示清单服务器识别在主控播放列表中指定的主流和故障转移流，并将它们视为不相交集。 这便于故障转移并防止时间错误。 （仅适用于Apple HLS设备。） 有关详细信息，请参 [阅促进HLS播放器切换](hls-switching-to-failover.md) | 仅HLS |
| ptmulticall | 如果启用此功能，则会针对VOD资产中的每个可用内容单独发出广告请求。  默认情况下，PrimetimeAd Insertion将尝试收集所有可用信息，并在一个请求中将其发送到广告服务器。 可能的值：true to enable忽略禁用（默认为禁用） | HLS/DASH |
| pttagds | 启用将EXT-X-DINSTRUCTION-SEQUENCE标记注入HLS头中。可能的值：true可启用禁用（默认禁用） | 仅HLS |
| pttimeline | 包含广告放置和内容所需时间线的字符串，它覆盖内容流中的广告分段。 [ 查看VOD时间轴格式 ] | HLS/DASH |
| pttoken | 为CDN启用内容片段／段授权令牌保护方案可能的值：akamai、lnw(limelight)、ctl(centurylink)（默认的tokenization被禁用） | HLS/DASH |
| pttrackingmode | 启用广告跟踪方案：可能的值：对于服务器端广告跟踪stm来说很简单，对于服务器端广告跟踪来说很简单，对于混合客户端／服务器广告跟踪来说则很简单（默认情况下，不执行广告跟踪） | HLS/DASH |
| pttrackversion |  |  |
| ptadtimeout（如20.9.2所示） |  |  |
| ptparallstream（如20.9.3中所示） |  |  |

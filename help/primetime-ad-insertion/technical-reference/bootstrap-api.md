---
title: BOOTSTRAPAPI
description: BOOTSTRAPAPI
exl-id: bc7fe244-8664-43ac-b9a1-3967ea8749b1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---

# BOOTSTRAPAPI {#bootstrap-api}

BootstrapAPI通常是发送到客户端/视频播放API的URL。  有关可配置的选项和参数，请参阅 [BootstrapAPI参数](#bootstrap-api-parameters).

## 向清单服务器发送命令 {#send-a-command-to-the-manifest-server}

1. 发送 `HTTP GET` 请求使用以下模式构建的引导URL：

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]
    ?{query parameters}
   ```

   * **文件扩展名** 已定义。 `.m3u8` 如果目标清单是HLS， `.mpd` 如果目标清单位于短划线中。

   * **PublisherAssetID** 必需。 特定内容的发布者唯一ID。

   * **内容URL** 必需。 内容M3U8文件的URL，在清单服务器URL中编码为安全的Base64。 内容URL必须指向变体M3U8文件，即使只有一个比特率流也是如此。

   * **查询参数** 这些构成了请求中最具多样性的部分。 它们告知清单服务器哪种客户端正在发出请求，以及它希望清单服务器做什么。

   例如：

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP与HTTPS请求**

   清单服务器使用客户端请求的相同HTTP协议创建URL。 如果播放器发出非安全HTTP (http)请求，则清单服务器会使用http协议返回清单URL和审核跟踪URL。 如果播放器建立了安全HTTP (https)连接、清单服务器，则会通过https协议返回清单URL和审核跟踪URL。

   >[!NOTE]
   >
   >清单服务器无法更改第三方跟踪信标的协议（HTTP或HTTPS）。 您必须联系内容和第三方广告提供商，以便他们配置所需的协议。  可以更改区段URL协议，但是，默认情况下，使用目标清单中定义的相同协议。

## BootstrapAPI参数 {#bootstrap-api-parameters}

查询参数告知清单服务器发送请求的客户端的类型以及该客户端希望清单服务器执行的操作。 有些是必需的，有些具有特定的可接受格式或值。
完整的URL由基本URL和问号组成，然后 `parameterName=value` 用&amp;符号分隔的参数。 例如， `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

清单服务器可识别以下参数。 所有查询字符串\
参数将传递到广告服务器。

| 参数 | 描述 | 格式 |
|---|---|---|
| _sid_ | 清单服务器将用于生成会话ID的唯一ID。 | 对于DASH/HLS都是必需的 |
| 实时 | 通知PrimetimeAd Insertion传递的内容项是实时流。  如果未传递此参数，则Primetime Ad insertion将在初始清单调用中发起辅助请求，以确定清单是live还是vod。<br>可能的值：<br>对于实时内容为true<br>对于vod内容，为false<br>省略以进行自动检测 | 对于HLS，它是可选项。  短划线必需 |
| z | 需要提供给PrimetimeAd Insertion的资源的区域ID。 由您的Adobe技术客户经理提供。 | 对于DASH/HLS都是必需的 |
| pabimode | 启用 [部分广告时间插入](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md#partial-ad-break-support) 用于实时流。<br>可能的值：<br>true表示启用<br>省略以禁用（默认禁用） | HLS/短划线 |
| ptadtimeout | 如果下游提供商响应时间过长，则启用对整体广告解析时间的限制。  长时间运行的响应可能会导致播放问题，这允许Primetime DAI强制在特定时间限制内进行响应。<br>可能的值：<br>以毫秒为单位的数字字符串。<br>省略以禁用（默认禁用） | HLS/短划线 |
| 路径窗口 | 回顾广告决策窗口的持续时间（以秒为单位） — PrimetimeAd Insertion在DVR用户加入流时将查找广告提示的时长。 如果值为零，则会在初始清单中禁用中置广告决策，并且仅在首次更新后恢复决策。 此参数可用于禁用在可能仅持续几秒的会话中进行广告插入（也称为频道翻转）。<br>可能的值：<br>数字字符串0-1800（默认为1800） | 仅限HLS |
| ptassetid | 发布者分配和维护的内容的唯一ID。  在与Akamai Ad Scaler一起使用时需要。 | HLS/短划线 |
| ptcdn | 托管转码资产的一个或多个CDN的列表。 有关更多信息，请参阅 [交付和存储](/help/primetime-ad-insertion/just-in-time-transcoding/delivery-and-storage.md).<br>可能的值：<br>akamai、level3、llnw(limelight networks)、comcast。<br>默认情况下，使用PrimetimeAd InsertionCDN。 | HLS/短划线 |
| ptcueformat | 用于执行广告决策的指定标记格式（例如，scte35）。<br>可能的值：<br>dpimple， dpiscte35， elements<br>对于自定义提示格式，请联系您的技术客户代表，以获取用于用例的值 | HLS/短划线 |
| ptfailover | 指示清单服务器识别主控播放列表中指定的主流和故障转移流，并将其视为不相交集。 这有助于故障切换并防止计时错误。 (仅适用于Apple HLS设备。) 有关更多信息，请参阅 [促进HLS播放器切换](hls-switching-to-failover.md) | 仅限HLS |
| ptmulticall | 如果启用，则会为VOD资源中的每项可用内容发出单独的广告请求。  默认情况下，PrimetimeAd Insertion将尝试收集所有可用信息，并在一次请求中将其发送到广告服务器。 可能的值：true表示启用， <br>省略以禁用（默认禁用） | HLS/短划线 |
| ptparallelstream | 允许播放器同时请求CMAF去模糊音频或视频流的客户确保音频和视频曲目中的广告一致。 | 仅限HLS |
| ptprotoswitch | 启用指定的清单重写规则和广告提取规则，这些规则通常由技术支持代表进行设置。<br>示例： adfetch_fw， cdn_akm | HLS/短划线 |
| pttagds | 允许将EXT-X-DISCONTINUITY-SEQUENCE标记插入到HLS标头中。可能的值：true表示允许禁用（默认禁用） | 仅限HLS |
| pttimeline | 一个字符串，其中包含广告投放和内容的所需时间轴，可覆盖内容流中的广告时间。 [ 请参阅VOD时间线格式 ] | HLS/短划线 |
| pttoken | 为CDN启用内容片段/区段授权令牌保护方案<br>可能的值：<br>akamai、llnw (limelight)、ctl (centurylink)（默认标记化处于禁用状态） | HLS/短划线 |
| pttrackingmode | 启用广告跟踪方案。<br>可能的值：<br>适用于客户端广告跟踪的简单方法<br>用于服务器端广告跟踪的sstm<br>简化客户端/服务器混合广告跟踪（默认情况下，不执行广告跟踪） | HLS/短划线 |
| pttrackingposition | 指示清单服务器仅返回广告跟踪信息。 请勿在引导请求中指定此参数。<br>注意：清单服务器将忽略所有传递的值。 但是，如果传递null或空字符串，清单服务器将返回M3U8 | HLS/短划线<br>客户端跟踪 |
| pttrackingversion | 设置要返回的格式版本。<br>可能的值：<br>v1、v2、v3或vmap | HLS/短划线<br>客户端跟踪 |
| sctetracking | 此参数向清单服务器指示获取M3U8的播放器需要检索SCTE标记信息。<br>可能的值：<br>true或false（默认false）<br>注意：SCTE-35数据在JSON侧边栏中返回，并包含以下查询参数值组合：<br>ptcueformat=turner | 元素 | nfl | DPIScte35<br>pttrackingversion=v2<br>sctetracking=true<br> | 仅限HLS |
| vetargetmultiplier | 来自实时点的区段数预滚偏移量的配置方式： ( vetargetmultiplier * targetduration ) + vebufferlength<br>注意：此参数仅适用于实时/线性HLS流<br>可能的值：<br>数值浮点数<br>（默认值： 3.0 — 与HLS规范相同） | 仅限HLS |
| vebufferLength | 从实时点开始的秒数，与vetargetmultiplier结合使用。<br>注意：此参数仅适用于实时/线性HLS流<br>可能的值：<br>数值浮点数<br>（默认值： 3.0） | 仅限HLS |

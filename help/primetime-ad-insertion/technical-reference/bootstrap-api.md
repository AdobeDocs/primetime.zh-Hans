---
title: BootstrapAPI
description: 'BootstrapAPI '
translation-type: tm+mt
source-git-commit: bf99c76bbbb67560adc675cf84297b8d3b04e19d
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---


# BootstrapAPI {#bootstrap-api}

BootstrapAPI通常是发送到客户端／视频播放API的URL。  有关可配置的选项和参数，请参阅[BootstrapAPI参数](#bootstrap-api-parameters)。

## 向清单服务器{#send-a-command-to-the-manifest-server}发送命令

1. 发送`HTTP GET`请求以使用以下模式构建的引导URL:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]
    ?{query parameters}
   ```

   * **文件扩** 展已定义。`.m3u8` 如果目标清单是HLS, `.mpd` 则目标清单在DASH中。

   * **需** 要PublisherAssetIDR。特定内容的发布者唯一ID。

   * **需要** 内容URLR。内容M3U8文件的URL,Base64编码为在清单服务器URL中是安全的。 内容URL必须指向变型M3U8文件，即使只有一个比特率流也是如此。

   * **查询** 参数这些参数构成请求中最多变的部分。它们告诉清单服务器发出请求的客户端类型以及清单服务器希望执行什么操作。

   例如：

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP与HTTPS请求**

   清单服务器使用客户端请求的相同HTTP协议创建URL。 如果播放器发出非安全HTTP(http)请求，清单服务器会使用http协议返回清单URL和Auditude跟踪URL。 如果播放器建立安全的HTTP(https)连接，清单服务器，则它会返回使用https协议的清单URL和Auditude跟踪URL。

   >[!NOTE]
   >
   >清单服务器无法更改第三方跟踪信标的协议（HTTP或HTTPS）。 您必须联系内容和第三方广告提供商，让他们配置所需的协议。  区段URL协议可以更改，但默认情况下，使用在目标清单中定义的相同协议。

## BootstrapAPI参数{#bootstrap-api-parameters}

查询参数告诉清单服务器发送请求的客户端类型以及客户端希望清单服务器执行的操作。 有些是必需的，有些具有特定的可接受格式或值。
完整的URL由基本URL后跟问号，然后由&amp;符分隔的`parameterName=value`参数组成。 例如，`Base URL?name1=value1&name2=value2& . . .&name n=value n`。

清单服务器识别以下参数。 所有查询字符串\
参数将传递给广告服务器。

| 参数 | 描述 | 格式 |
|---|---|---|
| _sid_ | 清单服务器将用于生成会话ID的唯一ID。 | DASH/HLS都必需 |
| live | 通知PrimetimeAd Insertion已传递的内容项是实时流。  如果未传递此参数，Primetime广告插入将对初始清单调用发出次要请求，以确定清单是实时清单还是vod。<br>可能的值：<br>实时内容<br>为true自动<br>检测vod内容为false | HLS为可选。  DASH必需 |
| z | 需要提供给PrimetimeAd Insertion的资产的区域ID。 由Adobe技术客户经理提供。 | DASH/HLS都必需 |
| pabimode | 为实时流启用[部分广告中断插入](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md#partial-ad-break-support)。<br>可能的值：<br>true to <br>enableomit to disable（默认为禁用） | HLS/DASH |
| ptadtimeout | 如果下游提供商响应时间过长，则允许限制整体广告分辨时间。  长时间运行的响应可能导致播放问题，这使Primetime DAI能够在特定时间限制内强制响应。<br>可能的值：数<br>字字符串（以毫秒为单位）。<br>忽略以禁用（默认为禁用） | HLS/DASH |
| ptadwindow | 回顾广告决策窗口的持续时间（以秒为单位）- PrimetimeAd Insertion在DVR用户加入流时将查找广告提示的时长。 值为零将禁用初始清单中的中间广告决策，并且决策仅在第一次更新后恢复。 此参数可用于禁用广告插入只能持续几秒钟的会话(又称渠道翻转)。<br>可能的值：<br>数字字符串0-1800（默认值1800） | 仅HLS |
| ptassetid | 由发布者分配和维护的内容的唯一ID。  与Akamai Ad Scaler一起使用时需要。 | HLS/DASH |
| ptcdn | 列表一个或多个CDN以托管转码资源。 有关详细信息，请参阅[投放和存储](/help/primetime-ad-insertion/just-in-time-transcoding/delivery-and-storage.md)。<br>可能的值<br>:akamai、level3、lnw(limelight networks)、comcast。<br>默认情况下，使用PrimetimeAd InsertionCDN。 | HLS/DASH |
| ptcuformat | 要执行广告决策的指定标记格式（例如，scte35）。<br>可能的值：<br>dpisimple、dpiscte35、elemental<br>对于自定义提示格式，请与技术帐户代表联系以获取用于您的用例的值 | HLS/DASH |
| ptfailover | 指示清单服务器识别在主控播放列表中指定的主流和故障转移流，并将它们视为不相交集。 这便于故障转移并防止时间错误。 （仅适用于Apple HLS设备。） 有关详细信息，请参阅[促进HLS播放器切换](hls-switching-to-failover.md) | 仅HLS |
| ptmulticall | 如果启用此功能，则会针对VOD资产中的每个可用内容单独发出广告请求。  默认情况下，PrimetimeAd Insertion将尝试收集所有可用信息，并在一个请求中将其发送到广告服务器。 可能的值：true可启用， <br>忽略可禁用（默认禁用） | HLS/DASH |
| ptparallestream | 允许具有请求CMAF的播放器的客户同时消除音频或视频流的混音，以确保音频和视频轨道中的广告保持一致。 | 仅HLS |
| pt协议 | 启用指定清单重写规则和广告获取规则，通常由技术支持代表设置。<br>示例：adfetch_fw, cdn_akm | HLS/DASH |
| pttagds | 启用将EXT-X-DINSTRUCTION-SEQUENCE标记注入HLS头中。可能的值：true可启用禁用（默认禁用） | 仅HLS |
| pttimeline | 包含广告放置和内容所需时间线的字符串，它覆盖内容流中的广告分段。 [ 查看VOD时间轴格式  ] | HLS/DASH |
| pttoken | 为CDN启用内容片段／段授权令牌保护方案<br>可能的值：<br>akamai、lnw(limelight)、ctl(centurylink)（禁用默认令牌化） | HLS/DASH |
| pttrackingmode | 启用广告跟踪方案。<br>可能的值：<br>对于服务器端和<br>跟踪客户端和跟踪来说很简<br>单，对于混合客户端／服务器广告跟踪来说很简单（默认情况下，不执行广告跟踪） | HLS/DASH |
| pttrackposition | 指示清单服务器仅返回广告跟踪信息。 请勿在引导请求中指定此参数。<br>注意：清单服务器忽略所有传递的值。但是，如果传递空字符串或空字符串，清单服务器将返回M3U8 | HLS/DASH<br>客户端跟踪 |
| pttrackversion | 设置要返回的格式版本。<br>可能的<br>值：v1、v2、v3或vmap | HLS/DASH<br>客户端跟踪 |
| scteTracking | 此参数向清单服务器指示获取M3U8的播放器需要检索SCTE标记信息。<br>可能的值：<br>true或false（默认为false）注<br>意：SCTE-35数据在JSON附加项中返回，查询参数值组合如下：<br>ptcueformat=turner | 元素 | nv | DPIScte35<br>pttrackingversion=v2<br>scteTracking=true<br> | 仅HLS |
| vetargetmultiplier | 起始点的段数预卷偏移使用以下方式进行配置：(vetargetmultiplier * targetduration)+ vebufferlength<br>注：此参数仅适用于实时／线性HLS流<br>可能值：<br>数字浮点<br>(默认值：3.0 —— 与HLS规范相同) | 仅HLS |
| vebufferLength | 与vetargetmultiplier一起使用的实时点的秒数。<br>注意：此参数仅适用于实时／线性HLS流<br>可能的值：<br>数字浮点<br>(默认值：3.0) | 仅HLS |

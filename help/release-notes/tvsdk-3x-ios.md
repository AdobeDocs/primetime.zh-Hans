---
title: 《适用于iOS的TVSDK 3.13发行说明》
description: 《适用于iOS的TVSDK 3.13发行说明》介绍了TVSDK iOS 3.13的新增内容或已更改内容、已解决的已知问题和设备问题。
exl-id: adf8ab23-86d6-4113-b243-2709d5f7f829
source-git-commit: 59ea8008c828f3bdf275fea5cc2a59c37b0c4845
workflow-type: tm+mt
source-wordcount: '7575'
ht-degree: 0%

---

# 《适用于iOS的TVSDK 3.13发行说明》 {#tvsdk-for-ios-release-notes}

《适用于iOS的TVSDK 3.12发行说明》介绍了TVSDK iOS 3.12的新增内容或已更改内容、已解决的已知问题和设备问题。

## 系统和软件要求 {#system-software-requirements}

在下载iOS 3.12之前，请确保您的硬件、操作系统和应用程序版本满足以下要求：

操作系统：iOS 8.0或更高版本。

## iOS TVSDK 3.13

此发行版本引入了对LIVE、VOD和FER流的“HLS/CMAF”（前置、中置和后置）广告的支持。

有关客户报告问题的修复，请参阅 [已解决的问题](#resolved-issues). 有关限制，请参阅 [已知问题和限制](#known-issues-and-limitations).

### 以前版本的新增功能和修复 {#whats-new-previous}

**iOS TVSDK 3.12**

修复了实时流在播放15分钟后失败的问题。

**iOS TVSDK 3.11**

修复了以下客户问题： `isFallbackOnInvalidCreativeEnabled` 和方法 `customParams` 导致应用程序崩溃。

**iOS TVSDK 3.10**

* 修复了TVSDK播放器无法触发的问题 `PTMediaPlayerStatusError` 网络不可用时通知。

**iOS TVSDK 3.9**

* 修复了VTT字幕无法回放导致应用程序冻结的问题。

* iOS TVSDK 3.9包含更新的个性化传输证书。

**iOS TVSDK 3.8.0.83修补程序**

该修补程序具有更新的个性化传输证书。

**iOS TVSDK 3.8**

iOS 13合规性并处理iOS 13 `UIWebView` API弃用。

**iOS TVSDK 3.7**

适用于以下情况的修补程序：当同时发出许多广告解析请求时播放停止。

**iOS TVSDK 3.6**

**修复了类的vastXML属性`PTNetworkAdInfo`**

此 `vastXML` 属性设置不正确，返回nil值。

**iOS TVSDK 3.5**

**启用背景音频**

*将应用程序配置为在进入后台时继续播放音频。*

要启用此功能，我们必须设置新的API `audioPlaybackInBackground` 已添加至 `PTMediaPlayer` 类。 启用此API后，您的应用程序可以播放背景音频。

**iOS TVSDK 3.4.0.19（修补程序）**

此版本修复了广告故障转移方案中发生的应用程序崩溃问题。

**iOS TVSDK 3.4**

**广告解决超时**

* 借助TVSDK 3.4，用户现在可以为整体广告解析和清单下载设置超时值。 如果在给定的超时时间内未解析某些广告，则TVSDK会播放其余广告。

* `PTAdMetadata: adRequestTimeout` API已被弃用，将删除。 默认值已设置为35秒。

* 中引入了两个新的替代API `PTAdMetadataClass: adResolutionTimeout`   — 整个广告解析调用adManifestTimeout的超时 — 广告清单下载的超时。

**收入优化**

启用了TVSDK来识别与广告插入工作流相关的问题区域，以向所选的分析端点报告。

**版本3.3**

TVSDK 3.3现在与iOS 11 SDK兼容。 所有已弃用的API已替换为合适的替代项。

**版本3.2**

**其他日志记录支持（第2阶段）**

为以下情况添加了对错误通知的支持：

* HLS版本的广告使用的级别高于内容。

* 排除纯音频变体。

* VAST/VMAP请求失败。

**版本3.1**

* **其他日志记录支持**
添加了对存在广告播放失败时的描述性通知的支持。

* **已添加 [!DNL Fairplay] 加密CMAF流支持**
   [!DNL Fairplay] 现在支持使用AVC编解码器播放的加密CMAF流。

**版本3.0.1**

此版本中没有新增功能或增强功能。

**版本3.0**

* TVSDK 3.0支持HEVC流。

* 即时 — 解决广告更接近广告标记的问题。

已添加 `enableDelayAdLoading` 应用程序级别接口上用于启用JIT的布尔类型的属性。 如果 `enableDelayAdLoading` 不是，它会 `setadMetadata.delayAdLoading`为True（PTAdMetadata接口的属性）。

启用此属性后，TVSDK会根据定义的容差值，解析每个广告时间在其位置之前。 默认情况下， `delayAdTolerance` 设置为5秒。

**版本1.4.45**

为了符合Xcode10，TVSDK已从 `libstdc++` 到 `libc++`，因此，支持的最低版本为iOS 7。 之前是iOS6。

**版本1.4.44**

此版本中没有新增功能或增强功能。

**版本1.4.43**

* 类似电视的体验：能够在广告中间加入，而不会触发部分广告的跟踪。\
   示例：用户在包含三个30秒广告的90秒广告时间的中间（40秒）加入。 此时是插播中第二个广告的10秒。

   * 第二个广告播放剩余的时长（20秒），然后是第三个广告。
   * 未触发播放的部分广告（第二个广告）的广告跟踪器。 仅触发第三个广告的跟踪器。

* 已添加 `enableVodPreroll` PTAdMetadata接口中布尔类型的属性。 属性可用于对VoD流启用前置滚动。 如果 `enableVodPreroll` 否，PSDK不播放前置广告。 然而，这对中端市场没有影响。 默认值 `enableVodPreroll` 是。
* `closedCaptionDisplayEnabled` 的API `PTMediaPlayer` 从iOS v1.4.43开始，界面被标记为已弃用。 要确定隐藏式字幕是否适用于给定字幕，请执行以下操作 `PTMediaPlayerItem`，检查 `subtitlesOptions` 属性 `PTMediaPlayerMediaItem`.

**版本1.4.42**

此版本中未添加任何新功能。 有关已修复问题的列表，请参阅 [已解决的问题](#resolved-issues).

**版本1.4.41**

API更改：

* **isSecure**：引入了一个新的API isSecure ，以防止播放器记录和引发错误。 默认值为true。

* **allowExternalRecording**：引入了一个新的API，以允许对安全内容进行播放镜像。 因此，播放镜像被视为记录 `allowExternalRecording` 值必须设置为 `True`，以允许播放镜像或设置为 `False` 停止安全内容的播放镜像。 默认情况下， `value` 为true。

**版本1.4.40**

无新功能。

**版本1.4.39**

* iOS TVSDK已通过VHL 2.0.1和VHL 2.0.1与Nielsen一起认证。

* iOS TVSDK已更新，可从新的Akamai主机发出CRS请求 `primetime-a.akamaihd.net`.

* 新的主机名配置更大范围地通过HTTP和HTTPS (SSL)提供CRS资产交付。

**版本1.4.36**

在iOS TVSDK中集成并认证VHL 2.0 ：降低 `VideoHeartbeatsLibrary` 通过降低API的复杂性来实施。

**版本1.4.34**

**网络广告信息**

TVSDK API现在提供有关第三方VAST响应的其他信息。 中提供了广告ID、广告系统和VAST广告扩展 `PTNetworkAdInfo` 类可通过以下方式访问  `networkAdInfo`  属性。 此信息可用于与其他Ad Analytics平台(例如 **Moat Analytics**.

**版本1.4.31**

* **计费量度** 为了适应那些只想按客户所使用内容支付而不是按固定费率支付而不想实际使用的客户，Adobe会收集使用情况量度，并使用这些量度来确定向客户收取多少费用。

   每当TVSDK生成一个流启动事件时，播放器就会开始定期向Adobe的计费系统发送HTTP消息。 该时段（称为可计费持续时间）对于标准VOD、专业VOD（启用了中置广告）和实时内容可能不同。 每种内容类型的默认持续时间为30分钟，但实际值由您的Adobe合同确定。

* **对CRS广告的多CDN支持** TVSDK现在支持CRS广告的多CDN 。 通过提供CRS广告的FTP详细信息，您可以指定CDN位置，而不是Adobe拥有的默认CDN，例如 [!DNL Akamai].

**版本1.4.29**

在 `PTSDKConfig` 类， `forceHTTPS` 已添加API。

此 `PTSDKConfig` 类提供了在向Adobe Primetime ad decisioning、DRM和Video Analytics服务器发出的请求上实施SSL的方法。 欲了解更多信息，请参见 `forceHTTPS` 和 `isForcingHTTPS` 方法。 如果清单是通过HTTPS加载的，则TVSDK会保留对HTTPS的内容使用，并在从该清单加载任何相对URL时遵循此用法。

>[!NOTE]
>
>不会修改对第三方域（如广告跟踪像素、内容和广告URL）的请求以及类似请求，内容提供商和广告服务器负责提供通过HTTPS支持的URL。

**版本1.4.18**

Primetime iOS TVSDK现在支持VPAID 2.0 JavaScript创意，以实现丰富的交互式流中广告体验。 有关VPAID 2.0的更多信息，请参阅VPAID广告支持。

**版本1.4.17**

* tvOS

   TVSDK支持tvOS本机应用程序。
* 可以播放以下类型的内容：

   * VOD
   * 实时
   * AES-128
   * 备用音频和字幕
   * FER

* 可以显示以下类型的广告：

   * 基本
   * VAST2
   * VAST3
   * VMA

* 当前不支持以下功能：

   * DIGITAL RIGHTS MANAGEMENTDRM
   * 广告横幅
   * 电视标记语言(TVML)

**版本1.4.13**

>[!NOTE]
>
>Nielsen模块已从TVSDK内部版本中删除，TVSDK将很快更新为新的Nielsen集成模块。

**广告回退，广告选择逻辑中的Daisy链接(Zendesk #3103)**

对于启用了回退规则的VAST广告（创意），TVSDK会将具有无效MIME类型的广告视为空广告，并尝试使用回退广告来替换该广告。 您可以在某些方面配置回退行为。 有关更多信息，请参阅VAST和VMAP广告的广告回退。

**版本1.4.9**

**使用替代内容替换发出封锁信号**

在1.4 TVSDK更新中，Adobe现在还支持进入和从对线性内容的区域封锁中返回。 TVSDK现在可以并行处理两个清单文件（主文件和备用文件），以监控中断信号，即使备用程序正在被显示来代替原始程序。

**版本1.4.8**

**视频心率库(VHL)已更新至版本1.5**

* 能够发送包含视频开始或视频/广告/章节开始作为上下文数据的元数据。

* 网络流量更少 — 心跳平均更少，大小更小。

**版本1.4.7**

* **内部部署个性化支持**

支持AdobeIndividualization Server的内部部署，以自定义客户端的个性化请求，从而转到其他端点。

* **基于分辨率的输出保护**

DRM策略现在可以指定允许的最高分辨率，具体取决于设备的输出保护功能。 例如， _如果HDCP可用，则允许播放分辨率高达1080p的内容；如果HDCP不可用，则允许播放分辨率高达480p的内容。_

**版本1.4.4**

* **视频心率库(VHL)已更新至版本1.4.1.1**

   * 添加了将其他SDK或播放器中的不同Analytics用例捆绑到Adobe Analytics Video Essentials的功能。
   * 广告跟踪已通过删除 `trackAdBreakStart` 和 `trackAdBreakComplete` 方法。 从以下位置推断广告时间 `trackAdStart` 和 `trackAdComplete` 方法调用。
   * 此 `playhead` 跟踪广告时不再需要属性。
   * 添加了对Experience CloudID服务的支持。

* **Nielsen SDK集成**

TVSDK现在支持将mTVR和MDPR ID3信标发送到Nielsen SDK，而无需任何自定义集成。 要开始配置，请下载3.1.2.19 Nielsen iOS应用程序SDK，并按照《iOS程序员指南》中的此处说明操作。

**版本1.4.0**

* **使用替代内容替换发出封锁信号**

在1.4 TVSDK更新中，TVSDK现在还支持进入线性内容区域封锁或从该区域封锁回访。 TVSDK现在可以并行处理两个清单文件（主文件和备用文件），以监控中断信号，即使备用程序正在被显示来代替原始程序。

* **删除/替换C3广告**

现在，无需额外的准备工作即可将新广告动态插入到从C3窗口出来的视频点播(VOD)资产中。 TVSDK现在提供了一个API，用于删除自定义内容范围并动态插入新广告。 此强大的新功能在以下情况下也很有用：在广播期间播放实时/线性内容，然后立即下拉以用作按需内容，而没有适当的时间清理资产。

## 已解决的问题 {#resolved-issues}

如果解决方法与报告的问题相关联，则会显示Zendesk引用，例如ZD#xxxxx。

<!-- 

Comment Type: draft

 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 

-->

<!--
Comment Type: draft

 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 
-->

**iOS TVSDK 3.13**

* (ZD 42085) - CMAF流播放问题。

* (ZD-43215) — 在广告进行期间取消播放器时崩溃。

* (ZD 43210) — 启用WebVTT子标题后，iOS HLS播放冻结。

**iOS TVSDK 3.12**

* 使用适用于iOS 3.10的TVSDK时，实时流在播放15分钟后失败。

### 以前版本中已解决的问题 {#resolved-issues-previous}

**iOS TVSDK 3.11**

* (ZD#40998) - `isFallbackOnInvalidCreativeEnabled` 导致应用程序崩溃。

* (ZD#41289) - `NSInvalidArgumentException` 用方法观察 `customParams` 导致应用程序崩溃。

**iOS TVSDK 3.10**

(ZD#40943) - TVSDK播放器未触发 `PTMediaPlayerStatusError` 网络不可用时通知。

**iOS TVSDK 3.9**

(ZD#40272) - iOS TVSDK无法播放VTT字幕并出101001错误，导致应用程序冻结。

**iOS TVSDK 3.8**

* (ZD#40087) - iOS崩溃，并出现播放器错误，显示过期的VOD内容。

* (ZD#40083) — 前置广告不用于直播流 `OpportunityGenerator` 播放器出错。

* (ZD#39828) - `CurrentItem` 属性缺少nullability注释，导致在通知中包含的播放器状态为时播放器崩溃 `PTMediaPlayerStatusStopped`.

**iOS TVSDK 3.7**

(ZD#38961) — 当将多个内容配置为在PiP中播放时，一个内容完成播放后，无法在“画中画(PiP)”窗口中播放内容。

**iOS TVSDK 3.6**

此版本中没有新问题。

**iOS TVSDK 3.5**

此版本中没有新问题。

**版本3.3**

(ZD#37820) — 为自定义标头HS-Id、HS-SSAI-TAG添加了允许列表。

**版本3.2**

* **Ticket#36588**  — 调用MediaPlayer STOP方法时观察到播放器崩溃。

修复了在为一些带有字幕的流调用STOP方法时观察到的间歇性崩溃。

* **Ticket#37080**  — 清单调用出现重复请求。
修复了在播放期间对清单URL发出的重复请求。 现在，TVSDK会对每个清单进行一次调用。

* **票证#37** - CRS标准化规则失败，出现eq匹配类型修复了以下情况：当播放器遇到为“eq”匹配类型的主机名设置的最后一个标准化规则时，该规则会崩溃。

**版本3.1**

**票证#36313**  — 线性广告时间期间的间歇性不可预测结果实时流中线性广告时间期间的固定间歇播放。

**版本3.0.1**

**票证36948** - CRS - iOS 12上的资源选择顺序不一致为CRS选择的资源并不总是在VAST或VMAP响应中返回的最高质量变体。

**版本3.0**

* **票证35311**  — 在电话中断期间，播放器状态未变为“已暂停”添加了中断处理程序以停止播放器中断。 中断时，播放器状态将变为“已暂停”，然后单击播放按钮继续播放。

* **票证36685**  — 实时资源 — 时间与播放器时间进度和SCTE标记时间不匹配。为实时点之前的SCTE标记计算正确时间。

* **票证36492** - `currentTime` 和 `localTime` 在暂停状态期间寻求新位置时不会更新播放器的当前时间现在可以设置为零，以防播放器处于暂停状态；以前当前时间仅用于播放状态时设置为零。

**版本1.4.45**

* **票证36294** - iOS TVSDK在Xcode 10上不起作用修复了TVSDK在XCode 10上的编译问题。 由于对XCode的十个要求，从iOS 1.4.45开始，在TVSDK上构建的应用程序需要最低部署目标为iOS 7.0

* **票证36321**  — 可搜寻范围中发现的以下项之间的差异： `PTMediaPlayer` 和 `AVPlayer` 实例位于 _正在播放_ 省/州。

* **票证36493** - `libstdc++` iOS 12支持修复了iOS 12上TVSDK的编译问题。 从iOS 1.4.45开始，在TVSDK上构建的应用程序需要最低部署目标为iOS 7.0

**版本1.4.44**

* **票证34683**  — 广告播放进度时间正以负数增长

当广告服务器报告的持续时间与实际广告内容不匹配时，会引入其他检查来处理这种情况。

* **票证34801** - `currentTime` 和 `localTime` 在暂停状态期间搜索新位置时未获得更新播放器的当前时间现在可以设置为零，以防播放器处于暂停状态；以前，当前时间仅用于播放状态时设置为零。

* **票证35037**  — 从基于信号的广告插入返回时，播放因错误URL而停止。
改进了对1.4.42版本中#34385关的已关闭问题的修复。 添加了isCanceled检查和异常处理代码，以使操作队列更稳健。

**版本1.4.43**

* (ZD#32990) - iOS：在某些提示点上播放内容而不是广告。 `selectedMediaOptionInMediaSelectionGroup` 作为AVPlayerItem接口一部分的API现已移至 `AVMediaSelection` 在iOS11中。 使用此新API解决了该问题。

* (ZD#33683)已删除TVSDK `==` 后缀。 此问题已在解析逻辑中修复。

* (ZD#33905) - iOS TVSDK通过两个用户代理调用清单文件。 首次m3u8调用（全新安装案例）中修复了用户代理问题。 现在，M3u8的所有呼叫都具有相同的用户代理。

* (ZD#34293) — 在iOS11上无法正确播放线性流上插入的预滚筒。 前置式广告的问题已修复。

* (ZD#34684) — 应用广告跳过策略时，前置广告帧会显示几秒钟。 一个新的API， `enableVodPreroll` 引入此功能，以禁用vod播放中的前置式播放。 此API的默认值为 _是_. 该API确保跳过主内容中的广告内容拼合。

* (ZD#34765) — 调用后 `stop()`，仍很少下载传输流区段。 增强了 `Stop()` 避免下载额外区段的API。

* (ZD#34865) — 前置广告 [!DNL Livestream] 在iOS上被截断。 与iOS11相关，并添加了额外的检查以确认流是前置内容还是主内容，从而解决了此问题。

* (ZD#35093) — 修复了以下故障转移情况：如果流的主要变体在启动时失败（返回404），则播放不会切换到备份流。

**1.4.42 (1.4.42.118)**

* (ZD#34385) — 从基于信号的广告插入返回时，播放因错误URL而停止。

   增加的最大并发计数 `CustomAVAssetLoaderOperations`，以便清单读取可以继续执行。

* (ZD#34373) — 不允许流记录时，最终用户无法流式传输到连接HDMI的设备。

* (ZD#32678) - TVSDK无法在iOS上收集正确的广告ID。

   如果存在VAST/VMAP重定向，则最终广告创意的广告ID现在可在VHL Ping中提取。

* (ZD#33904) - TVSDK未注册AVFoundation通知 `AVAudioSessionMediaServicesWereLostNotification` 和 `AVAudioSessionMediaServicesWereResetNotification`.

   `PTMediaServicesWereLostNotification` 和 `PTMediaServicesWereResetNotification` 现在可以在播放器应用程序中注册，以便在媒体服务重置或丢失时获取通知。

* (ZD#33815) — 客户无法在不更新应用程序的情况下更新其优先级和标准化CRS规则。

   添加了 `getCRSRulesJsonURL` 和 `setCRSRulesJsonURL` iOS TVSDK的API 。

**版本1.4.41 (1.4.41.76)**

* (ZD #34464) — 使用TVSDK版本1.4.41构建参考应用程序时出现问题

   从此版本开始，编译适用于iOS的TVSDK时需要Xcode 9。
* (ZD #29456) — 播放开始处于暂停状态

   修复了视频在进入Airplay时暂停的问题。
* (ZD #30371) — 在线性流中插入两个以上的广告时，AdBreak开始时间发生变化

   修复了尝试在Apple TV上播放内容时导致无法完全播放的错误
* (ZD #32146) — 否 `PTMediaPlayerStatusError` 收到有关阻止iOS 11 Dev Beta版的HLS Live内容的信息

   否 `PTMediaPlayerStatusError` 使用Charles进行阻止时，收到有关HLS实时和VOD内容的（放置连接和403）。

* (ZD #29242) — 启用广告后，Airplay视频播放失败。

   当启用广告并启用AirPlay开始播放视频时，视频播放从不开始且不会显示错误。

* (ZD#33341) - `DRMInterface.h` 触发Xcode 9中的生成警告。

   修复了中的两个块原型 `DRMInterface.h` 参数列表中缺少&#39;void&#39;一词。

* (ZD#31979) — 当它是iPhone 7/iPhone7+的iOS 10或更高版本时，不编译/运行。

   修复了不再支持编译iOS 7之前的IB文档的问题。

* (ZD#32920) — 广告时间中的空白屏幕，无广告时间完成。

   当广告时间演示广告实例时，在广告实例完成后，将显示一个空白屏幕。

* (ZD#32509) — 禁用iOS 11屏幕录制禁用iOS 11上的屏幕录制。

* (ZD#33179) - iOS11出现间歇性事件故障。

   修复了iOS 11上的事件故障。

**版本1.4.40** (1.4.40.72)

* (ZD #32465) — 播放器无法处理合并的播放列表。

   调用 `finishLoadingWithError`（带：错误），用于AV foundation尝试备用流/触发故障转移。

* (ZD #31951) — 许可证轮换期间出现TVSDK错误。

   修复了许可证轮换问题。
* (ZD #31951) — 广告时间内的空白屏幕，无广告时间完成。

   处理了Facebook VPAID广告通常在单个广告中返回多个CDATA块的问题 `<AdParameters>` vast节点。
* (ZD #33336) - iOS TVSDK — 尽管Freewheel返回了足够的广告，但广告盒未填充。

   在序列广告和回退广告之间创建了父子关系，并根据父序列和索引进行排序。

**版本1.4.39** (1.4.39.43)

* (ZD #32178) - iOS TVSDK版本不正确。

   日志文件中的TVSDK版本输出为1.0.211。它固定为输出正确的版本。

* (ZD #32199) — 延迟广告加载 — 不为内容显示视频。

   以前未初始化的本地Adbreak时间线现在在使用之前刷新。

* (ZD #27528) — 如果在iOS 1.2上将次级音频设置为非默认值，则在资产开始播放后的1-45秒内，视频、音频或两者都会冻结。

   准备并通知处于就绪状态的音轨。

* (ZD #30411) — 如果选择辅助Sap语言，您可能会收到意外结果，如没有音频或音频不正确。

   准备并通知处于就绪状态的音轨。

* (ZD #32199) — 延迟广告加载 — 不为内容显示视频。

   以前未初始化的本地Adbreak时间线现在在使用之前刷新。

* (ZD #27528) — 如果在iOS 1.2上将次级音频设置为非默认值，则在资产开始播放后的1-45秒内，视频、音频或两者都会冻结。

   准备并通知处于就绪状态的音轨。

* (ZD #30411) — 如果选择辅助Sap语言，您可能会收到意外结果，如没有音频或音频不正确。

   准备并通知处于就绪状态的音轨。

**版本1.4.38** (1.4.38.860)

* (ZD #29281) - iOS：将AdSystem和创作Id添加到CRS请求

根据CRS规范化规则在CRS请求中使用创作ID和AdSystem

* (ZD #29176) — 崩溃 `PTAdPolicyDeligate` `satAdBreakAsWatched:position`

由于空AdBreak而导致的崩溃现在已得到处理。

* (ZD #30125) — 程序化广告在iOS平台中不起作用

在iOS中添加了程序化广告支持。

* (ZD #30782) - #EXT-X-PROGRAM-DATE-TIME通知

使用实时DRM流的# EXT-X-PROGRAM-DATE-TIME标记不会触发定时元数据事件。

**版本1.4.37 (1.4.37.842)**

* (ZD #28950 ) - VOD播放问题

将流中的# EXT-X-PLAYLIST-TYPE标记设置为“事件”而不是“VOD”时，出现播放问题

* (ZD #29281) - iOS：将AdSystem和创作Id添加到CRS请求

根据CRS规范化规则在CRS请求中使用Creative Id和AdSystem。

* (ZD #29462) - A&amp;E VOD中的TremorHub广告导致iOS应用程序崩溃

**版本1.4.36 (1.4.36.835)**

* (ZD #29418) — 持续时间为0 (#EXT-X-CUE-OUT：0.000)的提示会导致iOS TVSDK停止播放或使其崩溃。

问题已修复，可正确开始播放。

* (ZD #29462) - VOD中的广告会导致iOS TVSDK发生崩溃。

问题已修复。 iOS TVSDK提升了 `exception(AUDNetworkAdInfo::initWithAdId)` 而不去处理它。 出现此异常是由于广告ID为空所致。

* (ZD #29281) — 将AdSystem和Creative ID添加到CRS请求。

在1401和1403请求中包含AdSystem和CreativeId作为新参数（所有其他参数保持不变）。

**版本1.4.35** (1.4.35.830)

* (ZD #27830) — 需要以编程方式确定iOS中隐藏式字幕与字幕之间的差异。

TVSDK现在公开两种类型，可用于过滤掉所需的字幕类型。

* (ZD #29160) - TVSDK iOS上未正确拼接EXT-X-CUE-OUT广告提示。

EXT-X-CUE-OUT midroll广告正在播放。

* (ZD #29100) — 当用户浏览到电影结尾时，应用程序崩溃。

修复了与同步相关的多次崩溃。

* (ZD #28785)、 (ZD #27712)和(ZD #25076) - iOS应用程序在大型直播活动中崩溃。

修复了与同步相关的多次崩溃。

**版本1.4.34** (对于iOS 6.0+，为1.4.34.815)

* (ZD #28481) - FER中断，原因是在广告时间结束时为这些FER流附加了错误的键

对于FER流，在广告时间结束之后插入广告时间之前的键。 通过附加 *上次查看的键* 在广告时间结束时。

**版本1.4.33** (对于iOS 6.0+，为1.4.33.803)

* (ZD# 21701)为子帐户启用CRS

根据CRS后端要求，通过发送1401 CRS请求的原始创意URL而不是规范化URL来启用。

* (ZD# 26218) - `PSDKResources.bundle` 加载问题

通过更新资源加载以从所有可用捆绑包中查找，此问题得以解决。

* (ZD# 27460)Midroll第一个广告调用 — POST `cdn.auditude.com` 返回403。

新的CDN帐户无法处理POSTCDN请求。 通过更新代码以使 `cdn.auditude.com` 广告请求成为GET而非POST。

**版本1.4.32** (对于iOS 6.0+，为1.4.32.792)

* (ZD# 27132)支持VMAP广告时间的小数值。

当内容未按照定义的广告时间分段时，整数会导致意外的广告投放位置。 通过将小数值转换为整数，解决了此问题。

* (ZD# 27189)带有EXT-X-DISCONTINUITY-SEQUENCE标记的AES内容无法正确播放。

通过将标记放在播放列表的开头解决了此问题。

**版本1.4.31** (对于iOS 6.0+，为1.4.31.785)

* (ZD# 24528)实施计费的TVSDK使用量度

有关更多信息，请参阅 [计费量度].

* (ZD# 24642)对TVSDK的画中画支持

有时无法正常工作的画中画功能已得到修复。

* (ZD# 25246)不正确的广告时间信号

通过调整变体清单中的不连续标记，解决了此问题。

* (ZD# 26218)在尝试包含时，应用程序构建过程变得复杂 `PSDKLibrary.framework` 在客户端的应用程序框架中

此问题可通过打包 `PSDKLibrary.framework` 根据要求。

* (ZD# 26364)支持CRS广告的多CDN

有关更多信息，请参阅CRS广告投放的多个CDN支持。

* (ZD# 27028)iOS 10中某些流的播放延迟。

通过为没有M3U8扩展的流提供解决方法，此问题得以解决。

**版本1.4.30** (对于iOS 6.0+，为1.4.30.754)

此版本中解决了TVSDK的以下问题：

* 允许列表 (ZD# 24180)添加自定义标题以。

允许列表新的自定义标头已添加到TVSDK。

* (ZD# 25016)设置ABR控制参数时随机选择故障转移流

通过按照提供ABR设置的顺序维护ABR流，此问题得以解决。 `initialBitrate` 在包含故障转移URL的流中设置。 这样可避免播放故障转移流而不是主故障转移流。

* (ZD# 25076)崩溃 `PTAuditudeAdResolver loadComplete`

修复了在快速启动/停止多个包含广告的PTMediaPlayer实例期间发生崩溃的问题。

* (ZD# 25960)没有其他订阅标记触发元数据更改通知广播

修复了当订阅标记出现在清单中的第一个区段之前时，不会通知该标记的问题。

* (ZD# 26084) PSDK抛出106000.101000.-11833从上一个广告时间转换回娱乐内容时，未找到解码器错误

当来自VMAP的最后一个广告时间开始时间早于总持续时间完成时，在某些情况下，直到最后一个广告时间结束之后，才会插入键。 此问题已修复。

* 视频心率库(VHL)已更新至版本1.5.9，以解决以下问题：

* (ZD #22351) VHL - Analytics：实时视频资源持续时间

通过添加  `assetDuration`  API目标 `PTVideoAnalyticsTrackingMetadata` 更新实时/线性流的资源持续时间，并提供用于检查实时流的逻辑。

* (ZD# 22675) VHL - Analytics：更新实时视频资源持续时间

此问题与ZD #22351相同。

* (ZD #25908) VHL - Analytics：Adobe心率事件崩溃

通过更新实施以使用最新版本的iOS 1.5.9版VHL来提高稳定性和性能，此问题得以解决。

* (ZD #25956) VHL - Analytics：重复播放视频时崩溃

此问题与ZD #25908相同。

**版本1.4.29** (1.4.29.743)

* (ZD# 23901)第三方广告未播放

通过迁移到CRS v3 URL结构以在重新打包的URL中包含区域ID，此问题得以解决。

* (ZD #25183)tvOS和iOS上的DRM播放问题

通过支持多DRM支持所需的多个关键标记来解决此问题。

* (ZD# 25334) TVSDK无法播放cDVR共享内容

通过阻止TVSDK将空字符串转换为绝对URL，此问题得以解决。

* (ZD# 25347)在AVURLAsset中设置自定义HTTP标头

支持对其区段请求使用自定义标头 `PTNetworkConfiguration` 已添加类。

**版本1.4.28** (1.4.28.722)

* (ZD #24549)多个广告跟踪调用

当创建多个播放器时，通过更新时间轴管理器以侦听特定对象的通知，解决了此问题。

* (#24758第纳尔) `PTManifestLogger` 不支持iOS 8

通过将记录器实用程序库更新到7.0版部署目标，此问题得以解决。

* (ZD #24775)由于广告导致流延迟

通过正确计算事件播放列表上的持续时间偏移，此问题得以解决。

* (ZD #24799)某些剧集没有在iOS应用程序上播放

当WebVTT文件受地理限制时，通过本地Web服务器为字幕解决此问题。

**版本1.4.27** (1.4.27.711)适用于iOS 6.0+

* (ZD #24089) — 针对长DVR流的广告解析优化

通过添加多个优化来减少在实时/线性流中处理DVR窗口所需的时间，此问题得以解决。

* (ZD #21554) — 未触发的TVSDK错误信标 `application-type = video/mp4`

通过使播放器能够ping通无效资源格式上的正确错误跟踪URL，此问题得以解决。

* (ZD #24424) — 类型的崩溃 `EXC_BAD_ACCESS KERN_INVALID_ADDRESS` 源自内部 `PSDKLib` 适用于新硬件设备上的iOS。

修复了在不同流之间快速切换播放时，由于取消分配的媒体播放器实例而发生的崩溃问题。

* (ZD #24575) - 32位设备上的TVSDK在以下情况下崩溃： `enableDebugLog=true`

修复了在启用日志记录时导致32位设备崩溃的日志格式问题。

**版本1.4.26** (1.4.26.702)适用于iOS 6.0+

* (ZD# 20213) - TVSDK FW必须为XCode7进行动态/模块化

通过更新具有模块支持的库修复了此问题

**版本1.4.25** (1.4.25.684)适用于iOS 6.0+

* (ZD #19629) — 进入ATV 4播放时出现实时视频暂停

通过删除旧项目后但在将新项目添加到之前添加等待期，此问题得以解决 `AVQueuePlayer`. 如果没有等待时间，则通知将发送到不正确的项目。

* (ZD #19856) — 默认启用时，不显示字幕

修复了webvtt播放列表中导致字幕显示不正确的问题。

* (ZD #21590) — 最新源内部版本中的视频性能和跟踪

中缺少视频长度的问题 `VideoAnalytics` 已修复。

* (ZD #20202) — 设置自定义字幕样式会使iOS应用程序崩溃

通过设置字幕样式时添加其他null对象检查，此问题已得到解决。

* (ZD #20709) — 视频开始跟踪中报告的视频长度为0

此问题与(ZD #21590)相同。

* (ZD #22280) - Analytics视频长度设置为0

此问题与(ZD #21590)相同。

* (ZD #22592) - Primetime中的Airplay问题

此问题与(ZD #19629)相同。

* (ZD#22922) — 适用于iOS的手动比特率切换

通过提供指定最大比特率的选项来解决此问题。

* (ZD #23084) — 适用于仅IPv6网络的Apple合规性

删除了Apple不推荐用于IPv6兼容性的符号。

**版本1.4.24** (1.4.24.661)适用于iOS 6.0+

* ZD #2548) - Primetime对移动设备交互式广告的支持 — VPAID 2.0

如果VPAID广告无法播放，则通过更新逻辑以取消隐藏播放器视图来解决此问题。

* (ZD #20101) — 自定义章节实施在广告播放期间触发章节开始事件

此问题已通过更新得到解决 `VideoAnalyticsTracker` 在章节与非章节边界之间过渡时，正确检测章节的开始/结束。

* (ZD #20784) - Analytics：触发实时视频过渡的内容完成

通过添加逻辑以在视频跟踪会话期间手动触发内容完成，解决了此问题。

已更新以下库：

* AdobeMobile库到4.10.0
* VHL库到1.5.6
* VHL-Nielsen库到1.6.7
* (ZD #21855) — 字幕中置后不播放

在此问题中，重复的不连续性标记导致字幕不出现在中置之后。 通过删除彼此相邻的不连续标记，此问题得以解决。

* (ZD #21994) — 字符串超出范围，位于 `PTHLSUtils`

崩溃的最可能原因是EXT-X-KEY的URL被引号括起来。

* #22074第纳尔) - `AUDVAST` iOS上每分钟发生一次崩溃

在版本1.4.23中，修复了由VAST重定向URL中存在不安全字符导致的崩溃。 但是，TVSDK继续跳过这些广告。

通过处理不安全字符和允许播放广告，此问题得以解决。

* (#22694第纳尔) - `PTMediaPlayer`.  播放器已隐藏视图

如果VPAID广告无法播放，则通过更新逻辑以取消隐藏播放器视图来解决此问题。

**版本1.4.23** (1.4.23.641)适用于iOS 6.0+

* (ZD #18016) - Primetime SDK在网络条件恶劣时未响应

通过改进发生致命错误时的错误通知，此问题得以解决。 `AVFoundation` 发生并允许应用程序处理错误后的重新启动。

* (ZD #20580) — 崩溃 `PTSplicerManager`

通过针对导致崩溃的并发问题提供额外保护，此问题得以解决。

* (ZD #21782) - iOS错误代码10100

修复了在Adobe访问DRM流上开始播放时TVSDK返回101000错误的问题。

* (ZD #21889) — 在线广告和离线内容播放失败

修复了在AES加密离线内容上的广告后播放失败的问题。

* (ZD #22074) - AUDVAST崩溃在iOS上每分钟发生一次

通过改进对URL中包含无效字符的第三方VAST广告标记的处理，此问题得以解决。

* (ZD #22257) - TVSDK无法播放DRM流

修复了在Adobe访问DRM流上开始播放时TVSDK返回101000错误的问题。

**版本1.4.22** (1.4.22.627)(适用于iOS 6.0+)

* (ZD #18709) — 适用于iOS的TVSDK崩溃

修复了一些受Adobe访问DRM保护的流上发生的崩溃问题。

* (ZD #18850) — 根据CRS规则更新创意选择逻辑

通过添加.json配置文件指定创意选择优先级，解决了此问题。

* (ZD #19770) — 受保护的AES视频馈送不再播放

修复了某些302重定向流无法播放的问题。

* (ZD #19629) — 进入ATV 4播放时出现实时视频暂停

在为Apple TV 4设备打开Airplay后，通过添加实时视频暂停的解决方法，此问题得以解决。 问题似乎是Apple TV 4问题。

* (ZD #21119) - TVSDK在广告播放后停止

在使用广告插入时，增加了对具有序列IV的AES加密流的支持。

* (ZD #21125) — 从实时/线性广告时间提前返回

添加了对在广告时间播放到完成之前从广告时间返回的支持。 通过自定义清单标记指示提前返回。

* (ZD #21224) — 支持Akamai的令牌化流

API已添加到 `PTNetworkConfiguration` 类，用于将Cookie作为URL参数附加到某些Akamai标记化的流的区段上。

* (ZD #21287) — 无关日志

修复了即使在禁用日志记录的情况下，xcode控制台中默认显示的某些log语句的问题。

* (ZD #21446) - TVSDK有时不会触发广告时间事件

在事件流上，无法正确触发先前版本内部版本中的广告时间。 此内部版本解决了此问题。

**版本1.4.21** (1.4.21.605)适用于iOS 6.0+

* (ZD #20749) — 回退跳过非空VAST响应；触发额外的广告跟踪URL

已解决后备广告上存在重复Ping的问题。

**版本1.4.20** (1.4.20.590)适用于iOS 6.0+

* (ZD #18639) - TVSDK在冗长的热记录资产上占用过多的CPU/资源

已在这两个级别中修复过度CPU/资源使用量。 首先，通过让时间更新函数在全局队列而不是主线程上运行，并通过优化CPU使用率来解析具有先前处理和缓存的m3u8的清单。

* (ZD #19349) — 限制网络连接时，将跳过前置广告。

通过为应用程序和 `adMetadata.adRequestTimeout` 用于覆盖默认的10秒超时的API。

* (ZD #19446) — 缺少实时流通知

通过允许应用程序订阅， `EXT-X-PROGRAM-DATE-TIME` 在实时流上。

* (ZD #19459) — 使用准备备用音频时崩溃 `PTMediaPlayerItem` `prepareAudioOptionsWithAVMediaSelectionOptions`
* (ZD #19460) — 崩溃 —  `[PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]`

此问题与Zendesk #19459相同。

* (ZD #19574) - TVSDK不返回DRM或非DRM内容的M3U8响应数据

在清单文件的初始加载中 `PTMediaPlayerItem.prepareToPlay`，如果加载清单失败，则TVSDK不会向应用程序报告失败响应的正文。

通过允许TVSDK将故障响应报告为错误，此问题得以解决。

* (ZD #19615) — 回退逻辑不起作用

在当前实施中，已跳过后备广告，除非这些广告采用m3u8格式，否则不会重新打包。 通过添加对重新打包后备广告的支持，此问题得以解决。

* (ZD #19770) - TVSDK无法使用302重定向播放任何受保护的AES内容

已修复重定向问题，因为重定向URL已被清除 `cleanConnectionData` 才能用于解析清单。

* (ZD #19856) — 默认启用时，某些比特率不会显示字幕

通过处理iOS中针对未显示字幕的流区段的错误，此问题得以解决。

* (ZD #19868) - TVSDK在贩运无效创意时崩溃

修复了TVSDK中错误取消分配Vast解析器实例的崩溃。

* (ZD #20180) - VPAID广告偶尔会被跳过

JavaScript MIME类型并不总是包含或被视为有效的MIME类型。 通过将JavaScript作为有效的MIME类型包含在内，此问题得以解决。

* (ZD #20749) — 回退跳过非空VAST响应；触发额外的广告跟踪URL

修复了某些创意内容未重新打包的问题。

**版本1.4.19** (1.4.19.563)(适用于iOS 6.0+)

* ZD #18639) - TVSDK在冗长的热记录资产上占用过多的CPU/资源

通过将DRM m3u8播放列表重写优化为先前已重写的播放列表的缓存位，该问题得以解决。 当您回放每次下载区段后都会为其下载m3u8的实时m3u8流时，此视频流最相关。

* (ZD#18956) - `player.drmManager` 在iOS演示播放器中设置断点时，为nil

通过更新 `PTMediaPlayer.drmManager` 用于从DRM框架提取DRMmanager的API实施。

**版本1.4.18** 适用于iOS 6.0+的( 1.4.18.557)

* (ZD #18844)在iOS播放器中跟踪实时内容的播放头。

通过允许应用程序设置自己的播放头值，此问题得以解决。

* (Zendesk #18518) — 如果未指定视频名称，则TVSDK的名称默认为*基于PSDK的播放器。*

通过删除播放器名称的默认值，此问题得以解决。

**版本1.4.17** (1.4.17.545)适用于iOS 6.0+

* (Zendesk #2228) — 增强TVSDK以返回获取清单的JSON响应

当内容不是M3U8时，DRM Framework不会发送错误，而是返回零DRMMetadata。 通过添加元数据以便在发出M3U8_PARSER_ERROR通知时公开内容，解决了此问题。

* (Zendesk #2231) — 获取在MediaPlayerNotification中不可用的清单时返回的错误

分辨率与Zendesk #2228相同

* (Zendesk #3304) - VAST 3.0 `[ERRORCODE]` 未填充宏

以下问题： [!DNL Auditude] 当跟踪URL的开头包含空格被解析后，SDK无法发送ping。

* (Zendesk #17294) — 崩溃 [!DNL SecKeyRawSign]

解决了客户代码使用密钥链时可能出现的崩溃问题。

* (Zendesk #18008) — 支持iOS8+的Cookie以支持标记化的流

Akamai令牌化流要求在区段请求时发送Cookie，但在iOS 7及更早版本上无法做到这一点。 从iOS 8开始，Apple添加了一个API，允许为区段请求传递Cookie。 TVSDK中现在提供了此支持。 此外，还增加了发送用户代理（如果可用）的支持。

* (Zendesk #18166) - TVSDK 1.4.15在使用编译时给出数百个警告 `DWARF` 替换为 `dSYM` 文件选项

所有警告均已解决。

**注释**：为TVSDK添加了与tvOS兼容的库。

**版本1.4.16** (1.4.16.1454)

* Zendesk #3875 — 在播放期间按Tab S崩溃

还原OKHTTP对的依赖关系 [!DNL Auditude] 对于CRS，因为TVSDK现在直接使用 `httpurlconnection` 而不是curl。 该问题通过在进行另一JNI调用之前清除异常而得以解决。

* (Zendesk #4487) — 跟踪线性内容渠道

通过在线性流播放会话期间重新初始化视频心率跟踪器，解决了此问题。

* (Zendesk #17919) - Android — 内容搜寻导致心率错误

问题出在当章节中有搜寻时，解决处于错误状态的心跳

* (Zendesk #18053) — 使用TVSDK的应用程序在Marshmallow上崩溃

当TVSDK库使用具有YUV功能的霓虹灯代码时，TVSDK在Android™ M操作系统上崩溃 `->` RGB颜色转换。 通过使用非霓虹灯版本的更新导致此问题的函数解决了此问题 `code`.

* (Zendesk #18072) - Android M — 应用程序崩溃

此崩溃发生在调用时 `MediaCodecList` 和 `MediaCodecInfo` 检查配置文件和级别是否受支持时的API。 Adobe正在寻求Google对额外洞察的支持。 通过提前加载所有编解码器信息以避免仅在需要编解码器信息时调用这些API，提供了临时解决方法，从而解决了此问题。

* (Zendesk #18074) — 使用Android™ 6.0的Nexus上无法使用阿拉伯字幕

通过支持Android™ CTS字体映射，此问题得以解决。

**版本1.4.15** (1.4.15.512)适用于iOS 6.0+

**注释**：Nielsen模块已从TVSDK内部版本中删除，但TVSDK将很快更新为新的Nielsen集成模块。

* (ZD #2228) — 获取清单时返回的错误，该清单在 `MediaPlayerNotification`

添加了元数据，以便在通知时公开内容 `M3U8_PARSER_ERROR` 发生。

* (ZD #4437) - Adobe Primetime SDK中的崩溃情况

修复了在准备字幕/备用音频时报告的崩溃。

* (ZD #4487) — 跟踪线性内容渠道

允许在线性流播放会话期间重新初始化视频心率跟踪器。

**版本1.4.14** (1.4.14.498)适用于iOS 6.0+

* (ZD #17260) — 崩溃 `playlistManagerForURL`

修复了由于并发问题导致的间歇性崩溃。

**版本1.4.13** (iOS 6.0+)

* (#3304第纳尔) - VAST 3.0 `[ERRORCODE]` 未填充宏

   * 如果内联广告的创意不正确，则显示错误代码400。
   * `[ERRORCODE]` 宏已进行URL编码。

* (ZD #3865)心率与IMA广告的集成

修复了报告视频长度不正确的错误。

* 更新了TVSDK演示播放器以支持iOS 9

要正确支持iOS 9，您必须配置Application Transportation Security的例外情况。 对于演示，ATS将被完全禁用。

**版本1.4.12** (1.4.12.464)适用于iOS 6.0+

* (ZD #4521) CRS测试客户端和SSAI

修复了3P URL中错误的反向MD5。

**版本1.4.12** (1.4.12.463)(适用于iOS 6.0+)

* (ZD #2751) CSAI和CRS/增强：处理某些媒体文件URL中的动态元素。

更新了Creative重新打包服务，以正确处理带有动态创意URL的广告。

* (ZD #3654) 1.3.4.166之后的PSDK版本中的内存泄漏

修复了中的内存泄漏 `drmFramework` 在iOS 8.2设备上定期播放

* (ZD #3988)首次播放后重新搜索到Preroll时，将跳过该项

修复了一个错误，以便可以正确禁用广告策略。

* (ZD #4017)请求iOS API强制向后搜寻播放广告

通过修复ZD #4279解决

* (ZD #4279) iOS和桌面上的HLS TVSDK ad insertion -302重定向问题

修复了广告资源使用相对重定向URL时的错误

**版本1.4.9** (1.4.9.427)(适用于iOS 6.0+)

* (ZD #3075) Internet可达性问题 — iOS

添加了用于检测播放何时停止的通知。

* (ZD #3193)在TVSDK中请求配置文件更改API

已更新 `PTPlaybackInformation` 以公开更新的指示比特率。 已更新 `BITRATE_CHANGE` 通知，以便对M3U8报告的比特率提供更可靠和精确的时间。

* (ZD #3324)当VMAP中没有广告媒体时，Primetime广告报告问题

TVSDK现在支持对空广告时间跟踪URL执行Ping操作，可验证空广告时间的广告时间开始和结束Ping。

**版本1.4.8** (1.4.8.402)

* (ZD #3158) IOS 7在完整事件重播中崩溃

**版本1.4.7** (1.4.7.382)

* (ZD #2197)跟踪广告错误。 为无法加载清单的资产添加了通知。
* (ZD #2894)播放器在播放期间发出四个顶级清单请求。
* (#2992第纳尔) [!DNL Auditude] 报告奇怪的持续时间和标识符。

**版本1.4.6**(1.4.6.325)

* (ZD #2197)跟踪广告错误。 为无法加载清单的资产添加了通知

**版本1.4.5** (1.4.5.283)

* (ZD #2141) Analytics实施，用于 [!DNL TreeHouse] 应用程序，已添加 `AdobeAnalyticsPlugin.a` 库以生成包。
* 视频心率库更新至1.4.1.2
* (PTPALY-4226)(与ZD #2423相关)执行DRM重置可能会导致应用程序文档数据被删除。

**版本1.4.4** (1.4.4.242)

* 视频心率库(VHL)已更新至1.4.1。

* (ZD #2435)有关Analytics需求更新的TV SDK文档

**版本1.4.2** (1.4.2.210 ：iOS 6.0+)

* (#1129第纳尔) `_player.currentItem.audioOptions` 返回空
* (ZD #2109) Primetime PSDK 1.4.1.125不适用于Xcode 5.1.1
* (ZD #2137)无法加载DRM元数据时，iOS上的PSDK崩溃

**版本1.4.1**(1.4.1.125)

* (#1107第纳尔) [!DNL CocoaLumberjack] 重复符号
* (ZD #1644)修改iOS用户代理以进行定位和报告
* (ZD #1850) iOS SDK中包含的Cocoa Lumberjack文件
* (ZD#1908)如果超过1个，则PSDK会忽略自定义标记

**版本1.4.0** (1.4.0.32)

* Zendesk #1024 — 通过清单从流中删除广告的功能

## 设备认证和支持 {#device-certification-and-support}

>[!NOTE]
>
>以下功能包括 **非** 在TVSDK中受支持：
>
>* 在任何平台或版本上慢动作。
>* 现场戏法游戏。


**版本1.4.43**

* TVSDK 1.4.43已针对iOS 11进行认证。

**版本1.4.29**

* TVSDK 1.4.29已通过iOS 10认证。

**版本1.4.28**

* TVSDK 1.4.28已通过iOS 10 Beta 7认证。
* DRM支持通过添加强制HTTPS  `forceHTTPS`  和 `isForcingHTTPS` API。
* 已将VHL库更新为1.5.8，将Mobile库Adobe为4.8.4，并将记录器实用程序库更新为7.0版部署目标。

**版本1.4.19**

此版本的TVSDK已获得对iOS和tvOS的FairPlay支持的认证。

**版本1.4.17**

* tvOS

   此版本的TVSDK包含对tvOS的支持，并且已针对未加密的HLS流进行认证。

   **注释**：请记住以下编译准则：

   * TVSDK tvOs支持仅限于非AdobeDRM加密流。 必须删除对的引用 `drmNativeInterface.framework` 在tvOS内部版本设置中。 仍支持AES加密流。
   * Apple要求所有Apple TV应用程序都启用位码，因此您必须在项目设置中打开此标记。

## 已知问题和限制 {#known-issues-and-limitations}

* 由于iOS UIWebView类已被弃用，在iOS TVSDK 3.6及更高版本中：
   * VPAID广告在iPad 13中无法按预期播放。
   * 伴随广告无法按预期播放。

* 在iOS TVSDK中，所有广告都会拼接到内容清单中。 广告行为是通过基于内容和广告区段的持续时间进行搜索来实现的。 因此，如果区段持续时间不准确，则搜寻可能不会始终在广告时间的开始或结束的确切帧结束。 即使帧具有持续时间，平台本身也会对搜索施加容差，并且可能会显示一些帧或广告或内容。 这是平台以及广告插入在iOS上与TVSDK配合使用的方式的限制。
* 在这种情况下，跳过的决定发生在搜寻事件上。 但是，由于清单中的广告区段持续时间无法准确表示广告的实际持续时间，因此搜寻的帧准确性不高。 因此，在应用广告策略时，您会看到一些广告帧。
* 它可能会体验到，许可证轮换视频不会在iOS 11上播放，并且在iOS 9.x和iOS 10.x上可以正常播放。
* 在VPAID 2.0支持中，如果通过AirPlay活动播放，则会跳过VPAID广告。
* 此 `drmNativeInterface.framework` 将最小目标设置为iOS7（或更高版本）时，无法正确链接。
解决方法：明确指定 `libstdc++.6.dylib` 库，如下所示：转到 **[!UICONTROL Target]** > **[!UICONTROL Build Phases]** > **[!UICONTROL Link Binary With Libraries]** 并添加 `libstdc++.6.dylib`.
* 没有为替换API插入后置广告。
* 在广告时间中搜寻（不退出）会发出重复的广告开始和广告时间通知
* 设置 `currentTimeUpdateInterval` 没有任何效果。
注意：在某些iOS版本中，操作系统不会加载 `PSDKLibrary.framework` 自动。 请务必手动复制 `PSDKResources.bundle` 到应用程序的捆绑包资源：转到 **构建阶段** 和复制捆绑包资源。
* 无法使用Xcode 8或更低版本构建引用应用程序。 iOS TVSDK版本1.4.41及更高版本，使用Xcode 9进行编译。
* VPAID广告不遵守 `delayAdLoadingTolerance` 值。
* 24077 — 对于某些带有字幕的HLS内容，播放器崩溃时间为 _停止_ 或 _重置_ 方法。
* 如果启用了及时广告解析，则详细的错误通知将不可用。
* 错误通知是按广告解决时间而不是按广告序列记录的。
* 此版本中的HEVC支持具有以下限制
   * 不支持DRM
   * CC (CEA 608/708)支持不可用，因为CMAF不支持它。
   * 4K支持尚不存在。
   * ID3标记支持不可用，因为CMAF不支持它。
   * 未验证未混合的实时HEVC流。
   * 未验证HEVC广告支持。
* 启用JIT并将容错设置为10秒后，如果存在VMAP > VAST重定向广告，则第一个中段广告时间不会看到VAST调用。
* 为了使广告分辨率超时正常工作，每次在实时流播放期间更新播放列表时，播放器预计会在20秒内生成一个拼合的播放列表。 如果在上述间隔内未收到拼接的播放列表，则会引发内部错误，并且播放器将停止。

## 有用资源 {#helpful-resources}

* [《 TVSDK 3.4 for iOS程序员指南》](/help/programming/tvsdk-3x-ios-prog/ios-3x-introduction/ios-3x-overview/ios-3x-overview.md)
* [TVSDK iOS 3.4 API参考](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v34/index.html)
* 请参阅完整的帮助文档，网址为 [Adobe Primetime学习与支持](https://experienceleague.adobe.com/docs/primetime.html) 页面。

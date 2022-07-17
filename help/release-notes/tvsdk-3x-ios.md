---
title: 适用于iOS的TVSDK 3.13发行说明
description: 适用于iOS的TVSDK 3.13发行说明介绍了TVSDK iOS 3.13中的新增功能或更改功能、已解决和已知问题以及设备问题。
exl-id: adf8ab23-86d6-4113-b243-2709d5f7f829
source-git-commit: 59ea8008c828f3bdf275fea5cc2a59c37b0c4845
workflow-type: tm+mt
source-wordcount: '7575'
ht-degree: 0%

---

# 适用于iOS的TVSDK 3.13发行说明 {#tvsdk-for-ios-release-notes}

适用于iOS的TVSDK 3.12发行说明介绍了TVSDK iOS 3.12中的新增功能或更改功能、已解决和已知问题以及设备问题。

## 系统和软件要求 {#system-software-requirements}

在下载iOS 3.12之前，请确保您的硬件、操作系统和应用程序版本满足以下要求：

操作系统：iOS 8.0或更高版本。

## iOS TVSDK 3.13

该版本引入了对用于实时、VOD和FER流的已删除的“HLS/CMAF”（前置、中置和后置）广告的支持。

有关客户报告问题的修复，请参阅 [已解决的问题](#resolved-issues). 有关限制，请参阅 [已知问题和限制](#known-issues-and-limitations).

### 以前版本中的新增功能和修复 {#whats-new-previous}

**iOS TVSDK 3.12**

修复了实时流在播放15分钟后失败的问题。

**iOS TVSDK 3.11**

为客户问题提供了修复，其中 `isFallbackOnInvalidCreativeEnabled` 方法 `customParams` 导致应用程序崩溃。

**iOS TVSDK 3.10**

* 修复了TVSDK播放器未触发的问题 `PTMediaPlayerStatusError` 通知。

**iOS TVSDK 3.9**

* 修复了VTT字幕播放失败导致应用程序冻结的问题。

* iOS TVSDK 3.9包含更新的个性化传输证书。

**iOS TVSDK 3.8.0.83修补程序**

修补程序具有更新的个性化传输证书。

**iOS TVSDK 3.8**

iOS 13合规性和处理的iOS 13 `UIWebView` 弃用API。

**iOS TVSDK 3.7**

适用于同时发出多个广告解决请求时停止播放的方案的修补程序。

**iOS TVSDK 3.6**

**修复了类的vastXML属性`PTNetworkAdInfo`**

的 `vastXML` 属性未正确设置，并返回nil值。

**iOS TVSDK 3.5**

**启用背景音频**

*将您的应用程序配置为在音频进入后台时继续播放音频。*

要启用此功能，我们必须设置新的API `audioPlaybackInBackground` 在 `PTMediaPlayer` 类。 启用此API后，您的应用程序即可播放后台音频。

**iOS TVSDK 3.4.0.19（修补程序）**

此版本修复了广告故障切换方案中发生的应用程序崩溃问题。

**iOS TVSDK 3.4**

**广告分辨率超时**

* 借助TVSDK 3.4，用户现在可以为整体广告分辨率和清单下载设置超时值。 如果在给定的超时内某些广告未得到解析，则TVSDK会播放剩余的广告。

* `PTAdMetadata: adRequestTimeout` API已弃用，将被删除。 默认值为35秒。

* 在 `PTAdMetadataClass: adResolutionTimeout`   — 整个广告解析调用adManifestTimeout的超时 — 广告清单下载的超时。

**收入优化**

启用TVSDK以识别与广告插入工作流相关的问题区域，以向Analytics的最终选择点报告。

**版本3.3**

TVSDK 3.3现在与iOS 11 SDK兼容。 所有已弃用的API都已替换为合适的替代方案。

**版本3.2**

**其他日志记录支持（阶段2）**

添加了对错误通知的支持，以防出现以下情况：

* 广告的HLS版本使用的级别比内容高。

* 排除纯音频变体。

* VAST/VMAP请求失败。

**版本3.1**

* **其他日志记录支持**
添加了对广告播放失败时的描述性通知的支持。

* **添加了 [!DNL Fairplay] 加密的CMAF流支持**
   [!DNL Fairplay] 现在支持使用AVC编解码器播放的加密CMAF流。

**版本3.0.1**

此版本中没有新增功能或增强功能。

**版本3.0**

* TVSDK 3.0支持HEVC流。

* 及时 — 解析更靠近广告标记的广告。

添加了 `enableDelayAdLoading` 应用程序级别界面中布尔类型的属性，以启用JIT。 如果 `enableDelayAdLoading` 否，它将 `setadMetadata.delayAdLoading`为True（PTAdMetadata接口的属性）。

启用此属性后，TVSDK会根据定义的容差值，在广告位置之前解析每个广告中断。 默认情况下， `delayAdTolerance` 设置为5秒。

**版本1.4.45**

为符合Xcode10,TVSDK已从 `libstdc++` to `libc++`，因此，支持的最低版本为iOS 7。 早些时候是iOS6号。

**版本1.4.44**

此版本中没有新增功能或增强功能。

**版本1.4.43**

* 类似电视的体验，即能够在广告中间加入而不触发部分广告跟踪。\
   示例：用户在包含三个30秒广告的90秒广告时间的中间（40秒）加入。 这是时间中第二个广告的10秒。

   * 第二个广告在剩余的持续时间（20秒）内播放，随后是第三个广告。
   * 不会触发播放的部分广告（第二个广告）的广告跟踪器。 仅触发第三个广告的跟踪器。

* 添加了 `enableVodPreroll` PTAdMetadata接口中布尔类型的属性。 该属性可用于在VoD流上启用前置。 如果 `enableVodPreroll` 为否，PSDK不会播放前置广告。 但是，这对中间辊没有影响。 默认值为 `enableVodPreroll` 是。
* `closedCaptionDisplayEnabled` API `PTMediaPlayer` 从iOS v1.4.43开始，界面被标记为已弃用。 确定给定的隐藏式字幕是否可用 `PTMediaPlayerItem`，检查 `subtitlesOptions` 财产 `PTMediaPlayerMediaItem`.

**版本1.4.42**

此版本中未添加任何新功能。 有关已修复的问题列表，请参阅 [已解决的问题](#resolved-issues).

**版本1.4.41**

API更改：

* **isSecure**:引入了新的API isSecure，以保护播放器不会记录和引发错误。 默认值为true。

* **allowExternalRecording**:引入了新的API，以允许对安全内容进行空中镜像。 因此，空播镜像被视为记录 `allowExternalRecording` 值必须设置为 `True`，允许播放镜像或将设置为 `False` 用于停止安全内容的播放镜像。 默认情况下， `value` 是真的。

**版本1.4.40**

无新增功能。

**版本1.4.39**

* iOS TVSDK已通过VHL 2.0.1和VHL 2.0.1的认证，并且已通过Nielsen的认证。

* iOS TVSDK已更新，可从新的Akamai主机发出CRS请求 `primetime-a.akamaihd.net`.

* 新的主机名配置可以更大规模地通过HTTP和HTTPS(SSL)来交付CRS资产。

**版本1.4.36**

在iOS TVSDK中集成和验证VHL 2.0 :减少 `VideoHeartbeatsLibrary` 通过降低API的复杂性来实施。

**版本1.4.34**

**网络广告信息**

TVSDK API现在提供有关第三方VAST响应的其他信息。 在 `PTNetworkAdInfo` 可通过  `networkAdInfo`  资产。 此信息可用于与其他Ad Analytics平台集成，例如 **Moat Analytics**.

**版本1.4.31**

* **计费量度** 为了迎合那些只想为所用内容付费（而不是不考虑实际使用情况的固定费率）的客户，Adobe会收集使用量度并使用这些量度来确定向客户收取的费用。

   每次TVSDK生成流开始事件时，播放器都会开始定期向Adobe的计费系统发送HTTP消息。 对于标准VOD、专业VOD（启用中置广告）和实时内容，称为可计费持续时间的时间段可以不同。 每种内容类型的默认持续时间为30分钟，但您与Adobe的合同会确定实际值。

* **对CRS广告的多CDN支持** TVSDK现在支持用于CRS广告的多CDN。 通过提供CRS广告的FTP详细信息，您可以指定CDN位置，而不是默认的Adobe拥有的CDN，例如 [!DNL Akamai].

**版本1.4.29**

在 `PTSDKConfig` 类、 `forceHTTPS` 已添加API。

的 `PTSDKConfig` 类提供了对向Adobe Primetime广告决策、DRM和Video Analytics服务器发出的请求实施SSL的方法。 有关更多信息，请参阅 `forceHTTPS` 和 `isForcingHTTPS` 方法。 如果通过HTTPS加载清单，则TVSDK将保留HTTPS的内容使用，并在加载来自该清单的任何相对URL时遵循此用法。

>[!NOTE]
>
>不会修改对第三方域（如广告跟踪像素、内容和广告URL）的请求以及类似请求，内容提供商和广告服务器有责任提供通过HTTPS支持的URL。

**版本1.4.18**

Primetime iOS TVSDK现在支持VPAID 2.0 JavaScript创意，以启用丰富的交互式流内广告体验。 有关VPAID 2.0的更多信息，请参阅VPAID广告支持。

**版本1.4.17**

* tvOS

   TVSDK支持tvOS本机应用程序。
* 可以播放以下类型的内容：

   * VOD
   * 实时
   * AES-128
   * 备用音频和字幕
   * FER

* 可显示以下类型的广告：

   * 基本
   * VAST2
   * VAST3
   * VMA

* 当前不支持以下功能：

   * Digital Rights Management(DRM)
   * 广告横幅
   * TV标记语言(TVML)

**版本1.4.13**

>[!NOTE]
>
>Nielsen模块已从TVSDK内部版本中删除，TVSDK将很快更新，并新增一个Nielsen集成模块。

**广告回退，广告选择逻辑中的菊花链(Zendesk #3103)**

对于启用回退规则的VAST广告（创意），TVSDK会将MIME类型无效的广告视为空广告，并尝试使用回退广告来替换广告。 您可以配置回退行为的某些方面。 有关更多信息，请参阅VAST和VMAP广告的广告回退。

**版本1.4.9**

**具有替代内容替换的封锁信令**

作为1.4 TVSDK更新的一部分，Adobe现在还支持针对线性内容进行区域封锁并从中返回。 现在，TVSDK可以并行处理主清单文件和备用清单文件，以监视封锁信号，即使替代程序显示代替原始程序时也是如此。

**版本1.4.8**

**视频心率库(VHL)已更新到版本1.5**

* 能够将包含视频开始或视频/广告/章节开始的元数据作为上下文数据发送。

* 网络流量减少 — 心率平均会减少，并且大小会减小。

**版本1.4.7**

* **内部部署个性化支持**

支持在本地安装Adobe个性化服务器，以自定义客户端的个性化请求以转到其他端点。

* **基于分辨率的输出保护**

DRM策略现在可以根据设备的输出保护功能指定允许的最高分辨率。 例如， _如果HDCP可用，则允许播放分辨率高达1080p的内容；如果HDCP不可用，则允许播放分辨率高达480p的内容。_

**版本1.4.4**

* **视频心率库(VHL)已更新到版本1.4.1.1**

   * 添加了将来自其他SDK或播放器的不同分析用例与Adobe Analytics Video Essentials捆绑在一起的功能。
   * 通过删除 `trackAdBreakStart` 和 `trackAdBreakComplete` 方法。 广告时间从 `trackAdStart` 和 `trackAdComplete` 方法调用。
   * 的 `playhead` 跟踪广告时不再需要属性。
   * 添加了对Experience CloudID服务的支持。

* **Nielsen SDK集成**

现在，TVSDK支持将mTVR和MDPR ID3信标发送到Nielsen SDK，而无需任何自定义集成。 要开始使用，请下载3.1.2.19 Nielsen iOS应用程序SDK，并按照《iOS程序员指南》中此处的说明操作。

**版本1.4.0**

* **具有替代内容替换的封锁信令**

作为1.4 TVSDK更新的一部分，TVSDK现在还支持针对线性内容通过区域封锁进入和返回。 现在，TVSDK可以并行处理主清单文件和备用清单文件，以监视封锁信号，即使替代程序显示代替原始程序时也是如此。

* **删除/替换C3广告**

现在，无需进行额外的准备工作，即可将新广告动态插入到从C3窗口发出的视频点播(VOD)资产中。 TVSDK现在提供了一个API，用于删除自定义内容范围和动态插入新广告。 当实时/线性内容在广播期间播放，并且会立即下拉以用作按需内容，而无需适当的时间来清理资产时，此强大的新功能也非常有用。

## 已解决的问题 {#resolved-issues}

如果分辨率与报告的问题相关联，则会显示Zendesk引用，例如ZD#xxxx。

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

* (ZD 42085) — 在CMAF流上播放时出现问题。

* (ZD-43215) — 在广告进行中取消播放器时崩溃。

* (ZD 43210) — 启用WebVTT子标题后，iOS HLS播放冻结。

**iOS TVSDK 3.12**

* 使用适用于iOS 3.10的TVSDK时，实时流在播放15分钟后失败。

### 已解决以前版本中的问题 {#resolved-issues-previous}

**iOS TVSDK 3.11**

* (ZD#40998)- `isFallbackOnInvalidCreativeEnabled` 导致应用程序崩溃。

* (ZD#41289)- `NSInvalidArgumentException` 用方法观察 `customParams` 导致应用程序崩溃。

**iOS TVSDK 3.10**

(ZD#40943)- TVSDK播放器未触发 `PTMediaPlayerStatusError` 通知。

**iOS TVSDK 3.9**

(ZD#40272)- iOS TVSDK无法播放VTT字幕，并出现101001错误，导致应用程序冻结。

**iOS TVSDK 3.8**

* (ZD#40087)- iOS崩溃，且VOD内容过期时出现播放器错误。

* (ZD#40083) — 前置广告不会通过 `OpportunityGenerator` 和播放器会出错。

* (ZD#39828)- `CurrentItem` 属性缺少nullability注释，当通知中包含的播放器状态为时，会导致播放器崩溃 `PTMediaPlayerStatusStopped`.

**iOS TVSDK 3.7**

(ZD#38961) — 当多个内容配置为在PiP中播放时，一个内容完成播放后，内容无法在“画中画(PiP)”窗口中播放。

**iOS TVSDK 3.6**

此版本中没有新问题。

**iOS TVSDK 3.5**

此版本中没有新问题。

**版本3.3**

(ZD#37820) — 为自定义标头HS-Id、HS-SSAI-TAG添加了允许列表。

**版本3.2**

* **票证#36588**  — 调用MediaPlayer STOP方法时，观察到播放器崩溃。

修复了在为一些带字幕的流调用STOP方法时观察到的间歇性崩溃。

* **票证#37080**  — 清单调用出现重复请求。
修复了在播放期间对清单URL发出的重复请求。 TVSDK现在对每个清单进行一次调用。

* **票证#37** - CRS标准化规则失败，包含eq匹配类型修复了播放器在与具有“eq”匹配类型的主机名的上次标准化规则集一起遇到时崩溃的情况。

**版本3.1**

**票#36313**  — 线性广告中断期间的间歇性不可预测结果修复了实时流中线性广告中断期间的间歇性播放。

**版本3.0.1**

**Ticket36948** - CRS -iOS 12中的资产选择顺序不一致为CRS选择的资产并非始终是VAST或VMAP响应中返回的最高质量变体。

**版本3.0**

* **Ticket35311**  — 在电话呼叫中断期间，播放器状态未变为“暂停”添加了中断处理程序，以阻止播放器中断。 中断时，播放器状态变为“暂停”，然后单击播放按钮以继续播放。

* **Ticket36685**  — 实时资产 — 与播放器时间进度和SCTE标记时间不匹配的时间针对处于实时点之前的SCTE标记计算正确的时间。

* **Ticket36492** - `currentTime` 和 `localTime` 暂停状态期间搜索到新位置时未更新现在，当播放器处于暂停状态时，播放器的当前时间可以设置为零；更早之前，仅在播放状态中将当前时间设置为0。

**版本1.4.45**

* **Ticket36294** - iOS TVSDK在Xcode 10中无法正常运行修复了XCode 10中TVSDK存在的编译问题。 由于Xcode 10要求，在适用于iOS 1.4.45的TVSDK上构建的应用程序需要最低部署目标(即iOS 7.0)

* **Ticket36321**  — 在可搜寻范围中， `PTMediaPlayer` 和 `AVPlayer` 实例 _正在播放_ 状态。

* **Ticket36493** - `libstdc++` iOS 12支持修复了iOS 12上TVSDK的编译问题。 在适用于iOS的TVSDK 1.4.45以上版本上构建的应用程序要求最低部署目标为iOS 7.0

**版本1.4.44**

* **Ticket34683**  — 广告播放进度为负

为了处理广告服务器报告的持续时间与实际广告内容之间不匹配的情况，引入了其他检查。

* **Ticket34801** - `currentTime` 和 `localTime` 在暂停状态期间搜索到新位置时，未更新。现在，当播放器处于暂停状态时，可以将播放器的当前时间设置为零；更早之前，仅在播放状态中将当前时间设置为0。

* **Ticket35037**  — 从基于信号的广告插入返回时，播放停顿为错误的URL。
改进了1.4.42版本中针对#34385已解决问题提供的修复。 添加了isCancelled检查和异常处理代码，以使操作队列更加稳健。

**版本1.4.43**

* (ZD#32990)-iOS:在某些提示点上播放内容而不是广告。 `selectedMediaOptionInMediaSelectionGroup` 作为AVPlayerItem接口一部分的API现在已移至 `AVMediaSelection` 在iOS11。 使用此新API解决了该问题。

* (ZD#33683)已删除TVSDK `==` 后缀。 解析逻辑中的问题已修复。

* (ZD#33905)- iOS TVSDK通过两个用户代理调用清单文件。 用户代理问题已在第一次m3u8调用（全新安装案例）中修复。 M3u8现在对所有调用都具有相同的用户代理。

* (ZD#34293) — 在线性流上插入的预滚动体在iOS11上无法正确播放。 已修复前置广告的问题。

* (ZD#34684) — 应用广告跳过策略时，前置广告帧会显示几秒钟。 新的API， `enableVodPreroll` 已引入以在vod播放中禁用前置播放。 此API的默认值为 _是_. API可确保跳过主内容中的广告内容拼合。

* (ZD#34765) — 致电后 `stop()`，则仍很少下载传输流区段。 增强了 `Stop()` 用于避免下载额外区段的API。

* (ZD#34865) — 适用于 [!DNL Livestream] 在iOS上被截断。 与iOS11相关，并添加额外的检查以确认流是前置内容还是主内容，可解决此问题。

* (ZD#35093) — 修复了一种故障转移方案，在该方案中，如果流的主变体在启动时失败（返回404），则播放不会切换到备份流。

**1.4.42(1.4.42.118)**

* (ZD#34385) — 从基于信号的广告插入返回时，播放停止为错误的URL。

   增加 `CustomAVAssetLoaderOperations`，以便能够继续执行清单读取。

* (ZD#34373) — 当不允许流记录时，最终用户无法流到HDMI连接的设备。

* (ZD#32678)- TVSDK在iOS上不收集正确的广告ID。

   如果存在VAST/VMAP重定向，则最终广告创作的广告ID现在会在VHL ping中被提取。

* (ZD#33904) — 未为AVFoundation通知注册TVSDK `AVAudioSessionMediaServicesWereLostNotification` 和 `AVAudioSessionMediaServicesWereResetNotification`.

   `PTMediaServicesWereLostNotification` 和 `PTMediaServicesWereResetNotification` 现在可以在播放器应用程序上注册，以在媒体服务重置或丢失时获取通知。

* (ZD#33815) — 客户无法在无需更新应用程序的情况下更新其优先级和标准化CRS规则。

   添加了 `getCRSRulesJsonURL` 和 `setCRSRulesJsonURL` 到iOS TVSDK的API 。

**版本1.4.41(1.4.41.76)**

* (ZD #34464) — 使用TVSDK版本1.4.41构建引用应用程序时出现问题

   从此版本开始，编译适用于iOS的TVSDK时需要Xcode 9。
* (ZD #29456) — 播放在暂停状态下开始

   修复了在进入播放时视频暂停的暂停问题。
* (ZD #30371) — 当我们在线性流中插入两个以上广告时，AdBreak开始时间会发生更改

   修复了尝试在Apple TV上播放内容时导致无法完全播放的错误
* (ZD #32146) — 否 `PTMediaPlayerStatusError` 接收有关阻止iOS 11开发测试版的HLS实时内容

   否 `PTMediaPlayerStatusError` 接收有关使用Charles阻止的HLS实时内容和VOD内容（丢弃连接和403）。

* (ZD #29242) — 启用广告后播放视频播放失败。

   当启用广告并启用AirPlay开始播放视频时，视频播放从不开始，且不显示错误。

* (ZD#33341)- `DRMInterface.h` 会在Xcode 9中触发生成警告。

   修复了 `DRMInterface.h` 参数列表中缺少“void”一词。

* (ZD#31979) — 对于iPhone 7/iPhone7+，当它是iOS 10或更高版本时，不编译/运行。

   不再支持编译早于iOS 7的IB文档。

* (ZD#32920) — 广告时间内的空白屏幕，没有广告时间结束。

   当广告时间显示广告实例，并且广告实例完成后，将显示空白屏幕。

* (ZD#32509) — 禁用iOS 11屏幕记录禁用iOS 11上的屏幕记录。

* (ZD#33179)- iOS11上的间歇性事件故障。

   修复了iOS 11上的事件失败。

**版本1.4.40** (1.4.40.72)

* (ZD #32465) — 播放器无法处理合并的播放列表。

   调用 `finishLoadingWithError`(具有：错误)，以便AV Foundation尝试替代流/触发故障转移。

* (ZD #31951) — 许可证轮转期间出现TVSDK错误。

   修复了许可证轮换问题。
* (ZD #31951) — 广告时间内的空白屏幕，没有广告时间结束。

   处理了Facebook VPAID广告通常在一个块中返回多个CDATA块的问题 `<AdParameters>` VAST节点。
* (ZD #33336)- iOS TVSDK — 尽管Freewheel返回了足够的广告，但广告Pod仍未填满。

   根据父序列和索引创建序列广告和回退广告之间的父子关系以及排序。

**版本1.4.39** (1.4.39.43)

* (ZD #32178)- iOS TVSDK版本不正确。

   日志文件中的TVSDK版本输出为1.0.211。已修复该版本，可输出正确的版本。

* (ZD #32199) — 延迟广告加载 — 不会为内容显示视频。

   以前未初始化的本地Adbreak时间轴现在在使用之前刷新。

* (ZD #27528) — 如果在iOS 1.2中将辅助音频设置为非默认值，则在资产开始播放后1-45秒内，视频、音频或两者都将冻结。

   准备并通知处于“就绪”状态的音频轨道。

* (ZD #30411) — 如果您选择辅助Sap语言，则可能会收到意外结果，如无音频或音频不正确。

   准备并通知处于“就绪”状态的音频轨道。

* (ZD #32199) — 延迟广告加载 — 不会为内容显示视频。

   以前未初始化的本地Adbreak时间轴现在在使用之前刷新。

* (ZD #27528) — 如果在iOS 1.2中将辅助音频设置为非默认值，则在资产开始播放后1-45秒内，视频、音频或两者都将冻结。

   准备并通知处于“就绪”状态的音频轨道。

* (ZD #30411) — 如果您选择辅助Sap语言，则可能会收到意外结果，如无音频或音频不正确。

   准备并通知处于“就绪”状态的音频轨道。

**版本1.4.38** (1.4.38.860)

* (ZD #29281)-iOS:向CRS请求添加AdSystem和创作ID

基于CRS标准化规则的CRS请求中创作ID和AdSystem的使用

* (ZD #29176) — 崩溃于 `PTAdPolicyDeligate` `satAdBreakAsWatched:position`

现在已处理由于空AdBreak导致的崩溃。

* (ZD #30125) — 程序化广告在iOS平台中不起作用

在iOS中添加了程序化广告支持。

* (ZD #30782)- #EXT-X-PROGRAM-DATE-TIME通知

对于具有实时DRM流的# EXT-X-PROGRAM-DATE-TIME标记，不会触发定时元数据事件。

**版本1.4.37(1.4.37.842)**

* (ZD #28950)- VOD播放问题

将流中的# EXT-X-PLAYLIST-TYPE标记设置为“事件”而不是VOD时，出现播放问题

* (ZD #29281)-iOS:向CRS请求添加AdSystem和创作ID

在基于CRS标准化规则的CRS请求中使用创作ID和AdSystem。

* (ZD #29462)- A&amp;E VOD中的ThuichHub广告导致iOS应用程序崩溃

**版本1.4.36(1.4.36.835)**

* (ZD #29418) — 持续时间为0的提示(#EXT-X-CUE-OUT:0.000)会导致iOS TVSDK停止或崩溃播放。

问题已修复且播放正确开始。

* (ZD #29462)- VOD中的广告导致iOS TVSDK崩溃。

问题已修复。 iOS TVSDK正在筹集 `exception(AUDNetworkAdInfo::initWithAdId)` 而不是处理它。 由于广告ID为空，因此出现异常。

* (ZD #29281) — 将AdSystem和创作ID添加到CRS请求。

在1401和1403请求中包含AdSystem和CreativeId作为新参数（所有其他参数保持不变）。

**版本1.4.35** (1.4.35.830)

* (ZD #27830) — 需要以编程方式确定iOS中隐藏式字幕和子标题之间的差异。

TVSDK现在公开了两种类型，可用于过滤掉所需的标题类型。

* (ZD #29160)- TVSDK iOS上的EXT-X-CUE-OUT广告提示未正确拼合到中。

正在播放EXT-X-CUE-OUT Midroll广告。

* (ZD #29100) — 当用户浏览到电影的结尾时，应用程序崩溃。

修复了与同步相关的多次崩溃。

* (ZD #28785)、(ZD #27712)和(ZD #25076)-iOS应用程序在大型实时事件中崩溃。

修复了与同步相关的多次崩溃。

**版本1.4.34** (1.4.34.815 for iOS 6.0+)

* (ZD #28481) — 由于在这些FER流的广告时间结束时附加的键不正确，导致FER中断

对于FER流，在广告时间结束后插入广告时间之前的键。 此问题已通过附加 *最后查看的键值* 在广告时间结束时。

**版本1.4.33** (1.4.33.803 for iOS 6.0+)

* (ZD# 21701)为子帐户启用CRS

根据CRS后端的要求，通过发送1401 CRS请求的原始创作URL而不是标准化的URL来启用。

* (ZD# 26218)- `PSDKResources.bundle` 加载问题

通过更新资源加载以从所有可用包中查找，此问题已得到解决。

* (ZD# 27460)Midroll首次广告调用 — POST到 `cdn.auditude.com` 返回403。

新的CDN帐户无法处理POSTCDN请求。 此问题已通过更新代码以使 `cdn.auditude.com` 广告请求为GET而不是POST。

**版本1.4.32** (1.4.32.792 for iOS 6.0+)

* (ZD# 27132)支持VMAP广告时间的小数值。

当内容未按定义的广告时间进行分段时，整数会导致意外的广告投放。 通过不将小数值转换为整数，问题得以解决。

* (ZD# 27189)具有EXT-X-DINSCRIPTION-SEQUENCE标记的AES内容未正确播放。

通过将标记放在播放列表的开头，解决了该问题。

**版本1.4.31** (1.4.31.785 for iOS 6.0+)

* (ZD# 24528)实施TVSDK使用量度以用于账单

有关更多信息，请参阅 [计费量度].

* (ZD# 24642)对TVSDK的画中画支持

修复了画中画功能，该功能有时无法正常工作。

* (ZD# 25246)广告时间信号不正确

通过对齐变体清单中的不连续标记，解决了此问题。

* (ZD# 26218)在尝试包含 `PSDKLibrary.framework` 在客户端的应用程序框架中

通过将 `PSDKLibrary.framework` 请求。

* (ZD# 26364)对CRS广告的多CDN支持

有关更多信息，请参阅CRS广告交付的多个CDN支持。

* (ZD# 27028)iOS 10中某些流的播放延迟。

通过为没有M3U8扩展的流提供解决方法，此问题得以解决。

**版本1.4.30** (1.4.30.754 for iOS 6.0+)

在此版本中，针对TVSDK解决了以下问题：

* (ZD# 24180)添加要的自定义标允许列表头。

TVSDK中已添加新的自定义标允许列表头。

* (ZD# 25016)在设置ABR控制参数时随机选择故障转移流

在向ABR设置提供 `initialBitrate` 在包含故障转移URL的流中进行设置。 这可避免播放故障转移流而不是主流。

* (ZD# 25076)崩溃 `PTAuditudeAdResolver loadComplete`

修复了在快速启动/停止包含广告的多个PTMediaPlayer实例期间发生崩溃的问题。

* (ZD# 25960)没有其他订阅的标记会触发元数据更改通知广播

修复了清单中第一个区段之前显示订阅标记时，不会通知该标记的问题。

* (ZD# 26084)PSDK抛出106000.101000。-11833解码器在从上一个广告时间转换回娱乐内容时未找到错误

当VMAP的最后一个广告时间开始时间在总持续时间完成之前时，在某些情况下，直到最后一个广告时间结束后才会插入键。 此问题已修复。

* 视频心率库(VHL)已更新到版本1.5.9，以解决以下问题：

* (ZD #22351)VHL - Analytics:实时视频资产持续时间

通过将  `assetDuration`  API到 `PTVideoAnalyticsTrackingMetadata` 要更新实时/线性流的资产持续时间，并提供用于检查实时流的逻辑。

* (ZD# 22675)VHL - Analytics:更新实时视频资产持续时间

此问题与ZD #22351相同。

* (ZD #25908)VHL - Analytics:Adobe心率事件崩溃

通过更新实施以使用最新版本的VHL for iOS版本1.5.9来提高稳定性和性能，解决了此问题。

* (ZD #25956)VHL - Analytics:反复播放视频时崩溃

此问题与ZD #25908相同。

**版本1.4.29** (1.4.29.743)

* (ZD# 23901)第三方广告未播放

通过迁移到CRS v3 URL结构以在重新打包的URL中包含区域ID，解决了此问题。

* (ZD #25183)tvOS和iOS上DRM播放问题

通过支持多DRM支持所需的多个关键标记，此问题已得到解决。

* (ZD# 25334)TVSDK无法播放cDVR共享内容

通过阻止TVSDK将空字符串转换为绝对URL，解决了此问题。

* (ZD# 25347)在AVURLAsset上设置自定义HTTP标头

通过 `PTNetworkConfiguration` 已添加类。

**版本1.4.28** (1.4.28.722)

* (ZD #24549)多个广告跟踪调用

通过更新时间轴管理器以在创建多个播放器时监听特定对象上的通知，解决了此问题。

* (ZD #24758) `PTManifestLogger` 不支持iOS 8

通过将logger实用程序库更新到版本7.0部署目标，解决了此问题。

* (ZD #24775)由于广告而延迟的流

通过正确计算事件播放列表上的持续时间漂移，此问题得以解决。

* (ZD #24799)某些剧集未在iOS APP上播放

当WebVTT文件受地域限制时，通过使用本地Web服务器进行字幕解决此问题。

**版本1.4.27** (1.4.27.711)适用于iOS 6.0+

* (ZD #24089) — 针对长DVR流上的广告解析进行优化

通过添加多种优化来解决此问题，以缩短在实时/线性流中处理DVR窗口所需的时间。

* (ZD #21554) — 未为 `application-type = video/mp4`

通过使播放器能够对无效资产格式上的正确错误跟踪URL执行Ping操作，解决了此问题。

* (ZD #24424) — 类型的崩溃 `EXC_BAD_ACCESS KERN_INVALID_ADDRESS` 源自内部 `PSDKLib` 用于较新硬件设备上的iOS。

修复了在不同流之间快速切换播放时，因取消分配的媒体播放器实例而发生的崩溃。

* (ZD #24575)- 32位设备上的TVSDK在 `enableDebugLog=true`

已修复在启用日志记录时导致32位设备崩溃的日志格式问题。

**版本1.4.26** (1.4.26.702)适用于iOS 6.0+

* (ZD# 20213) — 对于XCode7,TVSDK FW必须是动态/模块化的

通过使用模块支持更新库来修复

**版本1.4.25** (1.4.25.684)适用于iOS 6.0+

* (ZD #19629) — 进入ATV 4播放时，实时视频暂停

通过在删除旧项目后但在向 `AVQueuePlayer`. 如果没有等待期，则通知会发送到错误的项目。

* (ZD #19856) — 默认启用时不显示字幕

已修复Webvtt播放列表中导致字幕无法正确显示的问题。

* (ZD #21590) — 最新原始版本中的视频性能和跟踪

有关中缺少视频长度的问题 `VideoAnalytics` 已修复。

* (ZD #20202) — 设置自定义字幕样式会使iOS应用程序崩溃

通过在设置子标题样式时添加其他空对象检查，此问题已得到解决。

* (ZD #20709) — 视频开始跟踪中报告为0的视频长度

此问题与(ZD #21590)相同。

* (ZD #22280) — 将Analytics视频长度设置为0

此问题与(ZD #21590)相同。

* (ZD #22592)- Primetime中的Airplay问题

此问题与(ZD #19629)相同。

* (ZD#22922) — 用于iOS的手动比特率切换

通过提供一个用于指定最大比特率的选项，此问题得以解决。

* (ZD #23084) — 仅IPv6网络的Apple合规性

已删除Apple不建议用于IPv6兼容性的符号。

**版本1.4.24** (1.4.24.661)适用于iOS 6.0+

* ZD #2548)- Primetime对移动设备上交互式广告的支持 — VPAID 2.0

如果VPAID广告播放失败，可通过更新逻辑以取消隐藏播放器视图来解决此问题。

* (ZD #20101) — 自定义章节实施在广告播放期间触发章节开始事件

此问题已通过更新 `VideoAnalyticsTracker` 以在章节和非章节边界之间转换时正确检测章节开始/结束。

* (ZD #20784)- Analytics:为实时视频过渡触发内容结束

通过添加逻辑以在视频跟踪会话期间手动触发内容的完成，此问题已得到解决。

更新了以下库：

* 从AdobeMobile库到4.10.0
* 从VHL库到1.5.6
* 从VHL-Nielsen库到1.6.7
* (ZD #21855) — 字幕中置后不播放

在此问题中，重复的不连续标记导致中置后不显示字幕。 通过删除彼此相邻的不连续标记，解决了此问题。

* (ZD #21994) — 中的字符串越界 `PTHLSUtils`

导致崩溃的最可能原因是EXT-X-KEY的URL被引号包围。

* ZD #22074)- `AUDVAST` 在iOS每分钟发生一次崩溃

在版本1.4.23中，修复了由VAST重定向URL中存在不安全字符导致的崩溃。 但是，TVSDK仍在跳过这些广告。

通过处理不安全的字符并允许播放广告，解决了此问题。

* (ZD #22694)- `PTMediaPlayer`.  视图被播放器隐藏

如果VPAID广告播放失败，可通过更新逻辑以取消隐藏播放器视图来解决此问题。

**版本1.4.23** (1.4.23.641)适用于iOS 6.0+

* (ZD #18016) — 网络状况不佳的Primetime SDK无响应

通过改进在 `AVFoundation` 发生，以允许应用程序在错误后处理重新启动。

* (ZD #20580) — 坠机 `PTSplicerManager`

此问题已通过提供额外的保护来避免导致崩溃的并发问题而得到解决。

* (ZD #21782)- iOS错误代码10100

修复了在Adobe访问DRM流上开始播放时TVSDK返回101000错误的问题。

* (ZD #21889) — 在线广告和离线内容播放失败

修复了AES加密离线内容上的广告后播放失败的问题。

* (ZD #22074)- AUDVAST崩溃每分钟在iOS发生一次

通过改进对URL中包含无效字符的第三方VAST广告标记的处理，此问题得以解决。

* (ZD #22257)- TVSDK无法播放DRM流

修复了在Adobe访问DRM流上开始播放时101000返回错误的TVSDK的问题。

**版本1.4.22** (1.4.22.627)适用于iOS 6.0+

* (ZD #18709) — 适用于iOS的TVSDK中崩溃

已修复某些受Adobe访问DRM保护的流上发生崩溃的问题。

* (ZD #18850) — 根据CRS规则更新创意选择逻辑

通过添加.json配置文件以指定创作元素选择优先级，解决了此问题。

* (ZD #19770) — 受保护的AES视频馈送不再播放

修复了某些302个重定向流无法播放的问题。

* (ZD #19629) — 进入ATV 4播放时，实时视频暂停

解决了此问题，方法是在为Apple TV 4设备打开播放时，为实时视频暂停添加一个解决方法。 问题似乎是Apple TV 4问题。

* (ZD #21119) — 广告播放后，TVSDK停止

添加了对使用广告插入时序列IV的AES加密流的支持。

* (ZD #21125) — 提前从实时/线性广告时间返回

添加了对在广告时间播放到结束之前从广告时间提前返回的支持。 通过自定义清单标记指示提前返回。

* (ZD #21224) — 对来自赤麦的标记化流的播放支持

API已添加到 `PTNetworkConfiguration` 类，以将Cookie作为URL参数附加到某些Akamai标记化流的区段上。

* (ZD #21287) — 无关日志

修复了在xcode控制台中默认显示的某些日志语句的问题，即使禁用了日志记录也是如此。

* (ZD #21446) — 广告时间事件有时不是由TVSDK触发

在事件流上，广告时间在上一个版本内部版本中未正确触发。 此内部版本可解决此问题。

**版本1.4.21** (1.4.21.605)适用于iOS 6.0+

* (ZD #20749) — 回退会跳过非空的VAST响应；触发额外的广告跟踪URL

已解决回退广告上重复ping的问题。

**版本1.4.20** (1.4.20.590)适用于iOS 6.0+

* (ZD #18639)- TVSDK对冗长的热记录资产使用了过多的CPU/资源

已在两个级别中修复了CPU/资源的过度使用。 首先，让时间更新函数在全局队列（而不是主线程）上运行，并通过优化CPU使用率，以利用先前处理和缓存的m3u8来解析清单。

* (ZD #19349) — 限制网络连接时跳过前置广告。

通过为应用程序和 `adMetadata.adRequestTimeout` API覆盖默认的10秒超时。

* (ZD #19446) — 实时流上缺少通知

通过允许应用程序订阅 `EXT-X-PROGRAM-DATE-TIME` 在实时流中。

* (ZD #19459) — 准备备用音频时崩溃 `PTMediaPlayerItem` `prepareAudioOptionsWithAVMediaSelectionOptions`
* (ZD #19460) — 崩溃 —  `[PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]`

此问题与Zendesk #19459相同。

* (ZD #19574)- TVSDK不会返回DRM或非DRM内容的M3U8响应数据

在清单文件的初始加载中， `PTMediaPlayerItem.prepareToPlay`，如果加载清单失败，TVSDK不会向应用程序报告失败响应的正文。

通过允许TVSDK将失败响应报告为应用程序错误，此问题已得到解决。

* (ZD #19615) — 回退逻辑不起作用

在当前实施中，回退广告被跳过且未重新打包，除非这些广告采用m3u8格式。 此外，还添加了对重新打包回退广告的支持，以解决此问题。

* (ZD #19770)- TVSDK无法通过302重定向播放任何受保护的AES内容

已修复重定向问题，因为重定向URL被 `cleanConnectionData` 才能用于解析清单。

* (ZD #19856) — 默认情况下启用某些比特率时，不显示字幕

通过处理iOS中不显示字幕的流区段的错误，解决了此问题。

* (ZD #19868) — 当交换无效的创作元素时，TVSDK崩溃

修复了TVSDK中错误地取消分配vast解析器实例的崩溃。

* (ZD #20180) — 有时会跳过VPAID广告

JavaScript mime类型并非始终包含在内或视为有效的mime类型。 通过将JavaScript作为有效的mime类型包含在内，解决了此问题。

* (ZD #20749) — 回退会跳过非空的VAST响应；触发额外的广告跟踪URL

修复了某些创意未重新打包的问题。

**版本1.4.19** (1.4.19.563)适用于iOS 6.0+

* ZD #18639)- TVSDK对冗长的热记录资产使用过多的CPU/资源

通过优化DRM m3u8播放列表，将重写到播放列表中先前已重写的缓存位，解决了此问题。 当您回放实时的m3u8流时，这一点最为相关，在每次区段下载后，都会下载m3u8。

* (ZD#18956)- `player.drmManager` 在iOS演示播放器中设置断点时为nil

此问题已通过更新 `PTMediaPlayer.drmManager` 用于从DRM框架中选取DRManager的API实施。

**版本1.4.18** (1.4.18.557，适用于iOS 6.0+)

* (ZD #18844)跟踪iOS播放器中实时内容的播放头。

通过允许应用程序设置其自身的播放头值，此问题得以解决。

* (Zendesk #18518) — 如果未指定视频名称，则TVSDK的名称将默认为*基于PSDK的播放器。*

通过删除播放器名称的默认值，此问题得以解决。

**版本1.4.17** (1.4.17.545)适用于iOS 6.0+

* (Zendesk #2228) — 增强TVSDK，以返回获取清单的JSON响应

DRM框架不会在内容不是M3U8时发送错误，而是返回零DRMetadata。 在发生M3U8_PARSER_ERROR通知时，通过添加元数据来公开内容，解决了该问题。

* (Zendesk #2231) — 从获取MediaPlayerNotification中不可用的清单时返回错误

与Zendesk相同的决议#2228

* (Zendesk #3304)- VAST 3.0 `[ERRORCODE]` 未填充宏

在 [!DNL Auditude] 当跟踪URL的开头有空格时，SDK无法发送ping命令。

* (Zendesk #17294) — 崩溃 [!DNL SecKeyRawSign]

解决了客户代码使用密钥链时可能发生的崩溃问题。

* (Zendesk #18008) — 支持iOS 8及更高版本的Cookie以支持标记化流

Akamai标记化的流要求在区段请求中发送Cookie，而在iOS 7及更早版本中无法实现这一点。 从iOS 8开始，Apple已添加一个API，用于为区段请求传递Cookie。 现在，TVSDK中提供了此支持。 此外，还添加了对发送用户代理的支持（如果可用）。

* (Zendesk #18166)- TVSDK 1.4.15在使用编译时会发出数百个警告 `DWARF` with `dSYM` 文件选项

所有警告都已解决。

**注意**:为TVSDK添加了与tvOS兼容的库。

**版本1.4.16** (1.4.16.1454)

* Zendesk #3875 — 播放期间选项卡S崩溃

还原OKHTTP对的依赖项 [!DNL Auditude] ，因为TVSDK现在直接使用 `httpurlconnection` 而不是curl。 在进行另一个JNI调用之前，通过清除例外来解决此问题。

* (Zendesk #4487) — 跟踪内容线性渠道

通过在线性流播放会话期间重新初始化视频心率跟踪器，解决了该问题。

* (Zendesk #17919)- Android — 内容搜寻导致心率错误

问题是当章节中存在搜寻时，解决心率处于错误状态的问题

* (Zendesk #18053) — 使用TVSDK的应用程序在棉花糖上崩溃

当TVSDK库使用的Neon代码与YUV相同时，TVSDK在Android™ M操作系统上崩溃 `->` RGB颜色转换。 通过更新通过使用非Neon版本的 `code`.

* (Zendesk #18072)- Android M — 应用程序崩溃

在调用 `MediaCodecList` 和 `MediaCodecInfo` API。 Adobe正在寻求Google对更多洞察的支持。 通过提前加载所有编解码器信息以避免仅在需要编解码器信息时才调用这些API，解决了此问题。

* (Zendesk #18074) — 阿拉伯语字幕在Nexus与Android™ 6.0中不起作用

通过支持Android™ CTS字体映射，此问题得以解决。

**版本1.4.15** (1.4.15.512)适用于iOS 6.0+

**注意**:Nielsen模块已从TVSDK内部版本中删除，但TVSDK不久将会更新新的Nielsen集成模块。

* (ZD #2228) — 从获取中不可用的清单时返回的错误 `MediaPlayerNotification`

添加了元数据，可在通知时显示内容 `M3U8_PARSER_ERROR` 发生。

* (ZD #4437)-Adobe Primetime SDK中的崩溃情况

修复了准备字幕/替代音频时报告的崩溃。

* (ZD #4487) — 跟踪内容线性渠道

允许在线性流播放会话期间重新初始化视频心率跟踪器。

**版本1.4.14** (1.4.14.498)适用于iOS 6.0+

* (ZD #17260) — 崩溃于 `playlistManagerForURL`

修复了由于并发问题导致的间歇性崩溃。

**版本1.4.13** (iOS 6.0+)

* (ZD #3304)- VAST 3.0 `[ERRORCODE]` 未填充宏

   * 如果内联广告的创作效果不佳，则会显示错误代码400。
   * `[ERRORCODE]` 宏已进行URL编码。

* (ZD #3865)心率与IMA广告的集成

修复了视频长度报告不正确的错误。

* 更新了TVSDK演示播放器以支持iOS 9

要正确支持iOS 9，必须配置“应用程序运输安全”例外。 对于演示，ATS将完全禁用。

**版本1.4.12** (1.4.12.464)适用于iOS 6.0+

* (ZD #4521)CRS测试客户端和SSAI

修复了3P URL中错误的反向MD5问题。

**版本1.4.12** (1.4.12.463)适用于iOS 6.0+

* (ZD #2751)CSAI和CRS/增强：处理特定媒体文件URL中的动态元素。

更新了创意重新打包服务，以使用动态创意URL正确处理广告。

* (ZD #3654)1.3.4.166之后PSDK版本中的内存泄漏

修复了 `drmFramework` 在iOS 8.2设备上进行常规播放

* (ZD #3988)在首次播放后向前搜索时，会跳过前置播放

修复了一个错误，以便能够正确禁用广告策略。

* (ZD #4017)请求iOS API在向后搜寻时强制广告播放

通过修复ZD #4279而解决

* (ZD #4279)iOS和桌面上的HLS TVSDK广告插入–302重定向问题

修复了广告资产使用相对重定向URL时的错误

**版本1.4.9** (1.4.9.427)适用于iOS 6.0+

* (ZD #3075)Internet可达性问题 — iOS

添加了检测播放何时停止的通知。

* (ZD #3193)在TVSDK中请求配置文件更改API

已更新 `PTPlaybackInformation` 以显示更新的指示比特率。 已更新 `BITRATE_CHANGE` 通知M3U8报告的比特率更可靠、更准确。

* (ZD #3324)VMAP中没有广告媒体时的Primetime广告报告问题

现在，支持Ping空广告时间跟踪URL，TVSDK会验证广告时间开始和完成空广告时间的ping。

**版本1.4.8** (1.4.8.402)

* (ZD #3158)IOS 7在完整事件重播中崩溃

**版本1.4.7** (1.4.7.382)

* (ZD #2197)跟踪广告错误。 添加了资产通知无法加载清单。
* (ZD #2894)播放器在播放期间发出四个顶级清单请求。
* (ZD #2992) [!DNL Auditude] 报告奇怪的持续时间和标识符。

**版本1.4.6**(1.4.6.325)

* (ZD #2197)跟踪广告错误。 添加了资产通知无法加载清单

**版本1.4.5** (1.4.5.283)

* (ZD #2141)的Analytics实施 [!DNL TreeHouse] 应用程序，已添加 `AdobeAnalyticsPlugin.a` 库来构建包。
* 视频心率库更新到1.4.1.2
* (PTPALY-4226)(与ZD #2423相关)执行DRM重置可能会导致删除应用程序文档数据。

**版本1.4.4** (1.4.4.242)

* 视频心率库(VHL)已更新至1.4.1。

* (ZD #2435)有关Analytics需求更新的TV SDK文档

**版本1.4.2** (1.4.2.210 :iOS 6.0+)

* (ZD #1129) `_player.currentItem.audioOptions` 返回空
* (ZD #2109)Primetime PSDK 1.4.1.125不适用于Xcode 5.1.1
* (ZD #2137)无法加载DRM元数据时，iOS上的PSDK崩溃

**版本1.4.1**(1.4.1.125)

* (ZD #1107) [!DNL CocoaLumberjack] 重复符号
* (ZD #1644)修改iOS用户代理以进行定位和报告
* (ZD #1850)iOS SDK中包含的Cocoa Lumberjack文件
* (ZD#1908)如果自定义标记超过1，则PSDK会忽略自定义标记

**版本1.4.0** (1.4.0.32)

* Zendesk #1024 — 通过清单从流中删除广告的功能

## 设备认证和支持 {#device-certification-and-support}

>[!NOTE]
>
>以下功能包括 **not** 在TVSDK中受支持：
>
>* 在任何平台或版本上慢动作。
>* 现场戏法游戏。


**版本1.4.43**

* TVSDK 1.4.43已通过iOS 11的认证。

**版本1.4.29**

* TVSDK 1.4.29已通过iOS 10的认证。

**版本1.4.28**

* TVSDK 1.4.28已通过iOS 10 Beta 7的认证。
* 支持DRM通过添加  `forceHTTPS`  和 `isForcingHTTPS` API。
* 已将VHL库更新为1.5.8，将Mobile库更新为4.8.4，将日志记录器实用程序库更新为7.0版部署目标。

**版本1.4.19**

此版本的TVSDK已通过iOS和tvOS的FairPlay支持认证。

**版本1.4.17**

* tvOS

   此版本的TVSDK包含对tvOS的支持，并且已针对未加密的HLS流进行认证。

   **注意**:请记住以下编译准则：

   * TVSDK tvOs支持仅限于非AdobeDRM加密流。 必须删除对 `drmNativeInterface.framework` 在tvOS内部版本设置中。 仍支持AES加密流。
   * Apple要求启用所有Apple TV应用程序的bitcode，因此您必须在项目设置中打开此标记。

## 已知问题和限制 {#known-issues-and-limitations}

* 由于弃用了iOS UIWebView类，从iOS TVSDK 3.6开始：
   * VPAID广告在iPad 13中的播放未按预期进行。
   * 配套广告未按预期播放。

* 在iOS TVSDK中，所有广告都会拼合到内容清单中。 广告行为是通过根据内容和广告区段的持续时间进行搜寻来实现的。 因此，如果区段持续时间不准确，则搜寻可能并非总是在广告时间开始或结束的确切帧处结束。 即使持续时间在帧上，平台本身也存在对搜寻的容差，并且可能会显示一些帧或广告或内容。 这对平台以及广告插入在iOS上与TVSDK配合使用的方式存在限制。
* 在这种情况下，搜寻事件会发生跳过的决定。 但是，由于清单中的广告区段持续时间不能准确表示广告的实际持续时间，因此搜寻不准确。 因此，在应用广告策略时，您会看到几帧广告。
* 可能会遇到许可证轮换视频在iOS 11上不播放的情况，并且它在iOS 9.x和iOS 10.x上将可以正常播放。
* 在VPAID 2.0支持中，如果在AirPlay上播放处于活动状态，则会跳过VPAID广告。
* 的 `drmNativeInterface.framework` 将最小目标设置为iOS7（或更高版本）时，无法正确链接。
解决方法：明确指定 `libstdc++.6.dylib` 库如下所示：转到 **[!UICONTROL Target]** > **[!UICONTROL Build Phases]** > **[!UICONTROL Link Binary With Libraries]** 添加 `libstdc++.6.dylib`.
* 未插入后置广告以替换API。
* 在广告时间内进行搜寻（不会退出）会发出重复的广告开始和广告时间通知
* 设置 `currentTimeUpdateInterval` 没有任何效果。
注意：在某些iOS版本中，操作系统不会在 `PSDKLibrary.framework` 自动。 手动复制 `PSDKResources.bundle` 到应用程序的包资源：转到 **构建阶段** 和复制捆绑资源。
* 无法使用Xcode 8或更低版本构建引用应用程序。 iOS TVSDK版本1.4.41之后，使用Xcode 9进行编译。
* VPAID广告不遵守 `delayAdLoadingTolerance` 值。
* 24077 — 对于某些带有字幕的HLS内容，播放器崩溃 _停止_ 或 _重置_ 方法。
* 如果启用了“仅为时间广告”解析，则将不提供详细的错误通知。
* 错误通知按广告解决时间记录，而不按广告序列记录。
* 此版本中的HEVC支持具有以下限制
   * 不支持DRM
   * CC(CEA 608/708)支持不可用，因为CMAF不支持CC(CEA )。
   * 尚未提供4K支持。
   * ID3标记支持不可用，因为CMAF不支持ID3标记。
   * 未验证未混合的实时HEVC流。
   * 未验证HEVC广告支持。
* 启用JIT并将容差设置为10秒后，如果存在VMAP > VAST重定向广告，则在第一个媒体广告时间中不会看到VAST调用。
* 为了使广告分辨率超时正常工作，每次在实时流播放期间更新播放列表时，播放器都需要在20秒内生成一个拼合的播放列表。 如果在所述间隔内未收到拼合的播放列表，则会引发内部错误，并且播放器停止。

## 有用资源 {#helpful-resources}

* [适用于iOS的TVSDK 3.4程序员指南](/help/programming/tvsdk-3x-ios-prog/ios-3x-introduction/ios-3x-overview/ios-3x-overview.md)
* [TVSDK iOS 3.4 API参考](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v34/index.html)
* 请参阅以下完整帮助文档： [Adobe Primetime学习与支持](https://experienceleague.adobe.com/docs/primetime.html) 页面。

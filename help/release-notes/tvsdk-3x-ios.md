---
title: TVSDK 3.10 for iOS发行说明
description: TVSDK 3.10 for iOS发行说明描述了TVSDK iOS 3.10中的新增功能或更改功能、已解决和已知问题以及设备问题。
translation-type: tm+mt
source-git-commit: c6036a6777e9158861850b60dd1e0749c30fa280

---


# TVSDK 3.10 for iOS发行说明 {#tvsdk-for-ios-release-notes}

TVSDK 3.10 for iOS发行说明描述了TVSDK iOS 3.10中的新增功能或更改功能、已解决和已知问题以及设备问题。

## 系统和软件要求 {#system-software-requirements}

在下载iOS 3.10之前，请确保硬件、操作系统和应用程序版本满足以下要求：

操作系统：iOS 8.0或更高版本。

## iOS TVSDK 3.10

修复了当网络不可用时TVSDK播放器不触发PTMediaPlayerStatusError通知的问题。

有关当前版本中的修复，请参 [阅已修复的客户问题](#resolved-issues) ，有关限制，请参 [阅已知问题和限制部分](#known-issues-and-limitations) 。

### 先前发行版中的新增功能和修复 {#whats-new-previous}

**iOS TVSDK 3.9**

* 修复了VTT字幕无法播放导致应用程序冻结的问题。

* iOS TVSDK 3.9包含更新的个性化传输证书。

**iOS TVSDK 3.8.0.83修补程序**

修补程序具有更新的个性化传输证书。

**iOS TVSDK 3.8**

iOS 13规范和处理了iOS 13 UIWebView API弃用。

**iOS TVSDK 3.7**

同时发出大量广告分辨率请求时停止播放的场景的修补程序。

**iOS TVSDK 3.6**

**类的vastXML属性中的修复`PTNetworkAdInfo`**

vastXML属性未正确设置，返回nil值。

**iOS TVSDK 3.5**

**启用背景音频**

*将应用程序配置为在音频进入后台时继续播放。*

要启用此功能，我们需要设置PTMediaPlayer类 `audioPlaybackInBackground` 中添加的新API。 启用此API后，您的应用程序就可以播放背景音频了。

**iOS TVSDK 3.4.0.19（修补程序）**

此版本修复了广告故障切换场景中发生的应用程序崩溃问题。

**iOS TVSDK 3.4**

**广告分辨率超时**

* 使用TVSDK 3.4，用户现在可以为整体广告分辨率和清单下载设置超时值。 如果在给定超时内，某些广告未解决，TVSDK将播放其余广告。

* PTAd元数据：adRequestTimeout API已弃用，将被删除。 默认值已设置为35秒。

* 在PTAdMetadataClass中引入了两个新的备用API:adResolutionTimeout —— 针对广告分辨率调用的总超时adManifestTimeout —— 广告清单下载的超时。

**收入优化**

使TVSDK能够识别与广告插入工作流程相关的问题区域，以便向分析最终选择点报告。

**版本3.3**

TVSDK 3.3现在符合iOS 11 SDK的规范。 所有已弃用的API都已替换为合适的替代项。

**版本3.2**

**其他日志记录支持（阶段2）**

添加了对错误通知的支持，以防出现以下情况：

* HLS版本的广告使用的级别高于内容。

* 排除仅音频变体。

* VAST/VMAP请求失败。

**版本3.1**

* **其他记录支**&#x200B;持在广告播放失败时增加对描述性通知的支持。

* **新增了Fairplay加密CMAF流支持** Fairplay加密CMAF流，现在支持AVC编解码器回放。

**版本3.0.1**

此版本中没有新增功能或增强功能。

**3.0版**

* TVSDK 3.0支持HEVC流。

* 及时——在更靠近广告标记的地方解析广告。

在应 `enableDelayAdLoading` 用程序级界面上添加了布尔类型属性以启用JIT。 如 `enableDelayAdLoading` 果为NO，则将其 `setadMetadata.delayAdLoading`设置为True（PTAdMetadata接口的属性）。

启用此属性后，TVSDK会根据定义的容差值在其位置之前解析每个广告中断。 默认情况下， `delayAdTolerance` 设置为5秒。

**版本1.4.45**

为了符合Xcode10,TVSDK从“`libstdc++`”改为“`libc++`”，因此支持的最低版本为iOS 7。 更早的版本是iOS 6。

**版本1.4.44**

此版本中没有新增功能或增强功能。

**版本1.4.43**

* 类似电视的体验，即能够在广告中间加入广告而不会触发部分广告跟踪。\
   示例：用户在包含3个30秒广告的90秒广告分时段中间（40秒）加入。 这是片段内第二个广告的10秒。

   * 第二个广告在剩余持续时间（20秒）内播放，然后是第三个广告。
   * 不会触发已播放部分广告（第二个广告）的广告跟踪器。 只触发第三个广告的跟踪器。

* 在PTAdMetadata界面中添加了布尔类型的enableVodPreroll属性。 该属性可用于在VoD流上启用预滚动。 如果enableVodPreroll为NO，则PSDK不播放预卷。 然而，这并不会影响到这些人。 enableVodPreroll的默认值为YES。
* closedCaptionDisplayEnabled API of PTMediaPlayer interface从iOS v1.4.43开始标记为已弃用。 要确定给定PTMediaPlayerItem是否提供隐藏式字幕，请检查PTMediaPlayerMediaItem的subtitlesOptions属性。

**版本1.4.42**

此版本中不添加任何新功能。 有关已修复的问题列表，请参阅已 [解决的问题](#resolved-issues)。

**版本1.4.41**

API更改：

* **isSecure**:引入了新的API isSecure，以保护播放器不会录制和引发错误。 默认值为true。

* **allowExternalRecording**:引入了新的API以允许对安全内容进行播放镜像。 Airplay镜像视为录制，因此 `allowExternalRecording` 必须将值设置为 `True`，以允许Airplay镜像或设置为停 `False` 止安全内容的Airplay镜像。 默认情况下， `value` 为true。

**版本1.4.40**

无新增功能。

**版本1.4.39**

* iOS TVSDK通过VHL 2.0.1和VHL 2.0.1认证，Nielsen通过。

* 更新iOS TVSDK以从新的Akamai主机发出CRS请求 `primetime-a.akamaihd.net`。

* 新的主机名配置通过HTTP和HTTPS(SSL)提供更大规模的CRS资产交付。

**版本1.4.36**

在iOS TVSDK中集成和认证VHL 2.0:通过降低API的复 `VideoHeartbeatsLibrary` 杂性来减少实施中的障碍。

**版本1.4.34**

**网络广告信息**

TVSDK API现在提供有关第三方VAST响应的其他信息。 广告ID、广告系统和VAST广告扩展在可通过广告资产的 `PTNetworkAdInfo` 属性访问的类 `networkAdInfo` 中提供。 此信息可用于与其他Ad Analytics平台(如 **Moat Analytics)集成**。

**版本1.4.31**

* **计费指标** -为了迎合那些希望只支付其使用费用而不是固定费率的客户，Adobe会收集使用指标并使用这些指标来确定向客户收取的费用。

   每当TVSDK生成流启动事件时，播放器就会开始定期向Adobe的计费系统发送HTTP消息。 对于标准VOD、专业VOD（启用中间广告）和实时内容，期间（称为可计费持续时间）可以不同。 每种内容类型的默认持续时间为30分钟，但您与Adobe的合同将决定实际值。

* **针对CRS Ads的多CDN支持** TVSDK现在支持针对CRS广告的多CDN。 通过为CRS广告提供FTP详细信息，您可以指定CDN位置，而不是默认的Adobe拥有的CDN（如Akamai）。

**版本1.4.29**

在类 `PTSDKConfig` 中，已添加forceHTTPS API。

该 `PTSDKConfig` 类提供了对向Adobe Primetime广告决策、DRM和视频分析服务器发出的请求实施SSL的方法。 有关详细信息，请参 `forceHTTPS` 阅此类 `isForcingHTTPS` 的和方法。 如果清单是通过HTTPS加载的，则TVSDK会保留HTTPS的内容使用，并在从清单加载任何相对URL时考虑这种使用。

>[!NOTE] 对第三方域（如广告跟踪像素、内容和广告URL）的请求以及类似请求均不予修改，内容提供商和广告服务器有责任提供通过HTTPS支持的URL。
> 

**版本1.4.18**

Primetime iOS TVSDK现在支持VPAID 2.0 Javascript创意，以实现丰富的交互式流内广告体验。 有关VPAID 2.0的详细信息，请参阅VPAID广告支持。

**版本1.4.17**

* tvOS

   TVSDK支持tvOS本机应用程序。
* 可以播放以下类型的内容：

   * VOD
   * 实时
   * AES-128
   * 替代音频和字幕
   * FER

* 可显示以下类型的广告：

   * 基本
   * VAST2
   * VAST3
   * VMA

* 当前不支持以下功能：

   * 数字版权管理(DRM)
   * 广告横幅
   * 电视标记语言(TVML)

**版本1.4.13**

>[!NOTE] Nielsen模块已从TVSDK版本中删除，TVSDK将在不久的将来用新的Nielsen集成模块进行更新。


**广告回退，广告选择逻辑中的菊花链(Zendesk #3103)**

对于启用回退规则的VAST广告（创意）,TVSDK将MIME类型无效的广告视为空广告并尝试在其位置使用回退广告。 您可以配置回退行为的某些方面。 有关详细信息，请参阅VAST和VMAP广告的广告回退。

**版本1.4.9**

**具有替代内容替换的封锁信令**

作为1.4 TVSDK更新的一部分，我们现在还支持针对线性内容进行区域封锁后进入和返回。 TVSDK现在可以并行处理两个清单文件（主文件和备用文件），以监视断电信号，即使当替代原始编程显示备用程序时也是如此。

**版本1.4.8**

**更新到版本1.5的视频心率库(VHL)**

* 能够将视频开始和／或视频／广告／章节开始作为上下文数据发送元数据。

* 网络流量更少——心率平均更小，且更小。

**版本1.4.7**

* **预置个性化支持**

支持Adobe Indelication Server的预置安装，以自定义客户端的个性化请求以转到其他端点。

* **基于分辨率的输出保护**

DRM策略现在可以根据设备的“输出保护”功能指定允许的最高分辨率。 例如，“如果HDCP可用，则允许播放分辨率高达1080p的内容，如果HDCP不可用，则允许播放分辨率高达480p的内容”。

**版本1.4.4**

* **视频心率库(VHL)更新至版本1.4.1.1**

   * 添加了将其他SDK或播放器中的不同分析用例与Adobe Analytics Video Essentials捆绑在一起的功能。
   * 通过删除和方法优化了广告 `trackAdBreakStart` 跟踪 `trackAdBreakComplete` 功能。 广告中断从和方法调 `trackAdStart` 用中 `trackAdComplete` 推断出来。
   * 跟踪 `playhead` 广告时不再需要该属性。
   * 添加了对Marketing Cloud访客ID的支持。

* **Nielsen SDK集成**

TVSDK现在支持将mTVR和MDPR ID3信标发送到Nielsen SDK，而无需任何自定义集成。 要开始，请下载3.1.2.19 Nielsen iOS App SDK，然后按照iOS Programmers Guide中此处提供的说明操作。

**版本1.4.0**

* **具有替代内容替换的封锁信令**

作为1.4 TVSDK更新的一部分，TVSDK现在还支持针对线性内容的区域封锁进入和返回。 TVSDK现在可以并行处理两个清单文件（主文件和备用文件），以监视断电信号，即使当替代原始编程显示备用程序时也是如此。

* **删除／替换C3广告**

现在，无需再进行任何准备工作，即可将新广告动态插入从C3窗口发出的视频点播(VOD)资产中。 TVSDK现在提供了一个API，用于删除自定义内容范围和动态插入新广告。 当直播／线性内容在广播期间出现并且立即被拉下来作为点播内容使用时，这一强大的新功能在没有适当时间“清理”资产的情况下也很有用。

## 已解决的问题 {#resolved-issues}

如果分辨率与报告的问题相关联，则显示Zendesk引用，例如ZD#xxxxx。

<!-- 

Comment Type: draft

<note type="note"> 
 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 
</note>

 -->

<!--
Comment Type: draft

<note type="note"> 
 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 
</note>
 -->

**iOS TVSDK 3.10**

(ZD#40943)-当网络不可用时，TVSDK播放器不会触发PTMediaPlayerStatusError通知。

### 已解决先前版本中的问题 {#resolved-issues-previous}

**iOS TVSDK 3.9**

(ZD#40272)- iOS TVSDK无法播放VTT字幕，出现101001错误并导致应用程序冻结。

**iOS TVSDK 3.8**

* (ZD#40087)-对于过期的VOD内容，iOS崩溃，并出现播放器错误。

* (ZD#40083)- Pre-Roll广告不播放实时流，播放器 `OpportunityGenerator` 显示错误。

* (ZD#39828)- `CurrentItem` 属性缺少可空注释，当通知中包含的播放器状态为时，会导致播放器崩溃 `PTMediaPlayerStatusStopped`。

**iOS TVSDK 3.7**

* (ZD#38961)-当将多个内容配置为在PiP中播放时，在一个内容完成播放后，内容无法在画中画(PiP)窗口中播放。

**iOS TVSDK 3.6**

* 此版本中没有新问题。

**iOS TVSDK 3.5**

* 此版本中没有新问题。

**版本3.3**

* (ZD#37820)-为自定义标题HS-Id、HS-SSAI-TAG添加了白名单。

**版本3.2**

**Ticket#36588** —— 调用MediaPlayer STOP方法时，会观察到播放器崩溃。

修复了在对带字幕的少数流调用STOP方法时观察到的间歇性崩溃。

**Ticket#37080** - Manifest调用发现重复请求。

修复了在播放期间对清单URL发出的重复请求。 TVSDK现在对每个清单发出一个呼叫。

**Ticket#37** - CRS标准化规则失败，且EQ匹配类型

修复了在遇到具有“eq”匹配类型的主机名的上次标准化规则集时播放器会崩溃的情况。

**版本3.1**

**票证#36313** —— 线性广告中断期间的间歇性不可预测结果

修复了实时流中线性广告中断期间的间歇播放。

**版本3.0.1**

**Ticket36948** - CRS - iOS 12上的资产选择顺序不一致

为CRS选择的资产并不总是在VAST或VMAP响应中返回的最高质量变体。

**3.0版**

**Ticket35311** —— 在电话呼叫中断期间，播放器状态未变为“暂停”

添加了中断处理程序以阻止播放器中断。 中断时，播放器状态变为“暂停”，然后单击播放按钮后继续播放。

**Ticket36685** —— 实时资产——时间与播放器时间进度和SCTE标记时间不匹配

将为处于实时点之前的SCTE标记计算正确的时间。

**Ticket36492** - `currentTime` 在 `localTime` 暂停状态期间搜索新位置时不更新

当播放器处于暂停状态时，播放器的当前时间现在可以设置为零；以前，仅在播放状态中将当前时间设置为零。

**版本1.4.45**

**Ticket36294** - iOS TVSDK在Xcode 10中无法正常使用

修复了XCode 10上的TVSDK的编译问题。 由于XCode 10要求，从iOS 1.4.45版的TVSDK上构建的应用程序要求最低部署目标（如iOS 7.0）

**Ticket36321** —— 在“播放”状态中，在可搜索 `PTMediaPlayer` 范围 `AVPlayer` 与实例之间观察到的差异。
**Ticket36493** - `libstdc++` iOS 12支持

修复了iOS 12上TVSDK的编译问题。 从iOS 1.4.45版到TVSDK上构建的应用程序要求最低部署目标（如iOS 7.0）

**版本1.4.44**

**Ticket34683** —— 广告播放进度时间呈负数

当广告服务器报告的持续时间与实际广告内容之间不匹配时，将进行其他检查以处理这种情况。

**Ticket34801** —— 当在暂停状态期间搜索到新位置时，currentTime和localTime未更新

当播放器处于暂停状态时，播放器的当前时间现在可以设置为零；以前，仅在播放状态中将当前时间设置为零。

**Ticket35037** —— 从基于信号的广告插入返回时，播放会停止，并且URL不正确。

改进了针对1.4.42版中已解决问题#34385的修复。 添加了isCancelled检查和异常处理代码，使操作队列更加健壮。

**版本1.4.43**

* (ZD#32990)- iOS:内容播放而不是某些提示点上的广告。 `selectedMediaOptionInMediaSelectionGroup` 作为AVPlayerItem接口一部分的API现在在iOS 11中移到AVMediaSelection下。 使用此新API解决了该问题。
* (ZD#33683)从元数据字符串中删除了TVSDK ==后缀。 解析逻辑中修复了该问题。
* (ZD#33905)-iOS TVSDK使用两个用户代理调用清单文件。 用户代理问题已在第一次m3u8呼叫（新安装案例）中得到修复。 M3u8现在为所有呼叫拥有相同的用户代理。
* (ZD#34293)-在iOS11上无法正确播放在线性流上插入的预卷。 预卷广告的问题已修复。
* (ZD#34684)-应用广告跳过策略时，将显示前滚广告帧数秒。 新的API enableVodPreroll现已引入，可在vod播放中禁用预卷播放。 此API的默认值为“是”。 API可确保跳过主内容中的广告内容拼接。
* (ZD#34765)-调用stop()后，仍可下载少数传输流区段。 增强了Stop()API以避免下载额外的区段。
* (ZD#34865)-在iOS上，实时流的前置广告会被截断。 与iOS11相关，并添加一个额外的检查以确认流是前置内容还是主内容，可解决此问题。
* (ZD#35093)-修复了在启动时，如果流的主变体失败（返回404），则播放不切换到备份流的故障切换场景。

**1.4.42 (1.4.42.118)**

* (ZD#34385)-从基于信号的广告插入返回时，播放会停止，并且URL不正确。

   增加最大并发计数 `CustomAVAssetLoaderOperations`，以便清单读取可继续执行。
* (ZD#34373)-当禁止流录制时，最终用户无法流化到连接HDMI的设备。
* (ZD#32678)- TVSDK在iOS上不收集正确的广告ID。

   在VHL ping中，如果出现VAST/VMAP重定向，最终广告创意的广告ID现在会被拾取。
* (ZD#33904)- TVSDK未注册AVFoundation通知 `AVAudioSessionMediaServicesWereLostNotification` 和 `AVAudioSessionMediaServicesWereResetNotification`。

   `PTMediaServicesWereLostNotification` 现在， `PTMediaServicesWereResetNotification` 可以在播放器应用程序上注册，以在媒体服务重置或丢失时获取通知。

* (ZD#33815)-客户无需应用程序更新，就无法更新其优先级和标准化CRS规则。

   向iOS `getCRSRulesJsonURL` TVSDK添 `setCRSRulesJsonURL` 加了和API。

**版本1.4.41(1.4.41.76)**

* (ZD #34464)-在TVSDK版本1.4.41中构建参考应用程序时出现的问题

   从此版本开始，编译适用于iOS的TVSDK需要Xcode 9。
* (ZD #29456)-播放以暂停状态开始

   修复了进入播放时视频暂停时的暂停问题。
* (ZD #30371)-当我们在线性流中插入超过2个广告时，AdBreak开始时间会发生变化

   修复了尝试在Apple TV上播放内容时出错的问题，该错误会完全阻止播放
* (ZD #32146)-阻止iOS 11 `PTMediaPlayerStatusError` dev beta时，未收到HLS Live内容的通知

   使用 `PTMediaPlayerStatusError` Charles时，不会收到HLS Live和VOD内容的阻止（Drop connection和403）
* (ZD #29242)-启用广告后播放视频播放失败

   启用广告并启用AirPlay开始播放视频时，视频回放从不开始，不会显示错误
* (ZD#33341)-触发器 `DRMInterface.h` 在Xcode 9中构建警告

   修复了两个块原 `DRMInterface.h` 型，它们的参数列表中缺少“void”一词
* (ZD#31979)-对于iPhone 7/iPhone7+，如果iOS 10或更高版本，则不编译／运行

   不再支持针对iOS 7之前版本编译IB文档的修复
* (ZD#32920)-广告中断内的白屏，无广告中断完成

   当广告中断显示广告实例时，在广告实例完成后，将显示白屏
* (ZD#32509)-停用iOS 11屏幕录制在iOS 11上停用屏幕录制

* (ZD#33179)- iOS11上的间歇性事件故障

   修复了iOS 11上的事件失败

**版本1.4.40** (1.4.40.72)

* (ZD #32465)-播放器无法处理合并的播放列表。

   呼叫 `finishLoadingWithError`(通过：错误)，以使AV基础尝试替代流／触发故障转移。

* (ZD #31951)-许可证轮替期间TVSDK错误。

   修复了许可证轮替问题。
* (ZD #31951)-广告中断内的白屏，无广告中断完成。

   解决了Facebook VPAID广告通常在单个 `<AdParameters>` VAST节点中返回多个CDATA块的问题。
* (ZD #33336)- iOS TVSDK —— 广告窗格未填充，尽管Freewheel返回了足够多的广告。

   在序列广告和备用广告之间创建父子关系，并根据父序列和索引进行排序。

**版本1.4.39** (1.4.39.43)

* (ZD #32178)- iOS TVSDK版本不正确。

   日志文件中的TVSDK版本输出为1.0.211。修复了该问题，以输出正确的版本。

* (ZD #32199)-延迟广告加载——不显示内容的视频。

   以前未初始化的本地Adbreak时间线现在在使用前刷新。

* (ZD #27528)-如果在iOS 1.2上将辅助音频设置为非默认值，则在资产开始播放后1-45秒内，视频、音频或两者将冻结。

   准备音轨并通知其处于“就绪”状态。

* (ZD #30411)-如果选择辅助Sap语言，您可能会收到意外结果，如无音频或不正确的音频。

   准备音轨并通知其处于“就绪”状态。

* (ZD #32199)-延迟广告加载——不显示内容的视频。

   以前未初始化的本地Adbreak时间线现在在使用前刷新。

* (ZD #27528)-如果在iOS 1.2上将辅助音频设置为非默认值，则在资产开始播放后1-45秒内，视频、音频或两者将冻结。

   准备音轨并通知其处于“就绪”状态。

* (ZD #30411)-如果选择辅助Sap语言，您可能会收到意外结果，如无音频或不正确的音频。

   准备音轨并通知其处于“就绪”状态。

**版本1.4.38** (1.4.38.860)

* (ZD #29281)- iOS:向CRS请求添加AdSystem和Creative Id

基于CRS规范规则的CRS请求中创意ID和AdSystem的使用

* (ZD #29176)- Crash on `PTAdPolicyDeligate``satAdBreakAsWatched:position`

现在已处理空AdBreak导致的崩溃。

* (ZD #30125)-程序化广告在iOS平台中不起作用

在iOS中增加了程序化广告支持。

* (ZD #30782)- #EXT-X-PROGRAM-DATE-TIME通知

对于具有实时DRM流的# EXT-X-PROGRAM-DATE-TIME标签，不会触发定时元数据事件。

**版本1.4.37(1.4.37.842)**

* (ZD #28950)- VOD播放问题

流中# EXT-X-PLAYLIST-TYPE标签设置为“事件”而非VOD时的播放问题

* (ZD #29281)- iOS:向CRS请求添加AdSystem和Creative Id

在基于CRS标准化规则的CRS请求中使用创意ID和AdSystem。

* [ZD #29462)- A&amp;E VOD中导致iOS应用程序崩溃的TurichHub广告

**版本1.4.36(1.4.36.835)**

* (ZD #29418)-持续时间为0的提示(#EXT-X-CUE-OUT:0.000)导致iOS TVSDK停止或崩溃播放。

问题已修复，并且正确开始播放。

* (ZD #29462)-在iOS TVSDK上导致崩溃的VOD中的广告。

问题已修复。 iOS TVSDK正在提出并 `exception(AUDNetworkAdInfo::initWithAdId)` 未处理它。 此例外是由空广告ID造成的。

* (ZD #29281)-向CRS请求添加AdSystem和Creative ID。

在1401和1403请求中将AdSystem和CreativeId作为新参数包含在内（所有其他参数保持不变）。

**版本1.4.35** (1.4.35.830)

* (ZD #27830)-需要以编程方式确定iOS中隐藏字幕和子标题之间的差异。

TVSDK现在显示两种类型，可用于过滤掉所需的题注类型。

* (ZD #29160)- EXT-X-CUE-OUT广告提示在TVSDK iOS上无法正确插入。

EXT-X-CUE-OUT Midroll广告正在播放。

* (ZD #29100)-当用户浏览到电影结尾时，应用程序崩溃。

修复了与同步相关的多个崩溃。

* (ZD #28785),(ZD #27712)和(ZD #25076)- iOS应用程序在大型实时活动期间崩溃。

修复了与同步相关的多个崩溃。

**版本1.4.34** （适用于iOS 6.0+的1.4.34.815）

* (ZD #28481)-由于这些FER流的广告中断结尾附加了错误的密钥，导致FER中断

对于FER流，广告中断前的键在广告中断结束后插入。 此问题已通过在广告中断的 *结尾附加上* “最后看到的键”来解决。

**版本1.4.33** （适用于iOS 6.0+的1.4.33.803）

* (ZD# 21701)为子帐户启用CRS

根据CRS后端的要求，通过发送1401 CRS请求的原始创意URL而非标准化URL来启用。

* (ZD# 26218)- PSDKResources.bundle加载问题

通过更新资源加载以从所有可用包中查找，解决了此问题。

* (ZD# 27460)Midroll第一个广告电话— POST将返回403 `cdn.auditude.com` 个电话。

新的CDN帐户无法处理POST CDN请求。 通过更新代码以将广告请求设为GET而 `cdn.auditude.com` 非POST，解决了此问题。

**版本1.4.32** （适用于iOS 6.0+的1.4.32.792）

* (ZD# 27132)支持VMAP广告分段的小数值。

当内容未按定义的广告分段时，整数会导致意外的广告投放。 不将小数值转换为整数，从而解决了该问题。

* (ZD# 27189)带有EXT-X-DINSTRUCTION-SEQUENCE标签的AES内容播放不正确。

通过将标记放在播放列表的开头，解决了该问题。

**版本1.4.31** （适用于iOS 6.0+的1.4.31.785）

* (ZD# 24528)实施TVSDK使用量度以进行计费

有关详细信息，请参 [阅计费指标]。

* (ZD# 24642)对TVSDK的画中画支持

画中画功能（在某些情况下无法正常使用）已得到修复。

* (ZD# 25246)错误的广告中断信号

通过对齐不同清单上的不连续标签，解决了此问题。

* (ZD# 26218)当尝试将PSDKLibrary.framework包含在客户端的应用程序框架中时，应用程序构建过程变得复杂

通过按请求打包PSDKLibrary.framework解决了此问题。

* (ZD# 26364)对CRS广告的多CDN支持

有关详细信息，请参阅CRS广告交付的多个CDN支持。

* (ZD# 27028)在iOS 10中播放某些流的延迟。

通过为没有M3U8扩展的流提供补救方法解决了此问题。

**版本1.4.30** （适用于iOS 6.0+的1.4.30.754）

此版本中的TVSDK解决了以下问题：

* (ZD# 24180)向白名单添加自定义标题

TVSDK白名单中已添加新的自定义头。

* (ZD# 25016)设置ABR控制参数时，会随机选择故障转移流

解决了此问题的方法是，在ABR设置在包含故障转移URL的流上提供initialBitrate设置时，按顺序维护ABR流。 这将避免播放故障转移流而不是主流。

* (ZD# 25076)PTAuditudeAdResolver loadComplete上的崩溃

修复了在快速启动／停止包含广告的多个PTMediaPlayer实例期间发生崩溃的问题。

* (ZD# 25960)没有其他订阅的标签用于触发元数据更改通知广播

修复了在清单中第一段之前显示订阅标记时不通知该标记的问题。

* (ZD# 26084)PSDK抛出106000.101000.-11833解码器在从最后一个广告中断转换回娱乐内容时未发现错误

当来自VMAP的最后一个广告中断开始时间落在总持续时间之前时，在某些情况下，键直到最后一个广告中断结束后才插入。 此问题已修复。

* 视频心率库(VHL)已更新至版本1.5.9以解决以下问题：

* (ZD #22351)VHL —— 分析：实时视频资产持续时间

通过将assetDuration API添加到PTVideoAnalyticsTrackingMetadata来更新实时／线性流的资产持续时间并提供检查实时流的逻辑，解决了此问题。

* (ZD# 22675)VHL —— 分析：更新实时视频资产持续时间

此问题与ZD #22351相同。

* (ZD #25908)VHL —— 分析：Adobe心跳事件崩溃

通过更新实施以使用最新版iOS版VHL 1.5.9来提高稳定性和性能，解决了此问题。

* (ZD #25956)VHL —— 分析：重复播放视频时崩溃

此问题与ZD #25908相同。

**版本1.4.29** (1.4.29.743)

* (ZD# 23901)第三方广告不播放

通过切换到CRS v3 URL结构以在重新打包的URL中包含区域ID，解决了此问题。

* (ZD #25183)在tvOS和iOS上播放DRM的问题

通过提供对多DRM支持所需的多个关键标签的支持，解决了此问题。

* (ZD# 25334)TVSDK无法播放cDVR共享内容

通过阻止TVSDK将空字符串转换为绝对URL，解决了此问题。

* (ZD# 25347)在AVURLAsset上设置自定义HTTP头

已添加通过PTNetworkConfiguration类在其段请求上对自定义标题的支持。

**版本1.4.28** (1.4.28.722)

* (ZD #24549)多广告跟踪调用

通过更新时间轴管理器以在创建多个播放器时侦听特定对象上的通知，解决了此问题。

* (ZD #24758)PTManifestLogger不支持iOS 8

通过将记录器实用程序库更新到版本7.0部署目标，解决了此问题。

* (ZD #24775)由于广告而延迟的流

通过正确计算活动播放列表上的持续时间漂移已解决此问题。

* (ZD #24799)某些剧集在iOS应用程序上不播放

当WebVTT文件受地理限制时，通过对字幕使用本地Web服务器解决了此问题。

**适用于iOS 6.0+的版本1.4.27** (1.4.27.711)

* (ZD #24089)-针对长DVR流的广告解析进行优化

通过添加多个优化来减少实时／线性流中处理DVR窗口所需的时间，解决了此问题。

* (ZD #21554)-未为application-type = video/mp4触发TVSDK错误信标

通过使播放器能够ping无效资产格式上的正确错误跟踪URL，解决了此问题。

* (ZD #24424)- EXC_BAD_ACCESS KERN_INVALID_ADDRESS类型的崩溃来自较新硬件设备上的iOS的PSDKLib内部。

已修复因取消分配的媒体播放器实例而发生的在不同流之间快速切换播放时的崩溃。

* (ZD #24575)- 32位设备上的TVSDK中，当enableDebugLog=true时崩溃

已修复在启用日志记录时导致32位设备崩溃的日志格式问题。

**适用于iOS 6.0+的版本1.4.26** (1.4.26.702)

* (ZD# 20213)-对于XCode7,TVSDK FW需要动态／模块化

通过更新具有模块支持的库来修复

**适用于iOS 6.0+的版本1.4.25** (1.4.25.684)

* (ZD #19629)-进入Airplay到ATV 4时的实时视频暂停

通过在删除旧项目后但在将新项目添加到AVQueuePlayer之前添加等待期，解决了此问题。 没有等待期，通知会发送到错误的项目。

* (ZD #19856)-默认情况下启用时不显示字幕

webvtt播放列表中导致字幕无法正确显示的问题已修复。

* (ZD #21590)-最新源构建中的视频性能和跟踪

VideoAnalytics中缺失视频长度的问题已修复。

* (ZD #20202)-设置自定义字幕样式会使iOS应用程序崩溃

通过在设置子标题样式时添加额外的空对象检查解决了此问题。

* (ZD #20709)-视频开始跟踪中报告为0的视频长度

此问题与(ZD #21590)相同。

* (ZD #22280)-分析视频长度设置为0

此问题与(ZD #21590)相同。

* (ZD #22592)- Primetime中Airplay的问题

此问题与(ZD #19629)相同。

* (ZD#22922)- iOS的手动比特率切换

通过提供指定最大比特率的选项解决了此问题。

* (ZD #23084)- Apple Compliance for IPv6-Only Networks

Apple不建议使用的符号已被删除。

**适用于iOS 6.0+的版本1.4.24** (1.4.24.661)

* ZD #2548)- Primetime对移动上交互式广告的支持- VPAID 2.0

如果VPAID广告无法播放，则通过更新逻辑以取消隐藏播放器视图来解决此问题。

* (ZD #20101)-广告播放期间自定义章节实施将触发章节开始事件

通过更新VideoAnalyticsTracker，在章节和非章节边界之间转换时可正确检测章节开始／完成，解决了此问题。

* (ZD #20784)-分析：实时视频过渡的触发内容已完成

通过添加逻辑来在视频跟踪会话期间手动触发内容完成，解决了此问题。

更新了以下库：

* 到4.10.0的AdobeMobile库
* VHL库到1.5.6
* VHL-Nielsen库到1.6.7
* (ZD #21855)-字幕在中间镜头后不播放

在此期间，重复的不连续性标签导致字幕在中间滚动之后不显示。 通过删除彼此相邻的不连续标签解决了此问题。

* (ZD #21994)- PTHLSUtils中的字符串越界

导致崩溃的最可能原因是EXT-X-KEY的URL周围有引号。

* ZD #22074)-在iOS上每分钟发生一次AUDVAST崩溃

在版本1.4.23中，修复了由VAST重定向URL中存在不安全字符导致的崩溃。 但是，TVSDK继续跳过这些广告。

通过处理不安全字符并允许播放广告，解决了此问题。

* (ZD #22694)- PTMediaPlayer。  视图由播放器隐藏

如果VPAID广告无法播放，则通过更新逻辑以取消隐藏播放器视图来解决此问题。

**适用于iOS 6.0+的版本1.4.23** (1.4.23.641)

* (ZD #18016)- Primetime SDK没有网络状况不佳的响应

通过改进在发生AVFoundation的致命错误时的错误通知，并允许应用程序在错误后处理重新启动，解决了此问题。

* (ZD #20580)- PTSplicerManager中的崩溃

通过提供额外的保护来避免导致崩溃的并发问题，解决了此问题。

* (ZD #21782)- iOS错误代码10100

TVSDK在Adobe Access DRM流上开始播放时返回101000错误的问题已修复。

* (ZD #21889)-在线广告和脱机内容回放失败

解决了AES加密脱机内容上的广告播放失败的问题。

* (ZD #22074)-在iOS上每分钟发生一次AUDVAST崩溃

通过改进对URL中包含无效字符的第三方VAST广告标记的处理，解决了此问题。

* (ZD #22257)- TVSDK无法播放DRM流

修复了在Adobe Access DRM流上开始播放时返回101000错误的TVSDK的问题。

**适用于iOS 6.0+的版本1.4.22** (1.4.22.627)

* (ZD #18709)-在iOS的TVSDK中崩溃

已修复某些Adobe Access DRM保护的流上发生崩溃的问题。

* (ZD #18850)-根据CRS规则更新创意选择逻辑

通过添加。json配置文件以指定创意选择优先级，解决了此问题。

* (ZD #19770)-受保护的AES视频源不再播放

已修复某些302重定向流无法播放的问题。

* (ZD #19629)-进入Airplay到ATV 4时的实时视频暂停

通过为Apple TV 4设备打开播放时为实时视频暂停添加补救方法，解决了此问题。 此问题似乎是AppleTV 4问题。

* (ZD #21119)- TVSDK在广告播放后停止

在使用广告插入时，增加了对序列IV的AES加密流的支持。

* (ZD #21125)-提前从实时／线性广告中返回

添加了支持，以便在广告分时段播放到完成之前从广告分时段返回。 通过自定义清单标签指示提前返回。

* (ZD #21224)-对Akamai标记流的播放支持

已将API添加到PTNetworkConfiguration类，以将cookie作为特定Akamai标记流的段的URL参数附加。

* (ZD #21287)-无关日志

修复了在xcode控制台中默认显示的某些日志语句的问题，即使在禁用记录时也是如此。

* (ZD #21446)- Ad Break事件有时不是由TVSDK触发

在事件流中，广告中断在以前的版本中无法正确触发。 此版本解决了此问题。

**适用于iOS 6.0+的版本1.4.21** (1.4.21.605)

* (ZD #20749)-回退会跳过非空VAST响应；额外广告跟踪URL触发

已解决回退广告上ping重复的问题。

**适用于iOS 6.0+的版本1.4.20** (1.4.20.590)

* (ZD #18639)- TVSDK在冗长的热录制资产上使用过多的CPU/资源

在两个级别中修复了过度的CPU/资源使用。 首先，让时间更新功能在全局队列而不是主线程上运行，并通过优化CPU使用以利用先前处理和缓存的m3u8来分析清单。

* (ZD #19349)-在限制网络连接时，将跳过预先滚动广告。

通过向应用程序和adMetadata提供超时事件(requestTimeout)解决了此问题。  adRequestTimeout API以覆盖默认的10秒超时。

* (ZD #19446)-实时流上缺少通知

通过允许应用程序订阅实时流上的EXT-X-PROGRAM-DATE-TIME，解决了此问题。

* (ZD #19459)-使用PTMediaPlayerItem prepareAudioOptionsWithAVMediaSelectionOptions准备备用音频时崩溃
* (ZD #19460)-崩溃- `[PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]`

此问题与Zendesk #19459相同。

* (ZD #19574)- TVSDK不返回DRM或非DRM内容的M3U8响应数据

在PTMediaPlayerItem.prepareToPlay中清单文件的初始加载中，如果清单加载失败，TVSDK不会向应用程序报告失败响应的正文。

通过允许TVSDK将失败响应作为错误报告给应用程序，解决了此问题。

* (ZD #19615)-回退逻辑无效

在当前实施中，回退广告被跳过且未重新打包，除非这些广告采用m3u8格式。 通过添加对重新打包回退广告的支持，解决了此问题。

* (ZD #19770)- TVSDK无法播放任何带302重定向的受保护AES内容

修复了重定向问题，因为重定向URL在可用于分析清单之前已被cleanConnectionData清除。

* (ZD #19856)-默认情况下启用时，某些位速率不显示字幕

通过处理iOS中不显示字幕的流段的错误，解决了此问题。

* (ZD #19868)-当无效创意被交换时，TVSDK崩溃

已修复TVSDK中错误地取消分配广义分析器实例的崩溃。

* (ZD #20180)- VPAID广告偶尔会被跳过

JavaScript mime类型并不始终包含在内，或被视为有效的mime类型。 通过将JavaScript作为有效的mime类型来解决此问题。

* (ZD #20749)-回退会跳过非空VAST响应；额外广告跟踪URL触发

某些创意未重新打包的问题已解决。

**适用于iOS 6.0+的版本1.4.19** (1.4.19.563)

* ZD #18639)- TVSDK对一个冗长的热录制资源使用过多的CPU/资源

通过优化DRM m3u8播放列表重写到先前已重写的播放列表的缓存位，解决了此问题。 当您回放m3u8实时流时，这一点最相关，m3u8在每段下载后都会下载。

* (ZD#18956)-在iOS Demo Player中设置断点时，player.drmManager为nil

通过更新PTMediaPlayer.drmManager API实现以从DRM框架中获取DRMManager，解决了此问题。

**适用于iOS 6.0+的版本1.4.18** (1.4.18.557)

* (ZD #18844)在iOS播放器中跟踪实时内容的播放头。

通过允许应用程序设置其自己的播放头值，解决了此问题。

* (Zendesk #18518)-如果未指定视频名称，则TVSDK的名称默认为*基于PSDK的播放器。*

通过删除播放器名称的默认值解决了此问题。

**适用于iOS 6.0+的版本1.4.17** (1.4.17.545)

* (Zendesk #2228)-增强TVSDK以返回清单获取的JSON响应

DRM Framework返回零DRMMetadata，而不是在内容不是M3U8时发送错误。 通过在M3U8_PARSER_ERROR通知发生时添加元数据来公开内容，解决了该问题。

* (Zendesk #2231)-获取MediaPlayerNotification中不可用的清单时返回错误

与Zendesk #2228分辨率相同

* (Zendesk #3304)-未填充VAST 3.0 `[ERRORCODE]` 宏

已解决跟踪URL开头有空格时，Auditude SDK无法发送ping的问题。

* (Zendesk #17294)-崩溃SecKeyRawSign

解决了客户代码使用密钥链时可能发生的崩溃问题。

* (Zendesk #18008)-支持iOS8+的Cookie，以支持标记流

Akamai标记流要求在区段请求时发送cookie，而iOS 7及更早版本上无法发送。 从iOS 8开始，Apple已添加一个API，它允许为段请求传递cookie。 TVSDK中现在提供此支持。 此外，还添加了发送用户代理的支持（如果可用）。

* (Zendesk #18166)- TVSDK 1.4.15在使用dSYM文件选项使用DWARF进行编译时会发出数百个警告

所有警告都已解决。

**注意**:为TVSDK添加了与tvOS兼容的库。

**版本1.4.16** (1.4.16.1454)

* Zendesk #3875 - Tab S在播放期间崩溃

还原OKHTTP对CRSauditude的依赖关系，因为TVSDK现在直接使用httpurlconnection而不是curl。 通过在进行另一个JNI调用之前清除例外，解决了该问题。

* (Zendesk #4487)-跟踪内容的线性渠道

通过在线性流播放会话期间重新初始化视频心率跟踪器，解决了该问题。

* (Zendesk #17919)- Android —— 内容搜索导致心跳错误

问题是当一章中有搜索时解决错误状态中的心跳

* (Zendesk #18053)-使用TVSDK的应用程序在Marshmallow上崩溃

当TVSDK库使用执行YUV `->` RGB颜色转换的霓虹代码时，TVSDK在Android M OS上崩溃。 通过使用非Neon版本的更新导致此问题的函数解决了此问题 `code`。

* (Zendesk #18072)- Android M —— 应用程序崩溃

检查配置文件和级别是否受支持时，调用MediaCodecList和MediaCodecInfo API时发生此崩溃。 Adobe正在寻求Google的支持以获得更多洞察。 通过提前加载所有编解码器信息来避免仅在需要编解码器信息时才调用这些API，解决了此问题。

* (Zendesk #18074)-阿拉伯字幕在Nexus和Android 6.0上不工作

通过提供对Android CTS字体映射的支持解决了此问题。

**适用于iOS 6.0+的版本1.4.15** (1.4.15.512)

**注意**:Nielsen模块已从TVSDK版本中删除，但TVSDK将在不久的将来用新的Nielsen集成模块进行更新。

* (ZD #2228)-从获取MediaPlayerNotification中不可用的清单返回错误

添加了元数据，以在发生通知M3U8_PARSER_ERROR时显示内容。

* (ZD #4437)- Adobe Primetime SDK内部崩溃

修复了在准备字幕／替代音频时报告的崩溃问题。

* (ZD #4487)-跟踪内容的线性通道

允许在线性流播放会话期间重新初始化视频心跳跟踪器。

**适用于iOS 6.0+的版本1.4.14** (1.4.14.498)

* (ZD #17260)- playlistManagerForURL崩溃

修复了并发问题导致的间歇性崩溃。

**版本1.4.13** (iOS 6.0+)

* (ZD #3304)-未填充VAST 3.0 `[ERRORCODE]` 宏

   * 如果内联广告有不良创意，则会显示错误代码400。
   * `[ERRORCODE]` 宏将进行URL编码。

* (ZD #3865)心跳与IMA广告集成

修复了视频长度报告错误的错误。

* 更新了支持iOS 9的TVSDK演示播放器

要正确支持iOS 9，您需要配置Application Transportation Security的例外。 为了演示，ATS完全禁用。

**适用于iOS 6.0+的版本1.4.12** (1.4.12.464)

* (ZD #4521)CRS测试客户端和SSAI

修复了3P URL中错误的反向MD5。

**适用于iOS 6.0+的版本1.4.12** (1.4.12.463)

* (ZD #2751)CSAI和CRS / Enhance:处理某些媒体文件URL中的动态元素。

更新了Creative Repackaging Service以正确处理带有动态创意URL的广告。

* (ZD #3654)1.3.4.166之后PSDK版本中的内存泄漏

修复了drmFramework中的内存泄漏，并在iOS 8.2设备上定期播放

* (ZD #3988)在首次播放后搜索回预卷时，将跳过预卷

修复了一个错误，以便可以正确禁用广告策略。

* (ZD #4017)请求iOS API强制广告在向后搜索时回放

解决了ZD #4279的修复

* (ZD #4279)iOS和桌面上的HLS TVSDK和插入-302重定向问题

修复了广告资产使用相对重定向URL时的错误

**适用于iOS 6.0+的版本1.4.9** (1.4.9.427)

* (ZD #3075)Internet可接通性问题- iOS

添加了检测播放何时停止的通知。

* (ZD #3193)在TVSDK中请求配置文件更改API

更新了PTPlaybackInformation以显示更新的ishedBitrate。 更新了BITRATE_CHANGE通知，使M3U8报告的比特率更加可靠和准确。

* (ZD #3324)Primetime广告在VMAP中没有广告媒体时报告问题

支持ping空广告中断跟踪URL,TVSDK现在将验证广告中断开始和完成对空广告中断的ping。

**版本1.4.8** (1.4.8.402)

* (ZD #3158)IOS 7在完整事件重播中崩溃

**版本1.4.7** (1.4.7.382)

* (ZD #2197)跟踪广告错误。 为资产添加的通知无法加载清单。
* (ZD #2894)播放器在播放期间发出4个顶级清单请求。
* (ZD #2992)Auditude报告奇怪的持续时间和标识符。

**版本1.4.6**(1.4.6.325)

* (ZD #2197)跟踪广告错误。 为资产添加的通知加载清单失败

**版本1.4.5** (1.4.5.283)

* (ZD #2141)TreeHouse应用程序的分析实施，添加了用于构 `AdobeAnalyticsPlugin.a` 建包的库。
* 视频心率库更新到1.4.1.2
* [PTPALY-4226] [与ZD #2423相关)执行DRM重置可能导致应用程序文档数据的删除。

**版本1.4.4** (1.4.4.242)

* 视频心率库(VHL)更新至1.4.1。

* (ZD #2435)有关分析需求更新的TV SDK文档

**版本1.4.2** (1.4.2.210:iOS 6.0+)

* (ZD #1129) `_player.currentItem.audioOptions` 返回空
* (ZD #2109)Primetime PSDK 1.4.1.125不适用于Xcode 5.1.1
* (ZD #2137)无法加载DRM元数据时iOS上的PSDK中发生崩溃

**版本1.4.1**(1.4.1.125)

* (ZD #1107)CocoaLumberjack重复符号
* (ZD #1644)修改iOS用户代理以进行定位和报告
* (ZD #1850)iOS SDK中包含的Cocoa Lumberjack文件
* (ZD#1908)如果存在超过1个自定义标记，则PSDK将忽略这些标记

**版本1.4.0** (1.4.0.32)

* Zendesk #1024 —— 通过清单从流中删除广告的功能

## 设备认证和支持 {#device-certification-and-support}

>[!NOTE]
TVSDK中不 **支持** 以下功能：
* 在任何平台或版本上慢动作。
* 实时戏法播放。


**版本1.4.43**

* TVSDK 1.4.43已针对iOS 11进行认证。

**版本1.4.29**

* TVSDK 1.4.29已针对iOS 10进行认证。

**版本1.4.28**

* TVSDK 1.4.28已通过iOS 10 Beta 7的认证。
* 通过添加和API强制使用HTTPS的 `forceHTTPS` DRM `isForcingHTTPS` 支持。
* 将VHL库更新为1.5.8，将Adobe Mobile库更新为4.8.4，将记录器实用程序库更新为7.0版部署目标。

**版本1.4.19**

此版本的TVSDK已通过iOS和tvOS的FairPlay支持认证。

**版本1.4.17**

* tvOS

   此版本的TVSDK包含对tvOS的支持，并且已针对未加密的HLS流进行认证。

   **注意**:请记住以下编译准则：

   * TVSDK tvOs支持仅限于非Adobe DRM加密流。 必须在tvOS构建设置中删除对drmNativeInterface.framework的引用。 仍支持AES加密流。
   * Apple要求启用所有Apple TV应用程序的位代码，因此，必须在项目设置中打开此标志。

## 已知问题和限制 {#known-issues-and-limitations}

* 由于iOS UIWebView类被弃用，从iOS TVSDK 3.6开始：
   * VPAID广告在iPad 13中不会按预期播放。
   * 配套广告不会按预期播放。

* 在iOS TVSDK中，所有广告均被拼接到内容清单中。 广告行为是根据内容和广告细分的持续时间进行搜索实现的。 因此，如果区段持续时间不准确，搜索可能并不总是在广告中断开始或结束的确切帧结束。 即使持续时间在帧上，平台本身也具有对搜索的容差，并且可能显示一些帧或广告或内容。 这是平台的限制以及广告插入在iOS上与TVSDK一起工作的方式。
* 在这种情况下，在搜索事件上会发生跳过的决定。 但是，由于清单中的广告段持续时间不能准确地表示广告的实际持续时间，因此搜索不准确帧。 因此，在应用广告策略时，您会看到几个广告帧。
* 它可能会体验到，iOS 11上不播放许可证旋转视频，并且iOS 9.x和iOS 10.x上播放正常。
* 在VPAID 2.0支持中，如果在AirPlay上播放活动，则跳过VPAID广告。
* 当最小目标设置为iOS7（或更高版本）时，drmNativeInterface.framework无法正确链接。
解决方法：显式指定libstdc++.6.dylib库，如下所示：转到“目标”->“构建阶段”->“将二进制文件与库链接”，并添加libstdc++.6.dylib。
* 插入Post-Roll Ad不用于替换API。
* 在广告分时段中搜索（不退出）会发出重复的广告开始和广告分时段通知
* 设置currentTimeUpdateInterval没有任何效果。
注意：在某些iOS版本中，操作系统不会自动加载PSDKLibrary.framework内的资源。 手动将PSDKResources.bundle复制到应用程序的包资源很重要：转到“构建阶段”并复制捆绑包资源。
* 无法使用Xcode 8或更低版本构建参考应用程序。 从iOS TVSDK版本1.4.41开始，使用Xcode 9进行编译。
* VPAID广告不遵守delayAdLoadingTolerance值。
* 24077-对于具有字幕的某些HLS内容，播放器在“停止”或“重置”方法时崩溃。
* 在启用“及时广告”解决时，“详细错误通知”不可用。
* 错误通知按广告解决时间记录，而非按广告序列记录。
* HEVC支持在此版本中有以下限制
   * 不支持DRM
   * CC(CEA 608/708)支持不可用，因为CMAF不支持它。
   * 4K支持尚未提供。
   * ID3标记不支持，因为CMAF不支持它。
   * 未验证未混合的实时HEVC流。
   * HEVC广告支持未经验证。
* 启用JIT并将容差设置为10秒后，在出现VMAP->VAST重定向广告时，第一次midroll广告中断时不会看到VAST调用。
* 为了使广告分辨时间正常工作，每次在实时流播放期间更新播放列表时，播放器都希望在20秒内获得一个拼接的播放列表。 如果在所述间隔内它没有接收到拼接的播放列表，则引发内部错误并且播放器停止。

## 实用资源 {#helpful-resources}

* [TVSDK 3.4 for iOS程序员指南](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-for-ios/introduction/ios-3x-overview.html)
* [TVSDK iOS 3.4 API参考](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v34/index.html)
* 请参阅 [Adobe Primetime学习和支持页面上的完整帮助文档](https://helpx.adobe.com/support/primetime.html) 。

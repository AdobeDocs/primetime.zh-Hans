---
title: 适用于iOS的TVSDK 3.12发行说明
description: TVSDK 3.12 for iOS发行说明描述了TVSDK iOS 3.12中的新增或更改功能、已解决和已知问题以及设备问题。
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '7665'
ht-degree: 0%

---


# 适用于iOS的TVSDK 3.12发行说明 {#tvsdk-for-ios-release-notes}

TVSDK 3.12 for iOS发行说明描述了TVSDK iOS 3.12中的新增或更改功能、已解决和已知问题以及设备问题。

## 系统和软件要求 {#system-software-requirements}

在下载iOS 3.12之前，请确保硬件、操作系统和应用程序版本满足以下要求：

操作系统：iOS 8.0或更高版本。

## iOS TVSDK 3.12

修复了实时流在播放15分钟后失败的问题。

有关当前版本中的修复，请参 [阅已修复的客户问题](#resolved-issues) ，有关限制，请 [参阅已知问题和限制部分](#known-issues-and-limitations) 。

### 先前发行版中的新增功能和修复 {#whats-new-previous}

**iOS TVSDK 3.11**

为导致应用程序崩溃的客 `isFallbackOnInvalidCreativeEnabled` 户问题 `customParams` 提供了修复。

**iOS TVSDK 3.10**

* 修复了当网络不可用时TVSDK播放 `PTMediaPlayerStatusError` 器不触发通知的问题。

**iOS TVSDK 3.9**

* 修复了VTT字幕无法播放导致应用程序冻结的问题。

* iOS TVSDK 3.9包含更新的个性化传输证书。

**iOS TVSDK 3.8.0.83修补程序**

修补程序具有更新的个性化传输证书。

**iOS TVSDK 3.8**

iOS 13合规性和已处理iOS 13 UIWebView API的停用。

**iOS TVSDK 3.7**

同时发出大量广告分辨率请求时停止播放的场景的修补程序。

**iOS TVSDK 3.6**

**类的vastXML属性中的修复`PTNetworkAdInfo`**

vastXML属性设置不正确，返回零值。

**iOS TVSDK 3.5**

**启用背景音频**

*将应用程序配置为在音频进入后台时继续播放。*

要启用此功能，我们需要设置在PTMediaPlayer `audioPlaybackInBackground` 类中添加的新API。 启用此API后，您的应用程序就可以播放背景音频。

**iOS TVSDK 3.4.0.19（修补程序）**

此版本修复了广告故障转移场景中发生的应用程序崩溃问题。

**iOS TVSDK 3.4**

**广告分辨率超时**

* 使用TVSDK 3.4，用户现在可以为整体广告分辨率和清单下载设置超时值。 如果在给定的超时时间内某些广告无法解析，则TVSDK将播放剩余的广告。

* PTAd元数据：adRequestTimeout API已弃用，将被删除。 默认值已设置为35秒。

* PTAdMetadataClass中引入了两个新的备用API:adResolutionTimeout —— 针对广告分辨率调用的超时adManifestTimeout —— 广告清单下载的超时。

**收入优化**

使TVSDK能够识别与广告插入工作流相关的问题区域，以便向分析最终选择点报告。

**版本3.3**

TVSDK 3.3现在符合iOS 11 SDK的要求。 所有已弃用的API都已替换为合适的替代方式。

**版本3.2**

**其他日志记录支持（阶段2）**

添加了对错误通知的支持，在以下情况下：

* HLS版本的广告使用的级别高于内容。

* 排除纯音频变体。

* VAST/VMAP请求失败。

**版本3.1**

* **附加日志记录**&#x200B;支持在广告播放失败时增加对描述性通知的支持。

* **增加了Fairplay加密CMAF流支持** Fairplay加密CMAF流，现在支持AVC编解码器回放。

**版本3.0.1**

此版本中没有新增功能或增强功能。

**3.0版**

* TVSDK 3.0支持HEVC流。

* 及时——解析更接近广告标志符的广告。

在应 `enableDelayAdLoading` 用程序级界面上添加了布尔类型属性，以启用JIT。 如 `enableDelayAdLoading` 果为NO，则 `setadMetadata.delayAdLoading`为True（PTAdMetadata接口的属性）。

启用此属性后，TVSDK会根据定义的容差值，在其位置之前解析每个广告中断。 默认情 `delayAdTolerance` 况下，设置为5秒。

**版本1.4.45**

为了符合Xcode10,TVSDK已从“`libstdc++`”转`libc++`换为“”，因此支持的最低版本为iOS 7。 早些时候是iOS 6。

**版本1.4.44**

此版本中没有新增功能或增强功能。

**版本1.4.43**

* 一种类似电视的体验，能够加入广告中间而不触发部分广告跟踪。\
   示例：用户在包含3个30秒广告的90秒广告时段中间（40秒）加入。 这是休息时第二个广告的10秒。

   * 第二个广告在剩余持续时间（20秒）内播放，然后是第三个广告。
   * 不会触发已播放的部分广告（第二个广告）的广告跟踪器。 只触发第三个广告的跟踪器。

* 在PTAdMetadata接口中添加了布尔类型的enableVodPreroll属性。 该属性可用于在VoD流上启用预滚动。 如果enableVodPreroll为NO，则PSDK不播放预置。 然而，这并不影响微软。 enableVodPreroll的默认值为YES。
* 从iOS v1.4.43开始，PTMediaPlayer接口的closedCaptionDisplayEnabled API被标记为已弃用。 要确定给定PTMediaPlayerItem是否提供隐藏式字幕，请检查PTMediaPlayerMediaItem的subtitlesOptions属性。

**版本1.4.42**

此版本中未添加任何新功能。 有关已修复的一列表问题，请参 [阅已解决问题](#resolved-issues)。

**版本1.4.41**

API更改：

* **isSecure**:引入了新的API isSecure以保护播放器不录制和引发错误。 默认值为true。

* **allowExternalRecording**:引入了新的API以允许对安全内容进行播放镜像。 Airplay镜像视为录制，因 `allowExternalRecording` 此必须将值设 `True`置为，以允许airplay镜像，或设置为 `False` 停止airplay镜像以保护内容。 默认情 `value` 况为true。

**版本1.4.40**

无新增功能。

**版本1.4.39**

* iOS TVSDK通过VHL 2.0.1和VHL 2.0.1认证，Nielsen通过认证。

* 更新iOS TVSDK以从新的Akamai主机发出CRS请求 `primetime-a.akamaihd.net`。

* 新的主机名配置通过HTTP和HTTPS(SSL)提供更大规模的CRS资产投放。

**版本1.4.36**

在iOS TVSDK中集成和验证VHL 2.0:通过降低API的 `VideoHeartbeatsLibrary` 复杂性，减少实施中的障碍。

**版本1.4.34**

**网络广告信息**

TVSDK API现在提供有关第三方VAST响应的其他信息。 广告ID、广告系统和VAST广告扩展在可通过广告资 `PTNetworkAdInfo` 产的属性访 `networkAdInfo` 问的类中提供。 此信息可用于与Moat Analytics等其他广告分析平台 **集成**。

**版本1.4.31**

* **计费指标** 为了迎合那些希望只支付其使用费用而不是固定费用的客户，Adobe会收集使用情况指标并使用这些指标来确定向客户收取的费用。

   每次TVSDK生成流开始事件时，播放器开始会定期向Adobe的计费系统发送HTTP消息。 对于标准VOD、专业VOD（启用中间广告）和实时内容，期间（称为付费持续时间）可以不同。 每种内容类型的默认持续时间为30分钟，但您与Adobe的合同将决定实际值。

* **针对CRS Ads的多CDN支持** TVSDK现在支持针对CRS广告的多CDN。 通过为CRS广告提供FTP详细信息，您可以指定CDN位置，而不是默认的Adobe拥有的CDN（如Akamai）。

**版本1.4.29**

在类 `PTSDKConfig` 中，已添加forceHTTPS API。

该 `PTSDKConfig` 类提供对向Adobe Primetime广告决策、DRM和视频分析服务器发出的请求实施SSL的方法。 有关详细信息，请参 `forceHTTPS` 阅此 `isForcingHTTPS` 类的和方法。 如果清单是通过HTTPS加载的，TVSDK将保留HTTPS的内容使用，并在从该清单加载任何相对URL时遵守此用法。

>[!NOTE]
>
>对第三方域（如广告跟踪像素、内容和广告URL）的请求以及类似请求不会进行修改，内容提供商和广告服务器有责任提供通过HTTPS支持的URL。

**版本1.4.18**

Primetime iOS TVSDK现在支持VPAID 2.0 Javascript创意，以实现丰富的交互式流内广告体验。 有关VPAID 2.0的更多信息，请参阅VPAID广告支持。

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

   * Digital Rights Management(DRM)
   * 广告横幅
   * 电视标记语言(TVML)

**版本1.4.13**

>[!NOTE]
>
>Nielsen模块已从TVSDK版本中删除，TVSDK将在不久的将来用新的Nielsen集成模块进行更新。

**广告回退，广告选择逻辑中的菊花链(Zendesk #3103)**

对于启用回退规则的VAST广告（创意人员）,TVSDK将MIME类型无效的广告视为空广告并尝试在其位置使用回退广告。 您可以配置回退行为的某些方面。 有关详细信息，请参阅VAST和VMAP广告的广告回退。

**版本1.4.9**

**具有替代内容替换的封锁信号**

作为1.4 TVSDK更新的一部分，我们现在还支持针对线性内容进行区域封锁后进入和返回。 TVSDK现在可以并行处理两个清单文件，主文件和备用文件，以监视封锁信号，即使替代原始编程显示替代了替代编程。

**版本1.4.8**

**已更新至版本1.5的视频心跳库(VHL)**

* 能够将带有视频开始和／或视频／广告／章节开始的元数据作为上下文数据发送。

* 网络流量更少——心跳平均更少，且更小。

**版本1.4.7**

* **预置个性化支持**

支持Adobe个性化服务器的本地安装，以自定义客户端的个性化请求以转到其他端点。

* **基于分辨率的输出保护**

DRM策略现在可指定允许的最高分辨率，具体取决于设备的“输出保护”功能。 例如，“如果HDCP可用，则允许播放分辨率高达1080p的内容，如果HDCP不可用，则允许播放分辨率高达480p的内容”。

**版本1.4.4**

* **视频心率库(VHL)更新至版本1.4.1.1**

   * 添加了将来自其他SDK或播放器的不同分析用例与Adobe Analytics视频基础捆绑的功能。
   * 广告跟踪已通过删除和方法 `trackAdBreakStart` 进行 `trackAdBreakComplete` 优化。 广告中断从和方法调 `trackAdStart` 用 `trackAdComplete` 中推断出。
   * 跟踪 `playhead` 广告时不再需要该属性。
   * 增加了对Marketing Cloud访客ID的支持。

* **Nielsen SDK集成**

TVSDK现在支持将mTVR和MDPR ID3信标发送到Nielsen SDK，而无需任何自定义集成。 要开始，请下载3.1.2.19 Nielsen iOS App SDK，然后按照此处的“iOS Programmers Guide”中的说明操作。

**版本1.4.0**

* **具有替代内容替换的封锁信号**

作为1.4 TVSDK更新的一部分，TVSDK现在还支持针对线性内容的区域封锁进入和返回。 TVSDK现在可以并行处理两个清单文件，主文件和备用文件，以监视封锁信号，即使替代原始编程显示替代了替代编程。

* **删除／替换C3广告**

现在，无需进行额外的准备工作即可将新广告动态插入从C3窗口推出的视频点播(VOD)资产中。 TVSDK现在提供一个API，用于删除自定义内容范围和动态插入新广告。 当直播／线性内容在播出期间播放时，此强大的新功能也很有用，并且会立即作为点播内容下载，而无需适当时间“清理”资产。

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
**iOS TVSDK 3.12**

* 在使用TVSDK for iOS 3.10时，实时流在播放15分钟后失败。

### 已解决先前版本中的问题 {#resolved-issues-previous}

**iOS TVSDK 3.11**

* (ZD#40998)- `isFallbackOnInvalidCreativeEnabled` 导致应用程序崩溃。

* (ZD#41289)-使 `NSInvalidArgumentException` 用导致应用程序 `customParams` 崩溃的方法进行观察。

**iOS TVSDK 3.10**

(ZD#40943)-当网络不可用时，TVSDK播放器不会触发PTMediaPlayerStatusError通知。

**iOS TVSDK 3.9**

(ZD#40272)- iOS TVSDK无法播放VTT字幕，出现101001错误并导致应用程序冻结。

**iOS TVSDK 3.8**

* (ZD#40087)-对于过期的VOD内容，iOS崩溃，并出现播放器错误。

* (ZD#40083)- Pre-Roll广告不播放实时流，播放 `OpportunityGenerator` 器给出错误。

* (ZD#39828)-属 `CurrentItem` 性缺少可空注释，当通知中包含的播放器状态为时，会导致播放器崩溃 `PTMediaPlayerStatusStopped`。

**iOS TVSDK 3.7**

(ZD#38961)-当在PiP中播放多个内容时，当一个内容完成播放后，内容无法在画中画(PiP)窗口中播放。

**iOS TVSDK 3.6**

此版本中没有新问题。

**iOS TVSDK 3.5**

此版本中没有新问题。

**版本3.3**

(ZD#37820)-为自定义头HS-Id、HS-SSAI-TAG添加了允许列表。

**版本3.2**

* **Ticket#36588** —— 调用MediaPlayer STOP方法时，会观察到播放器崩溃。

修复了为带字幕的少数流调用STOP方法时观察到的间歇性崩溃。

* **Ticket#37080** —— 已看到清单呼叫的重复请求。
修复了在播放期间对清单URL发出的重复请求。 现在，TVSDK对每个清单发出一个呼叫。

* **Ticket#37** - CRS标准化规则失败（eq匹配类型）修复了玩家在遇到具有“eq”匹配类型的主机名的上次标准化规则集时用于崩溃的情况。

**版本3.1**

**票证#36313** —— 线性广告中断期间的间歇性不可预知结果在实时流中线性广告中断期间固定的间歇性播放。

**版本3.0.1**

**Ticket36948** - CRS —— 资产选择顺序在iOS 12上不一致为CRS选择的资产并不总是在VAST或VMAP响应中返回的最高质量变体。

**3.0版**

* **Ticket35311** —— 在电话呼叫中断期间，播放器状态未变为“暂停”添加的中断处理程序可阻止播放器中断。 中断时，播放器状态变为“暂停”，然后单击播放按钮后继续播放。

* **Ticket36685** - Live assets - Time mismatch with player time progress and SCTE marker time为处于实时点之前的SCTE标记计算正确的时间。

* **Ticket36492** - `currentTime` 在暂停 `localTime` 状态期间搜索到新位置时未更新在播放器处于暂停状态时，播放器的当前时间现在可设置为零；较早时，仅在播放状态中将当前时间设置为零。

**版本1.4.45**

* **Ticket36294** - iOS TVSDK在Xcode 10上无法工作修复了XCode 10上TVSDK的编译问题。 由于XCode 10要求，从iOS 1.4.45开始，在TVSDK上构建的应用程序需要最低部署目标（如iOS 7.0）

* **Ticket36321** —— 在“播放”状态中 `PTMediaPlayer` 与实 `AVPlayer` 例之间可搜索范围中观察到的差异。

* **Ticket36493** - `libstdc++` iOS 12支持修复了iOS 12上TVSDK的编译问题。 从iOS 1.4.45版到TVSDK上构建的应用程序需要最低部署目标（如iOS 7.0）

**版本1.4.44**

* **Ticket34683** —— 广告播放进度时间呈负数

当广告服务器报告的持续时间与实际广告内容不匹配时，将增加额外的检查以处理这种情况。

* **Ticket34801** - currentTime和localTime在暂停状态期间搜索到新位置时未更新。如果播放器处于暂停状态，播放器的当前时间现在可以设置为零；较早时，仅在播放状态中将当前时间设置为零。

* **Ticket35037** —— 从基于信号的广告插入返回时，播放停顿，URL不正确。
改进了针对1.4.42版本中已解决问题#34385的修复。 添加了isCancelled检查和异常处理代码，使操作队列更加健壮。

**版本1.4.43**

* (ZD#32990)- iOS:内容播放而非某些提示点上的广告。 `selectedMediaOptionInMediaSelectionGroup` 作为AVPlayerItem接口一部分的API现在已移到iOS 11中的AVMediaSelection下。 使用此新API解决了此问题。

* (ZD#33683)TVSDK已删除==从元数据字符串中添加后缀。 解析逻辑中修复了该问题。

* (ZD#33905)- iOS TVSDK使用两个用户代理调用清单文件。 用户代理问题已在第一个m3u8呼叫（新安装案例）中得到修复。 M3u8现在为所有呼叫提供相同的用户代理。

* (ZD#34293)-在iOS11上无法正确播放在线性流上插入的预滚动。 已修复前置广告的问题。

* (ZD#34684)-应用广告跳过策略时，将显示前滚广告帧数几秒钟。 新的API enableVodPreroll已引入，可在vod播放中禁用预卷播放。 此API的默认值为“是”。 API确保跳过主内容中的广告内容拼接。

* (ZD#34765)-调用stop()后，仍可下载的传输流区段很少。 增强了Stop()API以避免下载额外的区段。

* (ZD#34865)-在iOS上，实时流的前置广告被截断。 与iOS11相关，并添加一个额外的检查来确认流是前置还是主内容，从而解决了此问题。

* (ZD#35093)-修复了在启动时，如果流的主要变体失败（返回404），播放不切换到备份流的故障转移方案。

**1.4.42 (1.4.42.118)**

* (ZD#34385)-从基于信号的广告插入返回时，播放停顿时，URL不正确。

   增加清单读取的最 `CustomAVAssetLoaderOperations`大并发计数，以便继续执行清单读取。

* (ZD#34373)-当不允许流录制时，最终用户无法流化到连接HDMI的设备。

* (ZD#32678)- TVSDK在iOS上不收集正确的广告ID。

   在VHL ping中，如果出现VAST/VMAP重定向，则最终广告创意的广告ID现在会被拾取。

* (ZD#33904)- TVSDK未注册AVFoundation通知 `AVAudioSessionMediaServicesWereLostNotification` 和 `AVAudioSessionMediaServicesWereResetNotification`。

   `PTMediaServicesWereLostNotification` 现在 `PTMediaServicesWereResetNotification` 可在播放器应用程序上注册，以在媒体服务重置或丢失时获取通知。

* (ZD#33815)-客户无需更新应用程序，就无法更新其优先级和标准化CRS规则。

   已将 `getCRSRulesJsonURL` 和 `setCRSRulesJsonURL` API添加到iOS TVSDK。

**版本1.4.41(1.4.41.76)**

* (ZD #34464)-在TVSDK版本1.4.41中构建参考应用程序时出现问题

   从此版本开始，编译适用于iOS的TVSDK需要Xcode 9。
* (ZD #29456)-处于暂停状态的播放开始

   修复了进入播放时视频暂停时的暂停问题。
* (ZD #30371)-当我们在线性流中插入2个以上广告时，AdBreak开始时间会发生变化

   修复了尝试在Apple TV上播放内容时出错的问题，该错误会完全阻止播放
* (ZD #32146)-阻止iOS `PTMediaPlayerStatusError` 11开发测试版上的HLS Live内容未收到

   在使 `PTMediaPlayerStatusError` 用Charles（丢弃连接和403）进行阻止时，未收到HLS Live和VOD内容。

* (ZD #29242)-启用广告时播放视频播放失败。

   启用广告并启用AirPlay开始播放视频时，视频播放从不开始，不会显示错误。

* (ZD#33341)-触发 `DRMInterface.h` 器在Xcode 9中生成警告。

   修复了两个块原 `DRMInterface.h` 型，它们的参数列表中缺少“void”一词。

* (ZD#31979)-对于iPhone 7/iPhone7+，如果iOS 10或更高版本，则不编译／运行。

   不再支持为早于iOS 7编译IB文档。

* (ZD#32920)-广告中断内的空白屏幕，无广告中断完成。

   当广告中断显示广告实例时，在广告实例完成后，将显示空白屏幕。

* (ZD#32509)-禁用iOS 11屏幕录制在iOS 11上禁用屏幕录制。

* (ZD#33179)- iOS11上的间歇性事件故障。

   修复了iOS 11上的事件故障。

**版本1.4.40** (1.4.40.72)

* (ZD #32465)-播放器无法处理合并的播放列表。

   呼 `finishLoadingWithError`叫(使用：AV基础尝试替代流／触发故障转移时出错)。

* (ZD #31951)-许可证轮替期间TVSDK错误。

   修复了许可证轮替问题。
* (ZD #31951)-广告中断内的空白屏幕，无广告中断完成。

   处理了Facebook VPAID广告通常在单个VAST节点中返回多个CDATA块 `<AdParameters>` 的问题。
* (ZD #33336)- iOS TVSDK —— 广告窗格未填充，尽管Freewheel返回的广告足够多。

   根据父序列和索引创建了序列广告和回退广告以及排序之间的父子关系。

**版本1.4.39** (1.4.39.43)

* (ZD #32178)- iOS TVSDK版本不正确。

   日志文件中的TVSDK版本输出为1.0.211。修复了该错误以输出正确的版本。

* (ZD #32199)-延迟广告加载——不显示内容的视频。

   以前未初始化的本地Adbreak时间线现在在使用前刷新。

* (ZD #27528)-如果在iOS 1.2上将辅助音频设置为非默认值，则在资产开始播放后1-45秒内，视频、音频或两者都将冻结。

   准备音轨并将其通知为“就绪”状态。

* (ZD #30411)-如果您选择辅助Sap语言，您可能会收到意外结果，如没有音频或音频不正确。

   准备音轨并将其通知为“就绪”状态。

* (ZD #32199)-延迟广告加载——不显示内容的视频。

   以前未初始化的本地Adbreak时间线现在在使用前刷新。

* (ZD #27528)-如果在iOS 1.2上将辅助音频设置为非默认值，则在资产开始播放后1-45秒内，视频、音频或两者都将冻结。

   准备音轨并将其通知为“就绪”状态。

* (ZD #30411)-如果您选择辅助Sap语言，您可能会收到意外结果，如没有音频或音频不正确。

   准备音轨并将其通知为“就绪”状态。

**版本1.4.38** (1.4.38.860)

* (ZD #29281)- iOS:向CRS请求添加AdSystem和Creative Id

基于CRS规范规则的CRS请求中创意ID和AdSystem的使用

* (ZD #29176)- Crash on `PTAdPolicyDeligate` `satAdBreakAsWatched:position`

现在已处理空AdBreak导致的崩溃。

* (ZD #30125)-程序化广告在iOS平台中无效

在iOS中增加了程序化广告支持。

* (ZD #30782)- #EXT-X-项目-DATE-TIME通知

对于具有LIVE DRM流的# EXT-X-事件-DATE-TIME标签，未触发定时元数据项目。

**版本1.4.37(1.4.37.842)**

* (ZD #28950)- VOD播放问题

流中的# EXT-X-PLAYLIST-TYPE标签设置为事件而不是VOD时的播放问题

* (ZD #29281)- iOS:向CRS请求添加AdSystem和Creative Id

在基于CRS标准化规则的CRS请求中使用创意ID和AdSystem。

* [ZD #29462)- A&amp;E VOD中导致iOS应用程序崩溃的ThuocyHub广告

**版本1.4.36(1.4.36.835)**

* (ZD #29418)-持续时间为0的提示(#EXT-X-CUE-OUT:0.000)导致iOS TVSDK停止或崩溃播放。

问题已修复，且播放开始正确。

* (ZD #29462)-在iOS TVSDK上导致崩溃的VOD中的广告。

问题已修复。 iOS TVSDK正在提 `exception(AUDNetworkAdInfo::initWithAdId)` 出，但没有处理。 异常由于广告ID为空。

* (ZD #29281)-向CRS请求添加AdSystem和Creative ID。

在1401和1403请求中将AdSystem和CreativeId作为新参数包含在内（所有其他参数保持不变）。

**版本1.4.35** (1.4.35.830)

* (ZD #27830)-需要以编程方式确定iOS中隐藏字幕和子标题之间的差异。

TVSDK现在显示两种类型，它们可用于过滤掉所需的字幕类型。

* (ZD #29160)- EXT-X-CUE-OUT广告提示在TVSDK iOS上未正确插入。

EXT-X-CUE-OUT Midroll广告正在播放。

* (ZD #29100)-当用户浏览到电影末尾时，应用程序崩溃。

修复了与同步相关的多个崩溃。

* (ZD #28785)、(ZD #27712)和(ZD #25076)- iOS应用程序在大型实时事件期间崩溃。

修复了与同步相关的多个崩溃。

**版本1.4.34** （适用于iOS 6.0+的1.4.34.815）

* (ZD #28481)-由于在这些FER流的广告中断结束时附加了不正确的密钥，导致FER中断

对于FER流，广告中断前的键在广告中断结束后插入。 此问题通过在广告中断 *结束时附加* “上次看到的键”来解决。

**版本1.4.33** （适用于iOS 6.0+的1.4.33.803）

* (ZD# 21701)为子帐户启用CRS

根据CRS后端的要求，发送1401 CRS请求的原始创意URL而不是标准化URL，即可实现。

* (ZD# 26218)- PSDKResources.bundle加载问题

通过更新资源加载以从所有可用的包中查看，解决了此问题。

* (ZD# 27460)Midroll首次广告电话-POST将 `cdn.auditude.com` 返回403。

新的CDN帐户无法处理POSTCDN请求。 通过更新代码将广告请求变为 `cdn.auditude.com` GET而不是POST，解决了此问题。

**版本1.4.32** （适用于iOS 6.0+的1.4.32.792）

* (ZD# 27132)支持VMAP广告分段的小数值。

当内容未按定义的广告分段时，整数会导致意外的广告放置。 通过不将小数值转换为整数，解决了该问题。

* (ZD# 27189)带有EXT-X-DINESCUTION-SEQUENCE标签的AES内容播放不正确。

通过将标记放置在播放列表的开头，解决了该问题。

**版本1.4.31** （适用于iOS 6.0+的1.4.31.785）

* (ZD# 24528)实施TVSDK计费使用量度

有关详细信息，请参 [阅计费指标]。

* (ZD# 24642)对TVSDK的画中画支持

“画中画”功能在某些情况下无法正常工作，现已修复。

* (ZD# 25246)错误的广告中断信号

通过在变型清单之间对齐不连续标记，解决了此问题。

* (ZD# 26218)当尝试将PSDKLibrary.framework包含在客户端的应用程序框架中时，应用程序构建过程变得复杂

已按照请求打包PSDKLibrary.framework来解决此问题。

* (ZD# 26364)对CRS广告的多CDN支持

有关详细信息，请参阅CRS广告投放的多个CDN支持。

* (ZD# 27028)在iOS 10中播放某些流时的延迟。

通过为没有M3U8扩展的流提供补救方法，解决了此问题。

**版本1.4.30** （适用于iOS 6.0+的1.4.30.754）

此版本中的TVSDK解决了以下问题：

* (ZD# 24180)向允许列表添加自定义头。

新的自定义头已添加到TVSDK允许列表。

* (ZD# 25016)当设置ABR控制参数时，会随机选择故障转移流

解决了此问题的方法是，在ABR设置在包含故障转移URL的流上提供初始比特率设置时，按顺序维护ABR流。 这将避免播放故障转移流而不是主流。

* (ZD# 25076)PTAuditudeAdResolver loadComplete上的崩溃

已修复在快速开始/停止包含广告的多个PTMediaPlayer实例期间发生崩溃的问题。

* (ZD# 25960)没有其他订阅标签用于触发元数据更改通知广播

在清单中第一个段之前出现订阅标记时不通知该标记的问题。

* (ZD# 26084)PSDK抛出106000.101000。-11833解码器在从上一个广告中断转换回娱乐内容时找不到错误

当来自VMAP的最后一个广告中断开始时间在总持续时间完成之前，在某些情况下，直到最后一个广告中断结束后，密钥才会插入。 此问题已修复。

* 视频心跳库(VHL)已更新至版本1.5.9以解决以下问题：

* (ZD #22351)VHL —— 分析：实时视频资产持续时间

通过向PTVideoAnalyticsTrackingMetadata添加assetDuration API来更新实时／线性流的资产持续时间并提供检查实时流的逻辑，解决了此问题。

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

通过提供对多DRM支持所需的多个关键标记的支持，解决了此问题。

* (ZD# 25334)TVSDK无法播放cDVR共享内容

通过阻止TVSDK将空字符串转换为绝对URL，解决了此问题。

* (ZD# 25347)在AVURLAsset上设置自定义HTTP头

已添加通过PTNetworkConfiguration类在其段请求上对自定义标头的支持。

**版本1.4.28** (1.4.28.722)

* (ZD #24549)多广告跟踪调用

通过更新时间轴管理器以在创建多个播放器时监听特定对象的通知，解决了此问题。

* (ZD #24758)PTManifestLogger不支持iOS 8

通过将记录器实用程序库更新到版本7.0部署目标解决了此问题。

* (ZD #24775)由于广告而延迟的流

通过正确计算事件播放列表上的持续时间漂移，解决了此问题。

* (ZD #24799)某些剧集在iOS应用程序上不播放

当WebVTT文件受地理限制时，通过为字幕使用本地Web服务器来解决此问题。

**适用于iOS** 6.0+的1.4.27(1.4.27.711)版

* (ZD #24089)-针对长DVR流的广告解析优化

通过添加多个优化来减少实时／线性流中处理DVR窗口所需的时间，解决了此问题。

* (ZD #21554)-未为application-type = video/mp4触发TVSDK错误信标

通过使播放器能够ping无效资产格式上的正确错误跟踪URL，解决了此问题。

* (ZD #24424)- EXC_BAD_ACCESS KERN_INVALID_ADDRESS类型的崩溃来自较新硬件设备上iOS的PSDKLib内部。

已修复因取消分配的媒体播放器实例而发生的在不同流之间快速切换播放时的崩溃。

* (ZD #24575)-在32位设备上的TVSDK中，当enableDebugLog=true时崩溃

已修复在启用日志记录时导致32位设备崩溃的日志格式问题。

**适用于iOS** 6.0+的1.4.26(1.4.26.702)版

* (ZD# 20213)-对于XCode7,TVSDK FW需要动态／模块化

通过更新具有模块支持的库来修复

**适用于iOS** 6.0+的1.4.25(1.4.25.684)版

* (ZD #19629)-进入ATV 4的播放时暂停实时视频

通过在删除旧项目后但在向AVQueuePlayer添加新项目之前添加等待时间，解决了此问题。 如果没有等待期，通知将发送到错误的项。

* (ZD #19856)-默认情况下启用时不显示字幕

webvtt播放列表中导致字幕无法正确显示的问题已得到修复。

* (ZD #21590)-最新来源构建中的视频性能和跟踪

VideoAnalytics中缺失视频长度的问题已修复。

* (ZD #20202)-设置自定义字幕样式会使iOS应用程序崩溃

通过在设置子标题样式时添加额外的空对象检查解决了此问题。

* (ZD #20709)-视频开始跟踪中报告为0的视频长度

此问题与(ZD #21590)相同。

* (ZD #2280)-分析视频长度设置为0

此问题与(ZD #21590)相同。

* (ZD #22592)- Primetime播放问题

此问题与(ZD #19629)相同。

* (ZD#22922)- iOS的手动比特率切换

通过提供指定最大比特率的选项解决了此问题。

* (ZD #23084)- Apple Compliance for IPv6-Only Networks

Apple不建议与IPv6兼容的符号已被删除。

**适用于iOS** 6.0+的1.4.24(1.4.24.661)版

* ZD #2548)- Primetime对移动上交互式广告的支持- VPAID 2.0

如果VPAID广告播放失败，则更新逻辑以取消隐藏播放器视图，从而解决了此问题。

* (ZD #20101)- Custom Chapter实现在广告播放过程中触发章开始事件

通过更新VideoAnalyticsTracker，在章节和非章节边界之间转换时正确检测章节开始/完成，解决了此问题。

* (ZD #20784)-分析：实时视频过渡完成触发内容

通过添加逻辑来在视频跟踪会话期间手动触发内容完成，解决了此问题。

更新了以下库：

* AdobeMobile库到4.10.0
* VHL库到1.5.6
* VHL-Nielsen图书馆至1.6.7
* (ZD #21855)-字幕在中场后不播放

在此期间，重复不连续性标签导致字幕在中间滚动后不显示。 通过删除彼此相邻的不连续标记解决了此问题。

* (ZD #21994)- PTHLSUtils中的字符串越界

导致崩溃的最可能原因是EXT-X-KEY的URL被引号包围。

* ZD #22074)-每分钟在iOS上发生一次AUDVAST崩溃

在版本1.4.23中，修复了由VAST重定向URL中存在不安全字符导致的崩溃。 但是，TVSDK继续跳过这些广告。

通过处理不安全字符并允许播放广告，解决了此问题。

* (ZD #22694)- PTMediaPlayer。  视图被播放器隐藏

如果VPAID广告播放失败，则更新逻辑以取消隐藏播放器视图，从而解决了此问题。

**适用于iOS** 6.0+的1.4.23(1.4.23.641)版

* (ZD #18016)- Primetime SDK在网络状况不佳时无响应

通过改进在发生AVFoundation的致命错误时的错误通知，并允许应用程序在错误后处理重新启动，解决了此问题。

* (ZD #20580)- PTSplicerManager中的崩溃

通过提供额外的保护来避免导致崩溃的并发问题，此问题已得以解决。

* (ZD #21782)- iOS错误代码10100

TVSDK在Adobe访问DRM流上开始播放时返回101000错误的问题已修复。

* (ZD #21889)-在线广告和脱机内容回放失败

解决了AES加密脱机内容上的广告播放失败的问题。

* (ZD #22074)-每分钟在iOS上发生一次AUDVAST崩溃

通过改进对URL中包含无效字符的第三方VAST广告标记的处理，解决了此问题。

* (ZD #2257)- TVSDK无法回放DRM流

在Adobe访问DRM流上开始播放时返回101000错误的TVSDK已修复的问题。

**适用于iOS 6** .0+的1.4.22(1.4.22.627)版

* (ZD #18709)-在iOS的TVSDK中崩溃

已修复某些Adobe访问DRM保护流上发生崩溃的问题。

* (ZD #18850)-根据CRS规则更新创意选择逻辑

通过添加。json配置文件来指定创意选择优先级，解决了此问题。

* (ZD #19770)-受保护AES视频源不再播放

已修复某些302重定向流无法播放的问题。

* (ZD #19629)-进入ATV 4的播放时暂停实时视频

通过为Apple TV 4设备打开播放时添加实时视频暂停的解决方法，解决了此问题。 问题似乎是AppleTV 4问题。

* (ZD #21119)-广告播放后TVSDK停止

在使用广告插入时，已添加序列IV的AES加密流支持。

* (ZD #21125)-提前从实时／线性广告中断返回

添加了支持，以在播放广告间隔至完成之前从广告间隔返回。 通过自定义清单标签指示提前返回。

* (ZD #21224)-对来自Akamai的标记流的播放支持

已将API添加到PTNetworkConfiguration类，以将cookie作为URL参数附加到某些Akamai标记流的区段上。

* (ZD #21287)-无关日志

已修复在xcode控制台中默认显示的某些日志语句的问题，即使禁用日志记录也是如此。

* (ZD #21446)-广告中断事件有时不是由TVSDK触发

在事件流中，广告中断在以前的版本中无法正确触发。 此版本解决了此问题。

**适用于iOS** 6.0+的1.4.21(1.4.21.605)版

* (ZD #20749)-回退将跳过非空VAST响应；额外广告跟踪URL起火

已解决回退广告上的重复ping问题。

**适用于iOS** 6.0+的1.4.20(1.4.20.590)版

* (ZD #18639)- TVSDK正在对冗长的热录制资源使用过多的CPU/资源

在两个级别中修复了过度的CPU/资源使用。 首先，让时间更新函数在全局队列而不是主线程上运行，并通过优化CPU使用以利用先前处理和缓存的m3u8来分析清单。

* (ZD #19349)-限制网络连接时将跳过预卷广告。

通过为应用程序和adMetadata提供超时事件(requestTimeout)，解决了此问题。  adRequestTimeout API以覆盖默认的10秒超时。

* (ZD #19446)-实时流上缺少通知

通过允许应用程序订阅实时流上的EXT-X-项目-DATE-TIME，解决了此问题。

* (ZD #19459)-使用PTMediaPlayerItem prepareAudioOptionsWithAVMediaSelectionOptions准备备用音频时崩溃
* (ZD #19460)-崩溃- `[PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]`

此问题与Zendesk #19459相同。

* (ZD #19574)- TVSDK不返回DRM或非DRM内容的M3U8响应数据

在PTMediaPlayerItem.prepareToPlay中清单文件的初始加载中，如果加载清单失败，TVSDK不会报告对应用程序的失败响应的正文。

通过允许TVSDK将失败响应报告为应用程序错误，解决了此问题。

* (ZD #19615)-回退逻辑不工作

在当前实施中，回退广告被跳过且未重新打包，除非这些广告采用m3u8格式。 通过添加对重新打包回退广告的支持，解决了此问题。

* (ZD #19770)- TVSDK无法播放任何带302重定向的受保护AES内容

修复了重定向问题，因为重定向URL被cleanConnectionData清除，然后才能用于分析清单。

* (ZD #19856)-默认情况下启用时，某些位速率不显示字幕

通过处理iOS中不显示字幕的流区段的错误，解决了此问题。

* (ZD #19868)-当无效创意被贩卖时，TVSDK崩溃

已修复TVSDK中错误地取消分配大型分析器实例的崩溃。

* (ZD #20180)-偶尔会跳过VPAID广告

JavaScript mime类型并不始终包含或视为有效的mime类型。 通过将JavaScript作为有效的MIME类型来解决此问题。

* (ZD #20749)-回退将跳过非空VAST响应；额外广告跟踪URL起火

某些创意未重新打包的问题已解决。

**适用于iOS** 6.0+的1.4.19(1.4.19.563)版

* ZD #18639)- TVSDK对一个冗长的热录制资源使用过多的CPU/资源

通过将DRM m3u8播放列表重写优化为先前已重写的播放列表的缓存位，解决了此问题。 当您回放每段下载后下载m3u8的实时m3u8流时，这一点最相关。

* (ZD#18956)-在iOS Demo Player中设置断点时，player.drmManager为零

通过更新PTMediaPlayer.drmManager API实现以从DRM框架中获取DRMManager，解决了此问题。

**适用于iOS** 6.0+的1.4.18(1.4.18.557)版

* (ZD #18844)在iOS播放器中跟踪实时内容的播放头。

通过允许应用程序设置自己的播放头值，解决了此问题。

* (Zendesk #18518)-如果未指定视频名称，则TVSDK的名称默认为*基于PSDK的播放器。*

通过删除播放器名称的默认值解决了此问题。

**适用于iOS** 6.0+的1.4.17(1.4.17.545)版

* (Zendesk #228)-增强TVSDK以返回清单提取的JSON响应

DRM Framework返回零DRMetadata，而不是在内容不是M3U8时发送错误。 通过在M3U8_PARSER_ERROR通知发生时添加元数据来公开内容，解决了该问题。

* (Zendesk #2231)-提取MediaPlayerNotification中不可用的清单时返回错误

与Zendesk #2228分辨率相同

* (Zendesk #3304)-未填充VAST `[ERRORCODE]` 3.0宏

已解决跟踪URL开头有空格时Auditude SDK无法发送ping的问题。

* (Zendesk #17294)-崩溃SecKeyRawSign

已解决客户代码使用密钥链时可能发生的崩溃问题。

* (Zendesk #18008)-支持iOS8+的cookies以支持标记流

Akamai标记流要求在段请求时发送cookie，这在iOS 7及更早版本上不可能。 从iOS 8开始，Apple已添加一个API，它允许为段请求传递cookie。 现在TVSDK中提供此支持。 此外，还增加了发送用户代理的支持（如果可用）。

* (Zendesk #18166)-当使用dSYM文件选项的DWARF进行编译时，TVSDK 1.4.15会发出数百个警告

所有警告都已解决。

**注意**:已为TVSDK添加与tvOS兼容的库。

**版本1.4.16** (1.4.16.1454)

* Zendesk #3875 —— 播放过程中选项卡S崩溃

还原OKHTTP对CRSauditude的依赖关系，因为TVSDK现在直接使用httpurlconnection而不是curl。 通过在进行另一个JNI调用之前清除异常，该问题已得到解决。

* (Zendesk #4487)-跟踪内容的线性渠道

通过在线性流播放会话期间重新初始化视频心跳跟踪器，解决了该问题。

* (Zendesk #17919)- Android —— 内容搜索导致心跳错误

问题是当在章节中存在搜索时，解决错误状态中的心跳

* (Zendesk #18053)-使用TVSDK的应用程序在Marshmallow上崩溃

当TVSDK库使用进行YUV RGB颜色转换的霓虹代码时，TVSDK在Android M OS上 `->` 崩溃。 通过使用非Neon版本更新导致此问题的功能，解决了此问题 `code`。

* (Zendesk #18072)- Android M —— 应用程序崩溃

检查是否支持用户档案和级别时，调用MediaCodecList和MediaCodecInfo API时发生此崩溃。 Adobe正寻求谷歌的支持，以获得更多的洞察。 通过提前加载所有编解码器信息，以避免仅在需要编解码器信息时调用这些API，解决了此问题。

* (Zendesk #18074)-在Nexus和Android 6.0上不能使用阿拉伯语字幕

通过提供对Android CTS字体映射的支持，解决了此问题。

**适用于iOS** 6.0+的1.4.15(1.4.15.512)版

**注意**:Nielsen模块已从TVSDK版本中删除，但TVSDK将在不久的将来用新的Nielsen集成模块进行更新。

* (ZD #2228)-从获取MediaPlayerNotification中不可用的清单返回错误

添加了元数据，以在发生通知M3U8_PARSER_ERROR时显示内容。

* (ZD #4437)-Adobe PrimetimeSDK内部崩溃

修复了准备字幕／替代音频时报告的崩溃问题。

* (ZD #4487)-跟踪内容的线性渠道

允许在线性流播放会话期间重新初始化视频心跳跟踪器。

**适用于iOS** 6.0+的1.4.14(1.4.14.498)版

* (ZD #17260)- playlistManagerForURL崩溃

修复了并发问题导致的间歇性崩溃。

**版本1.4.13** (iOS 6.0+)

* (ZD #3304)-未填充VAST `[ERRORCODE]` 3.0宏

   * 如果内联广告创意不佳，则会显示错误代码400。
   * `[ERRORCODE]` 宏将进行URL编码。

* (ZD #3865)心跳与IMA广告集成

修复了视频长度报告不正确的错误。

* 更新了TVSDK演示播放器以支持iOS 9

要正确支持iOS 9，您需要配置Application Transportation Security的例外。 为了演示，ATS已完全禁用。

**适用于iOS 6** .0+的1.4.12(1.4.12.464)版

* (ZD #4521)CRS测试客户端和SSAI

修复了3P URL中错误的反向MD5。

**适用于iOS** 6.0+的版本1.4.12(1.4.12.463)

* (ZD #2751)CSAI和CRS/增强：处理某些媒体文件URL中的动态元素。

更新了Creative Repackaging Service，可通过动态创意URL正确处理广告。

* (ZD #3654)1.3.4.166后PSDK版本中的内存泄漏

在iOS 8.2设备上定期播放，drmFramework中的固定内存泄漏

* (ZD #3988)在首次播放后重新搜索预卷时，将跳过预卷

修复了一个错误，以便能够正确禁用广告策略。

* (ZD #4017)请求iOS API强制广告在向后搜索时回放

已通过修复ZD #4279解决

* (ZD #4279)iOS和桌面上的HLS TVSDK广告插入-302重定向问题

修复了广告资产使用相对重定向URL时的错误

**适用于iOS** 6.0+的版本1.4.9(1.4.9.427)

* (ZD #3075)Internet可接通性问题- iOS

添加了检测播放何时停止的通知。

* (ZD #3193)在TVSDK中请求用户档案更改API

更新了PTPlaybackInformation以显示更新的insedBitrate。 更新了BITRATE_CHANGE通知，使M3U8报告的比特率更加可靠和准确。

* (ZD #3324)Primetime广告报告问题（VMAP中无广告媒体）

支持ping空广告中断跟踪URL,TVSDK现在将验证广告中断开始并完成对空广告中断的ping。

**版本1.4.8** (1.4.8.402)

* (ZD #3158)IOS 7在完整事件重播中崩溃

**版本1.4.7** (1.4.7.382)

* (ZD #2197)跟踪广告错误。 为资产添加的通知无法加载清单。
* (ZD #2894)播放器在播放过程中发出4个顶级清单请求。
* (ZD #2992)Auditude报告奇怪的持续时间和标识符。

**版本1.4.6**(1.4.6.325)

* (ZD #2197)跟踪广告错误。 为资产添加的通知无法加载清单

**版本1.4.5** (1.4.5.283)

* (ZD #2141)TreeHouse应用程序的分析实施，添加 `AdobeAnalyticsPlugin.a` 了用于构建包的库。
* 视频心率库更新到1.4.1.2
* [PTPALY-4226] [与ZD #2423相关)执行DRM重置可导致删除应用程序文档数据。

**版本1.4.4** (1.4.4.242)

* 视频心率库(VHL)更新至1.4.1。

* (ZD #2435)有关分析需要更新的TV SDK文档

**版本1.4.2** (1.4.2.210:iOS 6.0+)

* (ZD #1129)返 `_player.currentItem.audioOptions` 回空
* (ZD #2109)Primetime PSDK 1.4.1.125不适用于Xcode 5.1.1
* (ZD #2137)无法加载DRM元数据时，iOS上的PSDK发生崩溃

**版本1.4.1**(1.4.1.125)

* (ZD #1107)CocoaLumberjack重复符号
* (ZD #1644)修改iOS用户代理以进行定位和报告
* (ZD #1850)iOS SDK中包含的Cocoa Lumberjack文件
* (ZD#1908)如果存在超过1个自定义标记，则PSDK会忽略这些自定义标记

**版本1.4.0** (1.4.0.32)

* Zendesk #1024 —— 通过清单从流中删除广告的功能

## 设备认证和支持 {#device-certification-and-support}

>[!NOTE]
>
>TVSDK不支 **持** 以下功能：
>
>* 在任何平台或版本上慢动作。
>* 实时戏法游戏。


**版本1.4.43**

* TVSDK 1.4.43已针对iOS 11进行认证。

**版本1.4.29**

* TVSDK 1.4.29已通过iOS 10的认证。

**版本1.4.28**

* TVSDK 1.4.28已通过iOS 10 Beta 7的认证。
* 通过添加和API强制使用 `forceHTTPS` HTTPS的 `isForcingHTTPS` DRM支持。
* 将VHL库更新为1.5.8，将Mobile库更新为4.8.4，将Logger实用程序库更新为7.0版部署目标。

**版本1.4.19**

此版本的TVSDK已通过iOS和tvOS的FairPlay支持认证。

**版本1.4.17**

* tvOS

   此版本的TVSDK包含对tvOS的支持，并已针对未加密的HLS流进行验证。

   **注意**:请记住以下编译准则：

   * TVSDK tvOs支持仅限于非AdobeDRM加密流。 必须在tvOS构建设置中删除对drmNativeInterface.framework的引用。 仍支持AES加密流。
   * Apple要求启用所有Apple TV应用程序的位代码，因此必须在项目设置中打开此标志。

## 已知问题和限制 {#known-issues-and-limitations}

* 由于iOS UIebView类的停用，从iOS TVSDK 3.6开始：
   * VPAID广告在iPad 13中不会按预期播放。
   * 配套广告不会按预期播放。

* 在iOS TVSDK中，所有广告都被拼接到内容清单中。 广告行为是通过根据内容和广告细分的持续时间进行搜索来实现的。 因此，如果段持续时间不准确，搜索可能并不总是在广告中断开始或结束的确切帧结束。 即使持续时间在帧上，平台本身也具有对搜索的容限，并且可能显示一些帧或广告或内容。 这是平台的限制，广告插入在iOS上与TVSDK一起使用的方式也是如此。
* 在这种情况下，在搜索事件上会做出跳过的决定。 但是，由于清单中的广告段持续时间不能准确地表示广告的实际持续时间，因此搜索不准确帧。 因此，在应用广告策略时，您会看到几个广告帧。
* 它可能会体验到许可证旋转视频在iOS 11上不播放，并且在iOS 9.x和iOS 10.x上播放正常。
* 在VPAID 2.0支持中，如果在AirPlay上播放活动，则跳过VPAID广告。
* 当最小目标设置为iOS7（或更高版本）时，drmNativeInterface.framework无法正确链接。
解决方法：显式指定libstdc++.6.dylib库，如下所示：转到“目标”->“构建阶段”->“将二进制文件与库链接”，并添加libstdc++.6.dylib。
* 插入后期广告以替换API。
* 在广告分时段进行搜索（不退出）会发布重复广告开始和广告分时段通知
* 设置currentTimeUpdateInterval没有任何效果。
注意：在某些iOS版本中，操作系统不会自动加载PSDKLibrary.framework内的资源。 手动将PSDKResources.bundle复制到应用程序的捆绑资源很重要：转到“构建阶段”并复制捆绑包资源。
* 无法使用Xcode 8或更低版本构建引用应用程序。 从iOS TVSDK版本1.4.41开始，使用Xcode 9进行编译。
* VPAID广告不接受delayAdLoadingTolerance值。
* 24077-对于具有字幕的某些HLS内容，播放器在“停止”或“重置”方法时崩溃。
* 启用“及时广告”解决时，详细错误通知不可用。
* 错误通知按广告解决时间记录，而非按广告序列记录。
* HEVC支持在此版本中有以下限制
   * 不支持DRM
   * CC(CEA 608/708)支持不可用，因为CMAF不支持它。
   * 4K支持尚未提供。
   * ID3标记支持不可用，因为CMAF不支持它。
   * 未验证未混合的实时HEVC流。
   * 未验证HEVC广告支持。
* 启用JIT并将容差设置为10秒，在VMAP->VAST重定向广告的情况下，第一次中间广告中断时不会看到VAST调用。
* 为了使广告分辨时间正常工作，每次在实时流播放期间更新播放列表时，播放器都希望在20秒内获得一个拼接的播放列表。 如果在所述间隔内它没有接收到拼接播放列表，则引发内部错误并且播放器停止。

## 实用资源 {#helpful-resources}

* [TVSDK 3.4 for iOS程序员指南](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-for-ios/introduction/ios-3x-overview.html)
* [TVSDK iOS 3.4 API参考](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v34/index.html)
* 请参阅Adobe Primetime学习和支 [持页面上的完整帮助](https://helpx.adobe.com/support/primetime.html) 文档。

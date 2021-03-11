---
title: 用于iOS的TVSDK 1.4发行说明
description: TVSDK 1.4 for iOS发行说明描述了TVSDK iOS 1.4中的新增或更改功能、已解决和已知问题以及设备问题
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '6550'
ht-degree: 0%

---


# 用于iOS的TVSDK 1.4发行说明{#tvsdk-for-ios-release-notes}

TVSDK 1.4 for iOS发行说明描述了TVSDK iOS 1.4中的新增或更改功能、已解决和已知问题以及设备问题。

## 新增功能{#new-features}

**版本1.4.45**

* 为了符合Xcode10,TVSDK已从“`libstdc++`”移动到“`libc++`”，因此支持的最低版本为iOS 7。 更早时候是iOS 6。

**版本1.4.44**

* 此版本中没有新增功能或增强功能。

**版本1.4.43**

* 在不触发部分广告跟踪的情况下加入广告的体验与电视类似。\
   示例：用户在包含3个30秒广告的90秒广告分时段中间（40秒）加入。 这是分时段的第二个广告。

   * 第二个广告在剩余的持续时间（20秒）内播放，然后是第三个广告。
   * 不会触发已播放的部分广告（第二个广告）的广告跟踪器。 只触发第三个广告的跟踪器。

* 在PTAdMetadata接口中添加了布尔类型的enableVodPreroll属性。 该属性可用于在VoD流上启用预滚动。 如果enableVodPreroll为NO，则PSDK不播放预卷。 然而，这对移民没有影响。 enableVodPreroll的默认值为YES。
* 从iOS v1.4.43开始，PTMediaPlayer接口的closedCaptionDisplayEnabled API被标记为已弃用。 要确定给定的PTMediaPlayerItem是否提供隐藏式字幕，请检查PTMediaPlayerMediaItem的subtitlesOptions属性。

**版本1.4.42**

此版本中未添加任何新功能。 有关已修复的问题的列表，请参阅已解决的问题。

**版本1.4.41**

API更改：

* **isSecure**:引入了一个新的API isSecure，以保护播放器不会录制和引发错误。默认值为true。
* **allowExternalRecording**:引入了新的API以允许对安全内容进行空播镜像。播放镜像视为录制，因此，allowExternalRecording值必须设置为“True”，以允许播放镜像或设置为“False”，以停止安全内容的播放镜像。 默认情况下，值为true。

**版本1.4.40**

无新增功能。

**版本1.4.39**

* iOS TVSDK通过VHL 2.0.1和VHL 2.0.1认证，Nielsen通过。
* 更新iOS TVSDK以从新的Akamai主机`primetime-a.akamaihd.net`发出CRS请求。
* 新的主机名配置通过HTTP和HTTPS(SSL)提供更大规模的CRS资产投放。

**版本1.4.36**

在iOS TVSDK中集成和验证VHL 2.0:通过降低API的复杂性，降低VideoHeartbeatsLibrary实现中的障碍。

**版本1.4.34**

* 网络广告信息

   TVSDK API现在提供有关第三方VAST响应的更多信息。 广告ID、广告系统和VAST广告扩展提供在`PTNetworkAdInfo`类中，可通过广告资产上的`networkAdInfo`属性访问。 此信息可用于与其他广告分析平台（如&#x200B;**Moat Analytics**）集成。

**版本1.4.31**

* **账单** 量度为了迎合那些希望只支付其使用费用而不是固定费率的客户，Adobe会收集使用情况量度并使用这些量度来确定向客户收取多少账单。

每次TVSDK生成流开始事件时，播放器都会开始定期向Adobe的付费系统发送HTTP消息。 对于标准VOD、专业VOD（启用中间广告）和实时内容，期间（称为可计费持续时间）可以不同。 每种内容类型的默认持续时间为30分钟，但您与Adobe的合同将决定实际值。

* **针对CRS Ads的多CDN支**&#x200B;持TVSDK现在支持针对CRS广告的多CDN。通过为CRS广告提供FTP详细信息，您可以指定CDN位置，而不是默认的Adobe拥有的CDN（如Akamai）。

**版本1.4.29**

在PTSDKConfig类中，已添加forceHTTPS API。

PTSDKConfig类提供了对向Adobe Primetime广告决策、DRM和Video Analytics服务器发出的请求实施SSL的方法。 有关详细信息，请参阅该类的`forceHTTPS`和`isForcingHTTPS`方法。 如果清单是通过HTTPS加载的，则TVSDK保留HTTPS的内容使用，并在从该清单加载任何相对URL时遵守此用法。

**注意**:对第三方域（如广告跟踪像素、内容和广告URL）的请求以及类似请求不会进行修改，内容提供者和广告服务器有责任提供通过HTTPS支持的URL。

**版本1.4.18**

Primetime iOS TVSDK现在支持VPAID 2.0 Javascript创意，以实现丰富的交互式流内广告体验。

有关VPAID 2.0的详细信息，请参阅[VPAID广告支持](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-vpaid-2.0-ads.md)。

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
   * TV标记语言(TVML)

**版本1.4.13**

**注意**:Nielsen模块已从TVSDK版本中删除，TVSDK将在不久的将来用新的Nielsen集成模块进行更新。

* **广告回退，广告选择逻辑中的菊花链(Zendesk #3103)**

对于启用回退规则的VAST广告（创意），TVSDK将MIME类型无效的广告视为空广告并尝试使用回退广告替代广告。 您可以配置回退行为的某些方面。

有关详细信息，请参阅[VAST和VMAP广告的广告回退](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-ad-fallback.md)。

**版本1.4.9**

* **具有替代内容替换的封锁信号**

作为1.4 TVSDK更新的一部分，我们现在还支持针对线性内容的区域封锁进入和返回。 TVSDK现在可以并行处理两个清单文件，主文件和备用文件，以监视封锁信号，即使在显示替代原始编程的替代编程时也是如此。

**版本1.4.8**

* **已更新至版本1.5的视频心率库(VHL)**

   * 能够将带有视频开始和/或视频/广告/章节开始的元数据作为上下文数据发送
   * 网络流量更少 — 心率平均更少，且更小

**版本1.4.7**

* **预置个性化支持**

支持在事先安装Adobe Indivialization Server以自定义客户端的个性化请求以转到其他端点。

* **基于分辨率的输出保护**

DRM策略现在可指定允许的最高分辨率，具体取决于设备的“输出保护”功能。 例如“如果HDCP可用，则允许播放分辨率高达1080p的内容；如果HDCP不可用，则允许播放分辨率高达480p的内容”。

**版本1.4.4**

* **视频心率库(VHL)更新至版本1.4.1.1**

   * 添加了将来自其他SDK或播放器的不同分析用例与Adobe Analytics Video Essentials捆绑在一起的功能。
   * 已通过删除trackAdBreakStart和trackAdBreakComplete方法优化了广告跟踪。 广告中断从trackAdStart和trackAdComplete方法调用推断出来。
   * 跟踪广告时不再需要playhead属性。
   * 增加了对Marketing Cloud访客ID的支持。

* **Nielsen SDK集成**

   * TVSDK现在支持将mTVR和MDPR ID3信标发送到Nielsen SDK，而无需任何自定义集成。 为了开始，请下载3.1.2.19 Nielsen iOS App SDK。

**版本1.4.0**

* **具有替代内容替换的封锁信号**

   * 作为1.4 TVSDK更新的一部分，TVSDK现在还支持针对线性内容的区域封锁进入和返回。 TVSDK现在可以并行处理两个清单文件，主文件和备用文件，以监视封锁信号，即使在显示替代原始编程的替代编程时也是如此。

* **删除/替换C3广告**

   * 现在，无需进行额外的准备工作，即可将新广告动态插入从C3窗口传出的视频点播(VOD)资产中。 TVSDK现在提供一个API，用于删除自定义内容范围和动态插入新广告。 当实时/线性内容在广播期间播放时，并且会立即作为点播内容被拉下来使用，而无需适当时间“清理”资源时，此强大的新功能也非常有用。

## 1.4 {#device-certification-and-support-in}中的设备认证和支持

>[!NOTE]
>
>TVSDK支持以下功能&#x200B;**不**:
>
>* 在任何平台或版本上慢动作。
>* 实时戏法。


**版本1.4.43**

* TVSDK 1.4.43已针对iOS 11进行认证。

**版本1.4.29**

* TVSDK 1.4.29已通过iOS 10认证。

**版本1.4.28**

* TVSDK 1.4.28已通过iOS 10 Beta 7认证。
* 通过添加forceHTTPS和isForcingHTTPS API来强制HTTPS的DRM支持。
* 将VHL库更新为1.5.8，将Adobe Mobile库更新为4.8.4，将记录器实用程序库更新为7.0版部署目标。

**版本1.4.19**

此版本的TVSDK已通过iOS和tvOS的FairPlay支持认证。

**版本1.4.17**

* tvOS

   此版本的TVSDK包含对tvOS的支持，并已针对未加密的HLS流进行验证。

   **注意**:请记住以下编译准则：

   * TVSDK tvOs支持仅限于非AdobeDRM加密流。 必须在tvOS构建设置中删除对drmNativeInterface.framework的引用。 仍支持AES加密流。
   * Apple要求启用所有Apple TV应用程序的位代码，因此必须在项目设置中打开此标志。

## 解决了1.4 {#resolved-issues-in}中的问题

<!-- 

Comment Type: draft

 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 
-->

<!-- 

Comment Type: draft

 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 

-->

**版本1.4.45{#ios-tvsdk}**

* 票证#36294 - iOS TVSDK在Xcode 10中无法正常工作

   * 修复了XCode 10上的TVSDK的编译问题。 由于XCode 10要求，从iOS 1.4.45版的TVSDK上构建的应用程序要求最低部署目标，因为iOS 7.0

* 票#36321 — 在PTMediaPlayer和处于“播放”状态的AVPlayer实例之间的可搜索范围中观察到的差异。
* 票证#36493 - iOS 12上的`libstdc++`支持

   * 修复了iOS 12上的TVSDK的编译问题。 从iOS 1.4.45版到TVSDK上构建的应用程序需要最低的部署目标，如iOS 7.0

**版本1.4.44**

* 票#34683 — 广告播放进度时间为负

   * 当广告服务器报告的持续时间与实际广告内容不匹配时，会引入其他检查来处理这种情况。

* 票证#34801 — 当在暂停状态期间搜索到新位置时，当前时间和localTime未更新

   * 当播放器处于暂停状态时，播放器的当前时间现在可以设置为零；之前，仅在播放状态中将当前时间设置为零。

* 票#35037 — 从基于信号的广告插入返回时，播放会停止有错误的URL。

   * 改进了针对1.4.42版中#34385问题提供的修复。 添加了isCancelled检查和异常处理代码，使操作队列更加健壮。

**版本1.4.43**

* (ZD#32990)- iOS:在某些提示点上播放内容，而不是投放广告。 属于AVPlayerItem接口的“selectedMediaOptionInMediaSelectionGroup”API现在已移到iOS 11中的AVMediaSelection下。 使用此新API解决了此问题。
* (ZD#33683)TVSDK removed == suffix from the metadata strings. 解析逻辑中修复了此问题。
* (ZD#33905)- iOS TVSDK使用两个用户代理调用清单文件。 用户代理问题已在第一次m3u8调用（新安装案例）中得到修复。 M3u8拥有相同的用户代理来处理所有呼叫。
* (ZD#34293) — 在iOS11上无法正确播放在线性流上插入的预滚动。 已修复前放广告的问题。
* (ZD#34684) — 应用广告跳过策略时，将显示前滚广告帧数几秒钟。 新的API enableVodPreroll已引入，可在vod播放中禁用预卷播放。 此API的默认值为“是”。 API可确保跳过主内容中的广告内容拼接。
* (ZD#34765) — 调用stop()后，仍有少数传输流区段被下载。 增强了Stop()API以避免下载额外的区段。
* (ZD#34865) — 在iOS上，实时流的前滚广告被截断。 与iOS11相关，并添加一个附加检查以确认流是前置内容还是主内容，可解决此问题。
* (ZD#35093) — 修复了在启动时，如果流的主要变体失败（返回404），则播放不切换到备份流的故障转移方案。

**版本1.4.42(1.4.42.118)**

* (ZD#34385) — 从基于信号的广告插入返回时，播放会停止，并且URL不正确。

   增加CustomAVAssetLoaderOperations的最大并发计数，以便清单读取可以继续执行。
* (ZD#34373) — 当不允许流录制时，最终用户无法流化到HDMI连接的设备。
* (ZD#32678)- TVSDK在iOS上不收集正确的广告ID。

   在VHL ping中，如果出现VAST/VMAP重定向，现在会拾取最终广告创意的广告ID。
* (ZD#33904)- TVSDK未注册AVFoundationnotifications AVAudioSessionMediaServicesWerLostNotification和AVAudioSessionMediaServicesWerResetNotification。

   现在可在播放器应用程序上注册PTMediaServicesWereLostNotification和PTMediaServicesWereResetNotification，以在媒体服务重置或丢失时获取通知。

* (ZD#33815) — 客户无需更新应用程序即可更新其优先级和标准化CRS规则。

   已将getCRSRulesJsonURL和setCRSRulesJsonURL API添加到iOS TVSDK。

**版本1.4.41(1.4.41.76)**

* (ZD #34464) — 使用TVSDK版本1.4.41构建参考应用程序时出现的问题

   启动此版本时，编译iOS的TVSDK需要Xcode 9。
* (ZD #29456) — 处于暂停状态的播放开始

   修复了进入播放时视频暂停的暂停问题。
* (ZD #30371) — 当我们在线性流中插入2个以上广告时，AdBreak开始时间会发生变化

   修复了尝试在Apple TV上播放内容时出错的问题，该错误会完全阻止播放
* (ZD #32146) — 阻止iOS 11开发测试版上的HLS Live内容未收到PTMediaPlayerStatusError

   使用Charles（Drop connection和403）阻止时，未收到HLS Live和VOD内容的PTMediaPlayerStatusError
* (ZD #29242) — 启用广告时播放视频播放失败

   启用广告并启用AirPlay后，开始播放视频时，视频播放不会开始，不会显示错误
* (ZD#33341)- DRMInterface.h触发器在Xcode 9中生成警告

   修复了DRMInterface.h中缺少参数列表中“void”一词的两个块原型
* (ZD#31979) — 对于iPhone 7/iPhone7+，如果iOS 10或更高版本，则不编译/运行

   不再支持为早于iOS 7编译IB文档
* (ZD#32920) — 广告中断内的空白屏幕，无广告中断完成

   当广告断点显示广告实例时，在广告实例完成后，将显示空白屏幕
* (ZD#32509) — 停用iOS 11屏幕录制停用iOS 11上的屏幕录制

* (ZD#33179)- iOS11上的间歇性事件故障

   修复了iOS 11上的事件故障

**版本1.4.40** (1.4.40.72)

* (ZD #32465) — 播放器无法处理合并的播放列表。

   调用finishLoadingWithError(with:错误)，以使AV基础尝试替代流/触发故障转移。

* (ZD #31951) — 许可证轮替期间TVSDK错误。

   修复了许可证轮换问题。
* (ZD #31951) — 广告中断内的空白屏幕，没有广告中断完成。

   处理了Facebook VPAID广告通常在单个\&amp;lt;AdParameters\&amp;gt；中返回多个CDATA块的问题；VAST节点。
* (ZD #33336)- [iOS] TVSDK — 尽管Freewheel返回的广告足够多，广告窗格仍未填写。

   创建了基于父序列和索引的序列广告和回退广告和排序之间的父子关系。

**版本1.4.39** (1.4.39.43)

* (ZD #32178)- iOS TVSDK版本不正确。

   日志文件中的TVSDK版本输出为1.0.211。修复了输出正确版本的问题。

* (ZD #32199) — 延迟广告加载 — 不显示内容的视频。

   以前未初始化的本地Adbreak时间轴现在在使用前刷新。

* (ZD #27528) — 如果在iOS 1.2上将辅助音频设置为非默认值，则在播放资源开始后1-45秒内，视频、音频或两者都将冻结。

   准备音轨并通知其处于“就绪”状态。

* (ZD #30411) — 如果您选择辅助Sap语言，您可能会收到意外结果，如没有音频或音频不正确。

   准备音轨并通知其处于“就绪”状态。

* (ZD #32199) — 延迟广告加载 — 不显示内容的视频。

   以前未初始化的本地Adbreak时间轴现在在使用前刷新。

* (ZD #27528) — 如果在iOS 1.2上将辅助音频设置为非默认值，则在播放资源开始后1-45秒内，视频、音频或两者都将冻结。

   准备音轨并通知其处于“就绪”状态。

* (ZD #30411) — 如果您选择辅助Sap语言，您可能会收到意外结果，如没有音频或音频不正确。

   准备音轨并通知其处于“就绪”状态。

**版本1.4.38** (1.4.38.860)

* (ZD #29281)- iOS:向CRS请求添加AdSystem和Creative Id

基于CRS规范规则的CRS请求中创意ID和AdSystem的使用

* (ZD #29176)- PTAdPolicyDeligate satAdBreakAsWatched:position上的崩溃

现在已处理空AdBreak导致的崩溃。

* (ZD #30125) — 程序化广告在iOS平台中不起作用

在iOS中增加了程序化广告支持。

* (ZD #30782)- #EXT-X-项目-DATE-TIME通知

对于包含LIVE DRM流的# EXT-X-项目-DATE-TIME标记，不会触发定时元数据事件。

**版本1.4.37(1.4.37.842)**

* (ZD #28950)- VOD播放问题

流中# EXT-X-PLAYLIST-TYPE标签设置为事件而非VOD时的播放问题

* (ZD #29281)- iOS:向CRS请求添加AdSystem和Creative Id

在基于CRS规范规则的CRS请求中使用创意ID和AdSystem。

* (ZD #29462)- A&amp;E VOD中的ThuochHub广告导致iOS应用程序崩溃

**版本1.4.36(1.4.36.835)**

* (ZD #29418) — 持续时间为0(#EXT-X-CUE-OUT:0.000)的提示导致iOS TVSDK停止或崩溃播放。

问题已修复，且播放开始正确。

* (ZD #29462) — 在iOS TVSDK上导致崩溃的VOD中添加广告。

问题已修复。 iOS TVSDK引发异常(AUDNetworkAdInfo::initWithAdId)，但未处理它。 此异常是由于空广告ID。

* (ZD #29281) — 向CRS请求添加AdSystem和Creative ID。

在1401和1403请求中将AdSystem和CreativeId包含为新参数（所有其他参数保持不变）。

**版本1.4.35** (1.4.35.830)

* (ZD #27830) — 需要以编程方式确定iOS中隐藏字幕和子标题之间的差异。

TVSDK现在公开两种类型，它们可用于过滤掉所需的题注类型。

* (ZD #29160)- EXT-X-CUE-OUT广告提示未在TVSDK iOS上正确拼接。

EXT-X-CUE-OUT Midroll广告正在播放。

* (ZD #29100) — 当用户滑到电影末尾时，应用程序崩溃。

修复了与同步相关的多个崩溃。

* (ZD #28785)、(ZD #27712)和(ZD #25076)- iOS应用程序在大型实时事件期间崩溃。

修复了与同步相关的多个崩溃。

**版本1.4.34** （适用于iOS 6.0+的1.4.34.815）

* (ZD# 28481) — 由于在这些FER流的广告中断结束时附加了不正确的密钥，导致FER中断

对于FER流，在广告中断结束后插入广告中断前的密钥。 通过在广告中断的末尾附加&#x200B;*最后查看的键*&#x200B;来解决此问题。

**版本1.4.33** （适用于iOS 6.0+的1.4.33.803）

* (ZD# 21701)为子帐户启用CRS

根据CRS后端的要求，为1401 CRS请求发送原始创意URL而不是标准化URL，从而启用。

* (ZD# 26218)- PSDKResources.bundle加载问题

通过更新资源加载以从所有可用的包中查找，解决了此问题。

* (ZD# 27460)Midroll第一个广告呼叫 — POST到cdn.auditude<span></span>.com返回403。

新的CDN帐户无法处理POST CDN请求。 通过更新代码使`cdn.auditude.com`广告请求成为GET而不是POST，解决了此问题。

**版本1.4.32** （适用于iOS 6.0+的1.4.32.792）

* (ZD# 27132)支持VMAP广告分段的小数值。

当内容未按定义的广告分段时，整数会导致意外的广告放置。 通过不将小数值转换为整数，解决了该问题。

* (ZD# 27189)带有EXT-X-DINSTRUCTION-SEQUENCE标签的AES内容播放不正确。

通过将标记放置在播放列表的开头，解决了该问题。

**版本1.4.31** （适用于iOS 6.0+的1.4.31.785）

* (ZD# 24528)实施TVSDK计费使用量度

有关详细信息，请参阅[帐单量度](../programming/tvsdk-1.4-for-ios/c-psdk-ios-1.4-billing/c-psdk-ios-1.4-billing.md)。

* (ZD# 24642)对TVSDK的画中画支持

画中画功能在某些情况下无法正常工作，现已修复。

* (ZD# 25246)错误的广告中断信号

通过对齐变体清单上的不连续标签，解决了此问题。

* (ZD# 26218)当尝试将PSDKLibrary.framework包含在客户端的应用程序框架中时，应用程序构建过程变得复杂

已按照请求打包PSDKLibrary.framework来解决此问题。

* (ZD# 26364)针对CRS广告的多CDN支持

<!-- 
Comment Type: draft
For more information, see [Multiple CDN support for CRS Ad Delivery](http://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-concept-Multiple_CDN_support_for_CRS_ad_delivery).
-->
* (ZD# 27028)在iOS 10中播放某些流时出现延迟。

通过为没有M3U8扩展的流提供解决此问题的方法。

**版本1.4.30** （适用于iOS 6.0+的1.4.30.754）

TVSDK在此版本中已解决以下问题：

* (ZD# 24180)向允许列表添加自定义标头

新的自定义标头已添加到TVSDK允许列表。

* (ZD# 25016)设置ABR控制参数时，会随机选择故障转移流

通过按在包含故障转移URL的流上为ABR设置提供initialBitrate设置时的顺序维护ABR流，解决了此问题。 这将避免播放故障转移流而不是主流。

* (ZD# 25076)PTAuditudeAdResolver loadComplete上的崩溃

已修复在快速开始/停止包含广告的多个PTMediaPlayer实例期间发生崩溃的问题。

* (ZD# 25960)没有其他订阅标记会触发元数据更改通知广播

在清单中第一段之前出现订阅标记时未通知的问题。

* (ZD# 26084)PSDK投106000.101000。-11833在从上一个广告中断转换回娱乐内容时找不到解码器错误

当来自VMAP的最后一个广告中断开始时间在总持续时间完成之前，在某些情况下，直到最后一个广告中断结束之后才插入密钥。 此问题已修复。

* 视频心率库(VHL)已更新为版本1.5.9，以解决以下问题：

   * (ZD #22351)VHL — 分析：实时视频资产持续时间

通过将assetDuration API添加到`PTVideoAnalyticsTrackingMetadata`来更新实时/线性流的资产持续时间并提供检查实时流的逻辑，解决了此问题。

* (ZD# 22675)VHL — 分析：更新实时视频资产持续时间

此问题与ZD #22351相同。

* (ZD #25908)VHL — 分析：Adobe心率事件崩溃

通过更新实施以使用最新版VHL for iOS版本1.5.9来提高稳定性和性能，解决了此问题。

* (ZD #25956)VHL — 分析：重复播放视频时崩溃

此问题与ZD #25908相同。

**版本1.4.29** (1.4.29.743)

* (ZD# 23901)第三方广告不播放

通过切换到CRS v3 URL结构以在重新打包的URL中包含区域ID，解决了此问题。

* (ZD #25183)在tvOS和iOS上播放DRM的问题

通过为多DRM支持所需的多个关键标签提供支持，解决了此问题。

* (ZD# 25334)TVSDK无法播放cDVR共享内容

通过阻止TVSDK将空字符串转换为绝对URL，解决了此问题。

* (ZD# 25347)在AVURLAsset上设置自定义HTTP头

已添加通过PTNetworkConfiguration类对其区段请求的自定义标头的支持。

**版本1.4.28** (1.4.28.722)

* (ZD #24549)多个广告跟踪调用

通过更新时间轴管理器以在创建多个播放器时侦听特定对象的通知，解决了此问题。

* (ZD #24758)PTManifestLogger不支持iOS 8

通过将记录器实用程序库更新到版本7.0部署目标解决了此问题。

* (ZD #24775)由于广告而延迟的流

通过正确计算事件播放列表上的持续时间漂移，解决了此问题。

* (ZD #24799)某些剧集在iOS APP上不播放

当WebVTT文件受地域限制时，通过为字幕使用本地Web服务器解决了此问题。

**适用于iOS 6.0** +的版本1.4.27(1.4.27.711)

* (ZD #24089) — 针对长DVR流的广告解析优化

通过添加多个优化来解决此问题，以缩短在实时/线性流中处理DVR窗口所需的时间。

* (ZD #21554) — 未为application-type = video/mp4触发TVSDK错误信标

通过使播放器能够ping无效资产格式上的正确错误跟踪URL，解决了此问题。

* (ZD #24424)- EXC_BAD_ACCESS KERN_INVALID_ADDRESS类型的崩溃源于较新硬件设备上iOS的PSDKLib内部。

已修复因取消分配的媒体播放器实例而发生的在不同流之间快速切换播放时的崩溃。

* (ZD #24575)- enableDebugLog=true时，在32位设备上的TVSDK中发生崩溃

已修复在启用日志记录时导致32位设备崩溃的日志格式问题。

**适用于iOS 6.0** +的版本1.4.26(1.4.26.702)

* (ZD# 20213) — 对于XCode7,TVSDK FW需要动态/模块化

   * 通过更新具有模块支持的库来修复

**适用于iOS 6.0** +的1.4.25(1.4.25.684)版

* (ZD #19629) — 进入ATV 4播放时暂停实时视频

通过在删除旧项目后但在向AVQueuePlayer添加新项目之前添加等待时间来解决此问题。 如果没有等待时间，则通知将发送到错误的项。

* (ZD #19856) — 默认情况下启用时不显示字幕

webvtt播放列表中导致字幕无法正确显示的问题已修复。

* (ZD #21590) — 最新来源构建中的视频性能和跟踪

VideoAnalytics中缺失视频长度的问题已修复。

* (ZD #20202) — 设置自定义字幕样式会使iOS应用程序崩溃

通过在设置子标题样式时添加其他空对象检查解决了此问题。

* (ZD #20709) — 在视频开始跟踪中，视频长度报告为0

此问题与(ZD #21590)相同。

* (ZD #22280) — 将“Analytics视频长度”设置为0

此问题与(ZD #21590)相同。

* (ZD #22592)- Primetime中Airplay的问题

此问题与(ZD #19629)相同。

* (ZD#22922)- iOS的手动比特率切换

通过提供指定最大比特率的选项解决了此问题。

* (ZD #23084)- Apple仅IPv6网络的规范

Apple不建议与IPv6兼容的符号已被删除。

**适用于iOS 6.** 0+的1.4.24(1.4.24.661)版

* ZD #2548)- Primetime对移动上交互式广告的支持 — VPAID 2.0

如果VPAID广告无法播放，则通过更新逻辑以取消隐藏播放器视图来解决此问题。

* (ZD #20101) — 自定义章节实现在广告播放过程中触发章节开始事件

通过更新VideoAnalyticsTracker，在章节和非章节边界之间转换时正确检测章节开始/完成，解决了此问题。

* (ZD #20784) — 分析：为实时视频过渡完成触发内容

通过在视频跟踪会话期间添加一个逻辑来手动触发内容完成，解决了此问题。

更新了以下库：

* AdobeMobile库到4.10.0
* VHL库到1.5.6
* VHL-Nielsen图书馆至1.6.7
* (ZD #21855) — 字幕在中间滚动后不播放

在此问题中，重复中断标签导致字幕在中间滚动后不显示。 通过删除彼此相邻的不连续标签解决了此问题。

* (ZD #21994)- PTHLSUtils中的字符串越界

导致崩溃的最可能原因是EXT-X-KEY的URL被引号包围。

* ZD #22074) — 每分钟在iOS上发生一次AUDVAST崩溃

在版本1.4.23中，修复了由VAST重定向URL中存在不安全字符导致的崩溃。 但是，TVSDK仍在跳过这些广告。

通过处理不安全字符和允许播放广告，解决了此问题。

* (ZD #22694)- PTMediaPlayer。  视图由播放器隐藏

如果VPAID广告无法播放，则通过更新逻辑以取消隐藏播放器视图来解决此问题。

**适用于iOS 6.0** +的版本1.4.23(1.4.23.641)

* (ZD #18016)- Primetime SDK没有对网络状况不佳的响应

通过改进发生AVFoundation的致命错误时的错误通知并允许应用程序在错误发生后处理重新启动，解决了此问题。

* (ZD #20580)- PTSplicerManager中的崩溃

通过提供额外保护来避免导致崩溃的并发问题，解决了此问题。

* (ZD #21782)- iOS错误代码10100

TVSDK在Adobe访问DRM流上启动播放时返回101000错误的问题已修复。

* (ZD #21889) — 在线广告和脱机内容播放失败

解决了AES加密脱机内容上的广告播放失败的问题。

* (ZD #22074) — 每分钟在iOS上发生一次AUDVAST崩溃

通过改进对URL中包含无效字符的第三方VAST广告标记的处理，解决了此问题。

* (ZD #22257)- TVSDK无法播放DRM流

修复了在Adobe访问DRM流上启动播放时返回101000错误的TVSDK的问题。

**适用于iOS 6.0** +的1.4.22(1.4.22.627)版

* (ZD #18709) — 在iOS的TVSDK中崩溃

已修复某些Adobe访问DRM保护流上发生崩溃的问题。

* (ZD #18850) — 根据CRS规则更新创意选择逻辑

通过添加.json配置文件来指定创意选择优先级，解决了此问题。

* (ZD #19770) — 受保护的AES视频源不再播放

已修复某些302重定向流无法播放的问题。

* (ZD #19629) — 进入ATV 4播放时暂停实时视频

通过为Apple TV 4设备打开播放时添加实时视频暂停的解决方法，解决了此问题。 问题似乎是AppleTV 4问题。

* (ZD #21119) — 在广告播放后，TVSDK停止

在使用广告插入时，增加了对序列IV的AES加密流的支持。

* (ZD #21125) — 提前从实时/线性广告中断返回

已添加支持，以在播放到完成之前从广告中断返回。 通过自定义清单标记指示提前返回。

* (ZD #21224) — 对来自Akamai的标记流的播放支持

API已添加到PTNetworkConfiguration类，以在某些Akamai标记流的区段上附加cookies作为URL参数。

* (ZD #21287) — 无关日志

修复了在xcode控制台中默认显示的某些日志语句的问题，即使在禁用日志记录时也是如此。

* (ZD #21446)- Ad Break事件有时不是由TVSDK触发

在事件流中，广告中断在上一个版本生成中无法正确触发。 此版本可解决此问题。

**适用于iOS**  6.0+的1.4.21(1.4.21.605)

* (ZD #20749) — 回退将跳过非空VAST响应；额外广告跟踪URL着火

已解决回退广告上的重复ping问题。

**适用于iOS**  6.0+的1.4.20(1.4.20.590)

* (ZD #18639)- TVSDK正在对冗长的热录制资源使用过多的CPU/资源

在两个级别中修复了CPU/资源使用过多的问题。 首先，让时间更新函数在全局队列而不是主线程上运行，并通过优化CPU使用以利用先前处理和缓存的m3u8来分析清单。

* (ZD #19349) — 在限制网络连接时将跳过预卷广告。

通过为应用程序和adMetadata提供超时事件(requestTimeout)来解决此问题。  adRequestTimeout API以覆盖默认的10秒超时。

* (ZD #19446) — 实时流上缺少通知

通过允许应用程序订阅实时流上的EXT-X-项目-DATE-TIME，解决了此问题。

* (ZD #19459) — 使用PTMediaPlayerItem prepareAudioOptionsWithAVMediaSelectionOptions准备备用音频时崩溃
* (ZD #19460) — 崩溃 — [PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]

此问题与Zendesk #19459相同。

* (ZD #19574)- TVSDK不返回DRM或非DRM内容的M3U8响应数据

在PTMediaPlayerItem.prepareToPlay中清单文件的初始加载中，如果加载清单失败，TVSDK不会报告对应用程序的失败响应的正文。

通过允许TVSDK将失败响应作为错误报告给应用程序，解决了此问题。

* (ZD #19615) — 回退逻辑无效

在当前实施中，回退广告被跳过且未重新打包，除非这些广告采用m3u8格式。 通过添加对重新打包回退广告的支持，解决了此问题。

* (ZD #19770)- TVSDK无法播放任何带302重定向的受保护AES内容

已修复重定向问题，因为在可用于分析清单之前，重定向URL已被cleanConnectionData清除。

* (ZD #19856) — 默认情况下启用时，某些位速率不显示字幕

通过处理iOS中不显示字幕的流段的错误，解决了此问题。

* (ZD #19868) — 当无效创意被贩卖时，TVSDK崩溃

已修复TVSDK中错误地取消分配广义分析器实例的崩溃。

* (ZD #20180) — 偶尔会跳过VPAID广告

JavaScript mime类型并非始终包含或视为有效的mime类型。 通过将JavaScript作为有效的mime类型来解决此问题。

* (ZD #20749) — 回退将跳过非空VAST响应；额外广告跟踪URL着火

某些创意未重新打包的问题已解决。

**适用于iOS 6.** 0+的1.4.19(1.4.19.563)版

* ZD #18639)- TVSDK对冗长的热录制资源使用过多的CPU/资源

通过优化DRM m3u8播放列表重写到缓存先前已重写的播放列表位，解决了此问题。 这在您播放每段下载后下载m3u8的实时m3u8流时最相关。

* (ZD#18956) — 在iOS Demo Player中设置断点时，player.drmManager为nil

通过更新PTMediaPlayer.drmManager API实现以从DRM框架中获取DRMManager，解决了此问题。

**适用于iOS 6.0** +的1.4.18(1.4.18.557)版

* (ZD #18844)跟踪iOS播放器中实时内容的播放头。

通过允许应用程序设置其自己的播放头值，解决了此问题。

* Zendesk #18518 — 如果未指定视频名称，则TVSDK的名称默认为&#x200B;*基于PSDK的播放器。*

通过删除播放器名称的默认值解决了此问题。

**适用于iOS 6.** 0+的1.4.17(1.4.17.545)版

* Zendesk #2228 — 增强TVSDK以返回清单获取的JSON响应

DRM框架返回零DRMetadata，而不是在内容不是M3U8时发送错误。 通过在M3U8_PARSER_ERROR通知发生时添加元数据以公开内容，解决了该问题。

* Zendesk #2231 — 从获取MediaPlayerNotification中不可用的清单返回错误

与Zendesk #2228分辨率相同

* Zendesk #3304 — 未填充VAST 3.0 `[ERRORCODE]`宏

解决了跟踪URL开头有空格时Auditude SDK无法发送ping的问题。

* Zendesk #17294 — 崩溃SecKeyRawSign

解决了客户代码使用密钥链时可能发生的崩溃问题。

* Zendesk #18008 - iOS8+支持Cookie以支持标记流

Akamai标记流要求在区段请求时发送cookie，而在iOS 7及更早版本上无法这样做。 从iOS 8开始，Apple已添加一个API，允许为区段请求传递Cookie。 TVSDK中现在提供此支持。 此外，还添加了对发送用户代理的支持（如果可用）。

* Zendesk #18166 - TVSDK 1.4.15在使用dSYM文件选项的DWARF进行编译时会发出数百条警告

所有警告都已解决。

**注意**:为TVSDK添加了与tvOS兼容的库。

**版本1.4.16** (1.4.16.1454)

* Zendesk #3875 - Tab S在播放期间崩溃

正在还原OKHTTP对CRSauditude的依赖关系，因为TVSDK现在直接使用httpurlconnection而不是curl。 通过在进行另一个JNI调用之前清除例外解决了此问题。

* Zendesk #4487 — 跟踪内容的线性渠道

通过在线性流播放会话期间重新初始化视频心率跟踪器，解决了该问题。

* Zendesk #17919 - Android — 内容搜索导致心跳错误

问题是当在章节中存在搜索时，解决错误状态中的心跳

* Zendesk #18053 — 使用TVSDK的应用程序在Marshmallow上崩溃

当TVSDK库使用执行YUV -> RGB颜色转换的neon代码时，TVSDK在Android M OS上崩溃。 通过使用非Neon版本的代码更新导致此问题的函数，解决了此问题。

* Zendesk #18072 - Android M — 应用程序崩溃

检查是否支持用户档案和级别时，调用MediaCodecList和MediaCodecInfo API时发生此崩溃。 Adobe正在寻求谷歌的支持，以获得更多洞察。 通过提前加载所有编解码器信息以避免仅在需要编解码器信息时才调用这些API，解决了此问题。

* Zendesk #18074 — 阿拉伯语字幕在Nexus和Android 6.0上不工作

通过提供对Android CTS字体映射的支持解决了此问题。

**适用于iOS 6.** 0+的1.4.15(1.4.15.512)版

**注意**:Nielsen模块已从TVSDK版本中删除，但TVSDK将在不久的将来用新的Nielsen集成模块进行更新。

* (ZD #2228) — 从获取MediaPlayerNotification中不可用的清单返回错误

添加了元数据，以在发生通知M3U8_PARSER_ERROR时公开内容。

* (ZD #4437)-Adobe Primetime SDK内部崩溃

修复了准备字幕/替代音频时报告的崩溃问题。

* (ZD #4487) — 跟踪内容的线性渠道

允许在线性流播放会话期间重新初始化视频心率跟踪器。

**适用于iOS 6.0** +的版本1.4.14(1.4.14.498)

* (ZD #17260)- playlistManagerForURL崩溃

修复了并发问题导致的间歇性崩溃。

**版本1.4.13** (iOS 6.0+)

* (ZD #3304) — 未填充VAST 3.0 `[ERRORCODE]`宏

   * 如果内嵌，则将显示错误代码400   广告的创意很差。
   * `[ERRORCODE]` 宏将进行URL编码。

* (ZD #3865)心率与IMA广告集成

修复了视频长度报告不正确的错误。

* 更新了TVSDK演示播放器以支持iOS 9

要正确支持iOS 9，您需要配置Application Transportation Security的例外。 为演示目的，ATS已完全禁用。

**适用于iOS 6.0** +的版本1.4.12(1.4.12.464)

* (ZD #4521)CRS测试客户端和SSAI

修复了3P URL中不正确的反向MD5。

**适用于iOS 6.0** +的版本1.4.12(1.4.12.463)

* (ZD #2751)CSAI和CRS |增强：处理特定媒体文件URL中的动态元素。

更新了Creative重新打包服务，以通过动态创意URL正确处理广告。

* (ZD #3654)1.3.4.166后PSDK版本中的内存泄漏

在iOS 8.2设备上定期回放，修复了drmFramework中的内存泄漏

* (ZD #3988)在首次播放后重新搜索时，会跳过预卷

修复了一个错误，以便可以正确禁用广告策略。

* (ZD #4017)请求iOS API在向后搜索时强制和回放

通过ZD #4279的修复解决

* (ZD #4279)iOS和桌面上的HLS TVSDK广告插入–302重定向问题

修复了广告资产使用相对重定向URL时的错误

**适用于iOS 6.** 0+的版本1.4.9(1.4.9.427)

* (ZD #3075)Internet可达性问题 — iOS

添加了通知以检测播放何时停止。

* (ZD #3193)在TVSDK中请求用户档案更改API

更新了PTPlaybackInformation以显示更新的assidedBitrate。 更新了BITRATE_CHANGE通知，使M3U8报告的比特率更加可靠和准确。

* (ZD #3324)Primetime广告报告问题（当VMAP中没有广告媒体时）

支持ping空广告中断跟踪URL，TVSDK现在将验证广告中断开始并完成对空广告中断的ping

**版本1.4.8** (1.4.8.402)

* (ZD #3158)IOS 7在完整事件重播中崩溃

**版本1.4.7** (1.4.7.382)

* (ZD #2197)跟踪广告错误。 为资产添加的通知无法加载清单。
* (ZD #2894)播放器在播放期间发出4个顶级清单请求。
* (ZD #2992)Auditude报告的奇怪持续时间和标识符。

**版本1.4.6**(1.4.6.325)

* (ZD #2197)跟踪广告错误。 为资产添加的通知无法加载清单

**版本1.4.5** (1.4.5.283)

* (ZD #2141)Analytics implementation for TreeHouse app，添加了要构建包的AdobeAnalyticsPlugin.a库。
* 视频心率库更新到1.4.1.2
* (PTPALY-4226)(与ZD #2423相关)执行DRM重置可能会导致删除应用程序文档数据。

**版本1.4.4** (1.4.4.242)

* 视频心率库(VHL)更新至1.4.1。

* (ZD #2435)有关分析需求更新的TV SDK文档

**版本1.4.2** (1.4.2.210:iOS 6.0+)

* (ZD #1129)_player.currentItem.audioOptions返回空
* (ZD #2109)Primetime PSDK 1.4.1.125不适用于Xcode 5.1.1
* (ZD #2137)无法加载DRM元数据时，iOS上的PSDK中崩溃

**版本1.4.1** (1.4.1.125)

* (ZD #1107)CocoaLumberjack重复符号
* (ZD #1644)为定位和报告修改iOS用户代理
* (ZD #1850)iOS SDK中包含的Cocoa Lumberjack文件
* (ZD#1908)如果存在1个以上的自定义标记，则PSDK会忽略这些自定义标记

**版本1.4.0** (1.4.0.32)

* Zendesk #1024 — 通过清单从流中删除广告的功能

## 1.4 {#known-issues-in}中的已知问题

* 在iOS TVSDK中，所有广告都拼接到内容清单中。 广告行为是通过根据内容和广告区段的持续时间进行搜索来实现的。 因此，如果区段持续时间不准确，搜索可能并不总是在广告中断开始或结束的确切帧结束。 即使持续时间是帧，平台本身对搜索也有容差，并且可能会显示一些帧或广告或内容。 这是平台的限制，广告插入在iOS上与TVSDK一起使用的方式也是有限的。
* 在这种情况下，在搜索事件上会做出跳过的决定。 但是，由于清单中的广告段持续时间不能准确地表示广告的实际持续时间，因此搜索不准确。 因此，在应用广告策略时，您会看到广告的几个帧。
* RECORDING_ERROR:录制屏幕时出错。
* 它可能会体验到，许可证旋转视频在iOS 11上无法播放，在iOS 9.x和iOS 10.x上播放正常。
* 在VPAID 2.0支持中，如果在AirPlay上播放时播放处于活动状态，将跳过VPAID广告。
* 当最小目标设置为iOS7（或更高版本）时，drmNativeInterface.framework无法正确链接。\
   解决方法：显式指定`libstdc++6`。  dylib库，如下所示：转到“目标” — >“构建阶段” — >“将二进制文件与库链接”并添加`libstdc++.6.dylib`。

* 未插入用于替换API的后滚广告。
* 在广告分时段内进行搜索（不退出）会发布重复广告开始和广告分时段通知
* 设置currentTimeUpdateInterval没有任何效果。\
   注意：在某些iOS版本中，操作系统不会自动加载PSDKLibrary.framework内的资源。 必须手动将PSDKResources.bundle复制到应用程序的包资源：转到“构建阶段”并复制捆绑包资源。
* 无法使用Xcode 8或更低版本构建引用应用程序。 从iOS TVSDK版本1.4.41开始，使用Xcode 9进行编译。

## 有用资源{#helpful-resources}

* 请参阅[Adobe Primetime学习和支持](https://helpx.adobe.com/support/primetime.html)页面上的完整帮助文档。
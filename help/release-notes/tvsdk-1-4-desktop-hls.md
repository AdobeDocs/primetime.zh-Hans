---
title: 用于桌面HLS的TVSDK 1.4发行说明
seo-title: 用于桌面HLS的TVSDK 1.4发行说明
description: 适用于桌面HLS的TVSDK发行说明描述了TVSDK DHLS中的新增功能或更改功能、已解决和已知问题。
seo-description: 适用于桌面HLS的TVSDK发行说明描述了TVSDK DHLS中的新增功能或更改功能、已解决和已知问题。
uuid: 84da27b7-299b-478d-88f5-ef943f0a8321
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: e4437a26-9454-4da1-ae87-0fce664aac3d
translation-type: tm+mt
source-git-commit: a94150abc2afff4af24ee83573e73124f8b3260a

---


# 用于桌面HLS的TVSDK 1.4发行说明 {#tvsdk-for-desktop-hls-release-notes}

适用于桌面HLS的TVSDK发行说明描述了TVSDK DHLS中的新增或更改功能、已解决的和已知的问题。

## 新增功能 {#new-features}

**1.4.31**

* **CRS广告的多CDN支持**

   * 默认情况下，所有转码的资源将托管在Akamai上的Adobe拥有的CDN上。 在最新版本中，Adobe Creative Repackaging Service(CRS)提供了将转码创意内容上传到客户指定的多个CDN的功能。
   * 将新API添加到TVSDK以启用在不使用默认URL时指定最终的CRS创作URL。 请参阅文档，了解如何使用这些新API。

### 先前版本的新增功能 {#new-features-previous}

**1.4.30**

* **计费指标**

为了照顾那些希望只支付其使用费用而不是固定费用（无论实际使用如何）的客户，Adobe会收集使用情况指标并使用这些指标确定向客户收取的费用。

**1.4.24**

* **永久网络连接**

重要说明：您必须至少安装了Adobe Flash Player版本22或更高版本。
永久网络连接创建并存储可重复用于多个请求的网络连接的内部列表，而不是为每个网络请求打开新连接。 永久网络连接应提高效率并减少网络代码的延迟。

在此版本中，Mac上的Apple Safari和Mozilla Firefox不支持此功能。

**1.4.19**

* 对VPAID广告的流完整性支持。
* 通过修复挂起问题，为Firefox 42及更高版本的Flash Player FP 20.0.0.267启用了静音选项卡选项。

**1.4.18**

* Primetime Desktop HLS TVSDK现在支持VPAID 2.0线性SWF创意，以实现丰富的交互式流内广告体验。

**1.4.10**

* **广告回退，广告选择逻辑中的菊花链(Zendesk #3103)** 对于启用回退规则的VAST广告（创意）,TVSDK将MIME类型无效的广告视为空广告并尝试在其位置使用回退广告。 您可以配置回退行为的某些方面。

有关详细信息，请参 [阅VAST和VMAP广告的广告回退](../programming/tvsdk-1.4-for-android/ad-insertion/ad-fallback/android-1.4-ad-fallback.md)。

**1.4.8**

* **更新到版本1.5的视频心率库(VHL)**

   * 能够将视频开始和／或视频／广告／章节开始作为上下文数据发送元数据
   * 网络流量更少——心率平均更小，且更小。

**1.4.7**

* **预置个性化支持**

支持Adobe Indelication Server的预置安装，以自定义客户端的个性化请求以转到其他端点。

**1.4.6**

* **范例AES加密（需要Flash Player版本17.0.0.134）**

现在支持基于样本的AES加密。

**1.4.2**

* **视频心率库(VHL)更新至版本1.4.0.1**

   * 添加了将其他SDK或播放器中的不同分析用例与Adobe Analytics Video Essentials捆绑在一起的功能。
   * 通过删除trackAdBreakStart和trackAdBreakComplete方法，广告跟踪已得到优化。 广告中断从trackAdStart和trackAdComplete方法调用推断出来。
   * 跟踪广告时不再需要播放头属性。

**1.4.0**

* **使用替代内容替换的封锁信号** TVSDK作为1.4 TVSDK更新的一部分，现在还支持针对线性内容的区域封锁进入和返回。 TVSDK现在可以并行处理两个清单文件（主文件和备用文件），以监视断电信号，即使当替代原始编程显示备用程序时也是如此。

* **删除／替换C3广告** “立即”，无需额外的准备工作即可将新广告动态插入从C3窗口发出的视频点播(VOD)资产中。 TVSDK现在提供了一个API，用于删除自定义内容范围和动态插入新广告。 当直播／线性内容在广播期间出现并且立即被拉下来作为点播内容使用时，这一强大的新功能在没有适当时间“清理”资产的情况下也很有用。

## 已解决的问题 {#resolved-issues}

>[!NOTE]
>
>强烈建议所有使用CRS的TVSDK客户至少在iOS、Android和桌面HLS上升级到TVSDK 1.4.32。 此升级将取代现有应用程序实施。 升级后，在代理工具（例如，Charles）中检查CRS创意URL请求，以验证路径中的版本是否反映版本3.1。例如，
>
>`https://adunit.cdn.auditude.com/assets/3p/v3.1/218747/94b/c1b/94bc1b964cc67e115a5a6781c7329b90_ee92607938ffff46b083121f044c2746.m3u8`

**版本1.4.41**

* Zendesk #33777 - DHLS分发内部版本的Localhost令牌SWF已过期。

   更新DHLS上PMP演示的localhost令牌。

### 已解决先前版本中的问题 {#resolved-issues-previous}

**版本1.4.38** (891)

* Zendesk #30731 - TVSDK不在AdBreak中播放多个VPAID广告。

   修复了在AdBreak中播放多个VPAID广告的问题。

* Zendesk #29968 - Double Billboard。

   当ABR切换发生时，视频播放器可以重复一段时间的最后一段。 因此，有时会重复最后一段预卷。 此问题已修复。

**版本1.4.35** (879)

* Zendesk #26058 —— 支持本机VPAID事件

**版本1.4.33** (873)

* Zendesk #21701 —— 发送1401 CRS请求的原始创意URL，而不是标准URL。

   根据CRS后端的要求，已修复请求重新打包的URL进行转码的问题。
* Zendesk #26197 —— 未在所需的显示分辨率中重播变形压缩。

   **注意**:此问题需要Flash Player 24.0.0.194或更高版本。

   宽高比表中缺失的条目用于计算输出宽度的问题已得到修复。

* Zendesk #26840 —— 在IE11 + Windows7上，在第二次尝试后HDCP检测失败。

   **注意**:此问题需要Flash Player 24.0.0.218或更高版本。

   通过修改AdobeCP的主消息队列处理以遍历整个队列，而不是仅仅阻止第一条消息，解决了此问题。

* Zendesk #27460 —— 新的Akamai帐户无法处理POST CDN请求。

   新的CDN帐户无法处理POST CDN请求。 通过更新代码使cdn.auditude.com广告请求成为GET而不是POST，解决了此问题。
* Zendesk #27619 - Windows 10上的Flash崩溃

   **注意**:此问题需要Flash Player 24.0.0.218或更高版本。

   通过防止长URL导致的错误，解决了此问题。

* Zendesk #28218 —— 跟踪事件在从恢复点回退时不会触发

   此问题与Zendesk #26592中的问题相同。 解决了媒体播放器处于VOD流的PREPARED状态时允许搜索操作的问题。

**版本1.4.32** (867)

* Zendesk #26592当回放从恢复点开始时，跟踪事件不会触发

当恢复点不是零时，代码不会更新前置和中断项。 通过添加逻辑在范围开始时间不匹配时刷新代码，解决了此问题。

* Zendesk #27022第二次播放资产时不会播放广告

数组方法的例外情况已得到修复。

**版本1.4.30** (855)

此版本中的TVSDK解决了以下问题：

* Zendesk #22898 —— 缺少字幕不会导致播放失败。

**注意**:此问题需要Flash Player 23.0.0.185或更高版本。

通过允许TVSDK继续播放，即使清单缺少WebVTT M3U8，并只注册一个警告，解决了此问题。

* Zendesk #23454 —— 第三方广告(VPAID)处理不正确

通过根据内容ID（而非时间范围）正确处理VPAID广告，解决了此问题。

* Zendesk #24528 - TVSDK Usage Metrics for Billing。

重要说明：此问题需要Flash Player 23.0.0.185或更高版本。

* Zendesk # 25432在调整播放器大小时出现隐藏式字幕问题。

重要说明：此问题需要Flash Player 23.0.0.185或更高版本。

字幕显示纹理映射代码已被修复，以在播放器调整大小时正确处理坐标。

视频心率库(VHL)已更新至版本1.5.9以解决以下问题：

* Zendesk #23730 —— 比特率度量为空

通过跟踪VideoAnalyticsTracker中的比特率更改解决了此问题。

* 向PTVideoAnalyticsTrackingMetadata添加了一个新的API assetDuration，以更新实时／线性流的资产持续时间。

**版本1.4.28** (848)

* Zendesk #25027 - Auditude在1.4.27桌面版本中不工作

通过添加检查AUDITUDE_METADATA_KEY的代码并使AUDITUDE_METADATA_KEY和ADVERTISING_METADATA_KEY可互换，解决了此问题。

* Zendesk #24428 —— 使用TVSDK播放DRM HLS时经常出现缓冲问题

通过考虑到没有广告设置时，TVSDK可以通过消除设计用于同步广告插入的时间线上的前置广告保持和实时保留保持来加快处理速度，从而解决了此问题。

* Zendesk #24344 —— 禁用WebVTT文件以缩短启动时间。

**注意**:此问题需要Flash Player 23或更高版本。

仅当需要显示字幕时，才加载WebVTT文件可解决此问题。

* Zendesk #24994 —— 从商业休息返回时，关闭的字幕会从播放器中删除

**注意**:此问题需要Flash Player 23或更高版本。

伪EOC代码导致字幕显示消失。 通过强制608字幕代码RU2、RU3和RU4在当前活动窗口中提供正确的可见性，解决了此问题。

**版本1.4.27** (844)

* Zendesk #21554 —— 未为应用程序类型= video/mp4触发TVSDK错误信标

通过启用TVSDK对无效资产格式的正确错误跟踪URL执行ping操作，解决了此问题。

* Zendesk #23402 —— 广告播放不完整

**注意**:此问题需要Flash Player 23或更高版本。

在某些请求上收到404错误后，可能会发生崩溃。 通过确保在处理响应时不关闭连接，已解决此问题。 此解决方案可确保不会将VPAID广告文件计数错误，因此下载时不会释放它们。

* Zendesk #23621 - Retry is failing on 400 and 404

**注意**:此问题需要Flash Player 23或更高版本。

修复了在不同配置文件之间切换时导致DRM元数据损坏的问题。

* Zendesk #23705 - AdSuncitd中断期间冻结视频广告

**注意**:此问题需要Flash Player 23或更高版本。

此问题与Zendesk #23621中的问题相同。

* Zendesk #23905 —— 某些广告中断跳过广告中断

**注意**:此问题需要Flash Player 23或更高版本。

已修复Windows本机网络代码，以确保连接不会关闭其他连接当前使用的句柄。

* 票证#24029 - HLS FER流不播放中间。json文件中的所有中间广告。

通过允许客户端在Opportunity实例上单独设置自定义参数，以便客户端不必覆盖OpportunityGenerator，解决了此问题。

**版本1.4.26** (839)

* Zendesk #18854 —— 更新基于CRS规则的创意选择逻辑
   * 提供了基于CRS规则更新创意选择逻辑的支持

* Zendesk #22725 —— 在桌面的范例应用程序中实现playbackManager.beginPlayback()

   * 通过在从setupVideo()调用方法时删除startPlaybackFromFlashVars末尾的此冗余调用来修复

* Zendesk #22807 - SeekManager空引用例外

   * 通过在与_dispatcher相关的SeekManager内提供必要的空指针保护来修复

* Zendesk #22822 —— 使用TVSDK播放清除的HLS时经常进行缓冲

   * 通过删除adSignalingModeOpportunityGenerator在没有广告的情况下生成的初始机会来修复

* Zendesk #23378 —— 流完整性阻止rules.xml

   * 通过流完整性工作流加载rules.xml文件来修复

**版本1.4.24** (817)

* Zendesk #19851 —— 当播放器适应不同的比特率时，会根据新的比特率跳回几个帧，从而带来尴尬的体验

**注意**:此问题需要Flash Player 22.0.0.175或更高版本。

已解决在下载一小部分段后重置DRM适配器无法正常恢复的问题。

* Zendesk #20784 - Analytics:实时视频过渡的触发内容已完成

通过添加API(trackVideoComplete)来在LINEAR/LIVE视频跟踪会话期间手动触发内容完成，解决了此问题。

更新了以下库：

* Zendesk #21643 - VPAID广告不全部播放

   * 到4.10.0的AdobeMobile库
   * VHL库到1.5.6
   * VHL-Nielsen库到1.6.7

通过在播放VPAID广告时使用零高度视口填充舞台，解决了此问题。

* Zendesk #22110 - Analytics:向心跳跟踪调用添加h:sc:ssl字段

修复了与SSL相关的问题，并将TVSDK中使用的VHL库更新至最新版本。

* Zendesk #22608 —— 视频间歇性地显示黑屏（需要Flash Player 22.0.0.175或更高版本）

在自适应比特率期间，在最大比特率限制下，即使客户端看到位置更新，视频的重新加载也会间歇性地显示黑屏，而客户端的行为就像在播放内容一样。

**版本1.4.23** (809)

* Zendesk #2887 —— 将广告规则逻辑应用于TVSDK时的后置广告跳转问题

**注意**:此问题需要Flash Player 21.0.0.240或更高版本。

在将广告规则逻辑应用于TVSDK时跳过广告后期的问题。

* Zendesk #19863 —— 放弃VPAID媒体文件的广告

如果一个大型内联广告有多个媒体文件，并且VPAID广告是第一个广告，则内联广告不会为实时流播放。 此问题已通过选取其他媒体文件来解决。

* Zendesk #21021 —— 延迟绑定音频导致音频段重复

**注意**:此问题需要Flash Player 21.0.0.240或更高版本。

已修复音频重复问题。

* Zendesk #21125 —— 提早退回实时／线性广告

**注意**:此问题需要Flash Player 21.0.0.240或更高版本。

此版本支持在广告中断播放到完成之前从广告中断返回。 通过自定义清单标签指示提前返回。

* Zendesk # 21369延迟绑定音频导致时间不一致

**注意**:此问题需要Flash Player 21.0.0.240或更高版本。

修复的音频重复问题也修复了此问题。

* Zendesk #21760, 20921 - Seek上的音频视频不同步。

**注意**:此问题需要Flash Player 21.0.0.240或更高版本。

已修复音频重复问题。

* Zendesk #22024 —— 运行TVSDK时出错

已修复引用播放器未播放任何流并且在启动时引发异常的问题。

**版本1.4.22** (791)

* Zendesk #17580 - Primetime运行时错误，代码为3357

**注意**:此问题需要Flash Player 21.0.0.197或更高版本。

修复了在调用storeVoucher()时通过正确初始化deviceID而发生的随机3357错误。

* Zendesk #21334 - TVSDK ad request timeout value for third party ad requests

在此版本中，已添加全局广告请求超时。

**版本1.4.21** (782)

* Zendesk #19580 TVSDK在发送通知之前等待内容解析程序完 `PTTimedMetadataChangedNotification` 成

**注意**:此问题需要Flash Player 21.0.0.182或更高版本。

通过提供设置广告标记和添加自定义机会生成器的功能，在桌面参考播放器中解决了此问题，该生成器显示如何订阅自定义提示以及如何在VOD文件中处理这些提示。

* Zendesk #20806在交换摄像机后，DVR窗口中的未来中间广告不会触发

**注意**:此问题需要Flash Player 21.0.0.182或更高版本。

通过更新应用程序以设置_resource.metadata.setValue(DefaultMetadataKeys.ENABLE_LIVE_PREROLL, &quot;false&quot;)来禁用PIP交换中的预卷广告插入，因此不会生成预卷机会，从而解决了此问题。

引入排序功能来修复导致主内容持续时间为负的无序广告放置。

* Zendesk #20522:无法跳过VPAID 2.0广告

**注意**:此问题需要Flash Player 21.0.0.182或更高版本。

* 通过在广告原谅期间跳过VPAID广告解决了此问题。
* 当adbreak策略设置为跳过时，仍会调度广告和广告分组事件。 播放器状态不一致。

此问题已解决，以便在跳过广告中断时正常工作，而不调度事件。

* Zendesk #20955通过业务机会生成器在customParameters属性中设置键值对

**注意**:此问题需要Flash Player 21.0.0.182或更高版本。

在为广告请求创建广告单元时，Auditude Request会分析AuditudeSettings的自定义参数。

此行为已更改为在请求中包括来自Opportunity对象的自定义参数。 此外，具有不同自定义参数的多个机会不能打包在一个Auditude请求中。

* Zendesk #21227 - m3u8无法一致地播放

**注意**:此问题需要Flash Player 21.0.0.211或更高版本。

通过允许TVSDK忽略包含TVSDK不支持的AC3编解码器的清单（HLS子配置文件），解决了此问题。

**版本1.4.20** (762)

* Zendesk #19181 —— 快速播放技巧可进入实时点锁定流。

**注意**:此问题需要Flash Player 20.0.0.306或更高版本。

* Zendesk #19286 —— 在FER流中来回搜索时，Flash Player崩溃。

**注意**:此问题需要Flash Player 20.0.0.306或更高版本。

在Google Chrome中搜索时发生的偶然挂起通过关闭查询来解决，如果查询需要太长时间才能得到响应，或者套接字正在关闭。

* Zendesk #19305 —— 播放带有A/V不连续的流时遇到的断断续续播放。

**注意**:此问题需要Flash Player 20.0.0.306或更高版本。

此问题已通过报告警告来解决。

* Zendesk # 19359 - Flash Player因#EXT-X-FAXS-CM的位置而崩溃：属性。

当#EXT-X-FAXS-CM标签显示在播放列表中各个比特率或段之前的顶部播放列表中时，此问题已解决。

* Zendesk #19489 - Fast Forward to Live Point storts plugin（实时流）

此问题与Zendesk #19181相同。

* Zendesk #19699 - TVSDK无法在WebVTT子标题轨道之间切换

通过在轨道发生更改时进行播放器转储并重新加载清单，以及纠正影响双字节WebVTT字幕轨道名称的UTF8字符串转换问题，解决了此问题。

**版本1.4.19** (1.4.19.738)

* Zendesk #18234 - Flash Player在CC中使用Unicode字符串播放流时崩溃

此问题需要Flash Player FP 20.0.0.267或更高版本，并通过正确处理Unicode字符串来解决。

* Zendesk #18304 - VPAID广告的流完整性支持

此功能需要Flash Player FP 20.0.0.267或更高版本，并在版本1.4.19中引入了该功能。

* Zendesk #18766 —— 参考播放器无法在CC音轨名称中显示非拉丁文Unicode字符

此功能需要Flash Player FP 20.0.0.267或更高版本，并通过正确处理Unicode字符串来修复该功能。

* Zendesk #18804 - Firefox 42中的播放器崩溃

此问题需要Flash Player FP 20.0.0.235或更高版本，与Zendesk #18723存在相同问题。

* Zendesk #18864 - Flash Player完整插件崩溃

此问题需要Flash Player FP 20.0.0.235或更高版本，并且与Zendesk #18723相同。

* Zendesk #18998 —— 如果音频和视频时间戳不匹配，则会发生不连续段的无休止下载。

通过忽略时间戳之间的间隙并仅播放下载的内容，解决了此问题。

* Zendesk #19093 —— 中间广告只能通过实时和全事件重播(FER)内容观看一次，但是当快速转发或寻找超过广告时，这些广告无法再次观看

在Primetime的默认adPolicy选择器中，如果观看中间广告，则在您完成搜索时，adBreak不会移到搜索位置。 要再次播放广告，在搜索后，应用程序需要覆盖selectAdBreaksToPlay()函数。

* Zendesk #19101 —— 重新绕入未解决的Midroll广告可删除广告投放。

通过允许播放器更新playbackMetrics时间、minimumOpportunityTime和时间轴，解决了此问题。

* Zendesk #19102 - FER和技巧模式的问题

此问题需要Flash Player FP 20.0.0.267或更高版本，并通过正确设置advertisingMetadata.adSignalingMode而解决。

* Zendesk #19175 —— 有时，在首次播放流时，预卷广告不显示。

通过向AuditudeSettings添加新的API adRequestTimeout来解决此问题，以获得广告请求超时。 用户现在可以覆盖默认的10秒广告请求超时。

**版本1.4.18** (1.4.18.722)

* Zendesk #3324 - Primetime广告报告不跟踪VMAP中没有广告媒体的广告中断。

当广告中断为空时，广告中断开始和完整跟踪事件不会被ping。 通过在空广告中断（如VMAP AdBreak）上发送广告中断开始ping以有效的AdSource点，解决了此问题。

**版本1.4.17** (1.4.17.702)

* Zendesk #17168 —— 切换可见性后，字幕在大约10秒内不显示

通过为vtt字幕文件提供EXT-X-MEDIA-TIME标记支持，解决了此问题。

* Zendesk #17983 —— 未能下载清单的任何键导致整个清单播放失败

**注意**:您必须至少拥有Flash Player FP 19.0.0.245或更高版本。

有时播放实时内容时，清单中可能有无效的键（例如，对于封锁期），但其他时间范围可能有有效的键，并且仍将播放。 以前，当清单中列出的密钥无法下载时，整个清单将失败。 现在，清单仅在无法下载所有列出的键时才会失败。 如果某些键有效，但其中某些键无法下载，则内容将播放。 如果我们尝试播放一个需要我们没有的密钥的区段，我们仍会失败。

* Zendesk #18554 - Stream Integrity trimming down the cookies in saces

**注意**:您必须至少拥有Flash Player FP 19.0.0.245或更高版本。

修复了Cookie操作代码中可能截断Cookie值的错误。

**版本1.4.16** (1.4.16.684)

* Zendesk #3732 —— 在Chrome中为流完整性添加代理支持（需要Flash Player FP 19.0.0.207或更高版本）

这是一个增强功能。

* Zendesk #4244 - PTS转换时的流问题

通过检测翻转并管理每个有效负荷类型的不连续性（而非一般），解决了此问题。

* Zendesk #4487 —— 跟踪内容线性渠道

通过在线性流播放会话期间重新初始化视频心率跟踪器，解决了此问题。

* Zendesk #17427 - Adobe Stream Integrity在Chrome上无法通过代理运行(Win7)()

**注意**:分辨率需要Flash Player FP 19.0.0.207或更高版本。

此问题与Zendesk #3732相同。

* Zendesk #17907 - Flash Player 19在pHLS实时流上的延迟

**注意**:分辨率需要Flash Player FP 19.0.0.207或更高版本。

通过处理实时流解决了此问题，在重新加载实时清单时，TS文件的域会发生更改，文件下载两次。

* Zendesk #17931 —— 开始为Slate的HLS内容回放失败

**注意**:分辨率需要Flash Player FP 19.0.0.207或更高版本。

通过在第一个TS文件的前2秒内处理没有音频的流，解决了该问题。

* Zendesk #17934 - Flash 19.0.0.185的实时流故障

**注意**:分辨率需要Flash Player FP 19.0.0.207或更高版本。

通过处理具有段边界上音频和视频帧之间的时间交织的实时流来解决该问题。

* Zendesk #17973 —— 最新版Flash Player 19.0.0.185在中间版期间崩溃

**注意**:分辨率需要Flash Player FP 19.0.0.207或更高版本。

通过中间广告插入处理未混音的音频解决了此问题。 （发生分析器切换，并且在播放中的任何点，内容都会过渡到中间广告或广告播放中间，依此类推。）

* Zendesk #18049 - Flash 19在Firefox 42测试版上崩溃

此问题与Zendesk #17973相同。

**版本1.4.15** (1.4.15.678)

* Zendesk #4377:因为广告策略而跳过广告中断时触发AD_BREAK_BRIPPED事件。

修复是在跳过广告时添加AD_BREAK_BRIPPED。

* Zendesk #4496 —— 流完整性：错误102100，重定向到标记化流。

修复是添加对通过TVSDK设置AVNetworkConfiguration属性useCookieHeaderForAllRequests的支持。

* Zendesk #17179 - Flash Player在加密内容的多个SAP更改上崩溃。

修复了播放某些加密内容时的崩溃问题。

**注意**:该修复需要Flash Player 19.0.0.200或更高版本。

* Zendesk #17499 —— 我们如何不删除观看后的midrol，但从Fer内容中删除preroll

为AdBreakTimelineItem(AdBreakTimelineItem.placementType)添加了一种类型，以便AdPolicySelector可以为前置、中置和后置内容返回不同的策略。

* Zendesk #17665 —— 带宽限制

修复是删除逻辑，在缓冲开始时将目标缓冲区大小更改为初始缓冲区大小。

**版本1.14.14** (1.4.14.771)

* Zendesk #17363 —— 修复参考播放器的自述文件

   * 阐明有关下载和安装playerglobal.swc的说明。
   * 添加有关使用特定Flash Player版本更新项目配置的说明。
   * 更新AdvertisingOverlay项目配置以使用最低播放器版本。
   * 更新引用核心项目配置以使用特定播放器版本11.9

* Zendesk #17471 —— 播放器冻结

部分修复了广告在搜索后从头开始不播放的问题。

* Zendesk #17496 —— 在DVR窗口中返回搜索时，播客器未解析

为每个广告中断提供自定义参数。

**版本1.4.13** (1.4.13.660)

* Zendesk #4037 —— 无可用配置文件错误（需要Flash Player 18.0.0.232或更高版本）

修复查询参数包含“http”时的url解析问题

* Zendesk #4260 - Flash Player 18在IE11中崩溃（需要Flash Player 18.0.0.232或更高版本）

修复了在IE11全屏模式下播放视频时的崩溃问题

* Zendesk #4262 - Adobe Primetime player在Windows 10上崩溃（需要Flash Player 18.0.0.232或更高版本）

修复了在Windows上使用FireFox以全屏模式播放视频时的崩溃问题。

* Zendesk #4279 - HLS TVSDK ad insertion -302 redirect issue on iOS and Desktop

修复了URL由于没有扩展名而无法正确识别其类型的问题

* Zendesk #4306 —— 仅在Win上全屏显示时Flash Player崩溃（需要Flash Player 18.0.0.232或更高版本）

修复了在Windows上以全屏模式播放视频时的崩溃问题。

* Zendesk #4480 —— 缺少ID3标记事件（需要Flash Player 18.0.0.232或更高版本）

**1.4.12 **(1.4.12.656)

* Zendesk #2751 - CSAI和CRS|增强：处理某些媒体文件URL中的动态元素。

更新了Creative Repackaging Service以正确处理带有动态创意URL的广告。

* PTPLAY - 2114 - MP4回放支持。

现在支持基本播放MP4内容，包括播放、暂停和搜索。

以下要求Flash Player 18.0.0.225或更高版本：

* Zendesk #3992 —— 更多TrickPlay速度。

TrickPlay现在接受高于16x的速率：+/- 32、+/-64和+/-128。

* Zendesk #3113 - Flash Player插件崩溃

修复了在Mac Firefox上尝试播放重定向广告时的崩溃问题。

* Zendesk #4037 —— 无可用配置文件错误
* Zendesk #4262 - Adobe Primetime播放器在Windows 10上崩溃

修复了在全屏播放期间在Windows Firefox中崩溃的问题。

**版本1.4.11** (1.4.11.648)

* Zendesk #1869 —— 更改字体大小的问题（需要Flash Player 18.0.0.200）

允许在WebVTT题注代码中使用题注大小。

* Zendesk #3113 - Flash Player插件崩溃（需要Flash Player 18.0.0.200）
* Zendesk #3268 —— 桌面：视频播放器在+- 40/50秒后开始闪烁，在+- 90秒后开始变黑（需要Flash Player 18.0.0.200）

修复舞台视频错误。

* Zendesk #3670 —— 在参考播放器中搜索时VOD中出现INVALID_PARAMETER错误（需要Flash Player 18.0.0.200）

检测到新时段时，ThreadSeek中的InvalidateProfiles。

* Zendesk #3896 - Flash Player崩溃，Chrome上的“流完整性”设置为“打开”（需要Flash Player 18.0.0.200）

修复了辣椒中的本机网络模式崩溃 

* Zendesk #3905 —— 在CDN上托管时，TVSDK播放器不加载

修复了当pageDomain与swf域不同时查找通配符令牌的问题。

**版本1.4.10** (1.4.10.642)

* Zendesk #3249 - TVSDK Web Player在Firefox上使Flash崩溃

修复了Mac上的Firefox偶尔出现的Flash Player崩溃，当在外部监视器上播放的流切换到较高比特率的流时。（需要Flash Player 18.0.0.160）

* Zendesk #3268 —— 桌面：视频播放器在40/50秒 `+-` 后开始闪烁，在90秒后开始 `+-` 黑色

修复了Mac Chrome上流开始闪烁并最终变为黑色的问题。 （需要Flash Player 18.0.0.161）

* Zendesk #3304 —— 未填充VAST 3.0 `[ERRORCODE]` 宏

   * 如果内联广告的创意不佳，则会显示错误代码400。
   * `[ERRORCODE]` 宏将采用URL编码

* Zendesk #3601 —— 增强请求：包装器配套管理

   * TVSDK将向内联显示包含资源（html、iframe或static）的包装器配套。 （如果行中不包含该大小的行）
   * 除非用于显示，否则将忽略资源的包装器。 （不用于跟踪）
   * 只有具有NO资源的包装器伴才可用于跟踪目的。 （包含跟踪的包装器配套）

**版本1.4.9**

* Zendesk #2615 —— 从桌面显示器删除HLS视图的问题

向MediaPlayer添加了clearVideo()方法。 通过从StageVideo对象中清除AVStream来清除显示的视频帧。 仅当视频暂停时才应调用，并且必须在再次调用play()之前调用replaceCurrentResource或replaceCurrentItem。 

* Zendesk #3169 —— 借助Adobe Analytics集成更新参考播放器

参考播放器已通过Adobe Analytics集成进行更新

* Zendesk #3296 —— 桌面HLS TVSDK —— 未播放的VAST第三方广告

HLS格式的MIME类型区分大小写，这不正确，并且已更改，因此不再区分大小写

**版本1.4.8**

* Zendesk #2737 - Desktop Player - Error 106000（需要Flash Player 17.0.0.184）
* Zendesk #3007 —— 更新到Flash Player 17后不显示的前置广告（需要Flash Player 17.0.0.184）
* Zendesk #3085 —— 桌面HLS Player在60秒后引发106000错误（需要Flash Player 17.0.0.184）

**版本1.4.7**

* Zendesk #2760 —— 在TrickPlay模式中忽略的DINSTRUCTION标签（需要Flash Player版本17.0.0.158）
* Zendesk #2760 —— 在TrickPlay模式中忽略的DINSTRUCTION标签（需要Flash Player版本17.0.0.158）

**版本1.4.6**

* Zendesk #2652 —— 桌面HLS的Auditude文档，Clarified Auditude media_id for desktop HLS文档

**版本1.4.5**

* Zendesk #2256 —— 访问主播放列表，更新了PSDK以为主播放列表上订阅的标记调度timedMetadata事件。 （需要Flash Player 17.0.0.134版）
* Zendesk #2417 —— 播放器尝试在播放开始前下载字幕，WebVTT使用错误的段号变量进行段号匹配。 只有区段索引从零开始的媒体才会显示错误。 （需要Flash Player 17.0.0.134版）
* Zendesk #2537 —— 将pepper插件与Chrome一起使用时，Flash Player崩溃（需要Flash Player版本17.0.0.134）
* Zendesk #2547 —— 阿拉伯语字幕：文本应当右对齐（需要Flash Player版本17.0.0.134）

**版本1.4.4**

* Zendesk #1561 —— 续：更 `[Adobe Primetime]` 新：桌面PSDK中基于HLS客户端的PROGRAM-DATE-TIME故障切换支持（需要Flash Player 16.0.0.305版或更高版本）
* Zendesk #2197 —— 跟 `[Ads]` 踪广告错误
* Zendesk #2286 —— 功能请求：提供有关广告加载状态(VPAID)的信息
* Zendesk #2285 —— 功能请求：在指定的超时持续时间后跳过广告
* 错误#3921755 - Flash Player中的OpenSSL库更新至版本1.0.1L（需要Flash Player版本16.0.0.305或更高版本）

**版本1.4.2**

* Zendesk #1303 —— 隐藏式字幕的垂直偏移(需要Flash Player版本16.0.0.235或更高版本，预期发布日期：2014年12月)
* Zendesk #1870 - Closed Caption On &amp; Off(需要Flash Player 16.0.0.235或更高版本，预期发布日期：2014年12月)
* Zendesk #2110 —— 在VPAID广告期间尝试进入全屏后，播放卡住(需要Flash Player版本16.0.0.235或更高版本，预期发布日期：2014年12月)
* Zendesk #2199 —— 在 `[VPAID]` Player搜索过去的广告中断时不响应
* Zendesk #2358 —— 续：章节 `[Analytics]` 数据不正确

**版本1.4.1**

* 更新了封锁期API以与Android和iOS实现保持一致。

**版本1.4.0**

* Zendesk #1024 —— 通过清单从流中删除广告的功能
* Zendesk #1423 - HLS回放失败正在锁定Flash Player（未报告错误）
* Zendesk #1674 - ClosedCaption未显示，当0x03 ETX代码缺失时，708字幕显示正确。

</p>
</details>

## 已知问题 {#known-issues}

* “隐藏式字幕”不能用于仅音频内容，因为字幕系统需要视频才能使用。
没有视频，就没有视口尺寸，没有视口尺寸，就无法显示任何字幕图形。
* 由于Chrome沙箱限制，Google Chrome中的流完整性稍慢。
* 在TVSDK 1.4中，如果禁用autoPlay，则播放器保持空闲至少一分钟时，可能会发生DRM错误。 要解决此问题，请在禁用自动播放但预载资源时，通 `ReferenceCore.as` 过更改以下内容进行修改 `onPlaybackManagerPrepared`:

>if(_playbackManager.autoPlay){
>_playbackManager.play();
>} else {
>_playbackManager.play();
>_playbackManager.pause();
>}

* **版本1.4.13** PTPLAY-8501 —— 当VMAP返回两个直接的MP4非转码广告时，相同的回落广告播放两次。

* **版本1.4.2** 在Flash Player版本16中，在播放器进入空缓冲事件后，用ABR &quot;switching down&quot;逻辑识别了问题。 该问题可防止在播放器进入缓冲状态后在不良带宽环境中降低比特率。 要解决此问题，请让应用程序将 `BufferControlParameters.initialBufferTime` 它设置为与缓冲状态（即，在事件上）期间的临时值相同，然后将它重置回事件上的设置 `BufferControlParameters.playbackBufferTime``BufferEvent.BUFFERING_BEGIN``BufferEvent.BUFFERING_END` 值。 此问题的修复将在Flash Player版本16的下一个修补程序版本中可用。

* **版本1.4.0**

   * PTPLAY-1634 —— 同一“订阅”标签在不同实时窗口中具有不同的时间戳。 移动实时窗口时，每个窗口中的同一标签应具有相同的时间戳。 但是，有时，相同的标记具有不同的时间戳。
   * PTPLAY-28 - MediaPlayer时间轴不包括空分段。
   * 跨域策略文件(crossdomain.xml)是从其他域流化内容的权限所必需的。 [为HTTP流设置crossdomain.xml文件](https://www.adobe.com/devnet/adobe-media-server/articles/cross-domain-xml-for-streaming.html)。
   * 错误#3694203 —— 在DVR流中，从播放的中间卷中搜索到另一个中间卷广告提示可能会导致浏览器冻结
   * 错误#3753725 - selectPolicyForSeekIntoAd在已观看广告中断时不会考虑
   * 错误#3754529 —— 在实时DVR流中回寻时，不会从流中删除预卷广告
   * 错误#3761896 —— 如果在广告播放期间允许搜索，则广告标记将在搜索后重新调整。 解决方法是在搜索期间不使用ITEM_UPDATED回调
   * 错误#3779889 —— 在视频分析中达到特技播放结束时，不会发出完整的呼叫
   * 错误#VA-779 —— 对于“增强的视频分析（包含心跳支持参考实施）”，不发送比特率更改事件心跳——在范例应用程序中不实现技巧播放。

## 实用资源 {#helpful-resources}

* 请参阅 [Adobe Primetime学习和支持页面上的完整帮助文档](https://helpx.adobe.com/support/primetime.html) 。

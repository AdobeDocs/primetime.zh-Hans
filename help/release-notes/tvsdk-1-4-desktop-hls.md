---
title: 桌面HLS的TVSDK 1.4发行说明
description: 桌面HLS的TVSDK发行说明描述了TVSDK DHLS中的新增或更改内容、已解决和已知问题。
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '5196'
ht-degree: 0%

---


# 桌面HLS的TVSDK 1.4发行说明{#tvsdk-for-desktop-hls-release-notes}

桌面HLS的TVSDK发行说明描述了TVSDK DHLS中的新增或更改内容、已解决和已知问题。

## 新增功能{#new-features}

**1.4.31**

* **CRS广告的多CDN支持**

   * 默认情况下，所有转码资源将托管在Akamai上的Adobe拥有的CDN上。 借助最新版本，Adobe Creative Repackaging Service(CRS)能够将转码创意内容上传到客户指定的多个CDN。
   * 新的API添加到TVSDK以启用在不使用默认URL时指定最终的CRS创作URL。 请参阅文档，了解如何使用这些新API。

### 先前版本{#new-features-previous}中的新增功能

**1.4.30**

* **账单量度**

为了照顾那些只想为所用内容而非固定费用付费（无论实际用途如何）的客户，Adobe会收集使用量度并使用这些量度来确定向客户收取多少费用。

**1.4.24**

* **永久网络连接**

重要说明：必须至少安装Adobe Flash Player版本22或更高版本。
永久网络连接创建并存储可对多个请求重用的网络连接的内部列表，而不是为每个网络请求打开新连接。 持久网络连接应提高效率并减少网络代码的延迟。

在此版本中，Mac上的Apple Safari和Mozilla Firefox不支持此功能。

**1.4.19**

* 支持VPAID广告的流完整性。
* 通过修复挂起问题，在适用于Firefox 42及更高版本的Flash播放器FP 20.0.0.267中启用了静音选项卡选项。

**1.4.18**

* Primetime桌面HLS TVSDK现在支持VPAID 2.0线性SWF创意，以实现丰富的交互式流内广告体验。

**1.4.10**

* **广告回退，广告选择逻辑中的菊花链(Zendesk #3103)** 对于启用回退规则的VAST广告（创意），TVSDK将MIME类型无效的广告视为空广告并尝试在其位置使用回退广告。您可以配置回退行为的某些方面。

有关详细信息，请参阅[VAST和VMAP广告的广告回退](../programming/tvsdk-1.4-for-android/ad-insertion/ad-fallback/android-1.4-ad-fallback.md)。

**1.4.8**

* **已更新至版本1.5的视频心率库(VHL)**

   * 能够将带有视频开始和/或视频/广告/章节开始的元数据作为上下文数据发送
   * 网络流量更少 — 心率平均更少，且更小。

**1.4.7**

* **预置个性化支持**

支持在事先安装Adobe Indivialization Server以自定义客户端的个性化请求以转到其他端点。

**1.4.6**

* **示例AES加密(需要Flash Player版本17.0.0.134)**

现在支持基于样本的AES加密。

**1.4.2**

* **视频心率库(VHL)更新至版本1.4.0.1**

   * 添加了将来自其他SDK或播放器的不同分析用例与Adobe Analytics Video Essentials捆绑在一起的功能。
   * 已通过删除trackAdBreakStart和trackAdBreakComplete方法优化了广告跟踪。 广告中断从trackAdStart和trackAdComplete方法调用推断出来。
   * 跟踪广告时不再需要playhead属性。

**1.4.0**

* **使用替代内容替** 换的封锁信号作为1.4 TVSDK更新的一部分，TVSDK现在还支持针对线性内容的区域封锁进入和返回。TVSDK现在可以并行处理两个清单文件，主文件和备用文件，以监视封锁信号，即使在显示替代原始编程的替代编程时也是如此。

* **删除/替换C3** 广告现在，无需进行任何额外的准备工作即可将新广告动态插入从C3窗口发出的视频点播(VOD)资产中。TVSDK现在提供一个API，用于删除自定义内容范围和动态插入新广告。 当实时/线性内容在广播期间播放时，并且会立即作为点播内容被拉下来使用，而无需适当时间“清理”资源时，此强大的新功能也非常有用。

## 已解决问题{#resolved-issues}

>[!NOTE]
>
>强烈建议所有使用CRS的TVSDK客户至少在iOS、Android和桌面HLS上升级到TVSDK 1.4.32。 此升级将取代现有应用程序实施。 升级后，在代理工具（例如，Charles）中检查CRS创意URL请求，以验证路径中的版本是否反映版本3.1。例如，
>
>`https://adunit.cdn.auditude.com/assets/3p/v3.1/218747/94b/c1b/94bc1b964cc67e115a5a6781c7329b90_ee92607938ffff46b083121f044c2746.m3u8`

**版本1.4.41**

* Zendesk #33777 - DHLS分发内部版本的Localhost令牌SWF已过期。

   正在更新DHLS上PMP演示的localhost令牌。

### 解决了以前版本{#resolved-issues-previous}中的问题

**版本1.4.38** (891)

* Zendesk #30731 - TVSDK不在AdBreak中播放多个VPAID广告。

   修复了在AdBreak中播放多个VPAID广告的问题。

* Zendesk #29968 - 多次 Billboard。

   当ABR切换发生时，视频播放器可以重复一段时间的最后一段。 因此，有时会重复最后一段预卷。 此问题已解决。

**版本1.4.35** (879)

* Zendesk #26058 — 支持本机VPAID事件

**版本1.4.33** (873)

* Zendesk #21701 — 发送1401 CRS请求的原始创意URL，而不是标准URL。

   已根据CRS后端的要求修复了要求重新打包的URL进行转码的问题。
* Zendesk #26197 — 变形压缩未在所需的显示分辨率中重播。

   **注意**:此问题需要Flash player 24.0.0.194或更高版本。

   宽高比表中缺少条目用于计算输出宽度的问题已得到修复。

* Zendesk #26840 - HDCP检测在第二次尝试后在IE11 + Windows7上失败。

   **注意**:此问题需要Flash player 24.0.0.218或更高版本。

   通过修改AdobeCP的主消息队列处理以对整个队列进行迭代而不是仅阻止第一条消息，解决了此问题。

* Zendesk #27460 — 新的Akamai帐户无法处理POST CDN请求。

   新的CDN帐户无法处理POST CDN请求。 通过更新代码使cdn.auditude.com广告请求成为GET而非POST，解决了此问题。
* Zendesk #27619 - Windows 10上的Flash崩溃

   **注意**:此问题需要Flash player 24.0.0.218或更高版本。

   通过防止长URL导致的错误，解决了此问题。

* Zendesk #28218 — 跟踪事件不会触发，而从恢复点进行回放

   此问题与Zendesk #26592中的问题相同。 解决了媒体播放器处于VOD流的PREPARED状态时允许执行搜索操作的问题。

**版本1.4.32** (867)

* 当回放事件从恢复点开始时，Zendesk #26592跟踪不会触发

当恢复点不为零时，代码未更新前滚和中断项。 通过添加逻辑在范围开始时间不匹配时刷新代码，解决了此问题。

* Zendesk #27022 Ads is not be played the saste is the second time asset is played

数组方法的例外已得到修复。

**版本1.4.30** (855)

TVSDK在此版本中已解决以下问题：

* Zendesk #22898 — 缺少字幕不会导致播放失败。

**注意**:此问题需要Flash player 23.0.0.185或更高版本。

通过允许TVSDK继续播放，即使清单缺少WebVTT M3U8，并且只注册警告，解决了此问题。

* Zendesk #23454 — 第三方广告(VPAID)处理不正确

通过根据内容ID（而非时间范围）正确处理VPAID广告，解决了此问题。

* Zendesk #24528 - TVSDK帐单使用量度。

重要说明：此问题需要Flash player 23.0.0.185或更高版本。

* Zendesk # 25432在调整播放器大小时出现“隐藏字幕”问题。

重要说明：此问题需要Flash player 23.0.0.185或更高版本。

题注显示纹理映射代码已被固定，以在播放器调整大小期间正确处理坐标。

视频心率库(VHL)已更新为版本1.5.9，以解决以下问题：

* Zendesk #23730 — 比特率量度为空

通过跟踪VideoAnalyticsTracker中的比特率更改解决了此问题。

* 向PTVideoAnalyticsTrackingMetadata添加了一个新APIassetDuration，以更新实时/线性流的资产持续时间。

**版本1.4.28** (848)

* Zendesk #25027 - Auditude在1.4.27桌面版本中不起作用

通过添加检查AUDITUDE_METADATA_KEY的代码并使AUDITUDE_METADATA_KEY和ADVERTISING_METADATA_KEY可互换，解决了此问题。

* Zendesk #24428 — 使用TVSDK播放DRM HLS时经常出现缓冲问题

解决此问题的方法是：考虑到没有广告设置时，TVSDK可以通过消除设计用于同步广告插入的时间轴上的滚动广告保持和实时保留保持来加快处理。

* Zendesk #24344 — 禁用WebVTT文件以缩短开始设置时间。

**注意**:此问题需要Flash player 23或更高版本。

只有在需要显示字幕时才加载WebVTT文件，解决了此问题。

* Zendesk #24994 — 从商业休息返回时，关闭的字幕会从播放器上删除

**注意**:此问题需要Flash player 23或更高版本。

虚假的EOC代码导致字幕显示消失。 通过强制608字幕代码RU2、RU3和RU4在当前活动窗口中提供正确的可见性，解决了此问题。

**版本1.4.27** (844)

* Zendesk #21554 — 未为application-type = video/mp4触发TVSDK错误信标

通过启用TVSDK对无效资产格式的正确错误跟踪URL执行ping操作，解决了此问题。

* Zendesk #23402 — 广告播放不完整

**注意**:此问题需要Flash player 23或更高版本。

在收到某些请求的404错误后，可能会发生崩溃。 通过确保在处理响应时不关闭连接，已解决此问题。 该解决方案可确保VPAID广告文件不会被错误计数，因此在下载时不会释放它们。

* Zendesk #23621 — 重试在400和404时失败

**注意**:此问题需要Flash player 23或更高版本。

修复了在不同用户档案之间切换时导致DRM元数据损坏的问题。

* Zendesk #23705 — 在AdSuncted中断期间冻结视频广告

**注意**:此问题需要Flash player 23或更高版本。

此问题与Zendesk #23621中的问题相同。

* Zendesk #23905 — 某些广告中断跳过广告中断

**注意**:此问题需要Flash player 23或更高版本。

Windows本机网络代码已修复，以确保连接不会关闭其他连接当前正在使用的句柄。

* 票#24029 - HLS FER流不会播放中间卷.json文件中的所有中间卷广告。

通过允许客户端在Opportunity实例上单独设置自定义参数，以便客户端不必覆盖OpportunityGenerator，解决了此问题。

**版本1.4.26** (839)

* Zendesk #18854 — 更新基于CRS规则的创意选择逻辑
   * 提供了基于CRS规则更新创意选择逻辑的支持

* Zendesk #22725 - PlaybackManager.beginPlayback()在桌面应用程序示例中的实现

   * 通过在startPlaybackFromFlashVars末尾删除此冗余调用(从setupVideo()调用该方法)来修复

* Zendesk #22807 - SeekManager空引用异常

   * 通过在与_dispatcher相关的SeekManager内提供必要的空指针保护来修复

* Zendesk #22822 — 使用TVSDK播放清除的HLS时经常缓冲

   * 通过删除由adSigningModeOpportunityGenerator生成的初始机会（如果没有广告）来修复

* Zendesk #23378 — 流完整性阻止rules.xml

   * 通过流完整性工作流加载rules.xml文件来修复

**版本1.4.24** (817)

* Zendesk #19851 — 当播放器调整为不同的比特率时，会根据新的比特率跳回几帧，这会带来尴尬的体验

**注意**:此问题需要Flash player 22.0.0.175或更高版本。

已解决在下载一小部分段后重置DRM适配器无法正确恢复的问题。

* Zendesk #20784 - Analytics:为实时视频过渡完成触发内容

通过添加API(trackVideoComplete)来在LINEAR/LIVE视频跟踪会话期间手动触发内容完成，解决了此问题。

更新了以下库：

* Zendesk #21643 - VPAID广告不全部播放

   * AdobeMobile库到4.10.0
   * VHL库到1.5.6
   * VHL-Nielsen图书馆至1.6.7

通过在播放VPAID广告时使用零高度视口填充舞台，解决了此问题。

* Zendesk #22110 - Analytics:向心率跟踪调用添加h:sc:ssl字段

修复了与SSL相关的问题，TVSDK中使用的VHL库已更新为最新版本。

* Zendesk #22608 — 视频间歇性地显示黑屏(需要Flash Player 22.0.0.175或更高版本)

在自适应比特率期间，如果比特率限制为最大，则视频的重新加载会间歇性地显示黑屏，即使客户端看到位置更新，而且客户端的行为就像在播放内容一样。

**版本1.4.23** (809)

* Zendesk #2887 — 将广告规则逻辑应用于TVSDK时的滚动广告跳过问题

**注意**:此问题需要Flash player 21.0.0.240或更高版本。

在将广告规则逻辑应用到TVSDK时，会跳过广告发布后的问题。

* Zendesk #19863 — 放弃VPAID媒体文件的广告

如果一个大型内联广告包含多个媒体文件，其中VPAID广告是第一个广告，则内联广告不会为实时流播放。 此问题已通过选取其他媒体文件而解决。

* Zendesk #21021 — 延迟绑定音频导致音频段重复

**注意**:此问题需要Flash player 21.0.0.240或更高版本。

已修复音频重复问题。

* Zendesk #21125 — 提前退回实时/线性广告

**注意**:此问题需要Flash player 21.0.0.240或更高版本。

此版本支持在播放到完成之前从广告中断返回。 通过自定义清单标记指示提前返回。

* Zendesk # 21369延迟绑定音频会导致时间不一致

**注意**:此问题需要Flash player 21.0.0.240或更高版本。

已修复的音频重复问题也修复了此问题。

* Zendesk #21760, 20921 - Seek上的音频视频不同步。

**注意**:此问题需要Flash player 21.0.0.240或更高版本。

已修复音频重复问题。

* Zendesk #22024 — 运行TVSDK时出错

已修复引用播放器未播放任何流且正在向开始上抛出异常的问题。

**版本1.4.22** (791)

* Zendesk #17580 - Primetime运行时错误，代码为3357

**注意**:此问题需要Flash player 21.0.0.197或更高版本。

修复了在调用storeVoucher()时正确初始化deviceID而发生的随机3357错误。

* Zendesk #21334 - TVSDK广告请求对第三方广告请求的超时值

在此版本中，已添加全局广告请求超时。

**版本1.4.21** (782)

* Zendesk #19580 TVSDK在发送`PTTimedMetadataChangedNotification`通知之前等待内容解析程序完成

**注意**:此问题需要Flash player 21.0.0.182或更高版本。

通过提供设置Ad标签和添加自定义机会生成器的功能，解决了桌面参考播放器中的此问题，该生成器显示如何订阅自定义提示以及如何在VOD文件中处理这些提示。

* Zendesk #20806交换摄像机后，DVR窗口中的未来中间广告不会触发

**注意**:此问题需要Flash player 21.0.0.182或更高版本。

通过更新应用程序以设置_resource.metadata.setValue(DefaultMetadataKeys.ENABLE_LIVE_PREROLL， &quot;false&quot;)来禁用PIP交换中的预卷广告插入，因此不生成预卷机会，解决了此问题。

引入分类功能来修复导致主内容持续时间为负的无序广告投放。

* 森德克#20522:无法跳过VPAID 2.0广告

**注意**:此问题需要Flash player 21.0.0.182或更高版本。

* 通过在广告原谅期间跳过VPAID广告解决了此问题。
* 当adbreak策略设置为跳过时，仍会调度广告和广告分段事件。 播放器状态不一致。

已解决此问题，以在跳过广告中断时正确行为，而不是分派事件。

* Zendesk #20955通过机会生成器在customParameters属性中设置键值对

**注意**:此问题需要Flash player 21.0.0.182或更高版本。

在为广告请求创建广告单元时，Auditude Request会解析AuditudeSettings的自定义参数。

此行为已更改为在请求中包含来自Opportunity对象的自定义参数。 此外，不能在一个Auditude请求中打包具有不同自定义参数的多个机会。

* Zendesk #21227 - m3u8无法一致地播放

**注意**:此问题需要Flash player 21.0.0.211或更高版本。

通过允许TVSDK忽略包含TVSDK不支持（环绕）的AC3编解码器的清单(HLS子用户档案)，解决了此问题。

**版本1.4.20** (762)

* Zendesk #19181 — 快速实现特技播放以锁定流。

**注意**:此问题需要Flash player 20.0.0.306或更高版本。

* Zendesk #19286 — 在FER流中来回搜索时发生Flash Player崩溃。

**注意**:此问题需要Flash player 20.0.0.306或更高版本。

在Google Chrome中搜索时发生的偶发挂起已通过关闭查询来解决，如果查询需要太长时间才能得到响应，或者套接字正在关闭。

* Zendesk #19305 — 在播放不连续的音频/视频流时遇到不连贯的播放。

**注意**:此问题需要Flash player 20.0.0.306或更高版本。

此问题已通过报告警告解决。

* Zendesk # 19359 -Flash Player因#EXT-X-FAXS-CM的位置而崩溃：属性。

当#EXT-X-FAXS-CM标签出现在播放列表中各个比特率或段之前的顶部播放列表时，此问题已解决。

* Zendesk #19489 - Fast Forward to Live Point Stolls plugin（实时流）

此问题与Zendesk #19181相同。

* Zendesk #19699 - TVSDK无法在WebVTT子标题轨道之间切换

通过在轨道发生更改时进行播放器转储并重新加载清单，并通过更正影响多次字节WebVTT题注轨道名称的UTF8字符串转换问题，解决了此问题。

**版本1.4.19** (1.4.19.738)

* Zendesk #18234 - CC中使用Unicode字符串回放流的Flash Player崩溃

此问题需要Flash Player FP 20.0.0.267或更高版本，并通过正确处理Unicode字符串解决。

* Zendesk #18304 — 针对VPAID广告的流完整性支持

此功能需要Flash Player FP 20.0.0.267或更高版本，已在1.4.19版中引入。

* Zendesk #18766 - Reference Player无法在CC轨道名称中显示非拉丁Unicode字符

此功能需要Flash Player FP 20.0.0.267或更高版本，并通过正确处理Unicode字符串来修复。

* Zendesk #18804 - Firefox 42中的播放器崩溃

此问题需要Flash Player FP 20.0.0.235或更高版本，与Zendesk #18723相同。

* Zendesk #18864 - Flash Player full plugin crash

此问题需要Flash Player FP 20.0.0.235或更高版本，且与Zendesk #18723相同。

* Zendesk #18998 — 如果音频和视频时间戳不匹配，则会在中断时进行无休止的区段下载。

通过忽略时间戳之间的间隙并仅播放下载的内容，解决了此问题。

* Zendesk #19093 — 只能通过实时和全事件重播(FER)内容观看一次中间版广告，但在快速转发或寻找超过广告时无法再观看这些广告

在Primetime的默认adPolicy选择器中，如果观看了中间广告，则在您完成搜索后，adBreak不会移到搜索位置。 要再次播放广告，在搜索后，应用程序需要覆盖selectAdBreaksToPlay()函数。

* Zendesk #19101 — 将广告重排到未解决的Midroll广告中可删除广告位置。

通过允许播放器更新playbackMetrics时间、minimumOpportunityTime和时间轴，解决了此问题。

* Zendesk #19102 - FER和技巧模式的问题

此问题需要Flash Player FP 20.0.0.267或更高版本，并通过正确设置advertisingMetadata.adSigningMode解决。

* Zendesk #19175 — 有时，在首次播放流时，预放广告不会显示。

通过向AuditudeSettings中添加新的API adRequestTimeout来解决此问题，以获得广告请求超时。 用户现在可以覆盖默认的10秒广告请求超时。

**版本1.4.18** (1.4.18.722)

* Zendesk #3324 - Primetime广告报告在VMAP中没有广告媒体时不会跟踪广告中断。

当广告中断为空时，广告中断开始和完整跟踪事件未被ping通。 通过在空广告中断（如VMAP AdBreak）上发送广告中断开始ping，用有效的AdSource点解决了此问题。

**版本1.4.17** (1.4.17.702)

* Zendesk #17168 — 切换可见性后，字幕在大约10秒内不显示

通过为vtt题注文件提供EXT-X-MEDIA-TIME标记支持，解决了此问题。

* Zendesk #17983 — 无法下载清单的任何键，导致整个清单播放失败

**注意**:您必须至少具有Flash Player FP 19.0.0.245或更高版本。

有时播放活动内容时，清单中可能有无效的键（例如，对于封锁期），但其他时间范围可能有有效的键并且仍将播放。 以前，当清单中列出的密钥无法下载时，整个清单将失败。 现在，仅当无法下载所有列出的键时，清单才会失败。 如果某些键有效，但其中某些键无法下载，则内容将播放。 如果我们尝试播放一个需要我们没有的密钥的区段，我们仍会失败。

* Zendesk #18554 - Stream Integrity在某些情况下修剪Cookie

**注意**:您必须至少具有Flash Player FP 19.0.0.245或更高版本。

修复了Cookie操作代码中可能截断Cookie值的错误。

**版本1.4.16** (1.4.16.684)

* Zendesk #3732 — 在Chrome中为流完整性添加代理支持(需要Flash Player FP 19.0.0.207或更高版本)

这是一种增强。

* Zendesk #4244 - PTS滚动时的流问题

通过检测滚动和管理每个有效负荷类型的中断（而非一般）来解决此问题。

* Zendesk #4487 — 跟踪内容的线性渠道

通过在线性流播放会话期间重新初始化视频心率跟踪器来解决此问题。

* Zendesk #17427 -Adobe流完整性无法通过Chrome上的代理运行(Win7)()

**注意**:该决议要求Flash Player FP 19.0.0.207或更高版本。

此问题与Zendesk #3732相同。

* Zendesk #17907 - pHLS实时流上的滞后Flash Player19

**注意**:该决议要求Flash Player FP 19.0.0.207或更高版本。

通过处理实时流解决了此问题，在实时流中，重新加载实时清单时TS文件的域会发生更改，文件下载两次。

* Zendesk #17931 — 开始时带石板的HLS内容无法回放

**注意**:该决议要求Flash Player FP 19.0.0.207或更高版本。

通过在第一个TS文件的前2秒处理没有音频的流，解决了该问题。

* Zendesk #17934 — 带Flash 19.0.0.185的实时流故障

**注意**:该决议要求Flash Player FP 19.0.0.207或更高版本。

通过处理具有段边界上音频和视频帧之间时间交织的实时流来解决该问题。

* Zendesk #17973 — 最新Flash Player19.0.0.185在中间版期间崩溃

**注意**:该决议要求Flash Player FP 19.0.0.207或更高版本。

通过使用中间滚动广告插入处理未混音音频解决了此问题。 (分析器切换发生，并且在播放的任何点，内容过渡到中间广告，或在广告播放的中间，等等。)

* Zendesk #18049 - Firefox 42测试版Flash19崩溃

此问题与Zendesk #17973相同。

**版本1.4.15** (1.4.15.678)

* 森德克#4377:由于广告策略，在跳过广告中断时触发AD_BREAK_BRIPPED事件。

修复是在跳过广告时添加AD_BREAK_BRIPPED。

* Zendesk #4496 — 流完整性：重定向到标记流时出错102100。

修复是添加对通过TVSDK设置AVNetworkConfiguration属性useCookieHeaderForAllRequests的支持。

* Zendesk #17179 -Flash播放器在加密内容的多个SAP更改上崩溃。

修复了播放某些加密内容时发生的崩溃。

**注意**:该修复需要Flash Player19.0.0.200或更高版本。

* Zendesk #17499 — 如何不删除观看后的蒙版，而从蒙版内容中删除预卷

为AdBreakTimelineItem(AdBreakTimelineItem.placementType)添加了一个类型，以便AdPolicySelector可以为前置、中置和后置内容返回不同的策略。

* Zendesk #17665 — 带宽限制

修复是删除逻辑，以在缓冲开始时将目标缓冲区大小更改为初始缓冲区大小。

**版本1.14.14** (1.4.14.771)

* Zendesk #17363 — 修复参考播放器的自述文件

   * 阐明有关下载和安装playerglobal.swc的说明。
   * 添加有关使用特定flash player版本更新项目配置的说明。
   * 更新AdvertisingOverlay项目配置以使用最低播放器版本。
   * 更新ReferenceCore项目配置以使用特定播放器版本11.9

* Zendesk #17471 — 播放器冻结

部分修复了广告在搜索后从头开始不播放的问题。

* Zendesk #17496 — 在DVR窗口中搜索时，播客器未解决

为每个广告中断提供自定义参数。

**版本1.4.13** (1.4.13.660)

* Zendesk #4037 — 无可用用户档案错误(需要Flash Player 18.0.0.232或更高版本)

修复了查询参数包含“http”时的url解析问题

* Zendesk #4260 - Flash Player 18在IE11中崩溃(需要Flash Player 18.0.0.232或更高版本)

修复了在IE11全屏模式下播放视频时的崩溃

* Zendesk #4262 - Adobe Primetime player在windows 10上崩溃(需要Flash Player 18.0.0.232或更高版本)

修复了在Windows上使用FireFox以全屏模式播放视频时的崩溃问题。

* Zendesk #4279 - HLS TVSDK广告插入 — iOS和桌面上的重定向问题

修复了URL未正确识别其类型，因为其没有扩展

* Zendesk #4306 — 仅在Win上全屏显示时Flash Player崩溃(需要Flash Player 18.0.0.232或更高版本)

修复了在Windows上以全屏模式播放视频时的崩溃问题。

* Zendesk #4480 — 缺少ID3标记事件(需要Flash Player 18.0.0.232或更高版本)

**1.4.12 **(1.4.12.656)

* Zendesk #2751 - CSAI和CRS |增强：处理特定媒体文件URL中的动态元素。

更新了Creative重新打包服务，以通过动态创意URL正确处理广告。

* PTPLAY - 2114 - MP4回放支持。

现在支持播放、暂停和搜索等MP4内容的基本播放。

以下要求Flash Player18.0.0.225或更高版本：

* Zendesk #3992 — 额外的TrickPlay速度。

TrickPlay现在接受高于16倍的费率：+/- 32、+/-64和+/-128。

* Zendesk #3113 - Flash Player Plugin Block

修复了在Mac Firefox上尝试播放重定向广告时的崩溃问题。

* Zendesk #4037 — 无可用用户档案错误
* Zendesk #4262 - Adobe Primetime player在Windows 10上崩溃

修复了在全屏播放期间在Windows Firefox中崩溃的问题。

**版本1.4.11** (1.4.11.648)

* Zendesk #1869 - Issue Changing Font Size(需要Flash Player 18.0.0.200)

允许在WebVTT题注代码中使用题注大小。

* Zendesk #3113 - Flash Player Plugin Brocking(需要Flash Player 18.0.0.200)
* Zendesk #3268 — 桌面：视频播放器开始在+- 40/50秒后闪烁，开始在+- 90秒后变黑(需要Flash Player18.0.0.200)

修复舞台视频错误。

* Zendesk #3670 — 在参考播放器中进行搜索时VOD中出现INVALID_PARAMETER错误(需要Flash Player18.0.0.200)

检测到新时段时，ThreadSeek中的InvalidateProfiles。

* Zendesk #3896 -Flash Player崩溃，Chrome上的“流完整性”设置为“打开”(需要Flash Player 18.0.0.200)

修复了在Pepper中的本机网络模式下发生崩溃

* Zendesk #3905 - TVSDK播放器在CDN上托管时不加载

修复了当pageDomain与swf域不同时查找通配符标记的问题。

**版本1.4.10** (1.4.10.642)

* Zendesk #3249 - TVSDK Web Player在Firefox上崩溃Flash

修复了在Mac上，当在外部显示器上播放的流切换到较高比特率的流时，Firefox偶尔会发生Flash Player崩溃。(需要Flash Player 18.0.0.160)

* Zendesk #3268 — 桌面：视频播放器开始在`+-` 40/50秒后闪烁，开始在`+-` 90秒后变黑

修复了Mac Chrome上流开始闪烁并最终变黑的问题。 (需要Flash Player 18.0.0.161)

* Zendesk #3304 — 未填充VAST 3.0 `[ERRORCODE]`宏

   * 如果内联广告有错误的创意，则将显示错误代码400。
   * `[ERRORCODE]` 宏将进行URL编码

* Zendesk #3601 — 增强请求：包装器配套管理

   * TVSDK将向行中显示包含资源（html、iframe或static）的包装器伴侣。 （如果行中不包含该大小的行）
   * 除非用于显示，否则将忽略资源的包装器。 （不用于跟踪）
   * 只有具有NO资源的包装器伴侣才可用于跟踪。 (仅包含跟踪的包装器配套

**版本1.4.9**

* Zendesk #2615 — 从桌面显示中删除HLS视图时出现问题

向MediaPlayer添加了clearVideo()方法。 通过从StageVideo对象中清除AVStream来清除显示的视频帧。 仅当视频已暂停时才应调用，并且必须在再次调用play()之前调用replaceCurrentResource或replaceCurrentItem。

* Zendesk #3169 — 使用Adobe Analytics集成更新参考播放器

参考播放器已通过Adobe Analytics集成更新

* Zendesk #3296 — 桌面HLS TVSDK — 未播放的VAST第三方广告

HLS格式的mime类型区分大小写，这不正确，已更改，因此不再区分大小写

**版本1.4.8**

* Zendesk #2737 - Desktop Player - Error 106000(需要Flash Player 17.0.0.184)
* Zendesk #3007 — 更新到Flash Player 17后不显示预置广告(需要Flash Player 17.0.0.184)
* Zendesk #3085 — 桌面HLS播放器在60秒后引发106000错误(需要Flash Player17.0.0.184)

**版本1.4.7**

* Zendesk #2760 — 在TrickPlay模式期间忽略的DINSCRIPUTION标签(需要Flash Player版本17.0.0.158)
* Zendesk #2760 — 在TrickPlay模式期间忽略的DINSCRIPUTION标签(需要Flash Player版本17.0.0.158)

**版本1.4.6**

* Zendesk #2652 — 桌面HLS的Auditude文档，桌面HLS文档的Clarified Auditude media_id

**版本1.4.5**

* Zendesk #2256 — 访问主控播放列表，更新了PSDK以为主控播放列表上的订阅标记调度timedMetadata事件。 (需要Flash Player 17.0.0.134版)
* Zendesk #2417 - Player尝试在播放开始前下载字幕，WebVTT使用错误的区段编号变量进行区段编号匹配。 只有从零开始的细分索引的媒体才会显示错误。 (需要Flash Player 17.0.0.134版)
* Zendesk #2537 — 将pepper插件与Chrome一起使用时，Flash播放器崩溃(需要Flash Player版本17.0.0.134)
* Zendesk #2547 — 阿拉伯语字幕：文本应右对齐(需要Flash Player版本17.0.0.134)

**版本1.4.4**

* Zendesk #1561 - Re:`[Adobe Primetime]`更新：桌面PSDK中基于HLS客户端的项目-DATE-TIME故障转移支持(需要Flash Player版本16.0.0.305或更高版本)
* Zendesk #2197 - `[Ads]`跟踪广告错误
* Zendesk #2286 — 功能要求：提供有关广告加载状态(VPAID)的信息
* Zendesk #2285 — 功能要求：在指定的超时持续时间后跳过广告
* 错误#3921755 - OpenSSL库在Flash Player中更新到版本1.0.1L(需要Flash Player版本16.0.0.305或更高版本)

**版本1.4.2**

* Zendesk #1303 — 隐藏字幕的垂直偏移(需要Flash Player版本16.0.0.235或更高版本，预期发布日期：2014年12月)
* Zendesk #1870 - Closed Caption Tonn &amp; Off(需要Flash Player版本16.0.0.235或更高版本，预期发布日期：2014年12月)
* Zendesk #2110 — 在VPAID广告期间尝试进入全屏后，播放会卡住(需要Flash Player版本16.0.0.235或更高版本，预期发布日期：2014年12月)
* Zendesk #2199 - `[VPAID]`播放器在搜索过去的广告中断时没有响应
* Zendesk #2358 - Re:`[Analytics]`章节数据不正确

**版本1.4.1**

* 更新了封锁期API以与Android和iOS实现一致。

**版本1.4.0**

* Zendesk #1024 — 通过清单从流中删除广告的功能
* Zendesk #1423 - HLS播放失败正在锁定Flash Player（未报告错误）
* Zendesk #1674 - ClosedCaption未显示，当0x03 ETX代码缺失时，正确显示708字幕。

## 已知问题{#known-issues}

* “隐藏式字幕”不能用于仅音频内容，因为字幕系统需要视频才能使用。
没有视频，就没有视口尺寸，没有视口尺寸，就无法显示字幕的任何图形。
* 由于Chrome沙箱限制，Google Chrome中的流完整性稍慢。
* 在TVSDK 1.4中，如果禁用自动播放，则当播放器保持空闲至少一分钟时，可能会发生DRM错误。 要解决此问题，当您禁用autoPlay但预载资源时，请通过更改`onPlaybackManagerPrepared`的内容来修改`ReferenceCore.as`:

```
if (_playbackManager.autoPlay) {
_playbackManager.play();
} else {
_playbackManager.play();
_playbackManager.pause();
}
```

* **版本1.4.13** PTPLAY-8501 — 当VMAP返回两个直接的MP4非转码广告时，相同的回落广告播放两次。

* **版本1.4.2在** Flash Player版本16中，播放器进入空缓冲事件后，使用ABR &quot;switching down&quot;逻辑识别了问题。该问题可防止在播放器进入缓冲状态后，在不良的带宽环境下切换比特率。 要解决此问题，请让应用程序在缓冲状态(即在`BufferEvent.BUFFERING_BEGIN`事件上)期间将`BufferControlParameters.initialBufferTime`临时设置为与`BufferControlParameters.playbackBufferTime`相同，然后将其重置回在`BufferEvent.BUFFERING_END`事件上的设置值。 此问题的修复将在Flash Player版本16的下一个修补程序版本中提供。

* **版本1.4.0**

   * PTPLAY-1634 — 同一“订阅”标签在不同实时窗口中具有不同的时间戳。 移动实时窗口时，每个窗口中的同一标签应具有相同的时间戳。 但是，有时相同的标记具有不同的时间戳。
   * PTPLAY-28 - MediaPlayer时间轴不包括空中断。
   * 需要跨域策略文件(crossdomain.xml)才能获得来自其他域的内容流的权限。 [为HTTP流设置crossdomain.xml文件](https://www.adobe.com/devnet/adobe-media-server/articles/cross-domain-xml-for-streaming.html)。
   * 错误#3694203 — 在DVR流中，从播放中的中间广告中搜索到另一个中间广告提示可能会导致浏览器冻结
   * 错误#3753725 - selectPolicyForSeekIntoAd在观看广告中断时不会考虑
   * 错误#3754529 — 在实时DVR流中进行搜索时，不会从流中删除前滚广告
   * 错误#3761896 — 如果在广告播放期间允许进行搜索，广告标记将在搜索后重新调整。 解决方法是在搜索期间不使用ITEM_UPDATED回调
   * 错误#3779889 — 在视频分析中以特技播放结束时，不会发出完整的呼叫
   * 错误#VA-779 — 不会为包含心率支持参考实施的增强视频分析发送比特率更改事件心跳 — 在示例应用程序中未实现特技播放。

## 有用资源{#helpful-resources}

* 请参阅[Adobe Primetime学习和支持](https://helpx.adobe.com/support/primetime.html)页面上的完整帮助文档。

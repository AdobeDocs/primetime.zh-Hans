---
title: 桌面HLS的TVSDK 1.4发行说明
seo-title: 桌面HLS的TVSDK 1.4发行说明
description: 桌面HLS的TVSDK发行说明描述了TVSDK DHLS中的新增或更改功能、已解决和已知问题。
seo-description: 桌面HLS的TVSDK发行说明描述了TVSDK DHLS中的新增或更改功能、已解决和已知问题。
uuid: 84da27b7-299b-478d-88f5-ef943f0a8321
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: e4437a26-9454-4da1-ae87-0fce664aac3d
translation-type: tm+mt
source-git-commit: ba291a4615a8e0713cf610f76f41e328da96ec4d
workflow-type: tm+mt
source-wordcount: '5222'
ht-degree: 0%

---


# 桌面HLS的TVSDK 1.4发行说明 {#tvsdk-for-desktop-hls-release-notes}

桌面HLS的TVSDK发行说明描述了TVSDK DHLS中的新增或更改内容、已解决和已知问题。

## 新增功能 {#new-features}

**1.4.31**

* **CRS广告的多CDN支持**

   * 默认情况下，所有转码资源都托管在Akamai上由Adobe拥有的CDN上。 Adobe创意重新打包服务(CRS)提供了将转码创意内容上传到客户指定的多个CDN的功能。
   * 新的API添加到TVSDK以启用在不使用默认URL时指定最终的CRS创作URL。 请参阅文档，了解如何使用这些新API。

### 先前版本的新增功能 {#new-features-previous}

**1.4.30**

* **计费指标**

为了迎合那些希望只支付其使用费用而不是固定费用的客户，Adobe会收集使用情况指标并使用这些指标来确定向客户收取的费用。

**1.4.24**

* **永久网络连接**

重要：您必须至少安装AdobeFlash Player版本22或更高版本。
永久网络连接创建并存储可对多个请求重用的网络连接的内部列表，而不是为每个网络请求打开新连接。 永久网络连接应提高效率并减少网络代码的延迟。

在此版本中，Mac上的Apple Safari和Mozilla Firefox不支持此功能。

**1.4.19**

* 对VPAID广告的流完整性支持。
* 通过修复挂起问题，为Firefox 42及更高版本的Flash播放器FP 20.0.0.267启用了静音选项卡选项。

**1.4.18**

* Primetime Desktop HLS TVSDK现在支持VPAID 2.0线性SWF创意，以实现丰富的交互式流内广告体验。

**1.4.10**

* **广告回退，广告选择逻辑中的菊花链(Zendesk #3103)** 对于启用回退规则的VAST广告（创意）,TVSDK将MIME类型无效的广告视为空广告，并尝试在其位置使用回退广告。 您可以配置回退行为的某些方面。

有关详细信息，请参 [阅VAST和VMAP广告的广告回退](../programming/tvsdk-1.4-for-android/ad-insertion/ad-fallback/android-1.4-ad-fallback.md)。

**1.4.8**

* **已更新至版本1.5的视频心跳库(VHL)**

   * 能将带有视频开始和／或视频／广告／章节开始的元数据作为上下文数据发送
   * 网络流量更少——心跳平均更少，且更小。

**1.4.7**

* **预置个性化支持**

支持Adobe个性化服务器的本地安装，以自定义客户端的个性化请求以转到其他端点。

**1.4.6**

* **示例AES加密(需要Flash Player版本17.0.0.134)**

现在支持基于样本的AES加密。

**1.4.2**

* **视频心率库(VHL)更新至版本1.4.0.1**

   * 添加了将来自其他SDK或播放器的不同分析用例与Adobe Analytics视频基础捆绑的功能。
   * 已通过删除trackAdBreakStart和trackAdBreakComplete方法优化了广告跟踪。 广告中断从trackAdStart和trackAdComplete方法调用推断出来。
   * 跟踪广告时不再需要播放头属性。

**1.4.0**

* **使用备用内容替换的封锁信号** 作为1.4 TVSDK更新的一部分，TVSDK现在还支持针对线性内容的区域封锁进入和返回。 TVSDK现在可以并行处理两个清单文件，主文件和备用文件，以监视封锁信号，即使替代原始编程显示替代了替代编程。

* **删除／替换C3广告** 现在，无需进行任何额外的准备工作即可将新广告动态插入从C3窗口推出的视频点播(VOD)资产中。 TVSDK现在提供一个API，用于删除自定义内容范围和动态插入新广告。 当直播／线性内容在播出期间播放时，此强大的新功能也很有用，并且会立即作为点播内容下载，而无需适当时间“清理”资产。

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

* Zendesk #29968 -多次公告牌。

   当ABR切换发生时，视频播放器可以重复一段时间的最后一段。 因此，有时会重复最后一段预卷。 已修复。

**版本1.4.35** (879)

* Zendesk #26058 —— 支持本机VPAID事件

**版本1.4.33** (873)

* Zendesk #21701 —— 发送1401 CRS请求的原始创意URL，而不是标准URL。

   已根据CRS后端的要求修复了要求重新打包的URL进行转码的问题。
* Zendesk #26197 —— 变形压缩未在所需的显示分辨率下重播。

   **注意**:此问题需要Flash播放器24.0.0.194或更高版本。

   宽高比表中缺失条目用于计算输出宽度的问题已得到修复。

* Zendesk #26840 —— 第二次尝试后IE11 + Windows7上的HDCP检测失败。

   **注意**:此问题需要Flash播放器24.0.0.218或更高版本。

   通过修改AdobeCP的主消息队列处理来循环访问整个队列，而不是仅阻止第一条消息，解决了此问题。

* Zendesk #27460 —— 新的Akamai帐户无法处理POSTCDN请求。

   新的CDN帐户无法处理POSTCDN请求。 通过更新代码使cdn.auditude.com广告请求成为GET而不是POST，解决了此问题。
* Zendesk #27619 - Windows 10上的Flash崩溃

   **注意**:此问题需要Flash播放器24.0.0.218或更高版本。

   通过防止长URL导致的错误，解决了此问题。

* Zendesk #28218 —— 跟踪事件在从恢复点进行回放时不会触发

   此问题与Zendesk #26592中的问题相同。 解决了媒体播放器处于VOD流的PREPARED状态时允许执行搜索操作的问题。

**版本1.4.32** (867)

* Zendesk #26592当回放事件从恢复点开始时，跟踪不会触发

当恢复点不为零时，代码未更新前置广告中断项。 通过添加逻辑在范围开始时间不匹配时刷新代码来解决此问题。

* Zendesk #27022第二次播放资产时，不会播放广告

数组方法的例外已得到修复。

**版本1.4.30** (855)

此版本中的TVSDK解决了以下问题：

* Zendesk #22898 —— 缺少字幕不应导致播放失败。

**注意**:此问题需要Flash播放器23.0.0.185或更高版本。

通过允许TVSDK继续播放，即使清单缺少WebVTT M3U8，并只注册警告，解决了此问题。

* Zendesk #23454 —— 第三方广告(VPAID)处理不正确

通过根据内容ID（而非时间范围）正确处理VPAID广告，解决了此问题。

* Zendesk #24528 - TVSDK账单使用量度。

重要：此问题需要Flash播放器23.0.0.185或更高版本。

* Zendesk # 25432调整播放器大小时出现“隐藏式字幕”问题。

重要：此问题需要Flash播放器23.0.0.185或更高版本。

字幕显示纹理映射代码已被固定，以在播放器调整大小时正确处理坐标。

视频心跳库(VHL)已更新至版本1.5.9以解决以下问题：

* Zendesk #23730 —— 比特率度量为空

通过跟踪VideoAnalyticsTracker中的比特率更改解决了此问题。

* 向PTVideoAnalyticsTrackingMetadata添加了一个新API assetDuration，以更新实时／线性流的资产持续时间。

**版本1.4.28** (848)

* Zendesk #25027 - Auditude在1.4.27桌面版本中不起作用

通过添加检查AUDITUDE_METADATA_KEY的代码并使AUDITUDE_METADATA_KEY和ADVERTISING_METADATA_KEY可互换，解决了此问题。

* Zendesk #24428 —— 使用TVSDK播放DRM HLS时经常出现缓冲问题

通过考虑到没有广告设置时，TVSDK可以通过消除设计用于同步广告插入的时间轴上的前置广告保持和实时保留保持来加快处理速度，从而解决了此问题。

* Zendesk #24344 —— 禁用WebVTT文件以缩短开始设置时间。

**注意**:此问题需要Flash播放器23或更高版本。

仅当需要显示字幕时，才加载WebVTT文件可解决此问题。

* Zendesk #24994 —— 从商业休息返回时，关闭的字幕从播放器中删除

**注意**:此问题需要Flash播放器23或更高版本。

虚假的EOC代码导致字幕显示消失。 通过强制608字幕代码RU2、RU3和RU4在当前活动窗口中提供正确的可见性，解决了此问题。

**版本1.4.27** (844)

* Zendesk #21554 —— 未为application-type = video/mp4触发TVSDK错误信标

通过启用TVSDK对无效资产格式的正确错误跟踪URL进行ping，解决了此问题。

* Zendesk #23402 —— 广告播放不完整

**注意**:此问题需要Flash播放器23或更高版本。

在收到某些请求的404错误后，可能会发生崩溃。 通过确保在处理响应时不关闭连接，已解决此问题。 该解决方案可确保VPAID广告文件计数不正确，因此下载时不会释放它们。

* Zendesk #23621 —— 重试在400和404时失败

**注意**:此问题需要Flash播放器23或更高版本。

修复了在不同用户档案之间切换时导致DRM元数据损坏的问题。

* Zendesk #23705 - AdSuctind中断期间冻结视频广告

**注意**:此问题需要Flash播放器23或更高版本。

此问题与Zendesk #23621中的问题相同。

* Zendesk #23905 —— 某些广告中断跳到广告中断

**注意**:此问题需要Flash播放器23或更高版本。

已修复Windows本机网络代码，以确保连接不会关闭其他连接当前正在使用的句柄。

* 票证#24029 - HLS FER流不播放中间卷。json文件中的所有中间卷广告。

通过允许客户端在Opportunity实例上单独设置自定义参数，以便客户端不必覆盖OpportunityGenerator，解决了此问题。

**版本1.4.26** (839)

* Zendesk #18854 —— 更新基于CRS规则的创意选择逻辑
   * 提供了基于CRS规则更新创意选择逻辑的支持

* Zendesk #22725 —— 在桌面范例应用程序中实现playbackManager.beginPlayback()

   * 通过在startPlaybackFromFlashVars末尾删除此冗余调用来修复，因为该方法是从setupVideo()调用的

* Zendesk #2807 - SeekManager空引用异常

   * 通过在与_dispatcher相关的SeekManager中提供必要的空指针保护来修复

* Zendesk #22822 —— 使用TVSDK播放清除的HLS时经常进行缓冲

   * 通过删除由adSigningModeOpportunityGenerator生成的初始机会（如果没有广告）来修复

* Zendesk #23378 —— 流完整性块rules.xml

   * 通过流完整性工作流加载rules.xml文件来修复

**版本1.4.24** (817)

* Zendesk #19851 —— 当播放器调整为不同的比特率时，它使用新的比特率跳回几帧，使体验变得尴尬

**注意**:此问题需要Flash播放器22.0.0.175或更高版本。

已解决下载一小部分段后DRM适配器重置未正确恢复的问题。

* Zendesk #20784 —— 分析：实时视频过渡完成触发内容

通过添加API(trackVideoComplete)来在LINEAR/LIVE视频跟踪会话期间手动触发内容完成，解决了此问题。

更新了以下库：

* Zendesk #21643 - VPAID广告不完整播放

   * AdobeMobile库到4.10.0
   * VHL库到1.5.6
   * VHL-Nielsen图书馆至1.6.7

在播放VPAID广告时，通过使用零高度视口填充舞台，解决了此问题。

* Zendesk #22110 —— 分析：向心跳跟踪调用添加h:sc:ssl字段

修复了与SSL相关的问题，TVSDK中使用的VHL库已更新至最新版本。

* Zendesk #22608 —— 视频间歇性地显示黑屏(需要22.0.0.175Flash Player或更高版本)

在自适应比特率期间，在最大比特率限制下，视频的重新加载会间歇性地显示黑屏，即使客户端看到位置更新，而且客户端的行为就像在播放内容一样。

**版本1.4.23** (809)

* Zendesk #2887 —— 将广告规则逻辑应用于TVSDK时的滚动后广告跳转问题

**注意**:此问题需要Flash播放器21.0.0.240或更高版本。

已修复将广告规则逻辑应用于TVSDK时，将跳过后期广告的问题。

* Zendesk #19863 —— 放弃VPAID媒体文件的广告

如果一个庞大的内联广告有多个媒体文件，并且VPAID广告是第一个广告，则不会为实时流播放内联广告。 此问题已通过选取其他媒体文件而解决。

* Zendesk #21021 —— 延迟绑定音频导致音频段重复

**注意**:此问题需要Flash播放器21.0.0.240或更高版本。

已修复音频重复问题。

* Zendesk #21125 —— 提早退回实时／线性广告

**注意**:此问题需要Flash播放器21.0.0.240或更高版本。

此版本支持在广告播放到完成之前，从广告中断返回。 通过自定义清单标签指示提前返回。

* Zendesk # 21369延迟绑定音频导致时间不一致

**注意**:此问题需要Flash播放器21.0.0.240或更高版本。

已修复的音频重复问题也修复了此问题。

* Zendesk #21760, 20921 - Seek上的音频视频不同步。

**注意**:此问题需要Flash播放器21.0.0.240或更高版本。

已修复音频重复问题。

* Zendesk #22024 —— 运行TVSDK时出错

已修复引用播放器未播放任何流并且正在向开始上抛出异常的问题。

**版本1.4.22** (791)

* Zendesk #17580 - Primetime运行时错误，代码3357

**注意**:此问题需要Flash播放器21.0.0.197或更高版本。

修复了在调用storeVoucher()时正确初始化deviceID时发生的随机3357错误。

* Zendesk #21334 - TVSDK广告请求第三方广告请求的超时值

在此版本中，已添加全局广告请求超时。

**版本1.4.21** (782)

* Zendesk #19580 TVSDK在发送通知之前等待内容解析程序完 `PTTimedMetadataChangedNotification` 成

**注意**:此问题需要Flash播放器21.0.0.182或更高版本。

通过提供设置广告标记和添加自定义机会生成器的功能，可以在桌面参考播放器中解决此问题，该生成器显示如何订阅自定义提示以及如何在VOD文件中处理这些提示。

* Zendesk #20806在交换摄像机后，DVR窗口中的未来中间广告不会触发

**注意**:此问题需要Flash播放器21.0.0.182或更高版本。

通过更新应用程序以设置_resource.metadata.setValue(DefaultMetadataKeys.ENABLE_LIVE_PREROLL, &quot;false&quot;)来禁用PIP交换中的预卷广告插入，因此不生成预卷机会，解决了此问题。

引入了分类功能来修复导致主内容持续时间为负的无序广告投放。

* Zendesk #20522:无法跳过VPAID 2.0广告

**注意**:此问题需要Flash播放器21.0.0.182或更高版本。

* 通过在广告原谅期间跳过VPAID广告，解决了此问题。
* 当adbreak策略设置为跳过时，仍会分派广告和广告中断事件。 播放器状态不一致。

此问题已解决，当跳过广告中断时，其行为正确且不会分派事件。

* Zendesk #20955通过机会生成器在customParameters属性中设置键值对

**注意**:此问题需要Flash播放器21.0.0.182或更高版本。

在为广告请求创建广告单元时，Auditude Request会解析AuditudeSettings的自定义参数。

此行为已更改为在请求中包含来自Opportunity对象的自定义参数。 此外，在一个Auditude请求中无法打包具有不同自定义参数的多个机会。

* Zendesk #21227 - m3u8无法一致地播放

**注意**:此问题需要Flash播放器21.0.0.211或更高版本。

通过允许TVSDK忽略包含TVSDK不支持的AC3编解码器（环绕）的清单(HLS子用户档案)，解决了此问题。

**版本1.4.20** (762)

* Zendesk #19181 —— 快速向前技巧播放可锁定流的实时点。

**注意**:此问题需要Flash播放器20.0.0.306或更高版本。

* Zendesk #19286 —— 在FER流中来回搜寻时发生Flash Player崩溃。

**注意**:此问题需要Flash播放器20.0.0.306或更高版本。

在Google Chrome中搜索时发生的偶然挂起通过关闭查询得到解决，如果查询需要太长时间才能得到响应，或者套接字正在关闭。

* Zendesk #19305 —— 播放带有A/V不连续的流时遇到生硬的播放。

**注意**:此问题需要Flash播放器20.0.0.306或更高版本。

此问题已通过报告警告解决。

* Zendesk # 19359 -Flash Player崩溃，原因是#EXT-X-FAXS-CM的位置：属性。

当#EXT-X-FAXS-CM标签出现在播放列表中各个比特率或段之前的顶级播放列表中时，此问题已解决。

* Zendesk #19489 - Fast Forward to Live Point停止插件（实时流）

此问题与Zendesk #19181相同。

* Zendesk #19699 - TVSDK无法在WebVTT子标题轨道之间切换

通过在轨道发生更改时进行播放器转储并重新加载清单，以及通过更正影响多次字节WebVTT字幕轨道名称的UTF8字符串转换问题，解决了此问题。

**版本1.4.19** (1.4.19.738)

* Zendesk #18234 - CC中使用Unicode字符串回放流的Flash Player崩溃

此问题需要Flash PlayerFP 20.0.0.267或更高版本，并通过正确处理Unicode字符串来解决。

* Zendesk #18304 - VPAID广告的流完整性支持

此功能需要Flash PlayerFP 20.0.0.267或更高版本，并在版本1.4.19中引入。

* Zendesk #18766 —— 引用播放器无法在CC音轨名称中显示非拉丁文Unicode字符

此功能需要Flash PlayerFP 20.0.0.267或更高版本，并通过正确处理Unicode字符串来修复。

* Zendesk #18804 - Firefox 42中的播放器崩溃

此问题需要Flash PlayerFP 20.0.0.235或更高版本，与Zendesk #18723存在相同问题。

* Zendesk #18864 -Flash Player完整插件崩溃

此问题需要Flash PlayerFP 20.0.0.235或更高版本，与Zendesk #18723相同。

* Zendesk #18998 —— 如果音频和视频时间戳不匹配，则会在中断时不断下载区段。

通过忽略时间戳之间的间隙并仅播放下载的内容，解决了此问题。

* Zendesk #19093 —— 中转广告只能通过实时和全事件重播(FER)内容观看一次，但在快速转发或寻找超过广告时无法再观看这些广告

在Primetime的默认adPolicy选择器中，如果观看中间广告，则完成搜索后，adBreak不会移至搜索位置。 要再次播放广告，在搜索后，应用程序需要覆盖selectAdBreaksToPlay()函数。

* Zendesk #19101 —— 重新收回未解决的Midroll广告将删除广告投放。

通过允许播放器更新playbackMetrics时间、minimumOpportunityTime和时间轴，解决了此问题。

* Zendesk #19102 - FER和技巧模式的问题

此问题需要Flash PlayerFP 20.0.0.267或更高版本，并通过正确设置advertisingMetadata.adSigningMode来解决。

* Zendesk #19175 —— 有时，在首次播放流时，前放广告不会显示。

通过向AuditudeSettings添加新的API adRequestTimeout来解决此问题，以获得广告请求超时。 用户现在可以覆盖默认的10秒广告请求超时。

**版本1.4.18** (1.4.18.722)

* Zendesk #3324 - Primetime广告报告在VMAP中没有广告媒体时不会跟踪广告中断。

当广告中断为空时，广告中断开始和完整跟踪事件未被ping通。 通过在空广告中发送广告中断开始ping（如VMAP AdBreak）并使用有效的AdSource Nod，解决了此问题。

**版本1.4.17** (1.4.17.702)

* Zendesk #17168 —— 切换可见性后字幕在10秒左右不显示

通过为vtt字幕文件提供EXT-X-MEDIA-TIME标记支持，解决了此问题。

* Zendesk #17983 —— 未能下载清单的任何键会导致整个清单播放失败

**注意**:您必须至少具有Flash PlayerFP 19.0.0.245或更高版本。

有时播放实时内容时，清单中可能有无效的键（例如，对于封锁期），但其他时间范围可能有有效的键并且仍将播放。 以前，当清单中列出的密钥无法下载时，整个清单将失败。 现在，清单仅在无法下载所有列出的密钥时才会失败。 如果某些键有效，但其中某些键无法下载，则内容将播放。 如果我们尝试播放需要我们没有的密钥的区段，则仍会失败。

* Zendesk #18554 - Stream Integrity在某些情况下修剪Cookie

**注意**:您必须至少具有Flash PlayerFP 19.0.0.245或更高版本。

修复了Cookie操作代码中可能截断Cookie值的错误。

**版本1.4.16** (1.4.16.684)

* Zendesk #3732 —— 在Chrome中为流完整性添加代理支持(需要Flash PlayerFP 19.0.0.207或更高版本)

这是一种增强。

* Zendesk #4244 - PTS滚动时的流问题

通过检测滚动和管理每个有效负荷类型的不连续性而非一般性，解决了此问题。

* Zendesk #4487 —— 跟踪内容的线性渠道

通过在线性流播放会话期间重新初始化视频心跳跟踪器，解决了此问题。

* Zendesk #17427 -Adobe流完整性无法通过Chrome上的代理运行(Win7)()

**注意**:该决议要求Flash PlayerFP 19.0.0.207或更高版本。

此问题与Zendesk #3732相同。

* Zendesk #17907 - pHLS实时流延迟(Flash Player19)

**注意**:该决议要求Flash PlayerFP 19.0.0.207或更高版本。

通过处理在重新加载活动清单时TS文件的域发生更改，并且下载两次文件的实时流，解决了此问题。

* Zendesk #17931 —— 开始处于平板状态的HLS内容回放失败

**注意**:该决议要求Flash PlayerFP 19.0.0.207或更高版本。

通过在第一个TS文件的前2秒处理没有音频的流，解决了该问题。

* Zendesk #17934 —— 实时流失败，Flash19.0.0.185

**注意**:该决议要求Flash PlayerFP 19.0.0.207或更高版本。

通过处理具有段边界上音频和视频帧之间的时间交织的实时流，解决了该问题。

* Zendesk #17973 —— 最新Flash Player19.0.0.185在中间卷期间崩溃

**注意**:该决议要求Flash PlayerFP 19.0.0.207或更高版本。

通过处理中间广告插入的未混音音频，解决了此问题。 (分析器切换发生，并且在播放的任何点，内容过渡都会到中间广告，或者在广告播放的中间，依此类推。)

* Zendesk #18049 -Flash19与Firefox 42测试版崩溃

此问题与Zendesk #17973相同。

**版本1.4.15** (1.4.15.678)

* Zendesk #4377:由于广告策略，在跳过广告中断时触发AD_BREAK_CRIPPED事件。

修复是在跳过广告时添加AD_BREAK_CLIPTED。

* Zendesk #4496 —— 流完整性：错误102100，重定向到标记流。

修复是添加对通过TVSDK设置AVNetworkConfiguration属性useCookieHeaderForAllRequests的支持。

* Zendesk #17179 -Flash播放器在加密内容的多个SAP更改上崩溃。

修复了播放某些加密内容时的崩溃问题。

**注意**:该修复需要Flash Player19.0.0.200或更高版本。

* Zendesk #17499 —— 我们如何不在观看后删除中间人，而从外部内容中删除前置人

为AdBreakTimelineItem(AdBreakTimelineItem.placementType)添加了一个类型，以便AdPolicySelector可以为前置、中置和后置内容返回不同的策略。

* Zendesk #17665 —— 带宽限制

修复是删除逻辑，在缓冲开始时将目标缓冲区大小更改为初始缓冲区大小。

**版本1.14.14** (1.4.14.771)

* Zendesk #17363 —— 修复参考播放器的自述文件

   * 阐明有关下载和安装playerglobal.swc的说明。
   * 添加有关使用特定flash player版本更新项目配置的说明。
   * 更新AdvertisingOverlay项目配置以使用最低播放器版本。
   * 更新ReferenceCore项目配置以使用特定播放器版本11.9

* Zendesk #17471 —— 播放器冻结

部分修复广告在搜索后从头开始不播放的问题。

* Zendesk #17496 —— 在DVR窗口中返回搜索时，播客器未解决

为每个广告中断提供自定义参数。

**版本1.4.13** (1.4.13.660)

* Zendesk #4037 —— 无可用用户档案错误(需要Flash Player18.0.0.232或更高版本)

修复查询参数包含“http”时的url解析问题

* Zendesk #4260 -Flash Player18在IE11中崩溃(需要Flash Player18.0.0.232或更高版本)

修复了在IE11全屏模式下播放视频时的崩溃

* Zendesk #4262 - Windows 10上的Adobe Primetime播放器崩溃(需要Flash Player18.0.0.232或更高版本)

修复了在Windows上使用FireFox以全屏模式播放视频时的崩溃问题。

* Zendesk #4279 - HLS TVSDK广告插入-iOS和桌面上的302重定向问题

修复了URL由于没有扩展名而无法正确识别其类型的问题

* Zendesk #4306 —— 仅在Win上全屏显示时Flash Player崩溃(需要Flash Player18.0.0.232或更高版本)

修复了在Windows上以全屏模式播放视频时的崩溃问题。

* Zendesk #4480 —— 缺少ID3标记事件(需要Flash Player18.0.0.232或更高版本)

**1.4.12 **(1.4.12.656)

* Zendesk #2751 - CSAI和CRS |增强：处理某些媒体文件URL中的动态元素。

更新了Creative Repackaging Service，可通过动态创意URL正确处理广告。

* PTPLAY - 2114 —— 支持MP4回放。

现在支持播放、暂停和搜索等MP4内容的基本播放。

以下要求Flash Player18.0.0.225或更高版本：

* Zendesk #3992 —— 其他TrickPlay速度。

TrickPlay现在接受高于16x的速率：+/- 32、+/-64和+/- 128。

* Zendesk #3113 -Flash Player插件崩溃

修复了在Mac Firefox上尝试播放重定向广告时的崩溃问题。

* Zendesk #4037 —— 无可用用户档案错误
* Zendesk #4262 -Adobe Primetime播放器在windows 10上崩溃

修复了在全屏播放期间在Windows Firefox中崩溃的问题。

**版本1.4.11** (1.4.11.648)

* Zendesk #1869 —— 问题更改字体大小(需要Flash Player18.0.0.200)

允许在WebVTT题注代码中使用题注大小。

* Zendesk #3113 -Flash Player插件崩溃(需要Flash Player18.0.0.200)
* Zendesk #3268 —— 台式机：视频播放器开始在+- 40/50秒后闪烁，开始在+- 90秒后变黑(需要Flash Player18.0.0.200)

修复舞台视频错误。

* Zendesk #3670 —— 在参考播放器中搜索时VOD中出现INVALID_PARAMETER错误(需要Flash Player18.0.0.200)

检测到新时段时，ThreadSeek中的InvalidateProfiles。

* Zendesk #3896 -Flash Player崩溃，流完整性设置为在Chrome上打开(需要Flash Player18.0.0.200)

修复了在椒盐本机网络模式下的崩溃

* Zendesk #3905 —— 在CDN上托管时，TVSDK播放器不加载

修复了当pageDomain与swf域不同时查找通配符令牌的问题。

**版本1.4.10** (1.4.10.642)

* Zendesk #3249 - TVSDK Web Player在Firefox上崩溃Flash

修复了在Mac上使用Firefox时，当在外部显示器上播放的流切换到较高比特率的流时，偶尔会发生Flash Player崩溃。(需要Flash Player18.0.0.160)

* Zendesk #3268 —— 台式机：视频播放器开始 `+-` 在40/50秒后闪烁，开始在90秒后 `+-` 变黑

修复了Mac Chrome上的一个问题，该问题导致流开始闪烁并最终变为黑色。 (需要Flash Player18.0.0.161)

* Zendesk #3304 —— 未填充VAST `[ERRORCODE]` 3.0宏

   * 如果内联广告的创意不佳，则将显示错误代码400。
   * `[ERRORCODE]` 宏将进行URL编码

* Zendesk #3601 —— 增强请求：包装器配套管理

   * TVSDK将向行中显示包含资源（html、iframe或static）的包装器伴侣关闭。 （如果行中不包含该大小的行）
   * 除非用于显示，否则具有资源的包裹将被忽略。 （不用于跟踪）
   * 只有具有NO资源的包装器伴侣才能用于跟踪目的。 （包含跟踪的包装器伴侣）

**版本1.4.9**

* Zendesk #2615 —— 从桌面显示中删除HLS视图时出现的问题

向MediaPlayer添加了clearVideo()方法。 通过从StageVideo对象中清除AVStream来清除显示的视频帧。 仅当视频已暂停时才应调用，并且必须先调用replaceCurrentResource或replaceCurrentItem，然后才能再次调用play()。

* Zendesk #3169 —— 借助Adobe Analytics集成更新参考播放器

参考播放器已更新，与Adobe Analytics集成

* Zendesk #3296 —— 桌面HLS TVSDK —— 未播放的广泛第三方广告

HLS格式的mime类型区分大小写，这不正确，并且已更改，因此不再区分大小写

**版本1.4.8**

* Zendesk #2737 - Desktop Player - Error 106000(需要Flash Player17.0.0.184)
* Zendesk #3007 —— 更新至Flash Player17后不显示预置广告(需要Flash Player17.0.0.184)
* Zendesk #3085 —— 桌面HLS播放器60秒后出错106000(需要Flash Player17.0.0.184)

**版本1.4.7**

* Zendesk #2760 —— 在TrickPlay模式中忽略的DINSTRUCTION标签(需要Flash Player版本17.0.0.158)
* Zendesk #2760 —— 在TrickPlay模式中忽略的DINSTRUCTION标签(需要Flash Player版本17.0.0.158)

**版本1.4.6**

* Zendesk #2652 —— 桌面HLS的Auditude文档，桌面HLS的Clarified Auditude media_id文档

**版本1.4.5**

* Zendesk #2256 —— 访问主控播放列表，更新了PSDK以为主控播放列表上的订阅标记调度timedMetadata事件。 (需要Flash Player版本17.0.0.134)
* Zendesk #2417 - WebVTT在播放开始前尝试下载字幕的播放器使用错误的段编号变量进行段编号匹配。 只有在细分索引从零开始的媒体中才会显示错误。 (需要Flash Player版本17.0.0.134)
* Zendesk #2537 —— 将pepper插件与Chrome一起使用时，Flash播放器崩溃(需要Flash Player版本17.0.0.134)
* Zendesk #2547 —— 阿拉伯语字幕：文本应右对齐(需要Flash Player版本17.0.0.134)

**版本1.4.4**

* Zendesk #1561 —— 续： `[Adobe Primetime]` 更新：桌面PSDK中基于HLS客户端的项目-DATE-TIME故障转移支持(需要Flash Player版本16.0.0.305或更高版本)
* Zendesk #2197 —— 跟 `[Ads]` 踪广告错误
* Zendesk #2286 —— 功能请求：提供广告加载状态(VPAID)相关信息
* Zendesk #2285 —— 功能请求：在指定超时持续时间后跳过广告
* 错误#3921755 - OpenSSL库在Flash Player中更新至版本1.0.1L(需要Flash Player版本16.0.0.305或更高版本)

**版本1.4.2**

* Zendesk #1303 —— 隐藏字幕的垂直偏移(需要Flash Player版本16.0.0.235或更高版本，预期发布日期：2014年12月)
* Zendesk #1870 - “Closed Caption Tonn &amp; Off(Requires Version 16.0.0.235 or reader)”Flash Player，预期发布日期：2014年12月)
* Zendesk #2110 —— 在VPAID广告期间尝试进入全屏后，播放卡住(需要Flash Player版本16.0.0.235或更高版本，预期发布日期：2014年12月)
* Zendesk #2199 —— 在寻 `[VPAID]` 找过去的广告休息时，播放器不响应
* Zendesk #2358 —— 续： `[Analytics]` 章节数据不正确

**版本1.4.1**

* 更新了封锁期API以与Android和iOS实现保持一致。

**版本1.4.0**

* Zendesk #1024 —— 通过清单从流中删除广告的功能
* Zendesk #1423 - HLS回放失败正在锁定Flash Player（未报告错误）
* Zendesk #1674 - ClosedCaption未显示，当缺少0x03 ETX代码时，正确的708字幕显示。

## 已知问题 {#known-issues}

* “隐藏式字幕”无法处理纯音频内容，因为字幕系统需要视频才能正常工作。
没有视频，就没有视口尺寸，没有视口尺寸，就无法显示任何字幕图形。
* 由于Chrome沙箱限制，Google Chrome中的流完整性稍慢。
* 在TVSDK 1.4中，如果禁用自动播放，则播放器至少保持空闲一分钟时，可能会发生DRM错误。 要解决此问题，请在禁用自动播放但预载资源时， `ReferenceCore.as` 通过更改以下内容进行修 `onPlaybackManagerPrepared`改：

```
if (_playbackManager.autoPlay) {
_playbackManager.play();
} else {
_playbackManager.play();
_playbackManager.pause();
}
```

* **版本1.4.13** PTPLAY-8501 —— 当VMAP返回两个直接的MP4非转码广告时，相同的回落广告会播放两次。

* **版本1.4.2在Flash Player版本** 16中，在播放器进入空缓冲事件后，用ABR“切换”逻辑识别了问题。 该问题可防止在播放器进入缓冲状态后在不良带宽环境下切换比特率。 要解决此问题，请让您的应用 `BufferControlParameters.initialBufferTime` 程序将缓冲状态 `BufferControlParameters.playbackBufferTime` (即在事件上)的临时值设置为相同，然后将其重置回在事件上的设置 `BufferEvent.BUFFERING_BEGIN``BufferEvent.BUFFERING_END` 值。 此问题的修复将在Flash Player版本16的下一个修补程序版本中提供。

* **版本1.4.0**

   * PTPLAY-1634 —— 同一“订阅”标签在不同实时窗口中具有不同的时间戳。 移动实时窗口时，每个窗口中的同一标签应具有相同的时间戳。 但是，有时相同的标记具有不同的时间戳。
   * PTPLAY-28 - MediaPlayer时间轴不包括空分段。
   * 需要跨域策略文件(crossdomain.xml)才能获得从其他域流式传输内容的权限。 [为HTTP流设置crossdomain.xml文件](https://www.adobe.com/devnet/adobe-media-server/articles/cross-domain-xml-for-streaming.html)。
   * 错误#3694203 —— 在DVR流中，从正在播放的中间卷中搜索到另一个中间卷广告提示可能会导致浏览器冻结
   * 错误#3753725 - selectPolicyForSeekIntoAd未考虑广告中断是否已观看
   * 错误#3754529 —— 在实时DVR流中进行搜索时，不会从流中删除预卷广告
   * 错误#3761896 —— 如果在广告播放期间允许进行搜索，则广告标记将在搜索后重新调整。 解决方法是在搜索期间不使用ITEM_UPDATED回调
   * 错误#3779889 —— 在视频分析中达到特技播放结束时，不会发出完整的呼叫
   * 错误#VA-779 —— 对于具有心跳支持参考实施的增强视频分析，不发送比特率更改事件心跳——不在范例应用程序中实现技巧播放。

## 实用资源 {#helpful-resources}

* 请参阅Adobe Primetime学习和支 [持页面上的完整帮助](https://helpx.adobe.com/support/primetime.html) 文档。

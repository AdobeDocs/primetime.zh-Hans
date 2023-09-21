---
title: 适用于桌面HLS的TVSDK 1.4发行说明
description: 《 TVSDK for Desktop HLS发行说明》介绍了TVSDK DHLS中的新增或更改内容、已解决问题和已知问题。
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '5194'
ht-degree: 0%

---

# 适用于桌面HLS的TVSDK 1.4发行说明 {#tvsdk-for-desktop-hls-release-notes}

《 TVSDK for Desktop HLS发行说明》介绍了TVSDK DHLS中的新增或更改内容、已解决问题和已知问题。

## 新增功能 {#new-features}

**1.4.31**

* **CRS广告的多CDN支持**

   * 默认情况下，所有转码资源将托管在Akamai的Adobe拥有的CDN上。 在最新版本中，AdobeCreative Repackaging Service (CRS)允许将转码创意上传到客户指定的多个CDN。
   * 新的API会添加到TVSDK中，以便能够在不使用默认URL时指定最终CRS创意URL。 请参阅文档以了解如何使用这些新API。

### 以前版本中的新增功能 {#new-features-previous}

**1.4.30**

* **计费量度**

为了适应那些只想按客户所使用内容支付而不是不管实际使用情况都按固定费率支付的客户，Adobe会收集使用情况量度，并使用这些量度来确定向客户收取多少费用。

**1.4.24**

* **永久网络连接**

重要信息：您必须至少安装AdobeFlash Player版本22或更高版本。
持久网络连接创建并存储可重复用于多个请求的网络连接的内部列表，而不是为每个网络请求打开一个新连接。 持久网络连接应该可以提高网络代码中的效率并减少延迟。

在此版本中，Mac上的Apple Safari和Mozilla Firefox不支持此功能。

**1.4.19**

* VPAID广告的流完整性支持。
* 通过修复挂起问题，在Firefox 42及更高版本的Flash播放器FP 20.0.0.267中启用了静音选项卡选项。

**1.4.18**

* Primetime Desktop HLS TVSDK现在支持VPAID 2.0线性SWF创意，以实现丰富的交互式流中广告体验。

**1.4.10**

* **广告回退，在广告选择逻辑中进行Daisy链接(Zendesk #3103)** 对于启用了回退规则的VAST广告（创意），TVSDK会将具有无效MIME类型的广告视为空广告，并尝试在其位置使用回退广告。 您可以在某些方面配置回退行为。

有关更多信息，请参阅 [VAST和VMAP广告的广告回退](../programming/tvsdk-1.4-for-android/ad-insertion/ad-fallback/android-1.4-ad-fallback.md).

**1.4.8**

* **视频心率库(VHL)已更新至版本1.5**

   * 能够将带有视频开始和/或视频/广告/章节开始的图像作为上下文数据发送元数据
   * 网络流量更少 — 心跳平均更少，大小更小。

**1.4.7**

* **内部部署个性化支持**

支持AdobeIndividualization Server的内部部署，以自定义客户端的个性化请求，从而转到其他端点。

**1.4.6**

* **示例AES加密(需要Flash Player版本17.0.0.134)**

现在支持基于示例的AES加密。

**1.4.2**

* **视频心率库(VHL)已更新至版本1.4.0.1**

   * 添加了将其他SDK或播放器中的不同Analytics用例捆绑到Adobe Analytics Video Essentials的功能。
   * 通过删除trackAdBreakStart和trackAdBreakComplete方法，广告跟踪已得到优化。 从trackAdStart和trackAdComplete方法调用中推断出广告时间。
   * 跟踪广告时不再需要播放头属性。

**1.4.0**

* **使用替代内容替换发出中断信号** 作为1.4 TVSDK更新的一部分，TVSDK现在还支持进入线性内容并从区域封锁返回。 TVSDK现在可以并行处理两个清单文件（主文件和备用文件），以监控中断信号，即使备用程序正在代替原始程序显示时也是如此。

* **删除/替换C3广告** 现在，无需额外的准备工作即可将新广告动态插入到从C3窗口出来的视频点播(VOD)资产中。 TVSDK现在提供了一个API，用于删除自定义内容范围并动态插入新广告。 在广播期间播放实时/线性内容，并且在不用适当时间“清理”资产的情况下立即提取内容作为按需内容时，这项强大的新功能也很有用。

## 已解决的问题 {#resolved-issues}

>[!NOTE]
>
>强烈建议所有使用CRS的TVSDK客户至少在iOS、Android和桌面HLS上升级到TVSDK 1.4.32。 此升级将替代现有应用程序实施。 升级后，在代理工具（例如，Charles）中检查CRS创意URL请求，以验证路径中的版本是否反映了3.1版。例如，
>
>`https://adunit.cdn.auditude.com/assets/3p/v3.1/218747/94b/c1b/94bc1b964cc67e115a5a6781c7329b90_ee92607938ffff46b083121f044c2746.m3u8`

**版本1.4.41**

* Zendesk #33777 - DHLS分发内部版本的Localhost令牌SWF已过期。

  正在更新DHLS上PMP演示的localhost令牌。

### 以前版本中已解决的问题 {#resolved-issues-previous}

**版本1.4.38** (891)

* Zendesk #30731 - TVSDK不会在AdBreak中播放多个VPAID广告。

  修复了AdBreak中的多个VPAID广告播放。

* Zendesk #29968 — 双告示牌。

  视频播放器可以重复发生ABR切换时的最后一个时段段。 因此，有时重复最后一个前置任务区段。 此问题已得到修复。

**版本1.4.35** (879)

* Zendesk #26058 — 支持本机VPAID事件

**版本1.4.33** (873)

* Zendesk #21701 — 发送1401 CRS请求的原始创意URL，而不是规范化URL。

  已按照CRS后端的要求，修复了已重新打包的URL请求进行转码的问题。
* Zendesk #26197 — 无法以所需的显示分辨率重播变形压缩。

  **注意**：此问题需要Flash播放器24.0.0.194或更高版本。

  修复了使用长宽比表中缺少的条目计算输出宽度的问题。

* Zendesk #26840 — 第二次尝试后，IE11 + Windows7上的HDCP检测失败。

  **注意**：此问题需要Flash播放器24.0.0.218或更高版本。

  通过修改AdobeCP的主消息队列处理以循环处理整个队列，而不是仅在第一条消息上阻止，此问题得以解决。

* Zendesk #27460 — 新的Akamai帐户无法处理POSTCDN请求。

  新的CDN帐户无法处理POSTCDN请求。 通过更新代码以使cdn.auditude.com广告请求成为GET而不是POST，此问题已得到解决。
* Zendesk #27619 - Windows 10上的Flash崩溃

  **注意**：此问题需要Flash播放器24.0.0.218或更高版本。

  通过防止长URL导致错误，此问题得以解决。

* Zendesk #28218 — 在从恢复点回放时不会触发跟踪事件

  此问题与Zendesk #26592中的问题相同。 修复了当媒体播放器处于VOD流的准备状态时允许进行搜寻操作的问题。

**版本1.4.32** (867)

* 当播放从恢复点开始时，Zendesk #26592跟踪事件不会触发

当恢复点不为零时，代码未更新前置广告时间项。 通过添加逻辑以在范围开始时间不匹配时刷新代码，解决了此问题。

* 第二次播放资产时，未播放Zendesk #27022广告

已修复数组方法的异常。

**版本1.4.30** (855)

此版本中解决了TVSDK的以下问题：

* Zendesk #22898 — 缺少字幕不应导致播放失败。

**注意**：此问题需要Flash播放器23.0.0.185或更高版本。

通过允许TVSDK继续播放（即使清单缺少WebVTT M3U8），并只注册警告，此问题已得到解决。

* Zendesk #23454 — 无法正确处理第三方广告(VPAID)

通过基于内容ID而不是时间范围正确处理VPAID广告，此问题已得到解决。

* Zendesk #24528 — 计费的TVSDK使用量度。

重要信息：此问题需要Flash播放器23.0.0.185或更高版本。

* Zendesk # 25432调整播放器大小时出现隐藏式字幕问题。

重要信息：此问题需要Flash播放器23.0.0.185或更高版本。

已固定题注显示纹理映射代码，以在播放器调整大小期间正确处理坐标。

视频心率库(VHL)已更新至版本1.5.9，以解决以下问题：

* Zendesk #23730 — 比特率量度为空

通过跟踪VideoAnalyticsTracker中的比特率更改，此问题已得到解决。

* 向PTVideoAnalyticsTrackingMetadata添加了一个新的API assetDuration，以更新实时/线性流的资源持续时间。

**版本1.4.28** (848)

* Zendesk #25027 -Auditude在1.4.27桌面版本中不起作用

通过添加代码以检查AUDITUDE_METADATA_KEY以及使AUDITUDE_METADATA_KEY和ADVERTISING_METADATA_KEY可互换，此问题已得到解决。

* Zendesk #24428 — 使用TVSDK播放DRM HLS时经常出现缓冲问题

在考虑到没有广告设置时，TVSDK可以通过消除时间轴上的前置广告保留和实时保留保留来加快处理速度，从而解决此问题，该时间轴旨在同步广告插入。

* Zendesk #24344 — 禁用WebVTT文件以缩短启动时间。

**注意**：此问题需要Flash播放器23或更高版本。

仅当需要显示字幕时才通过加载WebVTT文件解决了此问题。

* Zendesk #24994 — 从商业休息时间返回时，隐藏式字幕会从播放器中丢弃

**注意**：此问题需要Flash播放器23或更高版本。

虚假的EOC代码导致字幕显示消失。 通过强制608字幕代码RU2、RU3和RU4在当前活动窗口中提供正确的可见性，解决了此问题。

**版本1.4.27** (844)

* Zendesk #21554 — 没有为application-type = video/mp4触发TVSDK错误信标

通过启用TVSDK以ping无效资产格式上的正确错误跟踪URL，此问题得以解决。

* Zendesk #23402 — 广告播放不完整

**注意**：此问题需要Flash播放器23或更高版本。

在某些请求中收到404错误后，可能会发生崩溃。 通过确保在处理响应时连接不会关闭，此问题已得到解决。 解决方法可确保VPAID广告文件计数不正确，因此下载时不会被释放。

* Zendesk #23621 — 在400和404上重试失败

**注意**：此问题需要Flash播放器23或更高版本。

修复了在不同用户档案之间切换时导致DRM元数据损坏的问题。

* Zendesk #23705 — 视频广告在广告拼接时间冻结

**注意**：此问题需要Flash播放器23或更高版本。

此问题与Zendesk #23621中的问题相同。

* Zendesk #23905 — 一些广告时间会在广告时间跳过

**注意**：此问题需要Flash播放器23或更高版本。

Windows本机网络代码已修复，以确保连接不会关闭其他连接当前正在使用的句柄。

* 票证#24029 - HLS FER流不会播放中置.json文件中的所有中置广告。

通过允许客户端在Opportunity实例上单独设置自定义参数，使客户端不必覆盖OpportunityGenerator，此问题已得到解决。

**版本1.4.26** (839)

* Zendesk #18854 — 根据CRS规则更新创意选择逻辑
   * 为基于CRS规则更新创意选择逻辑提供支持

* Zendesk #22725 — 桌面示例应用程序中的playbackManager.beginPlayback()实施

   * 通过删除startPlaybackFromFlashVars末尾的此冗余调用(从setupVideo()调用方法)修复了此问题

* Zendesk #22807 - SeekManager null引用异常

   * 通过在SeekManager内提供与_dispatcher相关的必要NULL指针保护来修复此问题

* Zendesk #22822 — 使用TVSDK播放清晰HLS时频繁缓冲

   * 通过删除adSignalingModeOpportunityGenerator生成的初始机会来修复此问题（如果没有ad）

* Zendesk #23378 — 流完整性块rules.xml

   * 通过流完整性工作流加载rules.xml文件修复了此问题

**版本1.4.24** (817)

* Zendesk #19851 — 当播放器适应不同的比特率时，它会在新比特率上向后跳转几帧，这会造成尴尬

**注意**：此问题需要Flash播放器22.0.0.175或更高版本。

解决了下载区段的一小部分后无法正确恢复DRM适配器的问题。

* Zendesk #20784 - Analytics：触发实时视频过渡的内容完成

通过添加API (trackVideoComplete)在LINEAR/LIVE视频跟踪会话期间手动触发内容完成，解决了此问题。

已更新以下库：

* Zendesk #21643 - VPAID广告无法完全播放

   * AdobeMobile库到4.10.0
   * VHL库到1.5.6
   * VHL-Nielsen库升级到1.6.7

此问题可通过在播放VPAID广告时使用零高度视区填充舞台来解决。

* Zendesk #22110 - Analytics：添加:sc:用于心跳跟踪调用的ssl字段

修复了SSL相关问题，并将TVSDK中使用的VHL库更新到最新版本。

* Zendesk #22608 — 视频间歇性显示黑屏(需要Flash Player22.0.0.175或更高版本)

在最大比特率限制的自适应比特率期间，即使客户端看到位置更新，并且客户端的行为如同正在播放内容，视频重新加载会间歇性地显示黑屏。

**版本1.4.23** (809)

* Zendesk #2887 — 将广告规则逻辑应用于TVSDK时，出现后置广告跳过问题

**注意**：此问题需要Flash播放器21.0.0.240或更高版本。

修复了将广告规则逻辑应用于TVSDK时跳过后置广告的问题。

* Zendesk #19863 — 丢弃带有VPAID媒体文件的广告

如果大型内联广告具有多个媒体文件，并且其中一个VPAID广告是第一个广告，则不会为实时流播放内联广告。 通过选取其他媒体文件来解决此问题。

* Zendesk #21021 — 延迟绑定音频，导致音频区段重复

**注意**：此问题需要Flash播放器21.0.0.240或更高版本。

音频重复问题已修复。

* Zendesk #21125 — 从实时/线性广告时间提前返回

**注意**：此问题需要Flash播放器21.0.0.240或更高版本。

此版本支持在广告时间播放到完成之前提前从广告时间返回。 通过自定义清单标记指示提前返回。

* Zendesk # 21369延迟绑定音频导致时间不一致

**注意**：此问题需要Flash播放器21.0.0.240或更高版本。

已修复的音频重复问题也已修复此问题。

* Zendesk #21760， 20921 — 在搜寻时取消音频视频同步。

**注意**：此问题需要Flash播放器21.0.0.240或更高版本。

已修复音频重复问题。

* Zendesk #22024 — 运行TVSDK时出错

已修复引用播放器未在启动时播放任何流并引发异常的问题。

**版本1.4.22** (791)

* Zendesk #17580 - Primetime运行时错误，代码为3357

**注意**：此问题需要Flash播放器21.0.0.197或更高版本。

修复了在调用storeVoucher()时通过正确初始化deviceID发生的随机3357错误。

* Zendesk #21334 — 第三方广告请求的TVSDK广告请求超时值

在此版本中，添加了全局广告请求超时。

**版本1.4.21** (782)

* Zendesk #19580 TVSDK会等待内容解析程序完成后再发送 `PTTimedMetadataChangedNotification` 通知

**注意**：此问题需要Flash播放器21.0.0.182或更高版本。

在桌面引用播放器中，通过设置广告标记并添加自定义机会生成器解决了此问题，该生成器显示了如何订阅自定义提示以及如何在VOD文件中处理这些提示。

* Zendesk #20806 DVR窗口中的未来中置广告在交换营地后不会触发

**注意**：此问题需要Flash播放器21.0.0.182或更高版本。

通过更新应用程序以设置_resource.metadata.setValue(DefaultMetadataKeys.ENABLE_LIVE_PREROLL， &quot;false&quot;)来禁用PIP交换中的前置广告插入，从而不生成前置广告机会，从而解决了此问题。

引入了排序功能，以修复导致主内容持续时间为负的乱序广告投放位置。

* Zendesk #20522：无法跳过VPAID 2.0广告

**注意**：此问题需要Flash播放器21.0.0.182或更高版本。

* 在广告宽恕期间跳过VPAID广告，解决了此问题。
* 当广告时间策略设置为跳过时，仍会调度广告和广告时间事件。 播放器状态不一致。

此问题已得到解决，在跳过广告时间时，表现正确且不会调度事件。

* Zendesk #20955通过机会生成器在customParameters属性中设置键值对

**注意**：此问题需要Flash播放器21.0.0.182或更高版本。

在为广告请求创建广告单元时，Auditude请求会解析自定义参数的AuditudeSettings 。

此行为已更改为将来自Opportunity对象的自定义参数包含在请求中。 此外，不能将具有不同自定义参数的多个机会打包到一个Auditude请求中。

* Zendesk #21227 - m3u8无法持续播放

**注意**：此问题需要Flash播放器21.0.0.211或更高版本。

通过允许TVSDK忽略清单（HLS子配置文件），来解决此问题，该清单包含TVSDK不支持的AC3编解码器（环绕）。

**版本1.4.20** (762)

* Zendesk #19181 — 特技快进到实时点锁定流。

**注意**：此问题需要Flash播放器20.0.0.306或更高版本。

* Zendesk #19286 — 在FER流中来回搜索时发生Flash Player崩溃。

**注意**：此问题需要Flash播放器20.0.0.306或更高版本。

如果查询获得响应所花费的时间过长或者套接字正在关闭，则通过关闭查询解决了在Google Chrome中搜索时发生的偶尔挂起问题。

* Zendesk #19305 — 播放具有A/V不连续性的流时遇到断断续续的播放。

**注意**：此问题需要Flash播放器20.0.0.306或更高版本。

通过报告警告解决了此问题。

* Zendesk # 19359 — 由于#EXT-X-FAXS-CM：属性在集级别清单中的位置，Flash Player崩溃。

当#EXT-X-FAXS-CM标记出现在顶部播放列表上，且位于播放列表中的单个比特率或区段之前，此问题已得到解决。

* Zendesk #19489 - Fast Forward to Live Point插件（实时流）

此问题与Zendesk #19181相同。

* Zendesk #19699 - TVSDK无法在WebVTT字幕跟踪之间切换

通过在跟踪更改时进行播放器转储并重新加载清单，以及通过更正影响双字节WebVTT描述跟踪名称的UTF8字符串转换问题，此问题已得到解决。

**版本1.4.19** (1.4.19.738)

* Zendesk #18234 -Flash Player崩溃播放CC中带有Unicode字符串的流

此问题需要Flash PlayerFP 20.0.0.267或更高版本，可以通过正确处理Unicode字符串来解决此问题。

* Zendesk #18304 — 对VPAID广告的流完整性支持

此功能需要Flash PlayerFP 20.0.0.267或更高版本，并已在1.4.19版中引入。

* Zendesk #18766 — 引用播放器无法在CC轨道名称中显示非拉丁Unicode字符

此功能需要Flash PlayerFP 20.0.0.267或更高版本，并已通过正确处理Unicode字符串得到修复。

* Zendesk #18804 - Firefox 42中的播放器崩溃

此问题需要Flash PlayerFP 20.0.0.235或更高版本，并且与Zendesk #18723的问题相同。

* Zendesk #18864 -Flash Player完全插件崩溃

此问题需要Flash PlayerFP 20.0.0.235或更高版本，与Zendesk #18723相同。

* Zendesk #18998 — 如果音频和视频时间戳不匹配，则会发生因中断而不断下载区段的情况。

通过忽略时间戳之间的间隔并仅播放下载的内容，此问题得以解决。

* Zendesk #19093 — 中置广告只能与实时和全事件重播(FER)内容一起观看一次，但在快速转发或搜寻超过广告时无法再次观看这些广告

在Primetime的默认adPolicy选择器中，如果观看了中置广告，则当您完成搜寻时，adBreak不会移动到搜索位置。 要再次播放广告，在搜寻之后，应用程序需要覆盖selectAdBreaksToPlay()函数。

* Zendesk #19101 — 回退到未解决的Midroll广告会移除广告投放。

通过允许播放器更新playbackMetrics time、minimumOpportunityTime和Timeline，此问题已得到解决。

* Zendesk #19102 - FER和特技模式问题

此问题需要Flash PlayerFP 20.0.0.267或更高版本，可通过正确设置advertisingMetadata.adSignalingMode来解决。

* Zendesk #19175 — 有时，在首次播放流时，前置广告不会显示。

通过为Ad请求超时向AuditudeSettings添加新的API adRequestTimeout，此问题已得到解决。 用户现在可以覆盖默认的10s广告请求超时。

**版本1.4.18** (1.4.18.722)

* Zendesk #3324 — 当VMAP中没有广告媒体时，Primetime广告报告不会跟踪广告时间。

当广告时间为空时，将不会触发广告时间开始和完成跟踪事件。 通过在空的广告时间（例如VMAP AdBreak）上发送广告时间开始Ping，并使用有效的AdSource节点来解决此问题。

**版本1.4.17** (1.4.17.702)

* Zendesk #17168 — 切换可见性后，字幕不会出现10秒左右

通过为vtt描述文件提供EXT-X-MEDIA-TIME标记支持，此问题得以解决。

* Zendesk #17983 — 未能下载清单的任何键会导致整个清单播放失败

**注意**：您必须至少具有Flash PlayerFP 19.0.0.245或更高版本。

有时在播放实时内容时，清单中可能包含无效的键（例如，对于封锁期），但其他时间范围可能包含有效的键，并且仍会播放。 以前，当未能下载清单中列出的键时，整个清单失败。 现在，清单仅在无法下载列出的所有键值时失败。 如果某些密钥有效，但某些密钥无法下载，则将播放内容。 如果我们尝试播放需要我们不具备的键的区段，我们仍然会失败。

* Zendesk #18554 — 流完整性在某些情况下，会减少Cookie

**注意**：您必须至少具有Flash PlayerFP 19.0.0.245或更高版本。

修复了Cookie操作代码中可能截断Cookie值的错误。

**版本1.4.16** (1.4.16.684)

* Zendesk #3732 — 在Chrome中添加对代理的支持，以实现流完整性(需要Flash PlayerFP 19.0.0.207或更高版本)

这是一个增强功能。

* Zendesk #4244 - PTS滚动更新的流问题

通过检测变换图像并管理每个有效负载类型的不连续性（不泛型），此问题已得到解决。

* Zendesk #4487 — 跟踪线性内容渠道

通过在线性流播放会话期间重新初始化视频心率跟踪器，解决了此问题。

* Zendesk #17427 -Adobe流完整性不能通过Chrome (Win7)上的代理工作()

**注意**：分辨率要求Flash PlayerFP 19.0.0.207或更高版本。

此问题与Zendesk #3732相同。

* Zendesk #17907 - pHLS Live Stream上的滞后，Flash Player为19

**注意**：分辨率要求Flash PlayerFP 19.0.0.207或更高版本。

通过处理在重新加载实时清单时TS文件域发生更改且文件下载两次的实时流，解决了此问题。

* Zendesk #17931 — 开头为石板的HLS内容无法播放

**注意**：分辨率要求Flash PlayerFP 19.0.0.207或更高版本。

通过在第一个TS文件的前2秒内处理没有音频的流解决了此问题。

* Zendesk #17934 -Flash为19.0.0.185的实时流式传输失败

**注意**：分辨率要求Flash PlayerFP 19.0.0.207或更高版本。

通过在区段边界上处理音频帧和视频帧之间具有时间交错的实时流，解决了此问题。

* Zendesk #17973 — 最新Flash Player19.0.0.185中置广告崩溃

**注意**：分辨率要求Flash PlayerFP 19.0.0.207或更高版本。

通过处理带有中置广告插入的未设为静音的音频，解决了此问题。 （发生解析器切换，并且在播放的任何时刻，内容将转换为中置广告或广告播放中间，依此类推。）

* Zendesk #18049 — 使用Firefox 42测试版导致Flash19崩溃

此问题与Zendesk #17973相同。

**版本1.4.15** (1.4.15.678)

* Zendesk #4377：因广告策略而跳过广告时间时触发AD_BREAK_SKIPPED事件。

修复方法是，如果跳过某个广告，则添加AD_BREAK_SKIPPED。

* Zendesk #4496 — 流完整性：重定向到令牌化流的错误102100。

修复了以下问题：添加对通过TVSDK设置AVNetworkConfiguration属性useCookieHeaderForAllRequests的支持。

* Zendesk #17179 -Flash播放器对加密内容的多个SAP更改发生崩溃。

修复了播放某些加密内容期间的崩溃问题。

**注意**：此修补程序需要Flash Player19.0.0.200或更高版本。

* Zendesk #17499 — 我们如何在观看后删除midroll ，但从源内容中删除preroll

向AdBreakTimelineItem添加了类型(AdBreakTimelineItem.placementType)，以便AdPolicySelector可以为前置式广告、中置式广告和后置式广告内容返回不同的策略。

* Zendesk #17665 — 带宽调节

修复了以下问题：在缓冲开始时，删除将目标缓冲区大小更改为初始缓冲区大小的逻辑。

**版本1.14.14** (1.4.14.771)

* Zendesk #17363 — 修复参考播放器的自述文件

   * 澄清有关下载和安装playerglobal.swc的说明。
   * 添加使用特定flash player版本更新项目配置的说明。
   * 更新AdvertisingOverlay项目配置以使用最低播放器版本。
   * 更新ReferenceCore项目配置以使用特定播放器版本11.9

* Zendesk #17471 — 播放器冻结

部分修复了广告在搜寻后不会从头开始播放的问题。

* Zendesk #17496 — 在DVR窗口中进行搜索时，未解析Podbuster

为每个广告时间提供自定义参数。

**版本1.4.13** (1.4.13.660)

* Zendesk #4037 — 无可用配置文件错误(需要Flash Player18.0.0.232或更高版本)

修复了查询参数包含“http”时的url解析问题

* Zendesk #4260 - IE11中的Flash Player18次崩溃(需要Flash Player18.0.0.232或更高版本)

修复了使用IE11以全屏模式播放视频时出现的崩溃

* Zendesk #4262 - Adobe Primetime播放器在windows 10上崩溃(需要Flash Player18.0.0.232或更高版本)

修复了在Windows上使用FireFox以全屏模式播放视频时出现的崩溃。

* iOS和桌面上的Zendesk #4279 - HLS TVSDK广告插入–302重定向问题

修复了URL由于没有扩展名而无法正确识别其类型的问题

* Zendesk #4306 — 仅在Win上全屏运行时Flash Player崩溃(需要Flash Player18.0.0.232或更高版本)

修复了在Windows上以全屏模式播放视频时出现的崩溃。

* Zendesk #4480 — 缺少ID3标记事件(需要Flash Player18.0.0.232或更高版本)

**1.4.12 **(1.4.12.656)

* Zendesk #2751 - CSAI和CRS |增强：处理某些媒体文件URL中的动态元素。

更新了Creative重新打包服务，以正确处理具有动态创意URL的广告。

* ptplay - 2114 - MP4播放支持。

现在支持MP4内容的基本播放，包括播放、暂停和搜寻。

以下内容需要Flash Player18.0.0.225或更高版本：

* Zendesk #3992 — 额外的TrickPlay速度。

TrickPlay现在接受高于16x的速率：+/- 32、+/-64和+/-128。

* Zendesk #3113 -Flash Player插件崩溃

修复了尝试在Mac Firefox上播放重定向广告时出现的崩溃。

* Zendesk #4037 — 无可用配置文件错误
* Zendesk #4262 - Adobe Primetime播放器在Windows 10上崩溃

修复了在全屏播放期间在Windows Firefox中崩溃的问题。

**版本1.4.11** (1.4.11.648)

* Zendesk #1869 — 更改字体大小时出现问题(需要Flash Player18.0.0.200)

允许在WebVTT字幕代码中使用字幕大小。

* Zendesk #3113 -Flash Player插件崩溃(需要Flash Player18.0.0.200)
* Zendesk #3268 — 台式机：视频播放器在+- 40/50秒后开始闪烁，并在+- 90秒后开始变黑(需要Flash Player18.0.0.200)

修复暂存视频错误。

* Zendesk #3670 — 在引用播放器中搜索时，VOD中出现INVALID_PARAMETER错误(需要Flash Player18.0.0.200)

检测到新时段时ThreadSeek中的InvalidateProfiles。

* Zendesk #3896 — 在Chrome上，将Stream Integrity设置为ON的Flash Player崩溃(需要Flash Player18.0.0.200)

修复了Pepper本机联网模式下的崩溃

* Zendesk #3905 — 在CDN上托管时，未加载TVSDK播放器

修复了pageDomain与swf域不同时查找通配符令牌的问题。

**版本1.4.10** (1.4.10.642)

* Zendesk #3249 - TVSDK Web Player在Firefox上导致Flash崩溃

修复了Mac上的Firefox偶尔出现Flash Player崩溃的问题，当时，在外部监视器上播放的流将切换到更高的比特率流。(需要Flash Player18.0.0.160)

* Zendesk #3268 — 桌面：视频播放器在以下时间后开始闪烁 `+-` 40/50秒后开始变黑 `+-` 90秒

修复了Mac Chrome上流开始闪烁并最终变为黑色的问题。 (需要Flash Player18.0.0.161)

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` 未填充宏

   * 如果内联广告的创意效果不佳，则会显示错误代码400。
   * `[ERRORCODE]` 宏将进行URL编码

* Zendesk #3601 — 增强请求：包装器配套管理

   * TVSDK将显示包含接近内联的资源（html、iframe或静态）的包装器伴随。 （如果内联不包含该大小的标记）
   * 除非用于显示，否则将忽略具有资源的包装器。 （不用于跟踪）
   * 只有不含资源的包装器同类才会用于跟踪目的。 （仅包含跟踪的包装器伙伴）

**版本1.4.9**

* Zendesk #2615 — 从桌面显示中删除HLS视图的问题

向MediaPlayer添加了clearVideo()方法。 通过从StageVideo对象中清除AVStream来清除显示的视频帧。 仅当视频已暂停时才应调用，并且必须先调用replaceCurrentResource或replaceCurrentItem，然后才能再次调用play()。

* Zendesk #3169 — 通过Adobe Analytics集成更新引用播放器

引用播放器已更新与Adobe Analytics的集成

* Zendesk #3296 — 桌面HLS TVSDK — 未播放大型第三方广告

HLS格式的MIME类型区分大小写，这不正确，已进行更改以使其不再区分大小写

**版本1.4.8**

* Zendesk #2737 — 桌面播放器 — 错误106000(需要Flash Player17.0.0.184)
* Zendesk #3007 — 更新到Flash Player17后不显示前置广告(需要Flash Player17.0.0.184)
* Zendesk #3085 — 桌面HLS播放器在60秒后引发106000错误(需要Flash Player17.0.0.184)

**版本1.4.7**

* Zendesk #2760 — 在TrickPlay模式中忽略DISCONTINUITY标记(需要Flash Player版本17.0.0.158)
* Zendesk #2760 — 在TrickPlay模式中忽略DISCONTINUITY标记(需要Flash Player版本17.0.0.158)

**版本1.4.6**

* Zendesk #2652 — 桌面HLS的Auditude文档，阐明了桌面HLS的Auditudemedia_id文档

**版本1.4.5**

* Zendesk #2256 — 访问主播放列表，更新了PSDK以便为主播放列表上的订阅标记调度timedMetadata事件。 (需要Flash Player版本17.0.0.134)
* Zendesk #2417 — 播放器尝试在播放开始之前下载字幕，WebVTT使用错误的区段编号变量进行区段编号匹配。 只有区段索引从零开始的媒体才会显示错误。 (需要Flash Player版本17.0.0.134)
* Zendesk #2537 — 在将Pepper插件与Chrome结合使用时，Flash播放器崩溃(需要Flash Player版本17.0.0.134)
* Zendesk #2547 — 阿拉伯字幕：文本应右对齐(需要Flash Player版本17.0.0.134)

**版本1.4.4**

* Zendesk #1561 — 回复： `[Adobe Primetime]` 更新：桌面PSDK中基于HLS客户端的故障转移支持PROGRAM-DATE-TIME(需要Flash Player版本16.0.0.305或更高版本)
* Zendesk #2197 - `[Ads]` 跟踪广告错误
* Zendesk #2286 — 功能请求：提供有关广告加载状态的信息(VPAID)
* Zendesk #2285 — 功能请求：在指定的超时持续时间后跳过广告
* 错误#3921755 - Flash Player中的OpenSSL库更新到版本1.0.1L(需要Flash Player版本16.0.0.305或更高版本)

**版本1.4.2**

* Zendesk #1303 — 隐藏式字幕的垂直偏移(需要Flash Player版本16.0.0.235或更高版本，预计发行日期：2014年12月)
* Zendesk #1870 — 隐藏式字幕打开和关闭(需要Flash Player版本16.0.0.235或更高版本，预计发行日期：2014年12月)
* Zendesk #2110 — 在VPAID广告期间尝试进入全屏后播放卡住(需要Flash Player版本16.0.0.235或更高版本，预计发布日期：2014年12月)
* Zendesk #2199 - `[VPAID]` 搜索过去的广告时间时，播放器未响应
* Zendesk #2358 — 回复： `[Analytics]` 章节数据不正确

**版本1.4.1**

* 更新了封锁API，使其与Android和iOS实施保持一致。

**版本1.4.0**

* Zendesk #1024 — 通过清单从流中删除广告的功能
* Zendesk #1423 - HLS播放失败锁定Flash Player（未报告错误）
* Zendesk #1674 — 未显示ClosedCaption，缺少0x03 ETX代码时显示正确的708字幕。

## 已知问题 {#known-issues}

* 隐藏式字幕不适用于纯音频内容，因为字幕系统需要视频才能工作。
没有视频，就没有视区尺寸；如果没有视区尺寸，您将无法显示任何用于字幕的图形。
* 由于Chrome沙盒限制，Google Chrome中的流完整性会略微变慢。
* 在TVSDK 1.4中，如果禁用自动播放，则当播放器保持空闲至少一分钟时，可能会发生DRM错误。 要解决此问题，当您禁用自动播放但预加载资产时，请修改 `ReferenceCore.as` 通过更改的内容 `onPlaybackManagerPrepared`：

```
if (_playbackManager.autoPlay) {
_playbackManager.play();
} else {
_playbackManager.play();
_playbackManager.pause();
}
```

* **版本1.4.13** PTPLAY-8501 — 当VMAP返回两个直接MP4非转码广告时，同一后退广告会播放两次。

* **版本1.4.2** 在Flash Player版本16版本中，当播放器进入空缓冲事件后，使用ABR“downiting down”逻辑发现了一个问题。 该问题会阻止在播放器进入缓冲状态后，在带宽较差的环境中切换比特率。 要解决此问题，请让应用程序设置 `BufferControlParameters.initialBufferTime` 与相同 `BufferControlParameters.playbackBufferTime` 在缓冲状态期间临时(即 `BufferEvent.BUFFERING_BEGIN` 事件)，然后将其重置回设置的值 `BufferEvent.BUFFERING_END` 事件。 此问题的修复将在Flash Player版本16的下一个修补程序版本中提供。

* **版本1.4.0**

   * PTPLAY-1634 — 同一订阅标记在不同的Live Windows中具有不同的时间戳。 当Live Windows移动时，每个窗口中的相同标记应具有相同的时间戳。 但是，有时候，相同的标记具有不同的时间戳。
   * PTPLAY-28 - MediaPlayer时间轴不包含空分隔符。
   * 需要跨域策略文件(crossdomain.xml)才能从其他域流式传输内容。 [为HTTP流设置crossdomain.xml文件](https://helpx.adobe.com/adobe-media-server/dev/configure-dynamic-streaming-live-streaming.html).
   * 错误#3694203 — 在DVR流中，从播放中置广告内部搜索另一个中置广告提示可能会导致浏览器冻结
   * 错误#3753725 — 如果观看了广告时间，则不会考虑selectPolicyForSeekIntoAd
   * 错误#3754529 — 在实时DVR流中重新搜索时，不会从流中删除前置广告
   * 错误#3761896 — 如果在广告播放期间允许搜寻，则广告标记将在搜寻后重新调整。 解决方法是在搜寻期间不使用ITEM_UPDATED回调
   * 错误#3779889 — 在Video Analytics中，到达特技播放的结尾时，不会进行完整调用
   * 错误#VA-779 — 没有为具有心率支持参考实施的增强视频分析发送比特率更改事件心率 — 在示例应用程序中未实施特技播放。

## 有用资源 {#helpful-resources}

* 请参阅完整的帮助文档，网址为 [Adobe Primetime学习与支持](https://helpx.adobe.com/support/primetime.html) 页面。

---
title: 适用于Android™的TVSDK 2.7发行说明
description: 适用于Android™的TVSDK 2.7发行说明介绍了TVSDK Android™ 2.7中的新增功能或更改功能、已解决和已知问题以及设备问题
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: d64f0ef2-60a9-43a1-b2f9-44764a570538
source-git-commit: 59ea8008c828f3bdf275fea5cc2a59c37b0c4845
workflow-type: tm+mt
source-wordcount: '4037'
ht-degree: 0%

---

# 适用于Android™的TVSDK 2.7发行说明 {#tvsdk-for-android-release-notes}

适用于Android™的TVSDK 2.7发行说明介绍了TVSDK Android™ 2.7中的新增功能或更改功能、已解决和已知问题以及设备问题

## TVSDK Android™ 2.7 {#tvsdk-android}

Android™引用播放器随Android™ TVSDK一起提供，位于您分发的samples/目录中。 随附的README&lt;.md文件说明了如何构建引用播放器。

>[!NOTE]
>
>要成功构建引用播放器（如随发行版一起分发的README.md中所述），请确保执行以下操作：
>
>1. 从下载VideoHeartbeat.jar [https://github.com/Adobe-Marketing-Cloud/media-sdks/releases](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) (适用于Android™ v2.0.0的VideoHeartbeat库)
>1. 将VideoHeartbeat.jar解压到libs/文件夹中。

>


## 新增功能 {#new-features}

适用于Android™的TVSDK 2.7包含版本1.4的所有功能，但下面列出的不支持的功能除外 [功能矩阵](#feature-matrix).

**Android™ TVSDK 2.7**

* **并行广告解析支持**

TVSDK 2.7支持在广告时间并发解析所有广告请求，而不是连续解析。

### 以前版本中的新增功能 {#new-features-previous-releases}

**版本2.5.6**

* **TVSDK 2.5支持Android™ P**
* **启用背景音频**

   要在应用程序从前台移动到后台时启用音频播放，当播放器处于“准备”状态时，应用程序应调用MediaPlayer的enableAudioPlaybackInBackground API，并将true作为参数。

* **MediaPlayer类中的alwaysUseAudioOutputLatency(boolean val)**

设置后，在音频时间戳计算中使用输出延迟。
布尔参数val - True在计算音频时间戳时使用音频输出延迟。

* **优化后，即使带宽速度突然下降，也能获得最佳的播放体验。**
现在，TVSDK会在必要时取消持续区段的下载，并动态切换到相应的演绎版。 这是通过在比特率之间无缝切换而不中断来完成的。

**版本2.5.5**

* **部分广告时间插入**

   在广告中间加入时不触发部分已观看广告的跟踪的类似电视体验。\
   示例：用户在包含三个30秒广告的90秒广告时间的中间（40秒）加入。 这是时间中第二个广告的10秒。
   * 第二个广告在剩余的持续时间（20秒）内播放，随后是第三个广告。
   * 不会触发播放的部分广告（第二个广告）的广告跟踪器。 仅触发第三个广告的跟踪器。

* **通过HTTPS安全加载广告**

   Adobe Primetime提供了一个选项，用于请求首次调用primetime广告服务器和通过https的CRS。

* **添加到CRS请求的AdSystem和创作ID**

   * 现在包括 `AdSystem` 和 `CreativeId` 作为1401和1403请求中的新参数。

* **删除了NetworkConfiguration类中的API setEncodeUrlForTracking** 因为URL中的不安全字符应进行编码。

**版本2.5.4**

Android™ TVSDK v2.5.4提供了以下更新和API更改：

* 默认值的更改 `WebViewDebbuging`

   的 `WebViewDebbuging` 值设置为 _False_ 默认情况下。 要启用此功能，请调用 `setWebContentsDebuggingEnabled` to _True_ 中。

* OpenSSL和Curl版本升级已更新 `libcurl` 到v7.57.0和OpenSSL到v1.0.2k。
* 对VAST响应对象的应用程序级别访问引入了一个新的API NetworkAdInfo:getVastXml()，该API提供对应用程序的VAST响应对象的访问。

**版本2.5.3**

Android™ TVSDK v2.5.3提供了以下更新和API更改。

* 我们鼓励所有使用CRS的TVSDK客户使用TVSDK 2.5.3.85或Android™上的最新版本升级其应用程序。 这是现有应用程序实施的下拉插件替换。 升级TVSDK后，在代理工具中检查CRS创作URL请求(例如：Charles)，并确认路径中的主机名和版本与以下示例URL结构中的显示方式相同。

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* TVSDK的用户代理可自定义：我们添加了一些用于自定义用户代理的新API。

   * `setCustomUserAgent`（字符串值）
   * `getCustomUserAgent`()

* 在Android™应用程序和TVSDK之间共享Cookie:Android™ TVSDK现在支持在Java™层(存储在Android™应用程序的CookieStore中)和C++ TVSDK层之间访问Cookie。 现在，可以在本机C++层中设置和/或修改Cookie，因为它们会公开到Java™ Cookie存储区。
* API更改：

   * 添加了新的事件CookiesUpdatedEvent。 更新Cookie后，媒体播放器会调度该Cookie。
   * 将新API添加到 `NetworkConfiguration::set/ getCustomUserAgent()` 使用自定义用户代理。
   * 将新API添加到 `NetworkConfiguration::set/ getEncodedUrlForTracking` 强制对不安全字符进行编码。
   * 将新API添加到 `NetworkConfiguration::getNetworkDownVerificationUrl()` 设置网络验证URL（如果存在故障转移）。
   * TextFormat::treatSpaceAsAlphaNum中添加了一个新属性，此属性定义在显示字幕时是否将空格视为字母数字。

* 更改 `SizeAvailableEvent`:以前，的getHeight()和getWidth()方法 `SizeAvailableEvent` 在2.5.2中，用于返回由媒体格式返回的帧高和帧宽。 现在，它分别返回由解码器返回的输出高度和输出宽度。
* 缓冲行为的更改：缓冲行为已更改。 如果存在空缓冲区，则将其留给应用程序开发人员处理他们要执行的操作。 2.5.3在缓冲空时使用播放缓冲区大小。

**版本2.5.2**

Android™ TVSDK v2.5.2提供了重要的错误修复和一些API更改。

**版本2.5.1**

Android™ 2.5.1中发布的重要新增功能。

* **性能改进**&#x200B;新的TVSDK 2.5.1架构改进了性能。 根据来自第三方基准测试研究的统计数据，新架构提供的启动时间比行业平均值减少5倍，丢帧数减少3.8倍：

   * **适用于VOD和实时视频点播的即时 —** 启用“即时”时，TVSDK会在播放开始之前初始化和缓冲媒体。 由于您可以在后台同时启动多个MediaPlayerItemLoader实例，因此可以缓冲多个流。 当用户更改渠道，并且流已正确缓冲时，新渠道上的播放会立即开始。 TVSDK 2.5.1还支持用于的Instant On **live** 流。 当实时窗口移动时，将重新缓冲实时流。

      * **改进了ABR逻辑 —** 新的ABR逻辑基于缓冲长度、缓冲长度变化率和测量的带宽。 这确保ABR在带宽波动时选择正确的比特率，并且还通过监视缓冲长度变化的速率来优化比特率切换实际发生的次数。
      * **部分区段下载/子分段 —** TVSDK会进一步减小每个片段的大小，以便尽快开始播放。 其片段必须每两秒有一个关键帧。
      * **延迟广告解析 —** TVSDK在开始播放之前不会等待非前置广告的分辨率，从而缩短启动时间。 在解决所有广告之前，仍不允许使用搜寻和特技播放等API。 这适用于与CSAI一起使用的VOD流。 在广告解决完成之前，不允许执行搜寻和快进等操作。 对于实时流，无法在实时事件期间为广告分辨率启用此功能。
      * **永久性网络连接 —** 此功能允许TVSDK创建和存储永久网络连接的内部列表。 这些连接会重复用于多个请求，而不是为每个网络请求打开一个新连接，然后在此之后销毁它。 这可以提高网络代码的效率并减少延迟，从而提高播放性能。
当TVSDK打开连接时，它会向服务器询问 *保持活力* 连接。 某些服务器可能不支持此类连接，在这种情况下，TVSDK会返回为每个请求再次建立连接。 此外，虽然默认情况下会打开永久连接，但TVSDK现在有一个配置选项，以便应用程序可以根据需要关闭永久连接。
      * **并行下载 —** 以并行方式而不是以串联方式下载视频和音频可减少启动延迟。 此功能允许播放HLS实时文件和VOD文件，优化服务器的可用带宽使用情况，降低在运行情况下进入缓冲区的概率，并最大限度地减少下载和播放之间的延迟。
      * **并行广告下载 —** TVSDK在点击广告中断之前预取与内容播放并行的广告，从而实现广告和内容的无缝播放。

* **播放**

   * **MP4内容播放 —** 无需重新编码MP4短剪辑即可在TVSDK中播放。
注意：MP4播放不支持ABR切换、特技播放、广告插入、延迟音频绑定和子分段。
   * **使用自适应比特率(ABR)进行特技播放 —** 此功能允许TVSDK在特技播放模式下在iFrame流之间切换。 您可以使用非iFrame配置文件以较低的速度进行特技播放。
   * **更流畅的技巧游戏 —** 这些改进可增强用户体验：

          *在特技播放期间根据带宽和缓冲配置文件选择自适应比特率和帧速率
          *使用主流而不是IDR流，可快速播放多达30 fps。
      
* **内容保护**

   * **基于分辨率的输出保护 —** 此功能将播放限制与特定分辨率绑定，从而提供更细粒度的DRM控件。

* **工作流支持**

   * **直接计费集成 —** 这会将帐单量度发送到Adobe Analytics后端，该后端由Adobe Primetime针对客户使用的流进行认证。
TVSDK会自动收集量度，并遵守客户销售合同，以生成计费所需的定期使用报告。 在每个流开始事件中，TVSDK都使用Adobe Analytics数据插入API将计费量度（如内容类型、广告插入启用标记和基于可计费流持续时间的DRM启用标记）发送到Adobe Analytics Primetime拥有的报表包。 这不会妨碍或包含在客户自己的Adobe Analytics报表包或服务器调用中。 此账单使用情况报表会根据请求定期发送给客户。 这是付费功能的第一阶段，仅支持使用计费。 可以使用文档中描述的API根据销售合同进行配置。 此功能默认处于启用状态。 要关闭此功能，请参阅引用播放器示例。
   * **改进了故障转移支持 —** 实施了其他策略以继续无中断播放，尽管主机服务器、播放列表文件和区段出现故障。

* **广告**

   * **Moat集成 —** 支持从Moat中测量广告可见度。
   * **伴随横幅 —** 伴随横幅显示在线性广告旁边，并且通常在广告结束后继续显示在视图上。 这些横幅的类型可以是html(HTML代码片段)或iframe（指向iframe页面的URL）。

* **Analytics**

   * **VHL 2.0 -** 这是最新的优化视频心率库(VHL)集成，可自动收集Adobe Analytics的使用数据。 为简化实施，API的复杂性已降低。 下载VHL库 [适用于Android™的v2.0.0](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) 并解压缩libs文件夹中的JAR文件。

* **SizeAvaliableEventListener**
   * SizeAvailableEvent的getHeight()和getWidth()方法现在将分别以高度和宽度返回输出。 显示长宽比可按如下方式计算：

      ```
      SizeAvailableEvent e;
      
      DAR = e.getWidth()/ e.getHeight();
      
      Storage Aspect Ratio in terms of Sar width and Sar height can also be used to calculate Frame width and Frame height:
      
      SAR = e.getSarWidth()/e.getSarHeight();
      
      frameHeight = e.getHeight();
      
      frameWidth = e.getWidth()/SAR;    
      ```

* **Cookie**

   * Android™ TVSDK现在支持访问存储在Android™应用程序CookieStore中的Java™ Cookie。 当新Cookie作为“Set-Cookie”响应标头的一部分提供时，将提供一个回调API(onCookieUpdated)进行记录。 通过使用CookieStore在该特定URI/域上设置这些Cookie值，这些Cookie可用作其他URI/域使用的HttpCookie列表。 同样，TVSDK中的Cookie值也会使用CookieStore添加API进行更新。

## 特征矩阵 {#feature-matrix}

适用于Android™的TVSDK支持各种可实施的功能，以向视频应用程序添加功能。

在以下功能表中，“Y”表示当前版本支持该功能。

| 功能 | 内容类型 | HLS |
|---|---|---|
| 常规播放（播放、暂停、搜寻） | VOD +实时 | Y |
| FER — 常规播放（播放、暂停、搜寻） | 层VOD | Y |
| 在广告播放时进行搜寻 | VOD +实时 | 不支持 |
| AC3 | VOD +实时 | 不支持 |
| MP3 | VOD | 不支持 |
| MP4内容播放 | VOD | Y |
| 自适应比特率切换逻辑 | VOD +实时 | Y |
| 仅音频播放 | VOD +实时 | Y |
| 多CDN支持 | VOD +实时 | 不支持 |
| 使用纯音频媒体播放广告 | VOD +实时 | 不支持 |
| 隐藏式字幕 — 608/708 | VOD +实时 | Y |
| 隐藏式字幕 — WebVTT | VOD +实时 | Y |
| 清单故障转移 | VOD +实时 | Y |
| 高级故障切换 | VOD +实时 | Y |
| QoS和播放器通知 | VOD +实时 | Y |
| 支持Cookie标头 | VOD +实时 | Y |
| 支持自定义HTTP头 | VOD +实时 | Y（需要将其添加到允许列表） |
| 设置缓冲控制参数 | VOD +实时 | Y |
| 设置自适应比特率控制 | VOD +实时 | Y |
| 自定义清单标记 | VOD +实时 | Y |
| 延迟音频绑定 | VOD +实时 | Y |
| 302重定向 | VOD +实时 | Y |
| 带偏移的播放 | VOD +实时 | Y |
| 仅播放音频 | VOD +实时 | Y |
| 技巧游戏 | VOD +实时 | Y |
| 特技游戏中的慢动作 | VOD +实时 | 不支持 |
| 平滑技巧播放（使用ABR） | VOD +实时 | Y |
| ID3解析 | VOD +实时 | Y |
| 广告封锁 | VOD +实时 | 不支持 |
| 即时启用 | VOD +实时 | 不支持 |
| 不连续标记支持 | VOD +实时 | Y |
| 302重定向吸引力 | VOD +实时 | Y |

| 功能 | 内容类型 | HLS |
|---|---|---|
| 常规播放，已启用广告 | VOD +实时 | Y |
| 启用广告的FER内容 | VOD | Y |
| 默认广告行为 | VOD +实时 | Y |
| VAST 2.0/3.0 | VOD +实时 | Y |
| VMAP 1.0 | VOD +实时 | Y |
| MP4广告 | VOD +实时 | Y（来自CRS） |
| 启用广告的特技播放 | VOD +实时 | Y |
| 仅限广告 | VOD | Y |
| 定位参数 | VOD +实时 | Y |
| 自定义参数 | VOD +实时 | Y |
| 自定义广告行为 | VOD +实时 | Y |
| 自定义广告标记 | 实时 | Y |
| 自定义广告解析器 | VOD +实时 | Y |
| 自由轮自定义广告解析程序 | VOD | Y |
| C3 | VOD +实时 | 不支持 |
| 延迟广告解析 | VOD | Y |
| 不连续标记支持 — SSAI | VOD +实时 | Y |
| 伴随广告、横幅广告和可点击广告 | VOD +实时 | Y |
| VPAID 2.0 | VOD +实时 | Y(JS) |
| 抢先广告退出 | 实时 | Y |
| 基于规则的创意优先级 | VOD +实时 | Y |
| CRS规则 | VOD +实时 | Y |
| JSON广告解析程序 | VOD +实时 | 不支持 |
| Moat集成 | VOD +实时 | Y |

| 功能 | 内容类型 | HLS |
|---|---|---|
| AES加密 | VOD +实时 | Y |
| 示例AES加密 | VOD +实时 | Y |
| 标记化流 | VOD +实时 | Y |
| DRM | VOD +实时 | 仅限Primetime DRM(未来：维德维内) |
| 外部播放(RBOP) | VOD +实时 | 仅限Primetime DRM |
| 许可证轮换 | VOD +实时 | 仅限Primetime DRM |
| 键旋转 | VOD +实时 | 仅限Primetime DRM |

| 功能 | 内容类型 | HLS |
|---|---|---|
| Adobe Analytics VHL集成 | VOD +实时 | Y |
| 帐单 | VOD +实时 | Y |

## 已解决的问题 {#resolved-issues}

如果分辨率与报告的问题相关，则会显示Zendesk引用，例如ZD#xxxxx

**Android™ TVSDK 2.7**

本节概述TVSDK 2.7版本中解决的问题。

* ZD#37166 — 即使广告播放正常，也会触发错误跟踪调用。
* ZD#37134 — 返回错误的广告ID，以防在VMAP响应中包装器(3P)广告存在多个广告。

**Android™ TVSDK 2.5.6**

* ZD #34992 — 隐藏式字幕中的语言为空。
   * 修复了TVSDK未从主清单解析#EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS的情况，以获取字幕跟踪详细信息。
* ZD #35078 - Android P验证。
   * TVSDK 2.5.6已通过最新的Android™ P测试版内部版本进行验证。 由于新的Android™操作系统，未发现任何问题。
* ZD #34149 — 即使遇到错误，播放器仍继续显示请求。
   * 修复了即使所有配置文件都关闭，TVSDK仍会进行重复调用的情况（404错误）。
* ZD #31533 — 在应用程序发送到后台后，在Android™上播放音频。
   * 添加了 `enableAudioPlaybackInBackground` MediaPlayer的API，应使用“True”作为参数（当播放器处于PREPARED状态时）来调用该API，以便在应用程序处于后台时允许播放音频。

**Android™ TVSDK 2.5.5**

* ZD #21647 — 当视频实际大小为640x360时，Android TVSDK会通知640x368。
   * 由于变量m_nOutputHeight（在AndroidMCVideoDecoder内）已更新帧高而不是实际输出高度。 对函数getVideoFrame进行了相关更改，以正确计算m_nOutputHeight。
* ZD #26614 — 紧急 — 第三方广告投放/程序化 — 无法提供展示次数。
   * 通过处理XML解析中的情况，增强了之前的修复，当“空格”位于“等号”(如 &lt;vast version=&quot;2.0&quot;>
* ZD #29296 - Android:向CRS请求添加AdSystem和创作ID。
   * 现在，在1401和1403请求中包含“AdSystem”和“CreativeId”作为新参数。
* ZD #33062 - TVSDK在CDATA节点下的VAST响应中出现管道字符时崩溃
   * NetworkConfiguration类中的API setEncodeUrlForTracking作为要编码的URL中不安全的字符被删除。
* ZD #33063 - CRS文件选择逻辑已损坏 — TVSDK未发送CRS的webm格式请求，而是发送3gpp文件的CRS请求。
   * 现在已修复逻辑。 在将媒体文件与webm和3gpp格式结合使用时，将为webm发送CRS请求。 同时使用3gpp格式的媒体文件时，将为最高比特率的3gpp文件发送CRS请求。
* ZD #33125 - Android应用程序在VMAP中因特定DoubleClick标记而崩溃。
   * 修复了方案以避免崩溃。
* ZD #32256 — 许可证轮换和密钥轮换问题 — Adobe访问。
   * 修复了使用SampleAES内容的DRM元数据进行区段初始化的问题。 适用于AES128内容。
* ZD #33619 — 快速转发不断增长的播放列表内容，该内容在接近实时点的缓冲状态中卡住。
   * 在特技播放模式中跨越实时点时处理该案例。
* ZD #34151 - TimedMetadata对象无序。
   * 如果两个TimedMetadata事件属于时间轴中的同一时间，则它们会按随机顺序显示。 维护清单中的原始顺序。
* ZD #34189 — 搜寻广告时间开始时出现问题。
   * 问题出在使用不连续性拼合的SSAI广告。 原因是当我们寻找这些广告的开头，我们搜索一个关键帧，却找不到它时，我们就会发现。 原因是广告的最低音频时间戳早于最低视频时间戳。 因此，我们最终在错误的fragmentDump数据中搜索一个关键帧。 现已修复。
* ZD #34528 — 在FireTV第三代转换器上，视频分辨率不超过640x360。
   * 增强了修复功能，以包含最新的固件更新。
* ZD #34793 - TVSDK 2.5.x在VideoEngine假定auditudeSettings可用且不可用时，有时会与自定义内容解析程序一起崩溃。
   * 由于对空共享指针(auditudeSettings)的函数调用，导致崩溃。 在VideoEngineTimeline::placeToSourceTimeline()中添加了条件检查，以确保在对该对象调用任何内容之前，可使用auditudeSettings。
* ZD #32584 — 无法访问 &lt;extensions> VAST响应的节点。
   * 修复了与XML解析有关的问题，现在NetworkAdInfo提供了 &lt;extensions> 节点。
* ZD #35086 — 如果存在特定的VMAP响应，则无法从播放器获取完整的扩展数据。
   * 问题特定于扩展xml，因为如果扩展xml在属性值中有双引号，则XML解析不起作用。 修复了问题。

**Android™ TVSDK 2.5.4**

* ZenDesk#33659 — 启用Webview远程调试的播放会话。
   * 默认情况下，WebViewDebuging设置为False。 要启用调试，请使用setWebContentsDebuggingEnabled(true)通过应用程序将设置为true。
* ZenDesk#33011 — 如果存在失败的CRS请求，则广告时间轴无法解析。
   * 当对广告的CRS请求失败时，时间轴会得到解析，剩余的广告会被播放。
* ZenDesk#34528 — 在FireTV第三代转换器上，视频分辨率不会升级到640x360以上。
   * 视频分辨率会随着比特率的变化而增大。
* ZenDesk#33192 — 当通过AudioUpdatedEventListener::onAudioUpdated检索跟踪时， AudioTrack具有空名称。
   * 在FireTV Stick上的一些情况下，当没有实际音频更新时，onAudioUpdate事件会被触发。 此问题现已修复。

**Android™ TVSDK 2.5.3**

* Zendesk#32216 - TimedMetadata自定义标记订阅无法正常使用。
   * 我们将ID3数据作为字节数组（用于支持APIC或通用数据）返回给客户端，而在1.4中返回字符串。 字节数组不处理以空值结尾的字符本身，因此它向客户端显示特殊字符。 此问题现已修复。
* Zendesk#32670 — 播放器没有故障切换到冗余播放列表
   * 现在运行正常，并且setNetworkDownVerificationUrl可按预期工作。
* Zendesk#32369 — 隐藏式字幕显示不同的颜色垃圾或伪像。
   * CC故障的问题已在最新版本中修复
* Zendesk#25590 — 增强：TVSDK Cookie存储(从C++到Java™)
   * Android™ TVSDK现在支持在Java™层(存储在Android™应用程序的CookieStore中)和C++ TVSDK层之间访问Cookie。
* Zendesk#32252 - TVSDK_Android_2.5.2.12似乎没有修复PTPLAY-20269。此问题已修复并集成到2.5.2分支。
* Zendesk#31806 — 由于响应xml具有空标记，PREPARING Player中的Auditude棒卡在“正在准备”状态。 现在问题已修复。
* Zendesk#31727 - TVSDK 2.5隐藏式字幕字符被丢弃或拼写错误。
   * 问题已修复，我们未删除/错误拼写任何字符。
* Zendesk#31485 - DrmManager 2.5版
   * 通过新的DrmManager（上下文）创建DrmManager时出现一些问题。 实施了将提供DRMManager的DRMService类。
* Zendesk#32794- 1080P分辨率流在Android™上不播放。
   * 我们更改了SizeAvailableEvent。 以前， `getHeight()` 和 `getWidth()` 2.5中用于返回由媒体格式返回的帧高和帧宽的SizeAvailableEvent方法。 现在，它将分别返回解码器返回的输出高度和输出宽度。
* Zendesk #19359Flash Player因设置级别清单中#EXT-X-FAXS-CM属性的位置而崩溃。
   * 在播放列表中出现单个比特率或区段之前，#EXT-X-FAXS-CM标记必须始终显示在顶部的播放列表中。

**Android™ TVSDK 2.5.2**

* Zendesk#17305带有非不透明背景的隐藏式字幕中的工件。
将显示TextFormat中的setTreatSpaceAsAlphaNum属性。 默认情况下，属性为False。 在客户端中将属性设置为True可解决深空问题。

* Zendesk#25097 CC显示器具有带有CC设置的可视工件。
将显示TextFormat中的setTreatSpaceAsAlphaNum属性。 默认情况下，属性为False。 在客户端中将属性设置为True可解决深空问题。

* TVSDK播放器外的Zendesk #31620用户代理字符串会被截断。
用户代理字符串将在128个字符后不再被截断。
Adobe Primetime版本字符串已添加到系统用户代理。

* Zendesk #30809 Missing SEEK_END事件阻止应用程序转换到播放状态。
* 与以前的Primetime TVSDK版本相比，Zendesk #30415 Closed Caption的“青色”颜色现在更深，为蓝色（绿松石）。

   颜色从“深青”更改为“青”。

* Zendesk #30727 VOD广告无法下载/解析。

   在VMAP XML中，如果存在空的VAST标记且没有明确的结束标记(“&lt;/vast>&#39;)，并且后面没有换行符，则VMAP XML无法正确解析，广告可能无法播放。

**Android™ TVSDK 2.5.1**

* 特定于设备(Samsung Galaxy Tab 4)崩溃；包含Auditude的VOD DRM LBA，然后单击广告。
* VHL — 从偏移开始内容时，发送的心率调用不正确。
* 播放VPAID广告时，VHL心率会调用事件:type:播放广告缺失。
* 进入“完成”状态后，播放器将通过SKIP adBreakPolicy返回到后置广告的“正在播放”状态。
* Cookie未附加到传出广告回调。
* 广告提示点不可见。
* 不会加载具有单独EAC3 SAP跟踪的HLS。
* 在媒体播放器恢复后，播放器崩溃，因为TVSDK会收到“Screen On”（屏幕开启）意图。

## 已知问题和限制 {#known-issues-and-limitations}

**Android™ TVSDK 2.7**

* TVSDK 2.7支持最多五个广告的并行解析。
* 在VMAP响应时，单个广告时间中的广告调用会同时进行，并且广告时间会按顺序进行解析。
* 对于FER，将同时解决每个机会中的广告调用。

### 以前版本中的已知问题和限制{#known-issues-limitations-previous-releases}

**Android™ TVSDK 2.5.6**

* 不支持同时多个VMAP广告时间。

**Android™ TVSDK 2.5.3**

此版本存在以下问题：

* 实时视频播放在低端设备上可能出现音频 — 视频同步问题或网络状况不佳。
* 对于FER流，virtualTime和localTime可能不同。 此外，具有偏移的FER不起作用。
* 搜寻“延迟绑定音频”内容时，播放可能卡住。
* 对于实时内容，webVTT字幕可能会间歇性地变得不同步。
* 在从广告时间传出后，可以间歇性地快速播放少数帧。
* 有时，即使播放了广告，三包装广告中断也会引发303错误。

**Android™ TVSDK 2.5.2**

此版本存在以下问题：

* 实时视频播放在低端设备上可能出现音频 — 视频同步问题。
* 当搜索到VOD媒体的结尾时，播放可能会停止。
* 对于FER流，virtualTime和localTime可能不同。 此外，具有偏移的FER不起作用。

**Android™ TVSDK 2.5.1**

此版本的TVSDK存在以下问题：

* 实时视频播放在低端设备上可能出现音频 — 视频同步问题。
* 对于FER流，virtualTime和localTime可能不同。 此外，具有偏移的FER不起作用。
* 在VMAP XML中，如果存在空的VAST标记，且没有明确的结束标记(&lt;/vast>)，并且在后面没有换行符，则VMAP XML将无法正确解析，广告可能无法播放。
* 不支持VPAID后置显示。

## 有用资源 {#helpful-resources}

* [系统要求](/help/programming/tvsdk-2.7-for-android/c-psdk-android-2.7-requirements.md)
* [适用于Android™的TVSDK 2.7程序员指南](/help/programming/tvsdk-2.7-for-android/overview-prod-audience-guide/c-psdk-android-2.7-overview-prod-audience-guide.md)
* [TVSDK Android™ Javadoc for API参考](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html)
* [TVSDK Android™ C++ API文档](https://help.adobe.com/en_US/primetime/api/psdk/cpp/namespaces.html)  — 每个Java™类都有相应的C++类，而C++文档包含比Java™文档更多的解释性材料，因此请参阅C++文档，以深入了解Java™ API。
* [适用于Android™(Java™)的TVSDK 1.4到2.5迁移指南](/help/migration-guides/tvsdk-14-25-android.md)
* 有关处理屏幕开启/关闭方案的信息，请参阅 `Application_Changes_for_Screen_On_Off.pdf` 文件。
* 请参阅以下完整帮助文档： [Adobe Primetime学习与支持](https://experienceleague.adobe.com/docs/primetime.html) 页面。

---
title: TVSDK 2.7 for Android发行说明
description: TVSDK 2.7 for Android发行说明描述了TVSDK Android 2.7中的新增或更改功能、已解决和已知问题以及设备问题
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '4095'
ht-degree: 0%

---


# TVSDK 2.7 for Android发行说明{#tvsdk-for-android-release-notes}

TVSDK 2.7 for Android发行说明描述了TVSDK Android 2.7中的新增或更改功能、已解决和已知问题以及设备问题

## TVSDK Android 2.7 {#tvsdk-android}

Android参考播放器随Android TVSDK一起提供，位于您的分发的samples/目录中。 随附的README&lt;.md文件介绍了如何构建参考播放器。

>[!NOTE]
>
>要成功构建引用播放器（如随发行版分发的README.md中所述），请确保您执行以下操作：
>
>1. 从[https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases)下载VideoHeartbeat.jar（用于Android v2.0.0的VideoHeartbeat库）
>1. 将VideoHeartbeat.jar解压到libs/文件夹中。

>



## 新增功能{#new-features}

适用于Android的TVSDK 2.7包含版本1.4的所有功能，但[功能矩阵](#feature-matrix)下不支持的功能除外。

**Android TVSDK 2.7**

* **并行广告分辨率支持**

TVSDK 2.7支持在广告分段内并发解决所有广告请求，而不是顺序解决。

### 先前版本{#new-features-previous-releases}中的新增功能

**版本2.5.6**

* **TVSDK 2.5支持Android P**
* **启用背景音频**

   要在应用程序从前台移动到后台时启用音频播放，应用程序应在播放器处于PREPARED状态时调用MediaPlayer的enableAudioPlaybackInBackground API，参数为true。

* **alwaysUseAudioOutputLatency(boolean val)（在MediaPlayer类中）**

设置后，在音频时间戳计算中使用输出延迟。
布尔参数值 — True将在音频时间戳计算中使用音频输出延迟。

* **经过优化，即使带宽速度突然关闭，也能获得最佳播放体验。**
TVSDK现在取消当前区段的下载（如有需要），并动态切换至相应的再现。这是通过在比特率之间无中断地切换来实现的。

**版本2.5.5**

* **部分广告中断插入**

   加入广告中间而不触发部分观看广告的跟踪的电视体验。\
   示例**:**用户在包含3则30秒广告的90秒广告分时段中间（40秒）加入。 这是分时段的第二个广告。
   * 第二个广告在剩余的持续时间（20秒）内播放，然后是第三个广告。
   * 不会触发已播放的部分广告（第二个广告）的广告跟踪器。 仅触发第三个广告的跟踪器。

* **通过HTTPS安全广告加载**

   Adobe Primetime提供了通过https请求对primetime广告服务器和CRS的首次调用的选项。

* **添加到CRS请求的AdSystem和Creative Id**

   * 现在，在1401和1403请求中将“AdSystem”和“CreativeId”作为新参数。

* **NetworkConfiguration类中的API setEncodeUrlForTracking删** 除了URL中不安全的字符应进行编码。

**版本2.5.4**

Android TVSDK v2.5.4优惠以下更新和API更改：

* WebViewDebuging默认值的更改
默认情况下，WebViewDebuging值设置为False。 要启用它，请在应用程序中调用setWebContentDebuggingEnabled(true)。
* OpenSSL和Curl版本升级
已将libcurl更新为v7.57.0和OpenSSL更新为v1.0.2k。
* VAST响应对象的应用程序级访问
引入了一个新的API NetworkAdInfo::getVastXml()，它提供对应用程序的VAST响应对象的访问。

**版本2.5.3**

Android TVSDK v2.5.3优惠以下更新和API更改。

* 我们鼓励所有使用CRS的TVSDK客户使用TVSDK 2.5.3.85或最新的Android版升级其应用程序。 这将替换现有应用程序实施的插件。 TVSDK升级后，在代理工具中检查CRS创意URL请求(例如：并确认路径中的主机名和版本反映如下示例URL结构中。

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* TVSDK的用户代理可自定义：我们添加了一些新的API来自定义用户代理。

   * setCustomUserAgent（String值）
   * getCustomUserAgent()

* 在Android应用程序和TVSDK之间共享Cookie:Android TVSDK现在支持在JAVA层（存储在Android应用程序的CookieStore中）和C++ TVSDK层之间访问Cookie。 现在，可以在本机C++层设置和/或修改Cookie，因为它们将暴露在Java Cookie商店中。
* API更改：

   * 添加了新的事件CookiesUpdatedEvent。 它在更新其Cookie时由媒体播放器调度。
   * 新的API添加到NetworkConfiguration::set/getCustomUserAgent()以使用自定义用户代理。
   * NetworkConfiguration::set/getEncodedUrlForTracking中添加了一个新API，以强制对不安全字符进行编码。
   * NetworkConfiguration::getNetworkDownVerificationUrl()中添加了一个新API，用于在发生故障转移时设置网络验证URL。
   * TextFormat::treatSpaceAsAlphaNum中添加了一个新属性，该属性定义在显示字幕时是否将空间视为字母数字。

* SizeAvailableEvent中的更改：以前，2.5.2中SizeAvailableEvent的getHeight()和getWidth()方法用于返回由媒体格式返回的帧高和帧宽。 现在，它分别返回解码器返回的输出高度和输出宽度。
* “缓冲”行为中的更改：缓冲行为已更改。 在缓冲区空的情况下，这取决于App开发人员想要做什么。 2.5.3在缓冲区空的情况下使用播放缓冲区大小。

**版本2.5.2**

Android TVSDK v2.5.2优惠了重要的错误修复和一些API更改。

**版本2.5.1**

Android 2.5.1中发布的重要新增功能。

* **性**&#x200B;能改进新的TVSDK 2.5.1架构带来了许多性能改进。根据第三方基准测试研究的统计数据，新架构的启动时间比行业平均数减少了5倍，丢帧数减少了3.8倍：

   * **VOD和实时的即时启用 —** 启用即时启用时，TVSDK在播放开始之前初始化媒体并缓冲媒体。由于您可以在后台同时启动多个MediaPlayerItemLoader实例，因此可以缓冲多个流。 当用户更改渠道，且流已正确缓冲时，立即在新的渠道开始上播放。 TVSDK 2.5.1还支持&#x200B;**live**&#x200B;流的即时打开。 在实时窗口移动时重新缓冲实时流。

      * **改进的ABR逻** 辑 — 新的ABR逻辑基于缓冲区长度、缓冲区长度变化速率和测量带宽。这确保ABR在带宽波动时选择正确的比特率，还通过监视缓冲区长度变化的速率来优化比特率切换实际发生的次数。
      * **部分区段下载/子分段 —** TVSDK进一步减小每个片段的大小，以便尽快开始播放。ts片段必须每两秒有一个关键帧。
      * **延迟广告分** 辨率 — TVSDK在开始播放之前不等待非预卷广告的分辨率，因此缩短了启动时间。搜索和技巧播放等API在所有广告都解决之前仍不允许。 这适用于与CSAI一起使用的VOD流。 搜索和快进等操作在广告解决完成之前不允许。 对于实时流，无法在实时事件中为广告分辨率启用此功能。
      * **永久网络连接 —** 此功能允许TVSDK创建和存储永久网络连接的内部列表。这些连接被重用于多个请求，而不是为每个网络请求打开新连接，然后销毁它。 这提高了网络代码的效率并减少了等待时间，从而提高了播放性能。
当TVSDK打开连接时，它会要求服务器提供*keep-alive*&#x200B;连接。 某些服务器可能不支持此类连接，在这种情况下，TVSDK将回退到再次为每个请求建立连接。 此外，尽管永久连接在默认情况下处于打开状态，TVSDK现在有一个配置选项，以便应用程序可以根据需要关闭永久连接。
      * **并行下载 —** 以并行方式而不是以串联方式下载视频和音频可减少启动延迟。此功能允许播放HLS Live和VOD文件，优化来自服务器的可用带宽使用，降低在运行不足情况下进入缓冲区的可能性，并最小化下载和回放之间的延迟。
      * **并行广告下载 —** TVSDK在点击广告中断前预取与内容播放平行的广告，从而实现广告和内容的无缝播放。

* **播放**

   * **MP4内容播放 —** MP4短片无需重新转码即可在TVSDK中播放。注意：MP4播放不支持ABR切换、特技播放、广告插入、后期音频绑定和子分段。
   * **使用自适应比特率(ABR)进行特** 技播放 — 此功能允许TVSDK在特技播放模式下在iFrame流之间切换。您可以使用非iFrame用户档案以较低的速度进行特技播放。
   * **更流畅的特技播放**  — 这些改进增强了用户体验：

          *在特技播放期间，根据带宽和缓冲区用户档案选择自适应比特率和帧速率
          *使用主流而不是IDR流，最高可实现30 fps的快速播放。
      
* **内容保护**

   * **基于分辨率的输出保护 — 此** 功能将播放限制与特定分辨率关联起来，提供更精细的DRM控制。

* **工作流支持**

   * **直接计费集** 成 — 这会将计费指标发送到Adobe Analytics后端，后者由Adobe Primetime针对客户使用的流进行验证。TVSDK自动收集量度，遵守客户销售合同，以生成计费所需的定期使用情况报告。 在每个流开始事件中，TVSDK使用Adobe Analytics数据插入API向Adobe Analytics Primetime拥有的报表包发送付费量度，如内容类型、广告插入启用标记和drm启用标记（基于可计费流的持续时间）。 这不会干扰或包含在客户自己的Adobe Analytics报表包或服务器调用中。 根据要求，此账单使用情况报告会定期发送给客户。 这是付费功能的第一阶段，仅支持使用付费。 可以使用文档中描述的API根据销售合同进行配置。 默认情况下启用此功能。 要关闭此功能，请参阅参考播放器范例。
   * **改进了故障转移支** 持 — 实施了其他策略，以便在主机服务器、播放列表文件和区段出现故障的情况下继续无中断播放。

* **广告**

   * **Moat集成 — 支** 持从Moat进行广告可见性测量。
   * **配套横幅 —** 配套横幅在线性广告旁边显示，广告结束后通常继续显示在视图上。这些横幅的类型可以是html（HTML片段）或iframe（iframe页面的URL）。

* **分析**

   * **VHL 2.0 — 这是最** 新的优化的视频心率库(VHL)集成，可自动收集Adobe Analytics的使用数据。为了简化实施，降低了API的复杂性。 下载适用于Android](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases)的VHL库[v2.0.0，并解压libs文件夹中的JAR文件。

* **SizeAvaliableEventListener**
   * 现在，SizeAvailableEvent的getHeight()和getWidth()方法将分别以高度和宽度返回输出。 显示长宽比可以按如下方式计算：

      ```
      SizeAvailableEvent e;
      
      DAR = e.getWidth()/ e.getHeight();
      
      Storage Aspect Ratio in terms of Sar width and Sar height can also be used to calculate Frame width and Frame height:
      
      SAR = e.getSarWidth()/e.getSarHeight();
      
      frameHeight = e.getHeight();
      
      frameWidth = e.getWidth()/SAR;    
      ```

* **Cookie**

   * Android TVSDK现在支持访问存储在Android应用程序CookieStore中的JAVA Cookie。 当新Cookie作为“Set-Cookie”响应头的一部分出现时，将提供回调API(onCookiesUpdated)以进行记录。 通过使用CookieStore在该特定URI/域上设置这些Cookie值，这些Cookie可用作用于其他URI/域的HttpCookie的列表。 同样，TVSDK中的Cookie值也会使用CookieStore添加API进行更新。

## 功能矩阵{#feature-matrix}

适用于Android的TVSDK支持许多功能，您可以通过这些功能为视频应用程序添加功能。

在以下功能表中，“Y”表示当前版本中支持该功能。

| 功能 | 内容类型 | HLS |
|---|---|---|
| 常规播放（播放、暂停、搜索） | VOD +实时 | Y |
| FER — 常规播放（播放、暂停、搜索） | FER VOD | Y |
| 在广告播放时进行搜索 | VOD +实时 | 不支持 |
| AC3 | VOD +实时 | 不支持 |
| MP3 | VOD | 不支持 |
| MP4内容播放 | VOD | Y |
| 自适应比特率切换逻辑 | VOD +实时 | Y |
| 仅音频回放 | VOD +实时 | Y |
| 多CDN支持 | VOD +实时 | 不支持 |
| 使用纯音频媒体播放广告 | VOD +实时 | 不支持 |
| 隐藏式字幕 — 608/708 | VOD +实时 | Y |
| 隐藏式字幕 — WebVTT | VOD +实时 | Y |
| 清单故障转移 | VOD +实时 | Y |
| 高级故障转移 | VOD +实时 | Y |
| QoS和播放器通知 | VOD +实时 | Y |
| 支持Cookie头 | VOD +实时 | Y |
| 支持自定义HTTP头 | VOD +实时 | Y（允许列出） |
| 设置缓冲区控制参数 | VOD +实时 | Y |
| 设置自适应比特率控件 | VOD +实时 | Y |
| 自定义清单标记 | VOD +实时 | Y |
| 延迟音频绑定 | VOD +实时 | Y |
| 302重定向 | VOD +实时 | Y |
| 带偏移的回放 | VOD +实时 | Y |
| 仅音频回放 | VOD +实时 | Y |
| Trick Play | VOD +实时 | Y |
| 特技播放中的慢动作 | VOD +实时 | 不支持 |
| 流畅的技巧播放（使用ABR） | VOD +实时 | Y |
| ID3解析 | VOD +实时 | Y |
| 广告封锁 | VOD +实时 | 不支持 |
| 即时启动 | VOD +实时 | 不支持 |
| 间断标记支持 | VOD +实时 | Y |
| 302重定向粘性 | VOD +实时 | Y |

| 功能 | 内容类型 | HLS |
|---|---|---|
| 常规播放，支持广告 | VOD +实时 | Y |
| 支持广告的FER内容 | VOD | Y |
| 默认广告行为 | VOD +实时 | Y |
| VAST 2.0/3.0 | VOD +实时 | Y |
| VMAP 1.0 | VOD +实时 | Y |
| MP4广告 | VOD +实时 | Y（来自CRS） |
| 支持广告的特技播放 | VOD +实时 | Y |
| 仅广告 | VOD | Y |
| 定位参数 | VOD +实时 | Y |
| 自定义参数 | VOD +实时 | Y |
| 自定义广告行为 | VOD +实时 | Y |
| 自定义广告标记 | 实时 | Y |
| 自定义广告解析器 | VOD +实时 | Y |
| Freewheel自定义广告解析程序 | VOD | Y |
| C3 | VOD +实时 | 不支持 |
| 延迟广告解析 | VOD | Y |
| 间断标记支持 — SSAI | VOD +实时 | Y |
| 配套广告、横幅广告和可点击广告 | VOD +实时 | Y |
| VPAID 2.0 | VOD +实时 | Y(JS) |
| 早期广告退出 | 实时 | Y |
| 基于规则的创意优先排序 | VOD +实时 | Y |
| CRS规则 | VOD +实时 | Y |
| JSON广告解析程序 | VOD +实时 | 不支持 |
| Moat集成 | VOD +实时 | Y |

| 功能 | 内容类型 | HLS |
|---|---|---|
| AES加密 | VOD +实时 | Y |
| 示例AES加密 | VOD +实时 | Y |
| 标记流 | VOD +实时 | Y |
| DRM | VOD +实时 | 仅限Primetime DRM(未来：Widevine) |
| 外部播放(RBOP) | VOD +实时 | 仅限Primetime DRM |
| 许可证轮换 | VOD +实时 | 仅限Primetime DRM |
| 键旋转 | VOD +实时 | 仅限Primetime DRM |

| 功能 | 内容类型 | HLS |
|---|---|---|
| Adobe Analytics VHL集成 | VOD +实时 | Y |
| 帐单 | VOD +实时 | Y |

## 已解决问题{#resolved-issues}

如果分辨率与报告的问题相关联，则会显示Zendesk引用，例如ZD#xxxxx

**Android TVSDK 2.7**

本节概述TVSDK 2.7版中解决的问题。

* ZD#37166 — 即使广告播放正常，也会触发错误跟踪调用。
* ZD#37134 — 返回错误的广告ID，以防在VMAP响应中出现包装器(3P)广告包含多个广告。

**Android TVSDK 2.5.6**

* ZD #34992 — 隐藏字幕中的语言为空。
   * 修复了TVSDK未从主清单分析#EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS的情况，以获取题注轨道详细信息。
* ZD #35078 - Android P验证。
   * TVSDK 2.5.6已通过最新Android P测试版进行验证。 由于新的Android操作系统，未发现问题。
* ZD #34149 — 播放器会继续请求清单，即使遇到错误也是如此。
   * 修复了即使所有用户档案都关闭时TVSDK仍进行重复调用的情况（404错误）。
* ZD #31533 — 在应用程序发送到后台后在Android上播放音频。
   * 添加了MediaPlayer的`enableAudioPlaybackInBackground` API，该API应以“True”作为参数进行调用（当播放器处于PREPARED状态时），以在应用程序处于后台时启用音频回放。

**Android TVSDK 2.5.5**

* ZD #21647 — 当实际视频大小为640x360时，Android TVSDK将通知640x368。
   * 由于变量m_nOutputHeight（在AndroidMCVideoDecoder中）已更新为帧高而非实际输出高度。 在函数getVideoFrame中进行了相关更改，以正确计算m_nOutputHeight。
* ZD #26614 — 紧急 — 第三方广告投放/程序化 — 无法提供展示。
   * 通过处理XML分析中的情况（当“空格”位于&lt;VAST version =&quot;2.0&quot;>等“相等”符号之前时，问题可重现），增强了之前的修复
* ZD #29296 - Android:向CRS请求添加AdSystem和Creative ID。
   * 现在，在1401和1403请求中将“AdSystem”和“CreativeId”作为新参数。
* ZD #33062 - TVSDK在CDATA节点下的VAST响应中出现管道字符时崩溃
   * NetworkConfiguration类中的API setEncodeUrlForTracking作为要编码的URL中不安全的字符删除。
* ZD #33063 - CRS文件选择逻辑已损坏 — TVSDK不发送CRS请求webm格式，而是发送3gpp文件。
   * 已修复逻辑。 在使用webm和3gpp格式的媒体文件时，将为webm发送CRS请求。 同时使用3gpp格式的媒体文件时，将为最高比特率的3gpp文件发送CRS请求。
* ZD #33125 - Android应用程序在VMAP中使用特定的DoubleClick标记崩溃。
   * 修复了方案以避免崩溃。
* ZD #32256 — 许可证轮替和密钥轮替问题 — Adobe访问。
   * 修复了使用SampleAES内容的DRM元数据进行区段初始化的问题。 与AES128内容配合使用。
* ZD #33619 — 快速转发在实况点附近处于缓冲状态的不断增加的播放列表内容。
   * 在特技播放模式下跨越实时点时处理案例。
* ZD #34151 - TimedMetadata对象无序。
   * 如果两个TimedMetadata事件属于时间轴中的同一时间，则它们以随机顺序显示。 维护清单中的原始订单。
* ZD #34189 — 寻求开始广告中断时的问题。
   * 问题出在使用间断拼接的SSAI广告。 原因是当我们寻找这些广告的开始，我们搜索一个关键帧，却找不到它。 原因是广告的最小音频时间戳早于最小视频时间戳。 因此，我们最终在错误的fragmentDump数据上搜索关键帧。 现已修复。
* ZD #34528 — 在FireTV第3代转换器上，视频分辨率未超过640x360。
   * 增强了修复功能以包含最新固件更新。
* ZD #34793 - TVSDK 2.5.x用于在某些情况下与自定义内容解析程序崩溃，当VideoEngine假定auditudeSettings可用而它们不可用时。
   * 由于对空共享指针(auditudeSettings)的函数调用而发生崩溃。 在VideoEngineTimeline::placeToSourceTimeline()中添加了一个条件检查，以确保在对该对象调用任何内容之前，auditudeSettings可用。
* ZD #32584 — 无法访问VAST响应的&lt;Extensions>节点中存在的完整信息。
   * 修复了XML解析的问题，现在NetworkAdInfo提供&lt;Extensions>节点中提供的完整信息。
* ZD #35086 — 在特定VMAP响应的情况下，不从播放器获取完整的扩展数据。
   * 问题只针对扩展xml，因为如果扩展xml在属性值中包含多次引号，则XML解析不起作用。 已修复问题。

**Android TVSDK 2.5.4**

* ZenDesk#33659 — 启用Web视图远程调试的播放会话。
   * 默认情况下，WebViewDebuging设置为False。 要启用调试，请使用setWebContentsDebuggingEnabled(true)通过应用程序设置为true。
* ZenDesk#33011 — 在CRS请求失败时，无法解析广告时间轴。
   * 当对广告的CRS请求失败时，时间轴会被解析，其余的广告会被播放。
* ZenDesk#34528 - FireTV第三代转换器上的视频分辨率升级不超过640x360。
   * 视频分辨率会作为比特率切换而切换。
* ZenDesk#33192 — 当通过AudioUpdatedEventListener::onAudioUpdated检索轨道时，AudioTrack的名称为null。
   * 在FireTV Stick上的一些情况下，当没有实际的音频更新时，onAudioUpdate事件会被触发。 现在已修复。

**Android TVSDK 2.5.3**

* Zendesk#32216 - TimedMetadata自定义标记订阅无效。
   * 我们将ID3数据作为字节数组返回给客户端（以支持APIC或通用数据），而在1.4返回字符串中。 字节数组不处理以空结尾的字符本身，因此它向客户端显示特殊字符。 此问题现已修复。
* Zendesk#32670 - Player不会故障切换到冗余播放列表
   * 现在运行正常，setNetworkDownVerificationUrl正按预期工作。
* Zendesk#32369 — 隐藏式字幕显示不同的颜色垃圾或伪像。
   * CC故障问题已在最新版本中得到修复
* Zendesk#25590 — 增强：TVSDK Cookie存储（C++到JAVA）
   * Android TVSDK现在支持在JAVA层（存储在Android应用程序的CookieStore中）和C++ TVSDK层之间访问Cookie。
* Zendesk#32252 - TVSDK_Android_2.5.2.12似乎没有PTPLAY-20269的修复
此问题已修复并集成到2.5.2分支。
* Zendesk#31806 - Auditude加入PREPARING
Player因响应xml有空标签而卡在“准备”状态。 现在问题已解决。
* Zendesk#31727 - TVSDK 2.5隐藏字幕字符被丢弃或拼写错误。
   * 问题已修复，我们不会删除/错误拼写任何字符。
* Zendesk#31485 - DrmManager，2.5版
   * 通过新的DrmManager（上下文）创建DrmManager时出现一些问题。 实现了DRMService类，它将提供DRMManager。
* Zendesk#32794- 1080P分辨率流未在Android上播放。
   * 我们在2.5中更改了SizeAvailableEvent和Previsory、getHeight()和getWidth()方法，用于返回由媒体格式返回的帧高和帧宽。 现在，它分别返回解码器返回的输出高度和输出宽度。
* Zendesk #19359Flash Player因设置级清单中#EXT-X-FAXS-CM属性的位置而崩溃。
   * #EXT-X-FAXS-CM标签必须始终显示在顶部的播放列表中，然后才能在播放列表中显示单个比特率或区段。

**Android TVSDK 2.5.2**

* Zendesk#17305隐藏式字幕中具有非不透明背景的伪像。
显示TextFormat中的setTreatSpaceAsAlphaNum属性。 默认情况下，该属性为False。 在客户端中将属性设置为True可解决暗空间问题。

* Zendesk#25097 CC显示带有CC设置的视觉伪像。
显示TextFormat中的setTreatSpaceAsAlphaNum属性。 默认情况下，该属性为False。 在客户端中将属性设置为True可解决暗空间问题。

* Zendesk #31620 User agent字符串从TVSDK播放器退出被截断。
128个字符后将不再截断用户代理字符串。
Adobe Primetime版本字符串已添加到系统用户代理。

* Zendesk #30809 Missing SEEK_END事件可阻止应用程序转换到播放状态。
* 与Primetime TVSDK先前版本相比，Zendesk #30415 Closed Caption的“青色”颜色现在更深的蓝色（绿松石）色相。

   颜色从深青色更改为青色。

* Zendesk #30727 VOD广告无法下载/解析。

   在VMAP XML中，如果有空的VAST标签，而没有显式结束标签(“&lt;/VAST>”)，并且后面没有换行符，则VMAP XML无法正确分析，广告可能无法播放。

**Android TVSDK 2.5.1**

* 特定于设备的(Samsung Galaxy Tab 4)崩溃；具有Auditude的VOD DRM LBA，然后单击广告。
* VHL — 从偏移启动内容时发送的心跳调用不正确。
* 播放VPAID广告时，缺少VHL心跳调用事件:type:play广告。
* 进入“完成”状态后，对于后滚广告，播放器使用SKIP adBreakPolicy返回到“播放”状态。
* Cookie未附加到传出广告回呼。
* 广告提示点不可见。
* 带有单独EAC3 SAP轨道的HLS将无法加载。
* 在媒体播放器恢复后，TVSDK收到“屏幕开启”意图时播放器崩溃。

## 已知问题和限制{#known-issues-and-limitations}

**Android TVSDK 2.7**

* TVSDK 2.7支持最多5个广告的并发解析。
* 在VMAP响应的情况下，单个广告中断中的广告调用会同时进行，广告中断会按顺序解析。
* 在FER的情况下，将同时解决每个机会中的广告呼叫。

### 先前版本中的已知问题和限制{#known-issues-limitations-previous-releases}

**Android TVSDK 2.5.6**

* 不支持同时进行多个VMAP广告中断。

**Android TVSDK 2.5.3**

此版本有以下问题：

* 实时视频播放可能在低端设备上出现音频 — 视频同步问题，或者网络状况不佳。
* 对于FER流，virtualTime和localTime可能不同。 同时，具有偏移的FER不起作用。
* 搜索“延迟绑定音频”内容时，播放可能会卡住。
* 间歇性地，webVTT字幕可能会变得与实时内容不同步。
* 从广告中断出来后，可间歇性地快速播放少量帧。
* 有时，即使播放广告，三步包装广告分段也会引发303错误。

**Android TVSDK 2.5.2**

此版本有以下问题：

* 在低端设备上，实时视频播放可能存在音频 — 视频同步问题。
* 当搜索到VOD媒体的末尾时，播放可能会暂停。
* 对于FER流，virtualTime和localTime可能不同。 此外，具有偏移的FER不起作用。

**Android TVSDK 2.5.1**

此版本的TVSDK有以下问题：

* 在低端设备上，实时视频播放可能存在音频 — 视频同步问题。
* 对于FER流，virtualTime和localTime可能不同。 此外，具有偏移的FER不起作用。
* 在VMAP XML中，如果有空的VAST标签没有显式结束标签(&lt;/VAST>)，并且后面没有换行符，则VMAP XML无法正确分析，广告可能无法播放。
* 不支持VPAID后滚。

## 有用资源{#helpful-resources}

* [系统要求](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-2-7-for-android/overview/c-psdk-android-2_7-requirements.html)
* [TVSDK 2.7 for Android程序员指南](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-2-7-for-android/overview/c-psdk-android-2_7-overview-prod-audience-guide.html)
* [TVSDK Android Javadoc for API参考](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html)
* [TVSDK Android C++ API文档](https://help.adobe.com/en_US/primetime/api/psdk/cpp/namespaces.html)  — 每个Java类都有相应的C++类，而C++文档包含比Javadoc更多的解释性材料，因此请参阅C++文档以更深入地了解Java API。
* [适用于Android(Java)的TVSDK 1.4至2.5迁移指南](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* 要处理屏幕开/关情况，请参阅内部版本中包含的`Application_Changes_for_Screen_On_Off.pdf`文件。
* 请参阅[Adobe Primetime学习和支持](https://helpx.adobe.com/support/primetime.html)页面上的完整帮助文档。
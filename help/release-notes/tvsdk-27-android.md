---
title: 适用于Android™的TVSDK 2.7发行说明
description: 适用于Android™的TVSDK 2.7发行说明介绍了TVSDK Android™ 2.7中的新增或更改内容、已解决的问题和已知问题以及设备问题
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '4037'
ht-degree: 0%

---

# 适用于Android™的TVSDK 2.7发行说明 {#tvsdk-for-android-release-notes}

适用于Android™的TVSDK 2.7发行说明介绍了TVSDK Android™ 2.7中的新增或更改内容、已解决的问题和已知问题以及设备问题

## TVSDK Android™ 2.7 {#tvsdk-android}

Android™参考播放器随Android™ TVSDK一起包含在分发的samples/目录中。 随附的README&lt;.md文件说明了如何构建参考播放器。

>[!NOTE]
>
>要成功构建引用播放器（如随发行版一起分发的README.md中所述），请确保执行以下操作：
>
>1. 从下载VideoHeartbeat.jar [https://github.com/Adobe-Marketing-Cloud/media-sdks/releases](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) (适用于Android™ v2.0.0的VideoHeartbeat库)
>1. 将VideoHeartbeat.jar提取到libs/文件夹中。
>

## 新增功能 {#new-features}

适用于Android™的TVSDK 2.7包含版本1.4的所有功能，但不包含下列不受支持的功能 [功能矩阵](#feature-matrix).

**Android™ TVSDK 2.7**

* **并行广告分辨率支持**

TVSDK 2.7支持广告时间中所有广告请求的并发分辨率，而不是顺序分辨率。

### 以前版本中的新增功能 {#new-features-previous-releases}

**版本2.5.6**

* **TVSDK 2.5支持Android™ P**
* **启用背景音频**

  要在应用程序从前台移动到后台时启用音频播放，当播放器处于“已准备”状态时，应用程序应调用MediaPlayer的enableAudioPlaybackInBackground API，并将true作为参数。

* **MediaPlayer类中的alwaysUseAudioOutputLatency(boolean val)**

设置后，在音频时间戳计算中使用输出延迟。
布尔值参数val - True在音频时间戳计算中使用音频输出滞后。

* **经过优化，即使在带宽速度突然下降的情况下也能获得最佳的播放体验。**
现在，TVSDK会根据需要取消正在进行的区段下载，并动态切换到相应的演绎版。 这是通过在比特率之间无缝切换而没有中断来完成的。

**版本2.5.5**

* **部分广告时间插入**

  类似于电视的体验：在广告中间加入，而不触发部分观看广告的跟踪。\
  示例：用户在包含三个30秒广告的90秒广告时间的中间（40秒）加入。 此时是插播中第二个广告的10秒。
   * 第二个广告将播放剩余的时长（20秒），随后是第三个广告。
   * 对于播放的部分广告（第二个广告），不会触发广告跟踪器。 仅触发第三个广告的跟踪器。

* **通过HTTPS安全加载广告**

  Adobe Primetime提供了一个选项，用于请求通过https首次调用primetime广告服务器和CRS。

* **向CRS请求添加了AdSystem和Creative Id**

   * 现在包括 `AdSystem` 和 `CreativeId` 作为1401和1403请求中的新参数。

* **删除了NetworkConfiguration类中的API setEncodeUrlForTracking** 因为URL中的不安全字符应该进行编码。

**版本2.5.4**

Android™ TVSDK v2.5.4提供了以下更新和API更改：

* 默认值的更改 `WebViewDebbuging`

  此 `WebViewDebbuging` 值设置为 _假_ 默认情况下。 要启用该功能，请调用 `setWebContentsDebuggingEnabled` 到 _True_ 在应用程序中。

* OpenSSL和Curl版本升级已更新 `libcurl` 到v7.57.0和OpenSSL到v1.0.2k。
* 对VAST响应对象的应用程序级别访问引入了一个新的API NetworkAdInfo：：getVastXml()，它提供了对应用程序的VAST响应对象的访问。

**版本2.5.3**

Android™ TVSDK v2.5.3提供了以下更新和API更改。

* 我们鼓励所有使用CRS的TVSDK客户使用TVSDK 2.5.3.85或Android™最新版本升级其应用程序。 这是现有应用程序实施的下拉式替代。 TVSDK升级后，在代理工具（例如：Charles）中检查CRS创意URL请求，并确认路径中的主机名和版本反映为如下面的示例URL结构中所示。

  `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* 可自定义TVSDK的用户代理：我们添加了一些新的API以自定义用户代理。

   * `setCustomUserAgent`（字符串值）
   * `getCustomUserAgent`()

* 在Android™应用程序和TVSDK之间共享Cookie：Android™ TVSDK现在支持在Java™层(存储在Android™应用程序的CookieStore中)和C++ TVSDK层之间访问Cookie。 现在，可以在本机C++层中设置和/或修改Cookie，因为它们会公开到Java™ Cookie Store。
* API更改：

   * 添加了新事件CookieUpdatedEvent。 媒体播放器会在更新其Cookie时调度它。
   * 新的API已添加到 `NetworkConfiguration::set/ getCustomUserAgent()` 以使用自定义用户代理。
   * 新的API已添加到 `NetworkConfiguration::set/ getEncodedUrlForTracking` 强制编码不安全字符。
   * 新的API已添加到 `NetworkConfiguration::getNetworkDownVerificationUrl()` 设置网络验证URL（如果有故障转移）。
   * TextFormat：：treatSpaceAsAlphaNum中新增了一个属性，该属性定义在显示字幕时是否将空间视为字母数字。

* 中的更改 `SizeAvailableEvent`：以前，的getHeight()和getWidth()方法 `SizeAvailableEvent` 在2.5.2中，用于返回由媒体格式返回的帧高度和帧宽度。 现在，它分别返回解码器返回的输出高度和输出宽度。
* 缓冲行为的更改：缓冲行为已更改。 由应用程序开发人员自行决定当缓冲区为空时要执行的操作。 2.5.3在缓冲区为空的情况下使用播放缓冲区大小。

**版本2.5.2**

Android™ TVSDK v2.5.2提供了重要的错误修复和一些API更改。

**版本2.5.1**

Android™ 2.5.1中发布的重要新功能。

* **性能改进**&#x200B;新的TVSDK 2.5.1架构提供了多项性能改进。 根据第三方基准测试研究的统计数据，与业界平均水平相比，新架构的启动时间减少了5倍，丢帧减少了3.8倍：

   * **即时打开以进行VOD和直播 —** 启用instant on时，TVSDK会在播放开始之前初始化并缓冲媒体。 由于您可以在后台同时启动多个MediaPlayerItemLoader实例，因此您可以缓冲多个流。 当用户更改频道，并且流已正确缓冲时，新频道上的播放立即开始。 TVSDK 2.5.1还支持为以下对象启用“即时开启” **实时** 流。 当实时窗口移动时，实时流将被缓冲。

      * **改进了ABR逻辑 —** 新的ABR逻辑基于缓冲区长度、缓冲区长度变化率和测量带宽。 这样可以确保ABR在带宽波动时选择正确的比特率，还可以通过监控缓冲区长度变化的速率来优化比特率切换的实际次数。
      * **部分区段下载/子区段 —** TVSDK进一步减小了每个片段的大小，以便尽快开始播放。 ts片段必须每两秒具有一个关键帧。
      * **延迟广告分辨率 —** TVSDK在开始播放之前不会等待非前置广告的分辨率，因此缩短了启动时间。 直到解决所有广告后，才允许使用搜寻和特技播放等API。 这适用于与CSAI一起使用的VOD流。 在完成广告解析之前，不允许执行搜寻和快速前进等操作。 对于实时流，此功能无法在实时活动期间启用广告解析。
      * **永久网络连接 —** 此功能允许TVSDK创建和存储永久网络连接的内部列表。 这些连接会重复用于多个请求，而不是为每个网络请求打开一个新连接，然后将其销毁。 这会提高网络代码中的效率并减少延迟，从而加快播放性能。
当TVSDK打开连接时，会要求服务器提供 *保持活动状态* 连接。 某些服务器可能不支持这种连接，在这种情况下，TVSDK回退以再次为每个请求建立连接。 此外，在默认情况下打开永久连接的情况下，TVSDK现在提供了一个配置选项，以便应用程序可以根据需要关闭永久连接。
      * **并行下载 —** 并行下载视频和音频而非串行下载可减少启动延迟。 此功能允许播放HLS Live和VOD文件，优化服务器的可用带宽使用，降低在运行时进入缓冲区的概率，并最大限度地减少下载和播放之间的延迟。
      * **并行广告下载 —** TVSDK会在点击广告时间之前预取与内容播放平行的广告，从而支持无缝播放广告和内容。

* **播放**

   * **MP4内容播放 —** 在TVSDK中，MP4短剪辑无需重新编码即可播放。
注意：MP4播放不支持ABR切换、特技播放、广告插入、后期音频绑定和子分段。
   * **具有自适应比特率(ABR)的特技播放 —** 此功能允许TVSDK在特技播放模式中切换iFrame流。 您可以使用非iFrame配置文件在低速下玩特技游戏。
   * **更流畅的戏法 —** 这些改进增强了用户体验：

         *在特技播放期间根据带宽和缓冲配置文件进行自适应比特率和帧速率选择
         *使用主流而不是IDR流进行高达30 fps的快速播放。
     
* **内容保护**

   * **基于分辨率的输出保护 —** 此功能将回放限制绑定到特定分辨率，从而提供更细粒度的DRM控制。

* **工作流支持**

   * **直接账单集成 —** 这会将计费量度发送到Adobe Analytics后端，后者由Adobe Primetime针对客户使用的流进行认证。
TVSDK会根据客户销售合同自动收集量度，以生成计费所需的定期使用报告。 在每个流开始事件上，TVSDK使用Adobe Analytics数据插入API将计费指标(如内容类型、启用广告插入的标记以及启用drm的标记（基于可计费流的持续时间）)发送到Adobe Analytics Primetime拥有的报表包。 这不会干扰客户自己的Adobe Analytics报表包或服务器调用或包含在其中。 根据请求，定期向客户发送此计费使用情况报告。 这是计费功能的第一个阶段，仅支持使用计费。 它可以使用文档中描述的API，根据销售合同进行配置。 此功能默认处于启用状态。 要关闭此功能，请参阅参考播放器示例。
   * **改进的故障切换支持 —** 实施了其他策略以继续不间断的播放，尽管主机服务器、播放列表文件和区段出现故障。

* **广告**

   * **Moat集成 —** 支持从Moat进行广告可见性测量。
   * **随附横幅 —** 伴随横幅与线性广告一起显示，并且通常在广告结束后继续显示在视图中。 这些横幅可以是html类型(HTML片段)或iframe类型（iframe页面的URL）。

* **分析**

   * **VHL 2.0 -** 这是最新的优化视频心率库(VHL)集成，可自动收集Adobe Analytics的使用数据。 API的复杂性已降低，以简化实施。 下载VHL库 [适用于Android™的v2.0.0](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) 并提取libs文件夹中的JAR文件。

* **SizeAvaliableEventListener**
   * SizeAvailableEvent的getHeight()和getWidth()方法现在将分别返回高度和宽度的输出。 显示长宽比可按如下方式计算：

     ```
     SizeAvailableEvent e;
     
     DAR = e.getWidth()/ e.getHeight();
     
     Storage Aspect Ratio in terms of Sar width and Sar height can also be used to calculate Frame width and Frame height:
     
     SAR = e.getSarWidth()/e.getSarHeight();
     
     frameHeight = e.getHeight();
     
     frameWidth = e.getWidth()/SAR;    
     ```

* **Cookies**

   * Android™ TVSDK现在支持访问存储在Android™应用程序的CookieStore中的Java™ Cookie。 每当新Cookie作为“Set-Cookie”响应标头的一部分出现时，提供一个回调API (onCookiesUpdated)进行记录。 通过使用CookieStore在该特定URI/域中设置这些Cookie值，这些Cookie可用作用于不同URI/域的HttpCookie列表。 同样，使用CookieStore add API更新TVSDK中的Cookie值。

## 特征矩阵 {#feature-matrix}

适用于Android™的TVSDK支持您可以实施的各种功能，以便向视频应用程序添加功能。

在下面的功能表中，“Y”表示当前版本支持该功能。

| 功能 | 内容类型 | HLS |
|---|---|---|
| 常规播放（播放、暂停、搜寻） | VOD +实时 | Y |
| FER — 常规播放（播放、暂停、搜寻） | FER VOD | Y |
| 在广告播放时搜寻 | VOD +实时 | 不支持 |
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
| 支持自定义HTTP标头 | VOD +实时 | Y（需要列入允许列表） |
| 设置缓冲区控制参数 | VOD +实时 | Y |
| 设置自适应比特率控制 | VOD +实时 | Y |
| 自定义清单标记 | VOD +实时 | Y |
| 延迟音频绑定 | VOD +实时 | Y |
| 302重定向 | VOD +实时 | Y |
| 带偏移量的播放 | VOD +实时 | Y |
| 仅音频播放 | VOD +实时 | Y |
| 特技游戏 | VOD +实时 | Y |
| 特技游戏中的慢动作 | VOD +实时 | 不支持 |
| Smooth Trick Play（使用ABR） | VOD +实时 | Y |
| ID3解析 | VOD +实时 | Y |
| 广告封锁 | VOD +实时 | 不支持 |
| 即时打开 | VOD +实时 | 不支持 |
| 支持中断标记 | VOD +实时 | Y |
| 302重定向粘性 | VOD +实时 | Y |

| 功能 | 内容类型 | HLS |
|---|---|---|
| 常规播放，启用广告 | VOD +实时 | Y |
| 启用了广告的FER内容 | VOD | Y |
| 默认广告行为 | VOD +实时 | Y |
| VAST 2.0/3.0 | VOD +实时 | Y |
| VMAP 1.0 | VOD +实时 | Y |
| MP4广告 | VOD +实时 | Y（来自CRS） |
| 启用广告的特技播放 | VOD +实时 | Y |
| 仅广告 | VOD | Y |
| 定位参数 | VOD +实时 | Y |
| 自定义参数 | VOD +实时 | Y |
| 自定义广告行为 | VOD +实时 | Y |
| 自定义广告标记 | 实时 | Y |
| 自定义广告解析程序 | VOD +实时 | Y |
| Freewheel自定义广告解析程序 | VOD | Y |
| C3 | VOD +实时 | 不支持 |
| 延迟广告解决 | VOD | Y |
| 中断标记支持 — SSAI | VOD +实时 | Y |
| 伴随广告、横幅广告和可点击广告 | VOD +实时 | Y |
| VPAID 2.0 | VOD +实时 | Y (JS) |
| 提前广告退出 | 实时 | Y |
| 基于规则的创意优先级排序 | VOD +实时 | Y |
| CRS规则 | VOD +实时 | Y |
| JSON广告解析程序 | VOD +实时 | 不支持 |
| Moat集成 | VOD +实时 | Y |

| 功能 | 内容类型 | HLS |
|---|---|---|
| AES加密 | VOD +实时 | Y |
| AES加密示例 | VOD +实时 | Y |
| 标记化的流 | VOD +实时 | Y |
| DRM | VOD +实时 | 仅限Primetime DRM（未来：Widevine） |
| 外部播放(RBOP) | VOD +实时 | 仅限Primetime DRM |
| 许可证轮换 | VOD +实时 | 仅限Primetime DRM |
| 密钥轮替 | VOD +实时 | 仅限Primetime DRM |

| 功能 | 内容类型 | HLS |
|---|---|---|
| Adobe Analytics VHL集成 | VOD +实时 | Y |
| 计费 | VOD +实时 | Y |

## 已解决的问题 {#resolved-issues}

当解决方法与报告的问题相关联时，将显示Zendesk引用，例如ZD#xxxxx

**Android™ TVSDK 2.7**

本节概述TVSDK 2.7版本中已解决的问题。

* ZD#37166 — 即使广告播放正常，也会触发错误跟踪调用。
* ZD#37134 — 如果包装器(3P)广告在VMAP响应中存在多个广告，则返回错误的广告ID。

**Android™ TVSDK 2.5.6**

* ZD #34992 — 隐藏式字幕中的语言为空。
   * 修复了TVSDK未从主清单中解析#EXT-X-MEDIA：TYPE=CLOSED-CAPTIONS以获取字幕跟踪详细信息的情况。
* ZD #35078 - Android P验证。
   * TVSDK 2..5.6已通过最新Android™ P测试版内部版本验证。 由于新的Android™操作系统，未发现任何问题。
* ZD #34149 — 即使遇到错误，播放器仍会继续请求清单。
   * 修复了TVSDK进行重复调用的情况，即使所有用户档案都已关闭（404错误）。
* ZD #31533 — 在将应用程序发送到后台后，在Android™上播放音频。
   * 已添加 `enableAudioPlaybackInBackground` MediaPlayer的API，应使用“True”作为参数（当播放器处于“已准备”状态时）调用，以便在应用程序处于后台时启用音频播放。

**Android™ TVSDK 2.5.5**

* ZD #21647 — 当实际视频大小为640x360时，Android TVSDK会通知640x368。
   * 由于变量m_nOutputHeight（在AndroidMCVideoDecoder中）使用帧高度而不是实际输出高度进行更新。 对函数getVideoFrame进行了相关更改，以正确计算m_nOutputHeight。
* ZD #26614 — 紧急 — 第三方广告投放/编程 — 未能提供展示。
   * 通过处理XML解析中的案例，增强之前的修复，该案例中的问题在“空间”位于“等于”符号（例如）之前时可重现 &lt;vast version=&quot;2.0&quot;>
* ZD #29296 - Android：将AdSystem和Creative ID添加到CRS请求。
   * 现在，在1401和1403请求中包含“AdSystem”和“CreativeId”作为新参数。
* ZD #33062 - TVSDK在CDATA节点下的VAST响应中发生管道字符崩溃
   * NetworkConfiguration类中的API setEncodeUrlForTracking已删除，显示为要编码的URL中的不安全字符。
* ZD #33063 - CRS文件选择逻辑已损坏 — TVSDK未发送webm格式的CRS请求，而是改为发送3gpp文件的请求。
   * 现已修复逻辑。 在使用具有webm和3gpp格式的媒体文件时，为webm发送CRS请求。 在使用两种格式为3gpp的媒体文件时，会请求为最高比特率的3gpp文件发送CRS。
* ZD #33125 - Android应用程序崩溃，VMAP中包含特定的DoubleClick标记。
   * 修复了相应的场景以避免崩溃。
* ZD #32256 — 许可证轮换和密钥轮换问题 — Adobe访问。
   * 修复了使用SampleAES内容的DRM元数据初始化区段的问题。 可以对AES128内容正常使用。
* ZD #33619 — 快速转发在实时点附近停滞在缓冲状态的不断增长的播放列表内容。
   * 在特技播放模式下处理跨实时点时的情况。
* ZD #34151 - TimedMetadata对象顺序错误。
   * 如果两个TimedMetadata事件在时间轴中属于同一时间，则它们将以随机顺序出现。 维护了清单中它们的原始顺序。
* ZD #34189 — 尝试开始广告时间时出现问题。
   * 该问题与使用不连续性拼合的SSAI广告相关。 原因就是当我们寻找这类广告的开头时，我们寻找一个关键帧却找不到它。 原因是广告的最小音频时间戳在最小视频时间戳之前。 因此，我们最终在错误的fragmentDump数据处搜索关键帧。 现已修复。
* ZD #34528 - FireTV第三代转换器上的视频分辨率不能超过640x360。
   * 增强了修复功能，以包含最新的固件更新。
* ZD #34793 - TVSDK 2.5.x有时在VideoEngine假定auditudeSettings可用而不可用时，曾经与自定义内容解析程序一起崩溃。
   * 崩溃是由于对空共享指针(auditudeSettings)的函数调用而发生的。 在VideoEngineTimeline：：placeToSourceTimeline()中添加了条件检查，以确保auditudeSettings在该对象上调用任何内容之前均可用。
* ZD #32584 — 无法访问 &lt;extensions> vast响应的节点。
   * 修复了有关XML解析的问题，现在NetworkAdInfo提供了 &lt;extensions> 节点。
* ZD #35086 — 如果有特定的VMAP响应，则无法从播放器获取完整的扩展数据。
   * 该问题特定于扩展xml，因为如果扩展xml在属性值中有双引号，则XML解析将不起作用。 修复了问题。

**Android™ TVSDK 2.5.4**

* ZenDesk#33659 — 启用Webview远程调试的播放会话。
   * 默认情况下，WebViewDebugging设置为False。 要启用调试，请使用setWebContentsDebuggingEnabled(true)通过应用程序将设置为true。
* ZenDesk#33011 — 如果存在失败的CRS请求，则不会解析广告时间轴。
   * 当对广告的CRS请求失败时，时间线将解析并播放其余广告。
* ZenDesk#34528 - FireTV第三代转换器上的视频分辨率不能升级到640x360以上。
   * 视频分辨率会作为比特率切换而提高。
* ZenDesk#33192 — 通过AudioUpdatedEventListener：：onAudioUpdated检索曲目时，AudioTrack的名称为空。
   * 在FireTV Stick的少数场景中，在没有实际音频更新时触发onAudioUpdate事件。 此问题现已修复。

**Android™ TVSDK 2.5.3**

* Zendesk#32216 - TimedMetadata自定义标记订阅无法正常工作。
   * 我们将ID3数据作为字节数组（以支持APIC或通用数据）返回给客户端，而在1.4中返回字符串。 字节数组本身不处理空终止字符，因此，它对客户端显示特殊字符。 此问题现已修复。
* Zendesk#32670 — 播放器未故障切换到冗余播放列表
   * 此项现在工作正常，setNetworkDownVerificationUrl按预期工作。
* Zendesk#32369 — 隐藏式字幕显示不同的颜色垃圾或构件。
   * CC故障问题已在最新内部版本中修复
* Zendesk#25590 — 增强功能：TVSDK Cookie store(从C++到Java™)
   * Android™ TVSDK现在支持在Java™层(存储在Android™应用程序的CookieStore中)和C++ TVSDK层之间访问Cookie。
* Zendesk#32252 - TVSDK_Android_2.5.2.12似乎没有针对PTPLAY-20269的修补程序。此问题已修复并集成到2.5.2分支。
* Zendesk#31806 - PREPARING Player中的Auditude条卡在“正在准备”状态，因为响应xml的标记为空。 现已修复该问题。
* Zendesk#31727 - TVSDK 2.5隐藏式字幕字符被丢弃或拼写错误。
   * 问题已修复，并且我们不会删除任何字符/拼写错误。
* Zendesk#31485 - DrmManager，2.5版
   * 通过新的DrmManager（上下文上下文）创建DrmManager时存在一些问题。 已实现提供DRMManager的DRMService类。
* Zendesk#32794- 1080P分辨率流无法在Android™上播放。
   * 我们更改了SizeAvailableEvent。 以前， `getHeight()` 和 `getWidth()` 2.5中的SizeAvailableEvent方法，用于返回由媒体格式返回的Frame height和frame width。 它现在分别返回解码器返回的输出高度和输出宽度。
* Zendesk #19359Flash Player由于属性在集级别清单中#EXT-X-FAXS-CM位置而崩溃。
   * #EXT-X-FAXS-CM标记必须始终显示在顶部播放列表中，然后才能在播放列表中显示单个比特率或区段。

**Android™ TVSDK 2.5.2**

* Zendesk#17305隐藏式字幕中的伪像，具有不透明的背景。
TextFormat中的setTreatSpaceAsAlphaNum属性是公开的。 默认情况下，属性为False。 在客户端中将属性设置为True以解决深色空格问题。

* Zendesk#25097 CC显示包含带有CC设置的可视工件。
TextFormat中的setTreatSpaceAsAlphaNum属性是公开的。 默认情况下，属性为False。 在客户端中将属性设置为True以解决深色空格问题。

* 传出TVSDK播放器的Zendesk #31620用户代理字符串被截断。
用户代理字符串在128个字符后将不再被截断。
Adobe Primetime版本字符串将添加到系统用户代理。

* Zendesk #30809缺少SEEK_END事件可阻止应用程序转换为播放状态。
* 与之前的Primetime TVSDK版本相比，Zendesk #30415隐藏式字幕的“青色”颜色现在显示为较暗的蓝色（蓝绿色）。

  颜色从深青色更改为青色。

* 未下载/解析Zendesk #30727 VOD广告。

  在VMAP XML中，如果存在空的VAST标记，但没有明确的结束标记(&#39;&lt;/vast>&#39;)，并且后面没有换行符，则VMAP XML无法正确解析，广告可能无法播放。

**Android™ TVSDK 2.5.1**

* 设备特定(Samsung Galaxy Tab 4)崩溃；包含Auditude和点击广告的VOD DRM LBA。
* VHL — 从offset开始内容时，会发送错误的心跳调用。
* 播放VPAID广告时，VHL心率会调用事件:type:播放广告缺失。
* 在进入“完成”状态后，播放器会返回到“正在播放”状态，并显示后置广告的SKIP adBreakPolicy。
* Cookie未附加到传出广告回调。
* 广告提示点不可见。
* 无法加载具有单独的EAC3 SAP跟踪的HLS。
* 媒体播放器恢复后，由于TVSDK收到“屏幕开启”意图，播放器崩溃。

## 已知问题和限制 {#known-issues-and-limitations}

**Android™ TVSDK 2.7**

* TVSDK 2.7最多支持五个广告的并发分辨率。
* 对于VMAP响应，单个广告时间中的广告调用并发进行，并且广告时间按顺序解析。
* 在FER的情况下，同时解析每个机会中的广告调用。

### 以前版本中的已知问题和限制{#known-issues-limitations-previous-releases}

**Android™ TVSDK 2.5.6**

* 不支持同时使用多个VMAP广告时间。

**Android™ TVSDK 2.5.3**

此版本存在以下问题：

* 实时视频播放在低端设备上或网络条件较差时可能存在音频 — 视频同步问题。
* 对于FER流，virtualTime和localTime可能不同。 此外，包含偏移的FER不起作用。
* 对后期捆绑音频内容进行搜寻时，播放可能会卡住。
* WebVTT字幕可能会间歇性地变得与LIVE内容不同步。
* 间歇性地，在结束广告时间后可以看到快速播放的少量帧。
* 有时，即使播放了广告，也会为三包装器广告时间引发303错误。

**Android™ TVSDK 2.5.2**

此版本存在以下问题：

* 在低端设备上，实时视频播放可能存在音频 — 视频同步问题。
* 在搜寻到VOD媒体结尾时，播放可能会在某些时间停止。
* 对于FER流，virtualTime和localTime可能不同。 此外，带有偏移的FER不起作用。

**Android™ TVSDK 2.5.1**

此版本的TVSDK存在以下问题：

* 在低端设备上，实时视频播放可能存在音频 — 视频同步问题。
* 对于FER流，virtualTime和localTime可能不同。 此外，带有偏移的FER不起作用。
* 在VMAP XML中，如果存在没有显式结束标记的空VAST标记(&lt;/vast>)，并且后面没有换行符，则VMAP XML无法正确解析，广告可能无法播放。
* 不支持VPAID后置式广告。

## 有用资源 {#helpful-resources}

* [系统要求](/help/programming/tvsdk-2.7-for-android/c-psdk-android-2.7-requirements.md)
* [《 TVSDK 2.7 for Android™程序员指南》](/help/programming/tvsdk-2.7-for-android/overview-prod-audience-guide/c-psdk-android-2.7-overview-prod-audience-guide.md)
* [适用于API的TVSDK Android™ Javadoc参考](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html)
* [TVSDK Android™ C++ API文档](https://help.adobe.com/en_US/primetime/api/psdk/cpp/namespaces.html)  — 每个Java™类都有一个相应的C++类，并且C++文档比Java™文档包含更多说明性材料，因此请参阅C++文档以更深入地了解Java™ API。
* [适用于Android™ (Java™)的TVSDK 1.4到2.5迁移指南](/help/migration-guides/tvsdk-14-25-android.md)
* 有关处理屏幕打开/关闭情况的详细信息，请参阅 `Application_Changes_for_Screen_On_Off.pdf` 内部版本中包含的文件。
* 请参阅完整的帮助文档，网址为 [Adobe Primetime学习与支持](https://experienceleague.adobe.com/docs/primetime.html) 页面。

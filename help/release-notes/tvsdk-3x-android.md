---
title: Android版TVSDK 3.15发行说明
description: 适用于Android的TVSDK 3.15发行说明介绍了TVSDK Android 3.15中的新增或更改内容、已解决问题和已知问题以及设备问题
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: cd2c64ef-dd42-4dc2-805f-eeb64a8a53d9
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '5516'
ht-degree: 0%

---

# Android版TVSDK 3.15发行说明 {#tvsdk-for-android-release-notes}

适用于Android的TVSDK 3.15发行说明介绍了TVSDK Android 3.15中的新增或更改内容、已解决问题和已知问题以及设备问题。

Android参考播放器随Android TVSDK一起包含在分发的samples/目录中。 随附的README.md文件介绍了如何构建参考播放器。

>[!NOTE]
>
>要成功构建引用播放器（如随发行版一起分发的README.md中所述），请确保执行以下操作：
>
>1. 从下载VideoHeartbeat.jar [https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) （适用于Android v2.0.0的VideoHeartbeat库）
>1. 将VideoHeartbeat.jar提取到libs/文件夹中。


与以前的版本相比，适用于Android的TVSDK提供了许多性能改进。 它提供高品质的观看体验，并包含版本1.4的所有功能，但多CDN支持除外。

全面的支持和不支持功能集请参见 [功能表](#feature-matrix) 部分。

## Android TVSDK 3.15

此版本修复了以下问题：当缺少创意标记或以下情况时，应用程序会多次崩溃 [!UICONTROL url CDATA] 在中为空 [!UICONTROL VAST] 响应。

要了解此版本及更早版本中的错误修复，请参阅 [在TVSDK for Android中修复的问题](#resolved-issueszd).

### 以前版本中的新增功能和增强功能

**Android TVSDK 3.14**

此版本修复了以下情况下应用程序崩溃的问题 [!UICONTROL CDATA] 对于任意，节点为空 [!UICONTROL ClickTracking]， [!UICONTROL CustomClick] 或 [!UICONTROL CompanionClickTracking] VAST响应中的元素。

**Android TVSDK 3.13**

Widevine DRM流在FireTV设备（包括Fire TV第3代Pendant和Fire TV Cube第1代和第2代设备）上的ABR开关上冻结或显示黑色帧。

要解决此问题，请设置API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)` 在启动播放之前对于指定的Fire TV设备。 默认值为false。

**Android TVSDK 3.12**

Primetime引用应用程序的Gradle版本已更新到版本5.6.4。

要使用Android Studio设置和运行参考应用程序，请按照TVSDK zip文件提供的自述文件中的说明操作： `TVSDK_Android_x.x.x.x/samples/PrimetimeReference/src/README.md`.

有关当前版本中修复的常见客户问题，请参见 [已解决的问题](#resolved-issues) 部分。

**Android TVSDK 3.11**

* **允许获取保护系统特定标头(PSSH)框** - TVSDK允许提取与当前加载的媒体资源关联的Protection System特定的标头框。 新API `getPSSH()` 已添加至 `com.adobe.mediacore.drm.DRMManager`.

有关更多信息，请参阅 [Widevine DRM](../programming/tvsdk-3x-android-prog/android-3x-content-security/android-3x-drm-widevine.md).

**Android TVSDK 3.10**

该版本重点修复了中提到的常见客户问题 [已解决的问题](#resolved-issues) 部分。

**Android TVSDK 3.9**

* **通过HTTPS的安全交付** - Android TVSDK 3.9引入了通过HTTPS的安全交付功能，以无与伦比的规模和性能安全地交付内容。

   为了通过HTTPS实现安全交付，在中引入了新的API `NetworkConfiguration` 类。

   `public void setForceHTTPS (boolean value)`

   `public boolean getIsForceHTTPS()`

**Android TVSDK 3.8**

* **具有部分广告时间功能的前置支持**  — 通过此增强功能，TVSDK 3.8支持包含部分广告时间功能(PABI)的前置广告。

播放前置广告（如果可用），然后从直播点播放内容，模拟直播电视的体验。

**Android TVSDK 3.7**

* 对于Widevine测试内容，使用新的API `setMediaDrmCallback` DRManager类中的将覆盖MediaDrmCallback接口的缺省实现。

   `public static void setMediaDrmCallback(MediaDrmCallback callback)`

* 修复了无法处理的AppCrash错误 `MediaPlayerEvent.ITEM_UPDATED` 在C++层（Android 64位）中。

**Android TVSDK 3.6**

* **增强您的应用程序以满足64位要求**  — 本机库 `(libAVEAndroid.so)` 现已升级，并提供两个版本。 现有armeabi（32位）本机库位置已从 `/framework/Player to /framework/Player/armeabi` 以及中另外引入了一个arm64-v8a（64位）库 `/framework/Player/arm64-v8a.`

**版本3.5**

* **刚好及时解决广告** - TVSDK 3.5从时间轴中删除对播放的广告的支持。

* **启用对离线播放的支持**  — 通过离线播放，用户现在可以将视频内容下载到其设备并在未连接时观看。 有关详细信息，请参阅“[使用Android脱机播放](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_3.5.pdf).”

**版本3.4**

* TVSDK现在支持CBC加密流和纯流的CMAF流播放。

**版本3.3**

* **API更改**

   * 添加了一个新的API到 `NetworkConfiguration::setNumOfTimesManifestRetryBeforeError(n)*` 处理网络错误和超时。
      * 其中，(n)是重试的次数。

**版本3.2**

* **并行广告解析和清单下载支持**

   * TVSDK 3.2支持对所有广告请求和广告时间（VMAP除外）的同步分辨率，而不是顺序分辨率。

   * 同时下载广告时间中的所有广告清单。

* **启用了广告解析和清单下载超时支持。**

   * 用户现在可以为整体广告解析和清单下载设置超时值。  对于VMAP，超时值适用于单个广告时间，因为所有广告时间都是按顺序解析的。

* **在AdvertisingMetadata类中引入了新的API：**

   * `void setAdResolutionTimeout(int adResolutionTimeout)`

   * `int getAdResolutionTimeout()`

   * `void setAdManifestTimeout(int adManifestTimeout)`

   * `int getAdManifestTimeout()`

* **已从AdvertisingMetadata类中删除以下API：**

   * `void setAdRequestTimeout(int adRequestTimeout)`

   * `int getAdRequestTimeout()`

* **通过AC3/EAC3音频编解码器启用流播放**

   * `void alwaysUseAC3OnSupportedDevices(boolean val)` 在 `MediaPlayer` 类

* **TVSDK支持加密Widevine CTR的CMAF和纯流播放。**

* **现在支持播放4K HEVC流。**

* **并行广告调用请求** - TVSDK现在并行预取20个广告调用请求。

**版本3.0**

* **TVSDK 3.0支持高效视频编码(HEVC)流。**

* **即时 — 解决广告更接近广告标记的问题**
延迟广告解析现在可单独解析每个广告时间。 以前，广告解析是分两阶段进行的：在播放开始之前解析前置式广告，在播放开始之后合并所有中置/后置式广告插槽。 借助此增强功能，现在可以在广告提示点之前的特定时间解析每个广告时间。

>[!NOTE]
>
>延迟广告解析现在更改为默认关闭，明确需要启用。

添加了一个新的API到 `AdvertisingMetadata::setDelayAdLoadingTolerance` 以获取与此广告元数据关联的延迟广告加载容差。\
现在，在PREPARATION之后立即允许搜寻，搜寻广告时间将导致在完成搜寻之前立即解决。\
信令模式 `SERVER_MAP` 和 `MANIFEST_CUES` 受支持。

有关更多信息，请参阅 [《 TVSDK 3.0 for Android程序员指南》](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/c-lazy-ad-resolving.md) 关于API和事件更改。

* **已更新 `targetSdkVersion` 到最新版本**

已更新 `targetSdkVersion` 从19到27，顺利运行。

* **Placement.Type getPlacementType()现在是接口TimelineMarker上的方法**

   此方法将返回投放类型Placement.Type.PRE_ROLL、Placement.Type.MID_ROLL或Placement.Type.POST_ROLL。 如果广告时间未解析，则TimelineMarker界面上的getDuration()方法将返回0。

**版本2.5.6。**

* **TVSDK 2.5支持Android P。**

* **启用背景音频**

   要在应用程序从前台移动到后台时启用音频播放，应用程序应调用 `enableAudioPlaybackInBackground` 当播放器处于“已准备”状态时，将true作为参数的MediaPlayer API。

* **MediaPlayer类中的alwaysUseAudioOutputLatency(boolean val)**

设置后，在音频时间戳计算中使用输出延迟。
布尔参数val - True将在音频时间戳计算中使用音频输出延迟。

* **优化后即使在带宽速度突然下降的情况下也能获得最佳播放体验**

现在，TVSDK会根据需要取消正在进行的区段下载，并动态切换到相应的演绎版。 这是通过在比特率之间无缝切换来实现的，而不会出现中断。

**版本2.5.5**

* **部分广告时间插入**

   类似于电视的体验：在广告中间加入，而不触发部分观看广告的跟踪。\
   示例：用户在包含三个30秒广告的90秒广告时间的中间（40秒）加入。 此时是插播中第二个广告的10秒。

   * 第二个广告播放剩余的时长（20秒），然后是第三个广告。

   * 不触发播放的部分广告（第二个广告）的广告跟踪器。 仅触发第三个广告的跟踪器。

* **通过HTTPS的安全广告加载**

   Adobe Primetime提供了一个选项，用于请求通过https对primetime广告服务器和CRS的首次调用。

* **向CRS请求添加了AdSystem和Creative Id**

   现在包括 `AdSystem` 和 `CreativeId` 作为1401和1403请求中的新参数。

* **删除了NetworkConfiguration类中的API setEncodeUrlForTracking** 因为URL中的不安全字符应该编码。

**版本2.5.4**

Android TVSDK v2.5.4提供了以下更新和API更改：

* 默认值的更改 `WebViewDebbuging`

   `WebViewDebbuging` 值设置为 `Fals`e默认设置。 要启用该功能，请调用 `setWebContentsDebuggingEnabled(true)` 在应用程序中。

* **OpenSSL和Curl版本升级**

   已将libcurl更新至v7.57.0，将OpenSSL更新至v1.0.2k。

* VAST响应对象的应用程序级别访问权限

   引入了一个新的API `NetworkAdInfo::getVastXml()` 用于提供对应用程序的VAST响应对象的访问权限。

**版本2.5.3**

Android TVSDK v2.5.3提供了以下更新和API更改。

* 鼓励所有使用CRS的TVSDK客户使用TVSDK 2.5.3.85或最新的Android版升级其应用程序。 这将是现有应用程序实施的下拉式替代。 TVSDK升级后，在代理工具（例如：Charles）中检查CRS创意URL请求，并确认路径中的主机名和版本反映为如下面的示例URL结构中所示。

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* TVSDK的用户代理可自定义：我们添加了一些新的API以自定义用户代理。

   * `setCustomUserAgent(String value)`
   * `getCustomUserAgent()`

* 在Android应用程序和TVSDK之间共享Cookie： Android TVSDK现在支持在JAVA层（存储在Android应用程序的CookieStore中）和C++ TVSDK层之间访问Cookie。 现在，可以设置和/或修改本机C++层中的Cookie，因为它们将向Java Cookie Store公开。

* API更改：

   * 新事件 `CookiesUpdatedEvent` 添加了。 当媒体播放器的Cookie更新时，媒体播放器会调度该事件。

   * 添加了一个新的API到 `NetworkConfiguration::set/ getCustomUserAgent()` 以使用自定义用户代理。

   * 添加了一个新的API到 `NetworkConfiguration::set/ getEncodedUrlForTracking` 强制编码不安全字符。

   * 添加了一个新的API到 `NetworkConfiguration::getNetworkDownVerificationUrl()` 设置故障转移时的网络验证URL。

   * 新资产将添加到 `TextFormat::treatSpaceAsAlphaNum` 定义在显示字幕时是否将空格视为字母数字。

* 中的更改 `SizeAvailableEvent`. 以前， `getHeight()` 和 `getWidth()` 方法 `SizeAvailableEvent` 在2.5.2中，用于返回帧高度和帧宽度，该参数由媒体格式返回。 现在，它分别返回解码器返回的输出高度和输出宽度。

* 缓冲行为的更改：缓冲行为已更改。 由应用程序开发人员自行决定缓冲为空时要执行的操作。 2.5.3在缓冲区为空的情况下使用播放缓冲区大小。

**版本2.5.2**

Android TVSDK v2.5.2提供了重要的错误修复和一些API更改。

**版本2.5.1**

Android 2.5.1中发布的重要新功能。

* **性能改进 —** 新的TVSDK 2.5.1架构带来了大量性能改进。 根据第三方基准测试研究的统计数据，与业界平均水平相比，新架构的启动时间减少了5倍，丢帧减少了3.8倍：

* **即时打开以进行VOD和直播 —** 启用“即时打开”后，TVSDK会在播放开始之前初始化并缓冲媒体。 由于您可以在后台同时启动多个MediaPlayerItemLoader实例，因此可以缓冲多个流。 当用户更改频道，并且流已正确缓冲时，新频道上的播放立即开始。 TVSDK 2.5.1还支持的“即时开启” **实时** 流也是如此。 当实时窗口移动时，实时流将被重新缓冲。

* **改进了ABR逻辑 —** 该逻辑基于缓冲区长度、缓冲区长度变化率和测量带宽。 这样可以确保ABR在带宽波动时选择正确的比特率，并通过监控缓冲区长度变化的速率来优化比特率切换的实际次数。

* **部分区段下载/子区段 —** TVSDK进一步减小了每个片段的大小，以尽快开始播放。 ts片段必须每两秒具有一个关键帧。

* **延迟广告分辨率 —** TVSDK不会等待非前置广告解析后再开始播放，因此缩短了启动时间。 直到解决所有广告之后，才允许使用搜寻和特技播放等API。 这适用于与CSAI一起使用的VOD流。 在广告解析完成之前，不允许执行搜寻和快速前进等操作。 对于实时流，此功能无法在实时活动期间启用广告解析。

* **永久网络连接 —** 此功能允许TVSDK创建和存储永久网络连接的内部列表。 这些连接可重复用于多个请求，而不是为每个网络请求打开一个新连接，然后将其销毁。 这会提高网络代码的效率并减少延迟，从而实现更快的播放性能。
当TVSDK打开一个连接时，它要求服务器提供 *保持活动状态* 连接。 某些服务器可能不支持此类连接，在这种情况下，TVSDK将回退以再次为每个请求建立连接。 此外，尽管持久连接默认处于打开状态，但TVSDK现在提供了一个配置选项，以便应用程序可以根据需要关闭持久连接。

* **并行下载 —** 并行下载视频和音频而不是串行下载可减少启动延迟。 此功能允许播放HLS Live和VOD文件，优化服务器的可用带宽使用率，降低在运行时进入缓冲区的概率，并最大限度地减少下载和播放之间的延迟。

* **并行广告下载 —** TVSDK会在点击广告时间之前与内容播放并行预取广告，从而实现广告和内容的无缝播放。

* **播放**

* **MP4内容播放 —** 在TVSDK中，MP4短剪辑无需重新编码即可播放。

   >[!NOTE]
   >
   >MP4播放不支持ABR切换、特技播放、广告插入、后期音频绑定和子分段。

* **具有自适应比特率(ABR)的特技播放 —** 此功能允许TVSDK在特技播放模式中切换iFrame流。 您可以使用非iFrame配置文件以较低的速度进行特技播放。

* **更流畅的戏法游戏。** 这些改进增强了用户体验：

   * 在特技播放期间，基于带宽和缓冲器配置文件的自适应比特率和帧速率选择

   * 使用主流而不是IDR流获得最高30 fps的快速播放。

* **内容保护**

   * **基于分辨率的输出保护 —** 此功能将播放限制绑定到特定分辨率，从而提供更细粒度的DRM控制。

* **工作流支持**

   * **直接账单集成 —** 这会将计费量度发送到Adobe Analytics后端，该后端由Adobe Primetime针对客户使用的流进行认证。

   TVSDK根据客户销售合同自动收集量度，以生成计费所需的定期使用情况报告。 在每个流开始事件上，TVSDK使用Adobe Analytics数据插入API将计费指标（如内容类型、启用广告插入的标记和启用drm的标记）根据计费流的持续时间发送到Adobe Analytics Primetime拥有的报表包。 这不会干扰客户自己的Adobe Analytics报表包或服务器调用或使其包含在内。 根据请求，定期向客户发送此计费使用情况报告。 这是仅支持使用计费的计费功能的第一个阶段。 可以使用文档中描述的API，根据销售合同对其进行配置。 此功能默认处于启用状态。 要关闭此功能，请参阅参考播放器示例。

   * **改进的故障切换支持 —** 实施了其他策略以继续不间断播放，尽管主机服务器、播放列表文件和区段出现故障。


* **广告**

   * **Moat集成 —** 支持从Moat测量广告可见性。

   * **随附横幅 —** 随附横幅与线性广告一起显示，并且通常在广告结束后继续显示在视图中。 这些横幅可以是html类型(HTML片段)或iframe类型（iframe页面的URL）。

* **分析**

   * **VHL 2.0 -** 这是最新的优化视频心率库(VHL)集成，可自动收集Adobe Analytics的使用情况数据。 API的复杂性已降低，以简化实施。 下载VHL库 [适用于Android的v2.0.0](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) 并提取libs文件夹中的JAR文件。

* **SizeAvaliableEventListener**

   * `getHeight()` 和 `getWidth()` 方法 `SizeAvailableEvent` 现在将分别返回高度和宽度的输出。 显示长宽比可按如下方式计算：

      ```java
      SizeAvailableEvent e;
      DAR = e.getWidth()/ e.getHeight();
      ```

      以Sar宽度和Sar高度表示的存储宽高比还可用于计算帧宽度和帧高：

      ```java
      SAR = e.getSarWidth()/e.getSarHeight();
      frameHeight = e.getHeight();
      frameWidth = e.getWidth()/SAR;
      ```

* **Cookie**

   * Android TVSDK现在支持访问存储在Android应用程序的CookieStore中的JAVA Cookie。 提供一个回调API (onCookiesUpdated)，每当有新Cookie加入时便进行记录 **Set-Cookie** 响应标头。 通过使用CookieStore在该特定URI/域中设置这些Cookie值，这些Cookie可用作用于不同URI/域的HttpCookie的列表。 同样，TVSDK中的Cookie值也是使用CookieStore add API更新的。

## 特征矩阵 {#feature-matrix}

适用于Android的TVSDK支持许多功能，您可以实施这些功能向视频应用程序添加功能。

在下面的功能表中，“Y”表示当前版本支持该功能。

| 功能 | 内容类型 | HLS |
|---|---|---|
| 常规播放（播放、暂停、搜寻） | VOD +实时 | Y |
| FER — 常规播放（播放、暂停、搜寻） | FER VOD | Y |
| 在广告播放时搜寻 | VOD +实时 | 不支持 |
| HEVC播放 | VOD +实时 | 仅限fMP4容器 |
| AC3和EAC3 | VOD +实时 | 不支持 |
| MP3 | VOD | 不支持 |
| MP4内容播放 | VOD | Y |
| 自适应比特率切换逻辑 | VOD +实时 | Y |
| 纯音频播放 | VOD +实时 | Y |
| 多CDN支持 | VOD +实时 | 不支持 |
| 使用纯音频媒体播放广告 | VOD +实时 | 不支持 |
| 隐藏字幕 — 608/708 | VOD +实时 | Y |
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
| 偏移播放 | VOD +实时 | Y |
| 特技游戏 | VOD +实时 | Y |
| 戏法游戏中的慢动作 | VOD +实时 | 不支持 |
| Smooth Trick Play（使用ABR） | VOD +实时 | Y |
| ID3解析 | VOD +实时 | Y |
| 广告封锁 | VOD +实时 | 不支持 |
| 即时打开 | VOD +实时 | 不支持 |
| 间断标记支持 | VOD +实时 | Y |
| 302重定向粘性 | VOD +实时 | Y |

| 功能 | 内容类型 | HLS |
|---|---|---|
| 常规播放，启用广告 | VOD +实时 | Y |
| 启用了广告的FER内容 | VOD | Y |
| 默认广告行为 | VOD +实时 | Y |
| VAST 2.0/3.0 | VOD +实时 | Y |
| VMAP 1.0 | VOD +实时 | Y |
| MP4广告 | VOD +实时 | Y（来自CRS） |
| 启用广告的Trick Play | VOD +实时 | Y |
| 仅广告 | VOD | Y |
| 定位参数 | VOD +实时 | Y |
| 自定义参数 | VOD +实时 | Y |
| 自定义广告行为 | VOD +实时 | Y |
| 自定义广告标记 | 实时 | Y |
| 自定义广告解析程序 | VOD +实时 | Y |
| Freewheel自定义广告解析程序 | VOD | Y |
| C3 | VOD +实时 | 不支持 |
| 延迟广告解析 | VOD | Y |
| 中断标记支持 — SSAI | VOD +实时 | Y |
| 伴随广告、横幅广告和可点击广告 | VOD +实时 | Y |
| VPAID 2.0 | VOD +实时 | Y (JS) |
| 早期广告退出 | 实时 | Y |
| 基于规则的创意优先级排序 | VOD +实时 | Y |
| CRS规则 | VOD +实时 | Y |
| JSON广告解析程序 | VOD +实时 | 不支持 |
| Moat集成 | VOD +实时 | Y |
| 部分广告时间插入 | 实时 | Y |

| 功能 | 内容类型 | HLS |
|---|---|---|
| AES加密 | VOD +实时 | Y |
| 示例AES加密 | VOD +实时 | Y |
| 标记化的流 | VOD +实时 | Y |
| Widevine DRM | VOD +实时 | 仅限fMP4容器 |
| Primetime DRM | VOD +实时 | Y |
| 外部播放(RBOP) | VOD +实时 | 仅限Primetime DRM |
| 许可证轮换 | VOD +实时 | 仅限Primetime DRM |
| 密钥轮替 | VOD +实时 | 仅限Primetime DRM |

| 功能 | 内容类型 | HLS |
|---|---|---|
| Adobe Analytics VHL集成 | VOD +实时 | Y |
| 计费 | VOD +实时 | Y |

## 已解决的问题 {#resolved-issues}

如果解决方法与报告的问题相关联，则会显示Zendesk引用，例如ZD#xxxxx。

**Android TVSDK 3.15**

本节概述TVSDK 3.14 Android版本中已解决的问题。

* ZD#46903 — 当创意标记缺失或以下情况时，应用程序崩溃多次 [!UICONTROL url CDATA] 在中为空 [!UICONTROL VAST] 响应。

**Android TVSDK 3.14**

* ZD#46903 — 应用程序崩溃时 [!UICONTROL CDATA] 对于任意，节点为空 [!UICONTROL ClickTracking]， [!UICONTROL CustomClick] 或 [!UICONTROL CompanionClickTracking] 中的元素 [!UICONTROL VAST] 响应。

### 以前版本中已解决的问题

**Android TVSDK 3.12**

* ZD#40584 - Primetime引用应用程序未使用最新Gradle版本构建。

**Android TVSDK 3.11**

* ZD#41252 - Android 7.1之后，WebVTT中的韩文字符损坏。

**Android TVSDK 3.10**

* ZD#40340 — 在阻止列出所有TS (TypeScript)文件后，应用程序在尝试播放时崩溃，并显示“应用程序未响应”错误。

**Android TVSDK 3.8**

* 未添加新问题。

**Android TVSDK 3.7**

* 未添加新问题。

**Android TVSDK 3.6**

* 未添加新问题。

**版本3.5**

* ZD#37503 — 将缓存CRS规则的JSON响应，以避免重复请求。

**版本3.4**

* ZD#37996 — 修复了线性和VOD CMAF HEVC流播放时断续续的问题。
* ZD#37706 — 修复了乱码字幕的问题。
* ZD#37622 — 修复了关于特定广告的致命URISyntaxErrors的问题。
* ZD#36938 — 修复了比特率向下切换到中间比特率，然后在退出特技播放后提取到最高比特率的问题。

**版本3.3**

* ZD#37394 - CMAF资源快速前进会在速度更改后导致伪像。
   * 修复了在特技播放期间配置文件更改时出现的问题。
* ZD#37396 — 某些中置工作流程和后置工作流程缺少广告跟踪事件。
   * 修复了与广告跟踪事件有关的特定情况。
* ZD#37491 — 没有包含错误元的HTTP状态代码。
   * 已处理在栈栈中较高的位置传播网络错误。
* ZD#37808 -允许列表新的自定义标头。
   * SSAI_TAG支持作为此修复的一部分添加。
* ZD#37622 — 特定Ad Pod中的URISyntax错误。
   * 修复了向客户Android应用程序提供包含未编码%的广告时有关流播放崩溃的问题
* ZD#37631 - Android TVSDK的主控清单重试机制。
   * 在网络配置中添加了用于处理此增强功能的新API。 如果未使用此API，则不会重试清单。 如果使用，则将重试清单以处理网络错误和超时。

**版本3.2**

* ZD#37493 — 对于序列中的第一个广告，实时播放的跟踪信标不会间歇性地触发。
* ZD#36985- VMAP响应中不发送空广告时间的跟踪信标。
* ZD#37134 - TVSDK会间歇性地为VMAP响应抛出错误的ID。

**版本3.0**

* ZD#33740 - TVSDK在创建MediaPlayer对象并调用replaceCurrentResource()后立即引发不需要的警告

   * 通过仅在播放器处于暂停状态时调用restore改进了之前的修复

* ZD#36442 — 每次新播放都会断开远程调试会话的连接，导致无法调试。

   * 默认情况下，无法在Web视图上进行调试，因为默认情况下未启用调试。 如果需要，应用程序应通过调用setWebContentsDebuggingEnabled(true)对从MediaPlayer.getCustomAdView()返回的对象启用调试。

* ZD#33688 — 支持及时广告解决

   * 广告时间是在广告时间位置之前的指定时间间隔解析的。

* ZD#36441 — 实时时段的持续时间不断增加超过5分钟，从而导致出现多个问题。

   * 修复了在计算导致此问题的虚拟实时点时，virtualStartTime被添加两次的问题。

**Android TVSDK 2.5.6**

* ZD #34992 — 隐藏式字幕中的语言为空。

   * 修复了TVSDK未从主清单中解析#EXT-X-MEDIA：TYPE=CLOSED-CAPTIONS以获取字幕跟踪详细信息的问题。

* ZD #35078 - Android P验证。

   * TVSDK 2..5.6已通过最新Android P测试版内部版本验证。 由于新的Android操作系统，未发现任何问题。

* ZD #34149 — 即使遇到错误，播放器仍会继续请求清单。

   * 修复了TVSDK进行重复调用的情况，即使所有用户档案都已关闭（404错误）。

* ZD #31533 — 在将应用程序发送到后台后，在Android上播放音频。

   * 已添加 `enableAudioPlaybackInBackground` MediaPlayer的API，应使用“True”作为参数（当播放器处于“已准备”状态时）调用，以便在应用程序处于后台时启用音频播放。

**Android TVSDK 2.5.5**

* ZD #21647 — 当实际视频大小为640x360时，Android TVSDK会通知640x368。

   * 由于变量m_nOutputHeight（在AndroidMCVideoDecoder内）使用帧高度而不是实际输出高度进行更新。 对函数getVideoFrame进行了相关更改，以正确计算m_nOutputHeight。

* ZD #26614 — 紧急 — 第三方广告投放/编程 — 未能提供展示次数。

   * 通过处理XML解析中的案例，增强了以前的修复，在这种情况下，当“space”位于“equal”符号之前时，问题可重现，例如 &lt;vast version=&quot;2.0&quot;>

* ZD #29296 - Android：将AdSystem和Creative ID添加到CRS请求。

   * 现在，在1401和1403请求中包含“AdSystem”和“CreativeId”作为新参数。

* ZD #33062 - TVSDK在CDATA节点下的VAST响应中发生管道字符时崩溃

   * NetworkConfiguration类中的API setEncodeUrlForTracking已删除，显示为要编码的URL中的不安全字符

* ZD #33063 - CRS文件选择逻辑已损坏 — TVSDK未发送webm格式的CRS请求，而是改为发送3gpp文件。

   * 现在修复了逻辑。 在使用webm和3gpp格式的媒体文件时，会请求为webm发送CRS。 而在同时使用3gpp格式的媒体文件时，会请求为比特率最高的3gpp文件发送CRS。

* ZD #33125 - Android应用程序崩溃，VMAP中包含特定的DoubleClick标记。

   * 修复了相应情况以避免崩溃。

* ZD #32256 — 许可证轮换和密钥轮换问题 — Adobe访问

   * 修复了使用SampleAES内容的DRM元数据初始化区段的问题。 可对AES128内容正常使用。

* ZD #33619 — 快速转发在实时点附近陷入缓冲状态的不断增长的播放列表内容。

   * 处理在特技播放模式下跨实时点时的情况

* ZD #34151 - TimedMetadata对象顺序错误。

   * 如果两个TimedMetadata事件在时间轴中属于同一时间，则它们将以随机顺序出现。 在清单中维护了原始顺序。

* ZD #34189 — 尝试开始广告时间时出现问题。

   * 该问题与使用不连续性拼合的SSAI广告有关。 原因就是当我们开始寻找这类广告时，我们寻找一个关键帧却找不到它。 原因是广告的最小音频时间戳在最小视频时间戳之前。 因此，我们最终在错误的fragmentDump数据处搜索关键帧。 现已修复。

* ZD #34528 - FireTV第3代转换器上的视频分辨率不能升级到640x360以上。

   * 增强了修复以包含最新的固件更新

* ZD #34793 - TVSDK 2.5.x以前在VideoEngine假定auditudeSettings可用而不可用时，在某些情况下使用自定义内容解析器崩溃。

   * 由于对Null共享指针(auditudeSettings)的函数调用而发生崩溃。 在VideoEngineTimeline：：placeToSourceTimeline()中添加了条件检查，以确保在调用该对象上的任何内容之前，auditudeSettings都可用。

* ZD #32584 — 无法访问 &lt;extensions> vast响应的节点。

   * 修复了有关XML解析的问题，现在NetworkAdInfo提供了 &lt;extensions> 节点

* ZD #35086 — 对于特定的VMAP响应，无法从播放器获取完整的扩展数据。

   * 该问题特定于扩展xml，因为如果扩展xml的属性值中包含双引号，则XML解析将不起作用。 修复了问题。

**Android TVSDK 2.5.4**

* ZenDesk#33659 — 启用Webview远程调试的播放会话。

默认情况下，WebViewDebugging设置为False。 要启用调试，请使用setWebContentsDebuggingEnabled(true)通过应用程序将设置为true。

* ZenDesk#33011 — 如果CRS请求失败，广告时间轴未解析。

   当对广告的CRS请求失败时，时间轴会得到解析并且会播放其余广告。

* ZenDesk#34528 — 在FireTV第三代转换器上，视频分辨率不能升级到640x360以上。

   视频分辨率会随着比特率切换而提高。

* ZenDesk#33192 — 通过AudioUpdatedEventListener：：onAudioUpdated检索曲目时，AudioTrack的名称为空。

   在FireTV Stick的少数场景中，在没有实际音频更新时，会触发onAudioUpdate事件。 此问题现已修复。

**Android TVSDK 2.5.3**

* Zendesk#32216 - TimedMetadata自定义标记订阅不起作用。

   我们将ID3数据作为字节数组（以支持APIC或通用数据）返回到客户端，而在1.4中返回字符串。 字节数组本身不处理null终止字符，因此，它向客户端显示的是特殊字符。 此问题现已修复。
* Zendesk#32670 — 播放器未故障切换到冗余播放列表

   此项现在工作正常，setNetworkDownVerificationUrl按预期工作。
* Zendesk#32369 — 隐藏式字幕显示不同的颜色垃圾或构件。

   CC故障问题已在最新内部版本中修复
* Zendesk#25590 — 增强： TVSDK Cookie存储(从C++到JAVA )

   Android TVSDK现在支持在JAVA层（存储在Android应用程序的CookieStore中）和C++ TVSDK层之间访问Cookie。
* Zendesk#32252 - TVSDK_Android_2.5.2.12似乎没有针对PTPLAY-20269的修补程序

   此问题已得到修复并集成到2.5.2分支。
* Zendesk#31806 — 准备中的自大棒

   播放器在“正在准备”状态中卡住，因为响应xml具有空标记。 现已修复该问题。
* Zendesk#31727 - TVSDK 2.5隐藏式字幕字符被丢弃或拼写错误。

   问题已修复，并且我们不会删除任何字符/拼写错误。
* Zendesk#31485 - 2.5中的DrmManager

   通过新的DrmManager（上下文上下文）创建DrmManager时存在一些问题。 实现了DRMService类，该类将提供DRMManager。
* Zendesk#32794 — 在Android上未播放1080P分辨率流

   在2.5中，我们更改了SizeAvailableEvent的SizeAvailableEvent和Previous、getHeight()和getWidth()方法，用于返回由媒体格式返回的帧高度和帧宽度。 它现在分别返回解码器返回的输出高度和输出宽度。
* Zendesk #19359Flash Player由于属性在集级别清单中#EXT-X-FAXS-CM位置而崩溃。

   #EXT-X-FAXS-CM标记必须始终显示在顶部播放列表中，然后单个比特率或区段才会显示在播放列表中。

**Android TVSDK 2.5.2**

* Zendesk#17305具有非不透明背景的隐藏式字幕中的伪像。

   TextFormat中的setTreatSpaceAsAlphaNum属性公开。 默认情况下，属性为False。 在客户端中将属性设置为True以解决深色空间问题。

* Zendesk#25097 CC显示具有带有CC设置的视觉对象。

   TextFormat中的setTreatSpaceAsAlphaNum属性公开。 默认情况下，属性为False。 在客户端中将属性设置为True以解决深色空间问题。

* 传出TVSDK播放器的Zendesk #31620用户代理字符串被截断。

   用户代理字符串在128个字符后将不再被截断。

   Adobe Primetime版本字符串已添加到系统用户代理。

* Zendesk #30809缺少SEEK_END事件可阻止应用程序转换为正在播放状态。
* 与之前的Primetime TVSDK版本相比，Zendesk #30415隐藏式字幕的“青色”颜色现在显示为较深的蓝色（蓝绿色）。

   颜色从深青色更改为青色。

* 未下载/解析Zendesk #30727 VOD广告。

   在VMAP XML中，如果存在没有显式结束标记(&#39;)的空VAST标记&lt;/vast>&#39;)且后面没有换行符，则VMAP XML无法正确解析，广告可能无法播放。

**Android TVSDK 2.5.1**

* 设备特定(Samsung Galaxy Tab 4)崩溃；VOD DRM LBA with Auditude并单击广告。
* VHL — 从偏移量开始内容时，会发送不正确的心率调用。
* 播放VPAID广告时，VHL心率会呼叫事件:type:播放广告缺失。
* 在进入“完成”状态后，对于后置广告，播放器将返回到“正在播放”状态并显示SKIP adBreakPolicy。
* Cookie未附加到传出广告回调。
* 广告提示点不可见。
* 无法加载具有单独的EAC3 SAP跟踪的HLS。
* 媒体播放器恢复后，TVSDK收到Screen On意图，播放器崩溃。

## 已知问题和限制 {#known-issues-and-limitations}

**Android TVSDK 3.11**

* 未添加任何新限制。

### 以前版本中的已知问题和限制

**Android TVSDK 3.10**

* 未添加任何新限制。

**Android TVSDK 3.8**

* 未添加任何新限制。

**Android TVSDK 3.7**

* 未添加任何新限制。

**Android TVSDK 3.6**

* 未添加任何新限制。

**Android TVSDK 3.5**

* 未添加新的限制。

**Android TVSDK 3.4**

* 尚未验证CMAF (CBC)流是否支持ID3、隐藏式字幕、后期绑定音频。
* 在某些设备上，由于在CMAF流上的特技播放期间视频失真可能出现在顶部，因此存在可再现性低的问题。

**Android TVSDK 3.3**

* CMAF流播放不支持clcp：c608字幕。

**Android TVSDK 3.2**

* TVSDK 3.2不支持CMAF示例AES和AES128流播放。
* HEVC CMAF流不支持隐藏式字幕播放。
* 在围绕非加密区段执行搜索时，WV加密流会显示绿色颜色。
* CMAF流不支持ID3事件。
* hls流不支持TTML字幕格式。

**Android TVSDK 3.0**

* 此版本中的HEVC支持具有以下限制

   * 不支持DRM
   * CC (CEA 608/708)支持未经验证
   * 4K支持尚不存在
   * 未验证ID3标记支持

* 对于广告进度事件，时间轴栏可能无法反映100%准确的广告播放时间。 作为解决方法，我们可以使用 `adcompleteevent` 了解广告播放完成并更新UI，以达到各种目的，如更新时间线栏、删除广告相关UI等。
* 从VMAP返回的大量广告调用不遵循即时Lookahead位置。

**Android TVSDK 2.5.6**

* 不支持同时使用多个VMAP广告时间。

**Android TVSDK 2.5.3**

此版本具有以下问题：

* 实时视频播放在低端设备上或网络条件较差时可能存在音频 — 视频同步问题。
* 对于FER流，virtualTime和localTime可能不同。 此外，带有偏移的FER不起作用。
* 对后期绑定音频内容进行搜寻时，播放可能会卡住。
* 有时，LIVE内容的webVTT字幕可能会不同步。
* 间歇性地，在结束广告时间后可以看到少量帧的快速播放。
* 有时候，即使播放了广告，也会对三个包装器广告时间引发303错误。

**Android TVSDK 2.5.2**

此版本具有以下问题：

* 在低端设备上，实时视频播放可能存在音频 — 视频同步问题。
* 在搜寻到VOD媒体结尾时，播放可能会在某些时候停止。
* 对于FER流，virtualTime和localTime可能不同。 此外，带有偏移的FER不起作用。

**Android TVSDK 2.5.1**

此版本的TVSDK存在以下问题：

* 在低端设备上，实时视频播放可能存在音频 — 视频同步问题。
* 对于FER流，virtualTime和localTime可能不同。 此外，带有偏移的FER不起作用。
* 在VMAP XML中，如果存在没有显式结束标记的空VAST标记(&lt;/vast>)，并且后面没有换行符，则VMAP XML无法正确解析，广告可能无法播放。
* 不支持VPAID后置广告。

## 有用资源 {#helpful-resources}

* [系统要求](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/android-3x-requirements.md)
* [《 TVSDK 3.10 for Android程序员指南》](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/overview-prod-audience-guide/android-3x-overview-prod-audience-guide.md)
* [TVSDK Android Javadoc for API参考](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html)
* [TVSDK Android C++ API文档](https://help.adobe.com/en_US/primetime/api/psdk/cpp_3.5/namespaces.html)  — 每个Java类都有一个相应的C++类，并且C++文档比Javadocs包含更多说明性材料，因此请参阅C++文档以更深入地了解Java API。
* [适用于Android (Java)的TVSDK 1.4到2.5迁移指南](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* 有关处理屏幕打开/关闭方案，请参阅 `Application_Changes_for_Screen_On_Off.pdf` 内部版本中包含的文件。
* 请参阅完整的帮助文档，网址为 [Adobe Primetime学习与支持](https://helpx.adobe.com/support/primetime.html) 页面。

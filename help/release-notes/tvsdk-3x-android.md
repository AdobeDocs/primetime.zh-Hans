---
title: 适用于Android的TVSDK 3.12发行说明
seo-title: 适用于Android的TVSDK 3.12发行说明
description: TVSDK 3.12 for Android发行说明描述了TVSDK Android 3.12中的新增或更改功能、已解决和已知问题以及设备问题
seo-description: TVSDK 3.12 for Android发行说明描述了TVSDK Android 3.12中的新增或更改功能、已解决和已知问题以及设备问题
uuid: 685d46f5-5a02-4741-af5c-91e91babd6f7
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: 3a27379f-3cef-4ea3-bcae-21382dc1e9fd
translation-type: tm+mt
source-git-commit: 33509042e32c2167fab21788042bfb2bb877c0f4
workflow-type: tm+mt
source-wordcount: '5418'
ht-degree: 0%

---


# TVSDK 3.12 for Android发行说明{#tvsdk-for-android-release-notes}

TVSDK 3.12 for Android发行说明描述了TVSDK Android 3.12中的新增或更改功能、已解决和已知问题以及设备问题。

Android TVSDK随Android参考播放器提供在您的分发示例／目录中。 随附的README.md文件介绍如何构建参考播放器。

>[!NOTE]
>
>要成功构建引用播放器（如随版本分发的README.md中所述），请确保执行以下操作：
>
>1. 从[https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases)下载VideoHeartbeat.jar（用于Android v2.0.0的VideoHeartbeat库）
>1. 将VideoHeartbeat.jar解压到libs/文件夹中。


适用于Android的TVSDK比先前版本提供了许多性能改进。 它提供高质量的查看体验并提供版本1.4的所有功能，但多CDN支持除外。

发行说明的[功能列表](#feature-matrix)部分提供了支持和不支持的功能的全套。

## Android TVSDK 3.12

Primetime Reference应用程序的Gradle版本现已更新至5.6.4版。

要使用Android Studio设置和运行引用应用程序，请按照TVSDK zip提供的自述文件（位于`TVSDK_Android_x.x.x.x/samples/PrimetimeReference/src/README.md`）中的说明操作。

在[已解决的问题](#resolved-issues)部分介绍了当前版本中修复的主要客户问题。

### 先前发行版中的新增功能和增强功能

**Android TVSDK 3.11**

* **允许获取保护系统特定标头(PSSH)框** - TVSDK允许获取与当前加载的媒体资源关联的保护系统特定标头框。新API `getPSSH()`已添加到`com.adobe.mediacore.drm.DRMManager`。

有关详细信息，请参阅[Widevine DRM](../programming/tvsdk-3x-android-prog/android-3x-content-security/android-3x-drm-widevine.md)。

**Android TVSDK 3.10**

该版本侧重于解决[已解决的问题](#resolved-issues)部分中提到的客户主要问题。

**Android TVSDK 3.9**

* **通过HTTPS进行安全投放** - Android TVSDK 3.9通过HTTPS引入了安全投放功能，以无可比拟的规模和性能安全地交付内容。

   要启用通过HTTPS的安全投放,`NetworkConfiguration`类中引入了新的API。

   `public void setForceHTTPS (boolean value)`

   `public boolean getIsForceHTTPS()`

**Android TVSDK 3.8**

* **具有部分广告中断功能的预转广告支持** -借助此增强功能，TVSDK 3.8支持具有部分广告中断功能(PABI)的预转广告。

如果有预卷广告，则播放该广告，然后从实况点播放该内容，以模拟直播电视的体验。

**Android TVSDK 3.7**

* 对于Widevine测试内容，DRMManager类中的新API `setMediaDrmCallback`将公开以覆盖MediaDrmCallback接口的默认实现。

   `public static void setMediaDrmCallback(MediaDrmCallback callback)`

* 修复了C++层（Android 64位）中不处理`MediaPlayerEvent.ITEM_UPDATED`的AppCrash错误。

**Android TVSDK 3.6**

* **增强您的应用程序以满足64位** -原生库现 `(libAVEAndroid.so)` 在已升级并在两个版本中提供。现有armeabi（32位）本机库位置已从`/framework/Player to /framework/Player/armeabi`更改，并在`/framework/Player/arm64-v8a.`中引入了额外的arm64-v8a（64位）库

**版本3.5**

* **Just In Time Ad Resolution**  - TVSDK 3.5从时间轴中删除对已播放广告的支持。

* **支持脱机播放** -借助脱机播放，用户现在可以将视频内容下载到其设备并在未连接时观看。有关详细信息，请参阅“[Offline Playback with Android](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_3.5.pdf)”。

**版本3.4**

* TVSDK现在支持CBC加密和纯流的CMAF流播放。

**版本3.3**

* **API更改**

   * 将新API添加到`NetworkConfiguration::setNumOfTimesManifestRetryBeforeError(n)*`以处理网络错误和超时。
      * 其中(n)是重试数。

**版本3.2**

* **并行广告解析和清单下载支持**

   * TVSDK 3.2支持同步解析，而不是对除VMAP外的所有广告请求和广告中断的顺序解析。

   * 广告分时段中的所有广告清单将同时下载。

* **已启用广告解析和清单下载超时支持。**

   * 用户现在可以设置整个广告分辨率和清单下载的超时值。  对于VMAP，超时值适用于单个广告分段，因为所有广告分段都是按顺序解析的。

* **在AdvertisingMetadata类中引入了新的API:**

   * `void setAdResolutionTimeout(int adResolutionTimeout)`

   * `int getAdResolutionTimeout()`

   * `void setAdManifestTimeout(int adManifestTimeout)`

   * `int getAdManifestTimeout()`

* **从AdvertisingMetadata类中删除了以下API:**

   * `void setAdRequestTimeout(int adRequestTimeout)`

   * `int getAdRequestTimeout()`

* **使用AC3/EAC3音频编解码器实现流回放**

   * `void alwaysUseAC3OnSupportedDevices(boolean val)` 课 `MediaPlayer` 程

* **TVSDK支持CMAF和纯流回放，以用于加密的Widevine CTR。**

* **现在支持播放4K HEVC流。**

* **并行广告呼叫请求** - TVSDK现在可并行预取20个广告呼叫请求。

**3.0版**

* **TVSDK 3.0支持高效视频编码(HEVC)流。**

* **及时——解析更接近广告标志符的广告懒**
惰广告解析现在可独立解决每个广告中断。以前，广告解决是分两阶段进行的：在播放开始之前解决了预卷，在播放开始后所有中／后滚动槽都组合在一起。 利用此增强功能，现在可以在广告提示点之前的特定时间解决每个广告中断。

>[!NOTE]
>
>现在，懒惰广告解析已更改为默认关闭，并且显式需要启用。

向`AdvertisingMetadata::setDelayAdLoadingTolerance`添加了新的API，以获得与此广告元数据相关的延迟广告加载容限。\
搜索现在在准备后立即允许，搜索广告中断将导致在搜索完成之前立即解决。\
支持信令模式`SERVER_MAP`和`MANIFEST_CUES`。

有关详细信息，请参阅[TVSDK 3.0 for Android程序员指南](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/c-lazy-ad-resolving.md)中有关API和事件更改的内容。

* **已更 `targetSdkVersion` 新至最新版本**

已将`targetSdkVersion`从19更新为27，以实现顺利运行。

* **Placement.Type getPlacementType()现在是接口TimelineMarker上的一种方法**

   此方法将返回Placement.Type.PRE_ROLL、Placement.Type.MID_ROLL或Placement.Type.POST_ROLL的放置类型。 如果广告中断未解析，则TimelineMarker接口上的getDuration()方法将返回0。

**版本2.5.6。**

* **TVSDK 2.5支持Android P。**

* **启用背景音频**

   要在应用程序从前台移动到后台时启用音频播放，当播放器处于PREPARED状态时，应用程序应调用MediaPlayer的`enableAudioPlaybackInBackground` API，参数为true。

* **alwaysUseAudioOutputLatency(boolean val)在MediaPlayer类中**

设置后，在音频时间戳计算中使用输出延迟。
布尔参数val - True将在音频时间戳计算中使用音频输出延迟。

* **经过优化，即使带宽速度突然下降，也能获得最佳播放体验**

TVSDK现在可取消当前区段的下载（如果需要），并动态切换到相应的再现。 这是通过在比特率之间无缝切换而不中断来实现的。

**版本2.5.5**

* **部分广告中断插入**

   加入广告中间而无需为部分观看的广告触发跟踪的电视体验。\
   示例：用户在包含3个30秒广告的90秒广告时段中间（40秒）加入。 这是休息时第二个广告的10秒。

   * 第二个广告在剩余持续时间（20秒）内播放，然后是第三个广告。

   * 不会触发已播放的部分广告（第二个广告）的广告跟踪器。 仅触发第三个广告的跟踪器。

* **通过HTTPS安全加载广告**

   Adobe Primetime提供了通过https请求对primetime广告服务器和CRS进行首次呼叫的选项。

* **添加到CRS请求的AdSystem和Creative Id**

   现在，在1401和1403请求中将`AdSystem`和`CreativeId`作为新参数。

* **NetworkConfiguration类中的API setEncodeUrlForTracking删** 除了URL中不安全字符的编码。

**版本2.5.4**

Android TVSDK v2.5.4优惠以下更新和API更改：

* `WebViewDebbuging`默认值的更改

   `WebViewDebbuging` 默认情况下，值 `Fals`设置为e。要启用它，请调用应用程序中的`setWebContentsDebuggingEnabled(true)`。

* **OpenSSL和Curl版本升级**

   已将libcurl更新为v7.57.0和OpenSSL更新为v1.0.2k。

* VAST响应对象的应用程序级访问

   引入了一个新的API `NetworkAdInfo::getVastXml()`，它提供对应用程序的VAST响应对象的访问。

**版本2.5.3**

Android TVSDK v2.5.3优惠以下更新和API更改。

* 鼓励所有使用CRS的TVSDK客户使用TVSDK 2.5.3.85或最新版Android升级其应用程序。 这将替换现有应用程序实施的插件。 TVSDK升级后，在代理工具中检查CRS创意URL请求(例如：并确认路径中的主机名和版本反映如下示例URL结构中。

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* TVSDK的用户代理可自定义：我们添加了一些新的API来自定义用户代理。

   * `setCustomUserAgent(String value)`
   * `getCustomUserAgent()`

* 在Android应用程序和TVSDK之间共享Cookie:Android TVSDK现在支持在JAVA层（存储在Android应用程序的CookieStore中）和C++ TVSDK层之间访问cookie。 现在，可以在本机C++层设置和／或修改cookie，因为它们将暴露在Java Cookie商店中。

* API更改：

   * 新事件`CookiesUpdatedEvent`已添加。 它在更新其cookie时由媒体播放器调度。

   * 将新API添加到`NetworkConfiguration::set/ getCustomUserAgent()`以使用自定义用户代理。

   * 新的API被添加到`NetworkConfiguration::set/ getEncodedUrlForTracking`以强制对不安全字符进行编码。

   * 向`NetworkConfiguration::getNetworkDownVerificationUrl()`添加了一个新API，以在发生故障转移时设置网络验证URL。

   * 将新属性添加到`TextFormat::treatSpaceAsAlphaNum`，该属性定义在显示字幕时是否将空间视为字母数字。

* `SizeAvailableEvent`中的更改。 以前，使用2.5.2中`getHeight()`和`getWidth()`方法返回帧高和帧宽，由媒体格式返回。 `SizeAvailableEvent`现在，它分别返回由解码器返回的输出高度和输出宽度。

* 缓冲行为中的更改：缓冲行为已更改。 它留给App开发人员在缓冲区为空时要做什么。 2.5.3在缓冲区空的情况下使用播放缓冲区大小。

**版本2.5.2**

Android TVSDK v2.5.2优惠了重要错误修复和一些API更改。

**版本2.5.1**

Android 2.5.1中发布的重要新增功能。

* **性能改进-** 新的TVSDK 2.5.1体系架构带来许多性能改进。根据第三方基准测试研究的统计，与行业平均水平相比，新架构的启动时间缩短了5倍，丢帧率减少了3.8倍：

* **VOD和实时的即时启用-** 启用即时启用时，TVSDK在播放开始之前初始化和缓冲媒体。由于您可以在后台同时启动多个MediaPlayerItemLoader实例，因此可以缓冲多个流。 当用户更改渠道，且流已正确缓冲时，将立即在新渠道开始上播放。 TVSDK 2.5.1还支持&#x200B;**live**&#x200B;流的即时打开。 实时窗口移动时，将重新缓冲实时流。

* **改进的ABR逻** 辑——新的ABR逻辑基于缓冲区长度、缓冲区长度变化速率和测量带宽。这确保ABR在带宽波动时选择正确的比特率，还通过监视缓冲区长度变化的速率来优化比特率切换的实际发生次数。

* **部分段下载／子分段-** TVSDK进一步减小每个片段的大小，以便尽快开始回放。ts片段必须每两秒有一个关键帧。

* **延迟广告分** 辨率-TVSDK在开始播放之前不等待非预卷广告的分辨率，从而缩短启动时间。在解决所有广告之前，仍不允许搜索和技巧播放等API。 这适用于与CSAI一起使用的VOD流。 搜索和快进等操作在广告解决完成之前不允许。 对于实时流，在实时事件中无法启用此功能以获得广告分辨率。

* **永久网络连接-** 此功能允许TVSDK创建和存储永久网络连接的内部列表。这些连接被重用于多个请求，而不是为每个网络请求打开新连接，然后销毁它。 这提高了网络代码的效率并减少了延迟，从而提高了播放性能。
当TVSDK打开连接时，它会要求服务器进行*keep-alive*&#x200B;连接。 某些服务器可能不支持此类连接，在这种情况下，TVSDK将返回给再次为每个请求建立连接。 此外，尽管永久连接在默认情况下处于打开状态，TVSDK现在有一个配置选项，以便应用程序可以根据需要关闭永久连接。

* **并行下载-** 以并行而非串联方式下载视频和音频可减少启动延迟。此功能允许播放HLS Live和VOD文件，优化服务器的可用带宽使用，降低在运行不足的情况下进入缓冲区的可能性，并最小化下载和回放之间的延迟。

* **并行广告下载-** TVSDK在点击广告中断前预取与内容播放平行的广告，从而实现广告和内容的无缝播放。

* **播放**

* **MP4内容播放-** MP4短片无需重新转码即可在TVSDK中播放。

   >[!NOTE]
   >
   >MP4播放不支持ABR切换、特技播放、广告插入、后期音频绑定和子分段。

* **使用自适应比特率(ABR)进行特** 技播放——此功能允许TVSDK在特技播放模式下在iFrame流之间切换。您可以使用非iFrame用户档案以较低的速度进行特技播放。

* **更流畅的技巧播放** -这些改进增强了用户体验：

   * 在特技播放期间基于带宽和缓冲区用户档案的自适应比特率和帧速率选择

   * 使用主流（而非IDR流）可以快速回放30 fps。

* **内容保护**

   * **基于分辨率的输出保护-** 此功能将播放限制与特定分辨率联系起来，提供更精细的DRM控制。

* **工作流支持**

   * **直接计费集** 成——这会将计费指标发送到Adobe Analytics后端，后端由Adobe Primetime认证为客户使用的流。

   TVSDK会自动收集指标，遵守客户销售合同，生成计费所需的定期使用情况报告。 在每个流开始事件中，TVSDK使用Adobe Analytics数据插入API将付费指标（如内容类型、广告插入启用标记和根据收费流的持续时间启用drm的标记）发送到Adobe Analytics黄金时段拥有的报表包。 这不会干扰或包含在客户自己的Adobe Analytics报告套件或服务器调用中。 此计费使用情况报告会按要求定期发送给客户。 这是付费功能的第一阶段，仅支持使用付费。 可以使用文档中描述的API根据销售合同进行配置。 此功能默认处于启用状态。 要关闭此功能，请参阅参考播放器范例。

   * **改进的故障转移支** 持——实施了其他策略，以便在主机服务器、播放列表文件和段出现故障的情况下继续不间断地播放。


* **广告**

   * **Moat集成——支** 持从Moat进行广告可见性评估。

   * **配套横幅-** 配套横幅在线性广告旁边显示，广告结束后通常继续显示在视图上。这些横幅的类型可以是html（HTML片段）或iframe（iframe页面的URL）。

* **分析**

   * **VHL 2.0 —— 这是** 最新优化的视频心跳库(VHL)集成，可自动收集Adobe Analytics的使用数据。为了简化实施，API的复杂性已降低。 下载适用于Android](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases)的VHL库[v2.0.0，并解压libs文件夹中的JAR文件。

* **SizeAvaliableEventListener**

   * `getHeight()` 现 `getWidth()` 在， `SizeAvailableEvent` 将分别以高度和宽度返回输出。显示长宽比可以按如下方式计算：

      ```java
      SizeAvailableEvent e;
      DAR = e.getWidth()/ e.getHeight();
      ```

      存储宽高比（以Sar宽度和Sar高度衡量）也可用于计算帧宽和帧高：

      ```java
      SAR = e.getSarWidth()/e.getSarHeight();
      frameHeight = e.getHeight();
      frameWidth = e.getWidth()/SAR;
      ```

* **Cookie**

   * Android TVSDK现在支持访问存储在Android应用程序CookieStore中的JAVA cookie。 每当新Cookie作为&#x200B;**Set-Cookie**&#x200B;响应头的一部分出现时，都会提供回调API(onCookiesUpdated)来记录。 通过使用CookieStore在该特定URI/域上设置这些Cookie值，这些Cookie可用作用于不同URI/域的HttpCookie的列表。 同样，TVSDK中的cookie值也会使用CookieStore添加API进行更新。

## 功能矩阵{#feature-matrix}

适用于Android的TVSDK支持许多功能，您可以通过这些功能向视频应用程序添加功能。

在以下功能表中，“Y”表示当前版本支持该功能。

| 功能 | 内容类型 | HLS |
|---|---|---|
| 常规播放（播放、暂停、搜索） | VOD + Live | Y |
| FER —— 常规播放（播放、暂停、搜索） | FER VOD | Y |
| 在广告播放时进行搜索 | VOD + Live | 不支持 |
| HEVC播放 | VOD + Live | 仅fMP4容器 |
| AC3和EAC3 | VOD + Live | 不支持 |
| MP3 | VOD | 不支持 |
| MP4内容播放 | VOD | Y |
| 自适应比特率切换逻辑 | VOD + Live | Y |
| 仅播放音频 | VOD + Live | Y |
| 多CDN支持 | VOD + Live | 不支持 |
| 使用纯音频媒体播放广告 | VOD + Live | 不支持 |
| 隐藏式字幕- 608/708 | VOD + Live | Y |
| 隐藏字幕- WebVTT | VOD + Live | Y |
| 清单故障转移 | VOD + Live | Y |
| 高级故障转移 | VOD + Live | Y |
| QoS和播放器通知 | VOD + Live | Y |
| 支持Cookie头 | VOD + Live | Y |
| 支持自定义HTTP头 | VOD + Live | Y（需要允许列表） |
| 设置缓冲区控制参数 | VOD + Live | Y |
| 设置自适应比特率控件 | VOD + Live | Y |
| 自定义清单标记 | VOD + Live | Y |
| 延迟音频绑定 | VOD + Live | Y |
| 302重定向 | VOD + Live | Y |
| 带偏移的回放 | VOD + Live | Y |
| 技巧游戏 | VOD + Live | Y |
| 技巧播放中的慢动作 | VOD + Live | 不支持 |
| 平滑技巧播放（使用ABR） | VOD + Live | Y |
| ID3解析 | VOD + Live | Y |
| 广告封锁 | VOD + Live | 不支持 |
| 即时启动 | VOD + Live | 不支持 |
| 不连续标记支持 | VOD + Live | Y |
| 302重定向粘性 | VOD + Live | Y |

| 功能 | 内容类型 | HLS |
|---|---|---|
| 常规播放，支持广告 | VOD + Live | Y |
| 支持广告的FER内容 | VOD | Y |
| 默认广告行为 | VOD + Live | Y |
| VAST 2.0/3.0 | VOD + Live | Y |
| VMAP 1.0 | VOD + Live | Y |
| MP4广告 | VOD + Live | Y（来自CRS） |
| 支持广告的技巧播放 | VOD + Live | Y |
| 仅广告 | VOD | Y |
| 定位参数 | VOD + Live | Y |
| 自定义参数 | VOD + Live | Y |
| 自定义广告行为 | VOD + Live | Y |
| 自定义广告标记 | 实时 | Y |
| 自定义广告解析器 | VOD + Live | Y |
| 自由轮自定义广告解析程序 | VOD | Y |
| C3 | VOD + Live | 不支持 |
| 延迟广告解决 | VOD | Y |
| 不连续标记支持- SSAI | VOD + Live | Y |
| 配套广告、横幅广告和可点击广告 | VOD + Live | Y |
| VPAID 2.0 | VOD + Live | Y(JS) |
| 早期广告退出 | 实时 | Y |
| 基于规则的创意优先排序 | VOD + Live | Y |
| CRS规则 | VOD + Live | Y |
| JSON广告解析程序 | VOD + Live | 不支持 |
| Moat集成 | VOD + Live | Y |
| 部分广告中断插入 | 实时 | Y |

| 功能 | 内容类型 | HLS |
|---|---|---|
| AES加密 | VOD + Live | Y |
| 示例AES加密 | VOD + Live | Y |
| 标记流 | VOD + Live | Y |
| Widevine DRM | VOD + Live | 仅fMP4容器 |
| Primetime DRM | VOD + Live | Y |
| 外部播放(RBOP) | VOD + Live | 仅限Primetime DRM |
| 许可证轮换 | VOD + Live | 仅限Primetime DRM |
| 键旋转 | VOD + Live | 仅限Primetime DRM |

| 功能 | 内容类型 | HLS |
|---|---|---|
| Adobe AnalyticsVHL集成 | VOD + Live | Y |
| 计费 | VOD + Live | Y |

## 已解决问题{#resolved-issues}

如果分辨率与报告的问题相关联，则显示Zendesk引用，例如ZD#xxxxx。

**Android TVSDK 3.12**

本节概述TVSDK 3.12 Android版本中解决的问题。

* ZD#40584 - Primetime Reference应用程序不使用最新的Gradle版本构建。

### 已解决先前版本中的问题

**Android TVSDK 3.11**

* ZD#41252 - WebVTT中的韩文字符在Android 7.1后断开。

**Android TVSDK 3.10**

* ZD#40340 —— 在列出所有TS(TypeScript)文件的块后尝试播放时，应用程序会因“App Not Responding”错误而崩溃。

**Android TVSDK 3.8**

* 未添加新问题。

**Android TVSDK 3.7**

* 未添加新问题。

**Android TVSDK 3.6**

* 未添加新问题。

**版本3.5**

* ZD#37503 —— 缓存CRS规则的JSON响应以避免重复请求。

**版本3.4**

* ZD#37996 —— 修复了线性和VOD CMAF HEVC流的不稳定播放问题。
* ZD#37706 —— 修复了字幕乱码的问题。
* ZD#37622 —— 修复了特定广告的致命URISyntaxError问题。
* ZD#36938 —— 修复了在退出技巧播放后，比特率切换为中间比特率，然后接收到最高比特率的问题。

**版本3.3**

* ZD#37394 - CMAF资产快速前进会在速度更改后产生伪影。
   * 修复了在技巧播放过程中用户档案发生更改的问题。
* ZD#37396 —— 某些中间版和后滚动版广告跟踪事件缺失。
   * 修复了广告跟踪事件的特定案例。
* ZD#37491 - HTTP状态代码中不存在错误元。
   * 在堆栈中传播网络错误时工作过。
* ZD#37808 -允许列表新的自定义标题。
   * 作为此修复的一部分添加了SSAI_TAG支持。
* ZD#37622 - URI从特定广告窗格同步错误。
   * 修复了在向客户的Android应用程序提供包含未编码%的广告时，流播放崩溃的问题
* ZD#37631 —— 针对Android TVSDK的主控清单重试机制。
   * 在网络配置中添加了新的API以处理此增强。 如果未使用此API，则不重试清单。 如果使用清单，则将重试清单以处理网络错误和超时。

**版本3.2**

* ZD#37493-实时播放的跟踪信标不会间歇性地为序列中的第一个广告触发。
* ZD#36985-在VMAP响应中，不会为空广告中断发送跟踪信标。
* ZD#37134 - TVSDK间歇性地为VMAP响应抛出错误的ID。

**3.0版**

* ZD#33740 - TVSDK在创建MediaPlayer对象并调用replaceCurrentResource()后抛出一个不需要的警告

   * 通过仅在播放器处于挂起状态时调用恢复来改进先前的修复

* ZD#36442 —— 每个新播放都会断开远程调试会话的连接，使调试变得不可能。

   * 默认情况下，Web视图无法进行调试，因为默认情况下未启用调试。 应用程序应根据需要对从MediaPlayer.getCustomAdView()返回的对象调用setWebContentsDebuggingEnabled(true)来启用调试。

* ZD#33688 —— 支持及时解决

   * 广告中断在广告中断位置之前以指定的时间间隔解析。

* ZD#36441 —— 实时窗口的持续时间不断增加，超过5分钟，导致多个问题。

   * 修复了在计算虚拟实时点时添加两次virtualStartTime导致此问题的问题。

**Android TVSDK 2.5.6**

* ZD #34992 —— 隐藏字幕中的语言为空。

   * 修复了TVSDK未从主清单解析#EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS以获取题注轨道详细信息的情况。

* ZD #35078 - Android P验证。

   * TVSDK 2.5.6已通过最新的Android P测试版本进行验证。 未发现由于新的Android OS导致的问题。

* ZD #34149 —— 播放器会继续实现请求清单，即使遇到错误也是如此。

   * 修复了TVSDK在所有用户档案关闭时仍进行重复调用的情况（404错误）。

* ZD #31533 —— 在应用程序发送到后台后在Android上播放音频。

   * 添加了MediaPlayer的`enableAudioPlaybackInBackground` API，该API应以“True”作为参数进行调用（当播放器处于PREPARED状态时），以在应用程序处于后台时启用音频回放。

**Android TVSDK 2.5.5**

* ZD #21647 —— 当实际视频大小为640x360时，Android TVSDK将通知640x368。

   * 由于变量m_nOutputHeight（在AndroidMCVideoDecoder中）已更新为帧高而非实际输出高度。 在函数getVideoFrame中进行了相关更改，以正确计算m_nOutputHeight。

* ZD #26614 —— 紧急——第三方广告服务／程序化——无法提供展示。

   * 通过处理XML分析中的情况增强了以前的修复，当“空格”在“等号”（如&lt;VAST version =&quot;2.0&quot;>）之前时，问题可重现

* ZD #29296 - Android:向CRS请求添加AdSystem和Creative ID。

   * 现在，在1401和1403请求中将“AdSystem”和“CreativeId”作为新参数。

* ZD #33062 - TVSDK在CDATA节点下的VAST响应中出现管道字符时崩溃

   * NetworkConfiguration类中的API setEncodeUrlForTracking作为要编码的URL中的不安全字符删除

* ZD #33063 - CRS文件选择逻辑已中断- TVSDK不发送CRS请求webm格式，而是发送3gpp文件。

   * 已修复逻辑。 当使用webm和3gpp格式的媒体文件时，将为webm发送CRS请求。 同时使用3gpp格式的媒体文件时，CRS请求将发送给最高比特率的3gpp文件。

* ZD #33125 - Android应用程序在VMAP中使用特定的DoubleClick标记崩溃。

   * 修复了方案以避免崩溃。

* ZD #32256 —— 许可证轮换和密钥轮换问题-Adobe访问

   * 修复了SampleAES内容的DRM元数据的区段初始化。 适用于AES128内容。

* ZD #33619 —— 快速转发正在增长的播放列表内容，该内容在实况点附近卡在缓冲状态中。

   * 在特技播放模式下跨越实时点时处理案例

* ZD #34151 - TimedMetadata对象无序。

   * 如果两个TimedMetadata事件属于时间轴中的同一时间，则它们以随机顺序显示。 在清单中保持其原始顺序。

* ZD #34189 —— 寻求开始广告休息时的问题。

   * 问题出在使用不连续性拼接的SSAI广告。 原因是当我们寻找这些广告的开始，我们搜索一个关键帧却找不到它。 其原因是广告的最小音频时间戳早于最小视频时间戳。 因此，我们最终在错误的fragmentDump数据上搜索关键帧。 现已修复。

* ZD #34528 —— 在FireTV第3代转换器上，视频分辨率不会升级到640x360以上。

   * 增强了修复功能以包含最新的固件更新

* ZD #34793 - TVSDK 2.5.x用于在VideoEngine假定auditudeSettings可用且不可用时，在某些情况下与自定义内容解析程序崩溃。

   * 由于对空共享指针(auditudeSettings)的函数调用，发生了崩溃。 在VideoEngineTimeline::placeToSourceTimeline()中添加了条件检查，以确保在调用该对象上的任何内容之前，auditudeSettings可用。

* ZD #32584 —— 无法访问VAST响应的&lt;Extensions>节点中提供的完整信息。

   * 修复了XML解析的问题，现在NetworkAdInfo提供&lt;Extensions>节点中提供的完整信息

* ZD #35086 —— 在特定VMAP响应的情况下，无法从播放器获取完整的扩展数据。

   * 问题特定于扩展xml，因为如果扩展xml在属性值中包含多次引号，则XML解析不起作用。 修复了问题。

**Android TVSDK 2.5.4**

* ZenDesk#33659 —— 支持Web视图远程调试的播放会话。

默认情况下，WebViewDebuging设置为False。 要启用调试，请使用setWebContentsDebuggingEnabled(true)通过应用程序设置为true。

* ZenDesk#33011 —— 如果CRS请求失败，则无法解析广告时间轴。

   当对广告的CRS请求失败时，时间轴会得到解析，剩余的广告会被播放。

* ZenDesk#34528 - FireTV第三代转换器上的视频分辨率升级不超过640x360。

   视频分辨率随着比特率的变化而变高。

* ZenDesk#33192 —— 当通过AudioUpdatedEventListener::onAudioUpdated检索音轨时，AudioTrack的名称为空。

   在FireTV Stick上的几种情况下，当没有实际音频更新时，onAudioUpdate事件会被触发。 现在已修复。

**Android TVSDK 2.5.3**

* Zendesk#32216 - TimedMetadata自定义标记订阅无效。

   我们将ID3数据作为字节数组（用于支持APIC或通用数据）返回给客户端，而在1.4中返回字符串。 字节数组不处理以空结尾的字符本身，因此它向客户端显示特殊字符。 此问题现已修复。
* Zendesk#32670 —— 播放器不会故障切换到冗余播放列表

   现在运行正常，setNetworkDownVerificationUrl正按预期工作。
* Zendesk#32369 —— 隐藏式字幕显示不同的颜色垃圾或伪像。

   CC故障问题已在最新版本中得到修复
* Zendesk#25590 —— 增强：TVSDK cookie store（C++到JAVA）

   Android TVSDK现在支持在JAVA层（存储在Android应用程序的CookieStore中）和C++ TVSDK层之间访问cookie。
* Zendesk#32252 - TVSDK_Android_2.5.2.12似乎没有PTPLAY-20269的修复

   此问题已修复并集成到2.5.2分支。
* Zendesk#31806 - Auditude加入PREPARING

   播放器处于“准备”状态，因为响应xml有一个空标签。 现在问题已解决。
* Zendesk#31727 - TVSDK 2.5隐藏式字幕字符被丢弃或拼写错误。

   问题已修复，我们不会删除／错误拼写任何字符。
* Zendesk#31485 - DrmManager,2.5版

   通过新的DrmManager（上下文）创建DrmManager时出现问题。 已实现DRMService类，它将提供DRMManager。
* Zendesk#32794- 1080P分辨率流未在Android上播放

   我们更改了2.5中SizeAvailableEvent和Previsol、getHeight()和getWidth()方法，它们用于返回帧高和帧宽（由媒体格式返回）。 现在，它分别返回由解码器返回的输出高度和输出宽度。
* Zendesk #19359Flash Player因设置级清单中#EXT-X-FAXS-CM属性的位置而崩溃。

   #EXT-X-FAXS-CM标签必须始终出现在顶部播放列表中，然后在播放列表中显示单个比特率或段。

**Android TVSDK 2.5.2**

* Zendesk#17305隐藏式字幕中的不透明背景。

   显示TextFormat中的setTreatSpaceAsAlphaNum属性。 默认情况下，该属性为False。 在客户端中将属性设置为True可解决暗空间问题。

* Zendesk#25097 CC显示屏具有带有CC设置的视觉伪像。

   显示TextFormat中的setTreatSpaceAsAlphaNum属性。 默认情况下，该属性为False。 在客户端中将属性设置为True可解决暗空间问题。

* Zendesk #31620 TVSDK播放器外的用户代理字符串被截断。

   用户代理字符串在128个字符后不再被截断。

   Adobe Primetime版本字符串添加到系统用户代理。

* Zendesk #30809缺少SEEK_END事件可阻止应用程序转换到播放状态。
* Zendesk #30415 Closed Caption的“青色”颜色与Primetime TVSDK以前的版本相比现在为蓝色（绿松石）的较深色调。

   颜色从深青色更改为青色。

* Zendesk #30727 VOD广告无法下载／解析。

   在VMAP XML中，如果存在空的VAST标签，但没有明确的结束标签(‘&lt;/VAST>’)，并且后面没有换行符，则VMAP XML无法正确解析，广告可能无法播放。

**Android TVSDK 2.5.1**

* 设备特定的(Samsung Galaxy Tab 4)崩溃；带Auditude的VOD DRM LBA并单击广告。
* VHL —— 从偏移启动内容时发送的心跳调用不正确。
* 播放VPAID广告时，VHL心跳信号中缺少事件:type:play广告。
* 进入“完成”状态后，播放器使用SKIP adBreakPolicy返回到后滚广告的“播放”状态。
* Cookie未附加到传出广告回呼。
* 广告提示点不可见。
* 带有单独EAC3 SAP轨道的HLS将无法加载。
* 在恢复媒体播放器后，TVSDK收到“屏幕开启”意图时播放器崩溃。

## 已知问题和限制{#known-issues-and-limitations}

**Android TVSDK 3.11**

* 未添加任何新限制。

### 先前版本中的已知问题和限制

**Android TVSDK 3.10**

* 未添加任何新限制。

**Android TVSDK 3.8**

* 未添加任何新限制。

**Android TVSDK 3.7**

* 未添加任何新限制。

**Android TVSDK 3.6**

* 未添加任何新限制。

**Android TVSDK 3.5**

* 未添加新限制。

**Android TVSDK 3.4**

* 尚未验证CMAF(CBC)流的ID3、隐藏字幕、延迟绑定音频支持。
* 在某些设备上，由于在CMAF流上的特技播放期间在顶部可能出现视频失真，因此存在低再现性问题。

**Android TVSDK 3.3**

* clcp:c608字幕不支持CMAF流播放。

**Android TVSDK 3.2**

* TVSDK 3.2不支持CMAF Sample AES和AES128流播放。
* HEVC CMAF流不支持隐藏式字幕回放。
* 在非加密段周围执行搜索时，WV加密流会显示绿色。
* CMAF流不支持ID3事件。
* HLS流不支持TTML字幕格式。

**Android TVSDK 3.0**

* HEVC支持在此版本中有以下限制

   * 不支持DRM
   * 未验证CC(CEA 608/708)支持
   * 4K支持尚未提供
   * 未验证ID3标记支持

* 对于广告进度事件，时间轴栏可能无法反映100%准确的广告播放时间。 作为解决方法，您可以使用`adcompleteevent`了解广告播放完成情况并更新UI以用于各种用途，如更新时间轴栏、删除与广告相关的UI等。
* 从VMAP返回的广告呼叫不接受“及时查看”位置。

**Android TVSDK 2.5.6**

* 不支持同时进行多个VMAP广告中断。

**Android TVSDK 2.5.3**

此版本有以下问题：

* 实时视频播放在低端设备上可能存在音频——视频同步问题，或网络状况不佳。
* 对于FER流，virtualTime和localTime可能不同。 同时，带偏移的FER也不起作用。
* 搜索“延迟绑定音频”内容时，播放可能会卡住。
* 对于实时内容，webVTT字幕可能会间歇性地变得不同步。
* 从广告中断出来后，可间歇性地快速播放几帧。
* 有时，即使播放广告，三步包装广告分段也会引发303错误。

**Android TVSDK 2.5.2**

此版本有以下问题：

* 在低端设备上，实时视频播放可能存在音频——视频同步问题。
* 在寻求到VOD媒体的末尾时，播放可能会暂停。
* 对于FER流，virtualTime和localTime可能不同。 此外，具有偏移的FER不起作用。

**Android TVSDK 2.5.1**

此版本的TVSDK有以下问题：

* 实时视频播放在低端设备上可能存在音频——视频同步问题。
* 对于FER流，virtualTime和localTime可能不同。 此外，具有偏移的FER不起作用。
* 在VMAP XML中，如果有空的VAST标签没有显式结束标签(&lt;/VAST>)，并且后面没有换行符，则VMAP XML无法正确解析，广告可能无法播放。
* 不支持VPAID后置记录。

## 帮助资源{#helpful-resources}

* [系统要求](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-android-prog/introduction/android-3x-requirements.html)
* [TVSDK 3.10 for Android程序员指南](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-android-prog/introduction/android-3x-overview-prod-audience-guide.html)
* [TVSDK Android Javadoc for API参考](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html)
* [TVSDK Android C++ API文档](https://help.adobe.com/en_US/primetime/api/psdk/cpp_3.5/namespaces.html) -每个Java类都有相应的C++类，而C++文档包含比Javadoc更多的说明性材料，因此请参阅C++文档以进一步了解Java API。
* [TVSDK 1.4到2.5 for Android(Java)迁移指南](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* 要处理屏幕开启／关闭情况，请参阅构建中包含的`Application_Changes_for_Screen_On_Off.pdf`文件。
* 请参阅[Adobe Primetime学习和支持](https://helpx.adobe.com/support/primetime.html)页面上的完整帮助文档。

---
title: 浏览器TVSDK 2.4发行说明
description: 浏览器TVSDK 2.4发行说明介绍了浏览器TVSDK 2.4中新增的、受支持的和不支持的功能和已知问题。
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 83fdf530-5cbb-41d9-ab2a-28e117f04488
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '6812'
ht-degree: 0%

---

# 浏览器TVSDK 2.4发行说明 {#browser-tvsdk-release-notes}

浏览器TVSDK 2.4发行说明介绍了浏览器TVSDK 2.4中新增的、受支持的和不支持的功能和已知问题。

## 介绍 {#introduction}

浏览器TVSDK是一个工具包，可让您将高级视频播放功能、内容保护和广告添加到基于浏览器的视频播放器应用程序。

浏览器TVSDK 2.4提供JavaScript API来构建基于浏览器的视频应用程序，并在以下模式下提供播放支持：

* 仅HTML5
* 具有自动闪存回退的HTML5
* 始终Flash

此版本包括以下信息：

· [浏览器TVSDK API文档](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

· [浏览器TVSDK编程指南](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf).

· [《 TVSDK for 1.4 DHLS到浏览器TVSDK 2.4迁移指南》](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

· [从浏览器TVSDK 2.4.6转换为版本2.4.7](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html).

·引用实施，包含在内部版本中。

>[!NOTE]
>
>*有关此版本的安全注意事项的完整列表，请参阅安全注意事项。

## 新增功能和支持的功能 {#what-s-new-and-supported-features}

此版本的Browser TVSDK提供了可用于增强视频应用程序的新功能。

**2.4.12更新中的新增功能（内部版本204）**

浏览器TVSDK 2.4.12更新（内部版本204）中包含以下新增内容：

* AdobePSDK.MediaPlayer的卷API实施已更改为允许在播放处于静音状态时在iOS上自动播放。

·一个新的API， `auditudeSettings.ignoreVPAIDAds`添加了，以允许忽略从Auditude服务器接收的VPAID广告。 该API不适用于Flash回退。

**版本2.4.11**

以下增强功能和添加内容在浏览器TVSDK 2.4.11版本中提供：

· MSE和Flash回退模式支持HLS实时区段故障切换。

·支持 `AuditudeSettings.creativeRepackagingDomain` API现在也可用于MSE。 以前，仅支持Flash回退模式。

·此版本包含对关键客户问题的修复。 参见 *修复的问题* 列表。

**版本2.4.10**

以下增强功能和添加内容在浏览器TVSDK 2.4.10版本中提供：

· TVSDK提供enableLogging()来启用或禁用日志记录。 请参阅 [API文档](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)以供使用。

· TVSDK在使用Adobe Analytics时不再支持默认章节。 使用应用程序定义和管理章节。

·此版本包含对关键客户问题的修复。 请参阅*已修复的问题*a列表。

**版本2.4.9**

以下增强功能和添加内容在浏览器TVSDK 2.4.9版本中提供：

·支持具有时间间断但不具有间断标记的HLS VOD和实时流。

· HLS VOD和实时流的Safari视频标记支持ID3 v2.4.0帧。

·安全广告加载实施可确保广告服务器调用根据API配置升级到安全HTTP。 有关详细信息，请参阅AdobePSDK.AdvertisingMetadata和AdobePSDK.ForceHttpsAdConfiguration类。 Flash回退模式不支持此功能。

· TVSDK现在向应用程序提供与VAST 3.0响应关联的广告ID信息和扩展信息，这些信息可用于实施广告测量的Moat集成。 有关详细信息，请参阅AdobePSDK.NetworkAdInfo API。 Flash回退模式不支持此功能。

· AdobePSDK.ForceHttpsConfiguration类不再可用。 成功于

AdobePSDK.ForceHttpsAdConfiguration类。

·现在提供一个新的API AdobePSDK.optimizeFlashCalls ，用于优化调用以改善Flash回退模式中的HLS播放体验。 默认情况下禁用此功能。

**2.4.8更新中的新增功能（内部版本6002）**

此更新包含对关键客户问题的修复。 参见 *修复的问题*，以表示列表。

**版本2.4.8**

以下增强功能和添加内容在浏览器TVSDK 2.4.8版本中提供：

·此SDK现在与Chrome EME兼容，并且从Chrome v58开始提供了更改的最佳实践。 有关更多详细信息，请参阅 [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

· UI Framework现在支持Flash、仅限广告和定位信息工作流中的HLS访问DRM。

· setDRMAuthenticateData API已添加到UI框架中。 要播放受Adobe访问DRM保护的流，请调用此API。 或者，也可以在播放器中指定drmAuthenticateData属性。 参见 [AdobePSDK.videoBehavior ](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)了解详细信息。

**版本2.4.7**

以下功能是版本2.4.7中的新增功能：

· UI框架中添加了UI配置器

您可以通过以下方式之一配置播放器：

·使用JSON对象

·使用API

为帮助生成JSON对象，浏览器TVSDK提供了一个**UI配置器**工具。

在此工具中，您可以选择各种设置，单击**测试配置**以验证设置，然后单击**下载配置**以下载设置。 下载文件后，您可以将此文件的内容作为JSON对象传递到ptp.videoPlayer API。

·将MediaPlayerItemConfig API添加到UI框架

各种功能，包括advertisingMetadata、advertisingFactory、adSignalingMode、networkConfiguration、customRangeMetadata、useHardwareDecoder、subscribeTags、adTags、thumbnailScrubber、billingMetricsConfiguration，可以通过MediaPlayerItemConfig进行配置。 有关更多信息，请参阅中的AdobePSDK.MediaPlayerItemConfig文档 [浏览器TVSDK API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* * [文档](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

在UI框架中，修改了通过播放器配置传递网络配置的方式。

**版本2.4.6**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`networkConfiguration: <network configuration object>`

`}`

`};`

**版本2.4.7**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`mediaPlayerItemConfig: {`

`networkConfiguration: <network configuration object>`

`}`

`}`

`};`

* 在UI框架中支持DRM和Analytics工作流

可以通过UI框架启用DRM配置和Analytics跟踪。

* 添加 `AdobePSDK.embedSWFinFullScreenDiv` API

此新API使播放器应用程序能够灵活地选择可在其中嵌入FlashFallback.swf文件的div。

* 已替换 `getVersion`API来源 `AdobePSDK.MediaPlayer` 类与 `AdobePSDK.Version` 类以了解TVSDK版本相关信息。 有关详细信息，请参阅 `AdobePSDK.Version` API [此处](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html).

**版本2.4.6**

以下功能是版本2.4.6中的新增功能：

* **浏览器支持**

浏览器允许您在浏览器中使用node.js样式模块。 您可以定义依赖关系，Browserify会将所有内容捆绑到一个JavaScript文件中。

* **计费**

借助计费，浏览器TVSDK可以收集播放器使用情况量度，以便对Primetime客户计费。

>[!NOTE]
>
>在版本2.4.6中移除了Enum PSDKErrorCode中已弃用的枚举MediaPlayer.Events和已弃用的常量。有关更多信息，请参阅 [从浏览器TVSDK 2.4.5转换为版本2.4.6](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html).

**版本2.4.5**

以下功能是版本2.4.5中的新增功能：

* **完整事件重播和广告**

   HLS完整事件重播(FER)流现在支持广告分辨率和广告行为。 要启用此支持，请将广告信令模式设置为 `MANIFEST_CUES` 创建 `MediaPlayerItemConfig` 对象。

* **MediaplayerView ScalePolicy支持**

   应用程序开发人员现在可以使用MediaplayerView scalePolicy属性为视图指定不同的scalePolicy。

* **变形内容支持**

   现在，在使用MSE和Flash播放时，支持变形内容播放。

* **选择性应用`withCredentials`**

时间 `withCredentials` 设置为true，则 `Access-Control-Allow-Origin` 标头不能设置为通配符。 根据服务器的响应，Browser TVSDK会选择性地将 `withCredentials` 属性。 有关此支持的更多信息，请参阅 [浏览器TVSDK API文档](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

**版本2.4.4**

以下功能是版本2.4.4中的新增功能：

* **Chromecast示例应用程序**

此版本支持发送者和接收者应用程序，该应用程序演示通过客户端广告插入播放DASH VOD流和DASH Widevine流。

* **高级故障转移支持**

此版本包含对HLS VOD流的高级故障转移用例（区段和服务器故障转移）的支持。

**版本2.4.3**

以下功能是版本2.4.3中的新增功能：

* **虚线VOD的自定义标记**

   内联自定义标记（事件）可以订阅并作为TimedMetadata对象接收。

* **没有扩展的流播放**

   现在支持不带扩展的HLS和DASH流。 对于清单文件，加载资源时需要指定resourceType。 对于区段和VTT文件，使用内容类型响应标头确定内容类型。

**版本2.4.2**

以下功能是版本2.4.2中的新增功能：

* **API奇偶校验**

有关API奇偶校验的完整列表，请参见 [《 TVSDK for 1.4 DHLS到浏览器TVSDK 2.4迁移指南》](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

* **示例AES支持**

   此版本添加了对在MSE和Flash回退上播放Sample-AES加密内容的支持。 取消了在Google Chrome上通过安全源托管AES内容的要求。

* **对AAC容器的支持**

   现在支持播放扩展名为.aac的文件。 这可以是纯音频流或备用音频。

   >[!NOTE]
   >
   >尚不支持AC3和增强型AC3编解码器。

* **令牌化的流播放**

通过内容交付网络(CDN)交付的HLS流有时可以使用清单和区段请求上的身份验证令牌进行验证，并且这些令牌可以作为URL参数或Cookie标头提供。 现在支持播放此类流。

**版本2.4.1**

以下功能是版本2.4.1中的新增功能：

* **UI框架**

此框架旨在加快基于JavaScript的视频播放器应用程序的UI开发，它包含用于包含播放/暂停和音量等基本控件的API，以及用于轻松添加或删除推移栏状态和隐藏式字幕设置等元素的API。 您可以指定与控件关联的行为，创建自定义控件，并在播放器UI中显示外观。 所有这些都通过框架实现，无需直接操作DOM结构。

* **用于实时流的HLS播放增强**

此版本支持由广告插入导致的不连续性。 它使用EXT-PROGRAM-DATE-TIME标记，后跟EXT-MEDIA-SEQUENCE标记，以便跨自适应比特率配置文件进行同步，从而顺利播放。

* **VPAID 2.0支持**

视频播放器广告服务界面定义(VPAID)版本2.0为用户提供了富媒体体验，并允许发布者更好地定位广告、跟踪广告展示以及从视频内容中盈利。 此版本支持针对视频点播(VOD)内容的线性JavaScript VPAID广告。

* **自定义HLS标记**

媒体流可以播放列表/清单文件中的标记形式携带其他元数据。 通过浏览器TVSDK，您可以指定和订阅其他标记，并在这些标记出现在清单中时收到通知。

* **在播放器时间轴上显示的广告标记**

此版本支持在播放器时间轴上为VOD和实时内容显示广告标记。 您可以在引用播放器中看到此行为。

**在2.4中支持**

版本2.4中提供了以下功能：

* **MP3音频播放**

   此版本支持在具有Media Source Extensions (MSE)和Safari视频标记的浏览器上播放MP3音频。

* **MP4视频播放**

   支持以下功能：

   * 单流播放
   * 具有广告行为和跟踪的前置和后置MP4广告
   * 包含广告行为和跟踪的前置和后置HLS广告
   * 具有广告行为和跟踪的前置和后置短划线广告

## 支持的平台 {#supported-platforms}

浏览器TVSDK对运行它所需的平台和软件级别有特定要求。 支持以下平台和软件级别：

### 台式机配置 {#desktop-configurations}

* Microsoft Windows 7：

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft Windows 8.1

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft Windows 10

   * Edge+

* APPLE OS X

   * Safari 9+
   * Chrome 33+
   * Firefox 38+

### 移动Web配置 {#mobile-web-configurations}

* Android 4.4

   * 本机浏览器
   * Chrome 33+

* Android 5.0

   * 本机浏览器
   * Chrome 33+

* Android 6.0

   * · Chrome 33+

* APPLE IOS 9

   * Safari 9+
   * Chrome 33+

* Apple iOS 10

   * Safari 9+
   * Chrome 33+

**Google Chromecast（第二代；仅用于DASH播放）**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>技术</strong> </p> </td> 
   <td><p><strong>浏览器TVSDK视频标记</strong><sup>1</sup></p> </td> 
   <td><p><strong>浏览器TVSDK MSE</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>默认技术</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>iOS</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>-</p> </td> 
   <td><p>视频标记</p> </td> 
  </tr> 
  <tr> 
   <td><p>Android</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS和短划线</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Apple Safari 8</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>视频标记</p> </td> 
  </tr> 
  <tr> 
   <td><p>Google Chrome</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS和短划线</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Mozilla Firefox</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS和短划线</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>MSE<sup>2</sup></p> </td> 
  </tr> 
  <tr> 
   <td><p>Internet Explorer 11</p> <p>(Windows 7)</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>Flash</p> </td> 
  </tr> 
  <tr> 
   <td><p>Internet Explorer 11</p> <p>(Windows 8.1)</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS、短划线</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
 </tbody> 
</table>

## 特征矩阵 {#feature-matrix}

以下是此版本支持和不受支持的功能列表：

* *MP3音频功能 — 核心播放*
* *MP4视频功能 — 核心播放*
* *MP4视频功能 — 核心Ad Insertion*

>[!NOTE]
>
>*在下面的功能矩阵表中，“Y”表示当前版本中支持该功能。*

### MP3音频功能 {#mp-audio-features}

**表1：核心播放{#table-core-playback}**

| 类别 | 内容类型 | 功能 | Flash | HTML5：FF、IE、Chrome、Android Chrome | HTML5：Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 播放 | MP3 VOD | 常规播放（播放、暂停、搜寻） | 不支持 | Y | Y |

1浏览器TVSDK视频标记不支持流和DRM。 并非所有浏览器的编解码器和容器支持都相同。

2 Firefox在版本41或更早版本中默认为Flash Player。

### MP4音频功能 {#mp-audio-features-1}

**表2：核心播放**

| 类别 | 内容类型 | 功能 | Flash | HTML5：FF、IE、Chrome、Android Chrome | HTML5：Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 播放 | MP4 VOD | 常规播放（播放、暂停、搜寻） | 不支持 | Y | Y |

**表3：核心Ad Insertion**

| 类别 | 内容类型 | 功能 | Flash | HTML5：FF、IE、Chrome、Android Chrome | HTML5：Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | MP4 VOD | 前置式广告(MP4) | 不支持 | Y | Y |
| Ad Insertion | MP4 VOD | 后置式广告(MP4) | 不支持 | Y | Y |

有关HLS或DASH功能支持的更多信息，请参阅下文。

## HLS功能矩阵 {#hls-feature-matrix}

以下是浏览器TVSDK中HLS功能的功能矩阵。

* *HLS核心播放*
* *HLS高级播放功能*
* *HLS内容保护功能*
* *HLS核心广告插入功能*
* *HLS高级广告插入功能*
* *HLS集成*

>[!NOTE]
>
>*在下面的功能矩阵表中，“Y”表示当前版本中支持该功能。*

### HLS功能 {#hls-features}

支持以下功能：

**表4： HLS核心播放**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5：FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5：Safari、iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>常规播放（播放、暂停、搜寻）</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>常规播放（播放、暂停和搜寻）</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>自适应比特率</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>608/708字幕</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>仅限VOD</p> </td> 
   <td><p>仅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>清单故障转移</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>高级故障切换</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>QoS和播放器通知</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>有限的QoS支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>支持Cookie标头</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>设置缓冲区控制参数</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>设置自适应</p> <p>比特率控制</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>自定义标记</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td>后期绑定音频</td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>302重定向</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
 </tbody> 
</table>

**表5： HLS高级播放功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5：FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5：Safari、iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>在偏移处播放</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>纯音频播放</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>特技游戏</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>流畅的戏法游戏</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>ID3解析</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>间断标记支持</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>令牌化流</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>计费</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**表6： HLS内容保护功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5：FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5：Safari、iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>内容保护</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>内容保护</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>Sample-AES</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>内容保护</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>Adobe访问</p> </td> 
   <td><p>不支持</p> </td> 
   <td><p>公平竞争</p> </td> 
  </tr> 
 </tbody> 
</table>

**表7： HLS核心广告插入功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5：FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5：Safari、iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>前置式广告(MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>中置式广告(HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>后置式广告(MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>广告分辨率和行为</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>默认广告策略</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>创意重新打包（MP4到HLS）</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**表8： HLS高级广告插入功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5：FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5：Safari、iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>仅广告</p> </td> 
   <td><p>不支持</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>定位参数</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>自定义参数</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>自定义广告策略</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>延迟广告加载</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>不支持</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>伴随广告、横幅广告、可点击广告</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>SWF</p> </td> 
   <td><p>JavaScript</p> </td> 
   <td><p>JavaScript</p> </td> 
  </tr> 
 </tbody> 
</table>

**表9：HLS集成{#table-hls-integrations}**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5：FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5：Safari、iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>集成</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>Adobe Analytics VHL集成</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## 虚线特征矩阵 {#dash-feature-matrix}

以下是浏览器TVSDK中DASH功能的功能矩阵。

· *DASH核心播放功能*

· *DASH高级回放功能*

· *DASH内容保护功能*

· *DASH Core广告插入功能*

· *DASH高级广告插入功能*

· *DASH集成*

>[!NOTE]
>
>在下面的功能矩阵表中，Y表示当前版本中支持该功能。

### 短划线特征 {#dash-features}

支持以下功能：

**表10：虚线核心播放功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>HTML5 FF、IE、Chrome、Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>常规播放（播放、暂停、搜寻）</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>常规播放（播放、暂停和搜寻）</p> </td> 
   <td><p>不支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>自适应比特率</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>608/708字幕</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>仅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>故障转移</p> </td> 
   <td><p>仅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>QoS和播放器通知</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>支持Cookie标头</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>设置缓冲区控制参数</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>设置自适应比特率控制</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>自定义标记(EventStream)</p> </td> 
   <td><p>仅限VOD（内联）</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>晚到的音频</p> </td> 
   <td><p>仅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>302重定向</p> </td> 
   <td><p>仅限VOD</p> </td> 
  </tr> 
 </tbody> 
</table>

**表11： DASH高级回放功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><strong>HTML5 FF、IE、Chrome、Android Chrome</strong></td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>在偏移处播放</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>纯音频播放</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>特技游戏</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>流畅的戏法游戏</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>ID3解析</p> </td> 
   <td><p>不支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>多期间支持</p> </td> 
   <td><p>仅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>令牌化流</p> </td> 
   <td><p>不支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>计费</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**表12： DASH内容保护功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>HTML5 FF、IE、Chrome、Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>内容保护</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p>不支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>内容保护</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>Sample-AES</p> </td> 
   <td><p>不支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>内容保护</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>· Chrome、Firefox 47及更高版本和Chromecast上的Widevine</p> <p>· Windows 8.1和Edge上的Internet Explorer上的PlayReady</p> <p>· Primetime DRM for Windows Firefox（仅限视频）</p> </td> 
  </tr> 
 </tbody> 
</table>

**表13：DASH Core广告插入功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>HTML5 FF、IE、Chrome、Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>前置式广告（MP4/短划线）</p> </td> 
   <td><p>仅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>中置式广告（短划线）</p> </td> 
   <td><p>仅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>后置式广告（MP4/短划线）</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>广告分辨率和行为</p> </td> 
   <td><p>不支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>默认广告策略</p> </td> 
   <td><p>仅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>仅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>仅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>创意重新打包（MP4到DASH）</p> </td> 
   <td><p>不支持</p> </td> 
  </tr> 
 </tbody> 
</table>

**表14：DASH高级广告插入功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>HTML5</strong> FF、IE、Chrome、Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>仅广告</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>定位参数</p> </td> 
   <td><p>仅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>自定义参数</p> </td> 
   <td><p>仅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>自定义广告策略</p> </td> 
   <td><p>不支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>延迟广告加载</p> </td> 
   <td><p>不支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>伴随广告、横幅广告、可点击广告</p> </td> 
   <td><p>不支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>不支持</p> </td> 
  </tr> 
 </tbody> 
</table>

**表15：DASH集成**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>HTML5：FF、IE、Chrome、Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>集成</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>Adobe Analytics VHL集成</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## 修复的问题 {#issues-fixed}

**在2.4.12更新（内部版本204）中修复的问题**

已在浏览器TVSDK版本2.4.12更新（内部版本204）中修复以下问题：

· **21647**- TVSDK应允许在音频静音时在iOS设备上自动播放视频。

· **21465** — 播放DASH Live流后播放受DRM保护的DASH流时，收到错误密钥系统访问被拒绝。

· **21442** — 在使用用户手势播放前置广告后，在iOS Web上启用内容自动播放。

· **21240** — 提供了用于筛选从Auditude/VMAP解析的VPAID广告的API。

**在版本2.4.11中修复的问题**

已在浏览器TVSDK版本2.4.11中修复以下问题：

**核心播放功能：**

· **19192**： TVSDK现在实现TextFormat：bottomInset和TextFormat：safeArea。 由于这些增强功能，如果屏幕上显示控制栏，则隐藏式字幕可以重新定位。

· **21009**：如果跨不连续性搜寻，隐藏式字幕会持续保留在屏幕上，直到出现新字幕。

· **21141**：由于区段附加期间的争用情况，回搜寻被拒绝。

· **21142**：使可搜索的播放范围在播放器处于INITIALIZED状态时可用。 由于这些更改，现在支持在位置开始会话。

· **21363**：为DASH流插入广告后，608/708隐藏式字幕不同步。

**广告插入功能：**

· **21179**：现在，通过正确设置ad.primaryAsset.adParameters属性，可解决与VOD内容相关的中段问题（长暂停、黑色帧）。

· **21257**：如果MP4不是有效的MIME类型，并且启用了创意重新打包功能，则选择具有最高比特率的MP4文件进行转码。

· **21361**：TVSDK现在将VAST响应中的广告系统和创作ID作为查询参数传递到创作打包请求中，以支持其他标准化规则。

**在版本2.4.10中修复的问题**

已在浏览器TVSDK版本2.4.10中修复以下问题：

**核心播放功能：**

· **21060**：包含不连续性的HLS流和ISO BMFF框一直运行到流结尾，从而引发无效的编解码器错误。

· **21045**：播放列表中的首次视频播放完成后，自动播放在iOS上不起作用。

· **20975**：QoS提供商在Chrome浏览器上将帧速率返回为NaN。

· **20823**：遇到无数据的区段时引发不受支持的编解码器错误。

· **20769**：SDK现在从搜寻时的当前比特率开始，而不是根据ABR策略立即切换。

· **20031**：在IE 11 (Windows 8.1)上处于纵向模式时，视频屏幕会变小。 内容保护功能：

· **19316**：跳过对HLS AES-128流解密失败的区段。

**在版本2.4.9中修复的问题**

已在浏览器TVSDK版本2.4.9中修复以下问题：

**核心播放功能：**

· **13407**：如果Firefox在播放期间停止发送“ontimeupdate”事件，则DASH流可能会停止。

· **16380**：在通过MSE播放具有不匹配开始时间的区段的混合音频视频内容期间，表示之间的音频同步错误累积在ABR交换机上，最终导致错误(Chromium问题#663686)。

· **17985**：在Firefox浏览器上播放特定ISO-BMFF流时，播放卡住(Firefox问题#1342913)。 此问题自Firefox v53以来已得到修复。

· **19141**：未捕获（在Promise中）ReferenceError：宽度未定义。

· **18997， 19299**：区段边界出现视频闪烁问题。 发生此情况是因为SDK未正确计算最后一个示例的合成时间偏移。

· **19780**：Firefox v53上的HLS内容和HLS广告不会开始播放(Firefox问题#354653)。

· **20046**：作为定时元数据对象接收时，程序日期时间作为键接收，而不是作为值接收。

· **20047**： useDefaultResizeHandler会引发有关Flash回退的错误。

· **20179**：Flash回退不适用于Flash Playerv25.0.0.171。

· **20293**：Firefox停止缓冲某些HLS流的数据，从而导致停顿。

· **20626**：由于对零持续时间的视频示例处理不正确，播放器在Chrome上引发媒体解码错误。

· **20078**：浏览器错误“QuotaExceeded”导致播放停止。

· **18639**：在HLS实时流中，608 CC文本有时会显示为拼写错误。

· **20028**： ClosedCaptions size参数不会更改字体大小。

· **20613**：隐藏式字幕框彼此重叠，使其难以辨认。

**核心Ad Insertion(CSAI)功能：**

· **20043**：缺少具有多个广告和第三方重定向的广告展示和广告跟踪调用。

· **20044**：使用创意重新打包时，需要成功重新打包广告时间中的所有广告，否则广告时间会被完全丢弃。

· **20097**：如果广告清单不可用，则跳过广告播放并立即恢复主内容，而不是等待20秒的超时。

**在版本2.4.8更新（内部版本6002）中修复的问题**

已在浏览器TVSDK版本2.4.8更新（内部版本6002）中修复以下问题：

· **14126：** 由于MSE源缓冲区中的内部间隙，Firefox上的播放可能会停止(问题#1316024)。 尝试搜寻以继续播放

· **19608：** 修复以接受来自Auditude VMAP响应的时间偏移值。

· **19635：** 修复了Windows 10上Internet Explorer 11中的视频停止问题。

· **19761：** 修复了HLS的ABR问题。

· **19780：** 修复了Mozilla Firefox v53中包含HLS内容的广告播放。

· **19877和19744：** 该问题修复了在搜寻操作之后选择比特率的不一致性。 现在，搜寻时选择的比特率是启动时当前比特率和比特率的较低值。

· **19881：** 执行3-4次搜寻后，播放卡住和缓冲叠加会无限期显示。

· **19884：** 确认符合Chrome 59 Beta Verified Media Path (VMP)要求。 bTVSDK能够使用Chrome 59 Beta版播放Widevine DRM内容。

· **19916：** UI-Framework上的DRM播放中断。 现在，即使元数据中没有策略，它也会调用acquireLicense。

**在版本2.4.8中修复的问题**

浏览器TVSDK 2.4.8版本中修复了以下问题：

· **10075**：在时间轴之前进行搜寻时，未在Firefox和Chrome上收到播放完成事件，也未在Firefox上收到搜寻事件。

· **15775**：在Windows 8.1 Internet Explorer上未收到播放完成事件。

· **17306**：对于SSAI流，支持播放。 不支持跟踪拼接的广告。

· **19142**：有时倒带会导致视频播放器永远处于缓冲状态。

· **19218**：广告标记无法通过UI框架使用。

· **19219**：仅广告播放无法通过UI框架正常工作。

· **19222**：为播放列表请求一次AES-128密钥，然后从缓存中提供后续请求。 之前，系统会为每个区段请求该扩展。

· **19597**： Chrome Canary内部版本中显示“Uncated TypeError： Cannot read property &#39;log&#39; of undefined”。

· **19605**：在Flash回退模式下不可用adRequestDomain。

· **19608**：没有为HLS实时流插入VMAP广告。 SDK现在会考虑提示标记，而不依赖于VMAP响应中的时间偏移值。

· **19637**：仅广告播放会导致广告结束时的脚本错误。

· **19732**：CRS播放列表请求失败，出现404错误。 来自浏览器TVSDK的1401和1403请求现已更新以解决此问题。

· **19762**：由于setAuthenticationToken之前曾调用acquireLicense，因此返回了有效的许可证，而不考虑令牌的有效性。 现已修复此问题，并且仅在setAuthenticationToken响应后调用acquireLicense。

**在版本2.4.7中修复的问题**

版本2.4.7中修复了以下问题：

· **8397**：如果区段不以关键帧开头，则通过Adobe Medium服务器生成的HLS实时流可能无法播放。

· **13606**：修复了Chrome浏览器上HLS流的多个搜寻相关问题。

· **14807**：在Chrome浏览器上，如果在play()之后立即触发搜寻或暂停，播放可能会停止并出现错误DOMException：播放请求被调用……中断(Chromium问题# 593273)。

· **19085**：重置播放器时，MediaPlayer参数（例如volume、abrControlParameters和ccStyle）未设置为默认值。

**在版本2.4.6中修复的问题**

版本2.4.6中修复了以下问题：

· **18093**：在Flash回退模式下使用Flash Player版本24时，将返回订阅标记旁边的TimedMetadata。

**在版本2.4.4中修复的问题**

版本2.4.4中修复了以下问题：

· **8711**：使用MSE时，608/708字幕默认左对齐。

· **13934**：当播放HLS实时流时，广告的ABR设置不适用。

· **14079**：具有低DVR窗口的HLS实时流的使用寿命可能会失败，因为播放可能会由于网络延迟问题而延迟。 单击活动点以继续播放。

· **15037**：播放器UI框架附带的示例在Windows 7上的Microsoft Internet Explorer 10上不起作用。

· **15913**：对于HLS VOD流，在Chrome上，如果清单响应为304且未修改，则不会播放流。 此问题自Chrome v55(Chromium问题633696)以来已得到修复。

· **16103**：在Android Chrome上，在低带宽条件下，播放可能会因未捕获的TypeError：无法读取未定义错误的属性“programDateTime”而停止。

· **16265**：对于HLS VOD和实时流，跨不连续性进行搜寻不起作用。

· **16709**：恢复带有PDT和不连续性标记的HLS实时流可能会导致播放器卡在缓冲中。

## 已知问题和限制 {#known-issues-and-limitations}

下面介绍了浏览器TVSDK中的限制和已知问题。

**表16：核心播放功能**

<table> 
 <tbody> 
  <tr> 
   <td><strong>内容类型</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox、IE、Chrome、Android Chrome中的HTML5</strong></td> 
   <td><strong>Safari中的HTML5、iOS和Safari</strong></td> 
   <td><strong>Chromecast（仅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>常规播放（播放、暂停、搜寻）</td> 
   <td><p>·不支持HLS以外的媒体格式。</p> <p>8799：Flash回退不会处理混合内容，因此需要确保内容、广告和其他URL不会导致混合内容（将安全和不安全的内容放在一起）。</p> <p>· 19271：Flash回退模式不支持通过UI Framework进行多视图播放。</p> <p>·Flash回退在Windows 7上的Microsoft Internet Explorer 8和9上不起作用，因为SDK不支持这些版本。</p> <p>· 20262：Flash回退可在定位信息列表中添加自定义参数。 此外，对于Flash和MSE，自定义参数的优先级顺序也不同。</p> <p>· 20653：浏览器TVSDKFlash回退不适用于具有创建者更新的Win10。</p> <p>·Flash回退适用于Flash Player版本23及更高版本。</p> <p>· 20087 - Chrome 59 Beta，带</p> <p>Flash25.0.0.171</p> <p>Beta（默认），HLS播放在Flash回退模式下不起作用。 它在金丝雀上运作良好。</p> </td> 
   <td><p>· 12563：由于MPD中不受支持的音频编解码器字符串，使用音频编解码器mp4a.40.02的Dash Streams不会在Firefox上播放。 支持音频编解码器mp4a.40.2。</p> <p>15029：在UI-Framework的multiView中切换视频时，播放/暂停按钮未相应地更新。</p> <p>· 16034：在Windows 8.1 IE上，调用reset()会导致未知MIME类型错误。 请重新加载媒体以继续播放。</p> <p>· 18235：使用带有广告的DASH vod流时，发现某些搜寻问题。</p> <p>· 18727： MSE不支持错误API</p> <p>18750：在某些情况下，SDK和UI框架中的状态更改事件可能顺序不对，在UI框架中，加载资源后添加的事件侦听器可能缺少IDLE和Initializing StatusChange事件。</p> <p>· 18889：如果MediaPlayer处于ERROR状态，则不会返回视图对象。</p> <p>· 19039：如果是AdobePSDK。 MediaPlayer。 seekToLocal()与大于EOF的值一起使用，如果是MSE，则从头开始播放。</p> <p>· 19049：当视频在播放期间被阻止时，未报告Chrome、IE、Firefox上Flash Player的错误状态。</p> <p>· 17205：当音频继续播放时，视频播放停止播放未设为静音的流几个小时(Chromium issue# 664033)。</p> <p>· 12308：指定了composition_ time_offset的DASH流在Chrome浏览器上可能应用了timeStampOffset，从而导致负解码时间，从而导致MEDIA_ERR_ SRC_NOT_SUPPORTED错误(Chromium问题#398141)。</p> <p>· 14126：由于MSE源缓冲区中的内部间隙，播放可能会在Firefox上停止(问题# 1316024)。 尝试搜寻以继续播放。</p> <p>· 19115： MS Edge和IE 11（Win 8.1和10）未在CORS重定向上将Origin设置为null，但因为标头不是null而失败，从而导致播放错误。</p> <p>· 19861：在已播放媒体的源缓冲区上附加行为时出现问题。 Chrome会拒绝包括moov在内的附加片段，从而导致后续解码错误。 (Chromium第#735335期)</p> <p>19921：某些HLS内容的播放停止，即使其缓冲成功也是如此(Chromium问题#713540)</p> <p>· 20444：搜寻以结束IE和Edge上的缓冲范围可能会导致播放停止。</p> <p>· 20511：有时，对于包含或不包含广告的HLS流，可以观察到搜寻拒绝。</p> <p>· 20743：在Windows 10 Chrome上，HLS Live流会在MP4前置播放之前播放几秒钟。</p> <p>· 21043：由于缺少元数据，视频维度在初始加载时可能不正确。</p> <p>· 21115：如果播放列表中的视频有前置广告，则需要使用Android用户手势开始播放。</p> <p>· HLS Live不支持时间戳滚存。</p> <p>·不支持AAC-SSR音频。</p> <p>不支持音频编解码器AC3和增强型AC3。</p> <p>·对于具有时间戳不连续但不具有不连续标记的流</p> <p>·由于跳转，播放可能有故障和错误搜寻。</p> <p>·内容持续时间和播放持续时间可能不匹配。</p> <p>·表示和演绎版之间的不连续性与其他智慧匹配可能会导致同步和停滞问题。</p> <p>·字幕和WebVTT可能不会出现在流末尾附近。</p> <p>·不支持跨时间戳跳转更改音频编解码器。</p> <p>·不支持广告插入。</p> <p>·快速前进特技模式可能会导致在Win 8.1 IE 11上出现播放循环(MS问题#12446268)。</p> <p>短划线：</p> <p>·对于实时流 — 支持动态类型的实时个人资料。</p> <p>·对于VoD流 — 支持静态类型的实时配置文件。</p> <p>对于VoD流 — 按需用户档案未针对广告工作流进行认证。</p> </td> 
   <td><p>·不支持DASH Live和DASH视频点播流。</p> <p>·全屏模式下iOS不支持PIP（画中画）视频播放。</p> <p>在Safari（视频标记）扩展上，如果没有正确的内容类型标头，则较少清单不起作用。</p> </td> 
   <td><p>·发件人应用程序中的applicationID必须与将接收人的URL注册为自定义接收人应用程序时生成的相同。</p> <p>·参考播放器已针对DASH工作流进行认证。 UI框架未经过认证。</p> <p>有关支持的媒体编解码器的列表，请参阅 <a href="https://developers.google.com/cast/docs/media"><em>此处</em></a>.</p> </td> 
  </tr> 
  <tr> 
   <td>FER VOD</td> 
   <td>常规播放（播放、暂停、搜寻）</td> 
   <td> </td> 
   <td>18098：发现HLS LBA FER流存在某些搜寻问题。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>自适应比特率</td> 
   <td><p>· 20079：在缓冲范围内的搜寻时进行缓冲重写。</p> <p>20080：FlashABR行为与MSE一致。</p> </td> 
   <td><p>·由于缓冲区相关限制，忽略ABR流中的仅音频回退变量。</p> <p>· 12289：如果是HLS/DASH流未设为多路复用，则ABR控制参数不适用于音频。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>608/708字幕</td> 
   <td> </td> 
   <td><p>· 7810：在Android 4.4.4上，Chrome似乎不支持播放器使用的基本CSS字体系列，因此字体样式更改功能不起作用。</p> <p>·如果存在608个字幕，则无法更改CC渠道。</p> <p>· 608字幕不支持高级样式功能。</p> <p>支持通过Accessibility标记发信号的嵌入式字幕(608/708)。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>· 5206：播放器在显示字幕时忽略WebVTT文件中的区域标记。</p> <p>· DASH：不支持碎片/分段VTT文件。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>清单故障转移</td> 
   <td>21056：使用Flash回退，如果主流在播放期间返回404错误，则不会为实时流执行故障转移。</td> 
   <td>清单故障转移仅适用于内容，而不适用于广告。</td> 
   <td>仅对于HTTP错误代码404，缺少播放列表故障转移在Safari上有效。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>高级故障切换</td> 
   <td> </td> 
   <td><p>·区段故障转移不支持跳过不可用的区段并继续播放。</p> <p>20533：播放列表中缺少的区段应被视为中断，并应从下一个可用区段继续播放。</p> <p>21267：由于故障转移而导致的流切换可能会导致下载旧区段。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>QoS和播放器通知</td> 
   <td>21129：在Flash回退的情况下，帧速率不可用。</td> 
   <td><p>• 11170:</p> <p>与具有Flash回退的浏览器TVSDK不同，Timed_Event不适用于具有MSE的浏览器TVSDK。</p> <p>21129：不计算实时流的帧速率。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>支持Cookie标头</td> 
   <td> </td> 
   <td> </td> 
   <td><p>Safari不支持withCredentials标记和Cookie标头。</p> <p>21051：要在Safari中允许Cookie，请在“首选项”&gt;“隐私”中启用“Cookie和网站数据”设置。</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>自定义标记</td> 
   <td>14763：不支持除#开头的自定义标记。 现在，将在Flash回退期间为此类标记创建和报告TimedMetadata对象。</td> 
   <td>未验证带内自定义标记的流。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>后期绑定音频</td> 
   <td> </td> 
   <td><p>· HLS Live LBA流不支持广告插入。</p> <p>· 17273：在发生故障转移时，HLS VOD LBA流切换到默认演绎版，并且无法切换回上次选择的演绎版。</p> <p>· 20251： HLS实时LBA流可能在搜寻时停滞。</p> <p>· 20497：如果HLS LBA未设为多路混音的流在流结尾附近丢失了音频或视频帧，则播放器仍处于缓冲状态。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>302重定向</td> 
   <td> </td> 
   <td><p>15787: 302</p> <p>windows Edge和IE浏览器不支持重定向优化，因为这些浏览器不支持XMLHttpRequest对象中的responseURL属性。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表17：高级播放功能**

<table> 
 <tbody> 
  <tr> 
   <td>内容类型</td> 
   <td>功能</td> 
   <td>Flash</td> 
   <td><strong>Firefox、IE、Chrome、Android Chrome中的HTML5</strong></td> 
   <td><strong>Safari中的HTML5、iOS和Safari</strong></td> 
   <td><strong>Chromecast（仅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>在偏移处播放</td> 
   <td><p>不支持以特定偏移值开始播放MP4内容。</p> </td> 
   <td>20492：在内容从偏移值恢复之前，播放偏移之前的中置广告。</td> 
   <td>iOS不支持具有偏移功能的播放。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>特技游戏</td> 
   <td>平滑点击播放不适用于没有iFrame呈现的流。</td> 
   <td><p>· Firefox和Internet Explorer不支持Trick Play自适应，因此这些浏览器上不提供Trick Play反向模式。</p> <p>·在与广告一起播放内容时，点击播放不可用。</p> <p>· 10435：在DASH播放期间，视频在Internet Explorer上的正向特技播放时冻结(Win 8.1)</p> <p>断断续续。 发生这种情况是因为我们使用的是video elements playbackRate属性而没有特技播放自适应。</p> <p>14182：有时，在Chrome浏览器上倒带期间，可能不会收到搜寻事件，因此特技模式将无效。</p> <p>· 14942：可以在适用于Android的Chrome中设置播放速率，即使在非特技播放流的情况下也是如此，但不会应用此设置，并且将继续以正常速率播放。</p> <p>· 17308：搜寻功能在点击播放模式下不起作用。</p> <p>· 17309：在Chrome浏览器上，反向特技模式不能持续超过2秒。</p> <p>19272：对于DASH流，特技播放可能无法从Windows 10 Edge浏览器上的缓冲中恢复。</p> </td> 
   <td>不支持倒带特技模式。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>ID3解析</td> 
   <td>20346： SDK还应返回ID3帧的文本编码字节。</td> 
   <td><p>SDK会忽略音频数据传输流(ADTS)中可用的ID3标记。</p> <p>· 12378：ID3定时元数据在支持MSE的Flash和浏览器上的不同时间解析，因此，引用播放器时间轴上的显示行为也不同。</p> <p>· 19247： UI框架不支持ID3解析。</p> </td> 
   <td><p>· 20323：Safari不会解析用于指示aac区段第一个样本的时间戳的PRIV ID3标记(Safari问题#32422733)</p> <p>· 20350：在某些设备(包括MAC OS X 10.1、iPad10)上，当处于特技模式时，Safari不提供提示更改事件，因此未收到ID3帧。 (Safari #32450526期)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>间断标记支持</td> 
   <td> </td> 
   <td><p>·包含不连续性的HLS流不支持客户端广告插入。</p> <p>· HLS流中的不连续情况不允许更改音频编解码器。</p> <p>·带有不连续标记的HLS流不支持音频轨道切换</p> </td> 
   <td>具有不连续性的HLS流必须具有不连续序列号才能在Safari上播放。</td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表18：内容保护功能**

<table> 
 <tbody> 
  <tr> 
   <td><strong>内容类型</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox、IE、Chrome、Android Chrome中的HTML5</strong></td> 
   <td><strong>Safari中的HTML5、iOS和Safari</strong></td> 
   <td><strong>Chromecast（仅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>AES-128</td> 
   <td> </td> 
   <td>AES-128加密内容不支持字节范围。</td> 
   <td>12324：如果未指定IV标记，则HLS AES-128加密流无法在Safari上播放。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>DRM</td> 
   <td> </td> 
   <td><p>· 12660：对于过期的PlayReady加密短划线内容，HTML5播放器引发内部服务器错误。</p> <p>· 16720：如果缺少时段标记中的start属性，则DASH DRM加密内容无法正常工作。</p> <p>· 18589：带有Xlink的受保护DRM的Dash VoD多时段流不支持播放。</p> <p>· 18653：使用多个键播放Widevine MultiPeriod内容，在第一时段停止，无法切换到下一时段。</p> <p>· 18656：使用不同密钥加密的Playready MultiPeriod流无法播放。</p> <p>Playready 2.0 for Dash未经过认证。</p> <p> </p> <p> </p> </td> 
   <td>12602：HTML5播放器在Safari上反复刷新HLS公平播放DRM元数据</td> 
   <td><p>可以播放通过Bento4打包的DASH Widevine DRM内容。 通过Offline Packager和Shaka Packager打包的内容不会播放。 不支持DASH PlayReady DRM。</p> </td> 
  </tr> 
 </tbody> 
</table>

**表19：核心Ad Insertion功能(CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>内容类型</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox、IE、Chrome、Android Chrome中的HTML5</strong></td> 
   <td><strong>Safari中的HTML5、iOS和Safari</strong></td> 
   <td><strong>Chromecast（仅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>前/中/后</td> 
   <td> </td> 
   <td><p>·在双播放器模式下播放包含HLS实时内容的前置广告。</p> <p>·不支持包含HLS内容的短划线广告和包含DASH内容的HLS广告。</p> <p>· 19002：在带有MSE adBreak的HTML5播放器中。 insertionType未返回正确的值以描述正确的插入类型，即客户端插入和/或服务器插入。</p> <p>7794：在全屏模式下显示默认控制栏的移动设备(iOS、带有Chrome 33或更低版本的Android或本机浏览器)上，可在广告播放时使用搜寻栏和快速前进按钮。</p> <p>· 11048：如果是Media Source Extensions，则从广告切换到HLS实时内容会不平稳。</p> <p>· 16083：在Android 4.4 Chrome v52上，有时在播放停止后，包含HLS内容的HLS广告可能会导致管道解码错误。</p> <p>· 16097：未处理广告时间遇到的错误，可能会导致主流停止播放。</p> <p>· 18095： HLS实时内容不支持MP4广告。</p> <p>19120：对包含HLS内容的HLS广告进行多次搜寻可能会导致流停止播放。</p> <p>· 19131：从前置广告时间切换到内容时，可能会显示缓冲叠加。</p> <p>· 20296：对于HLS实时流，在DVR窗口中回头搜索，随后在已解析的中段上搜索可能会导致播放停滞。</p> <p>· 20298：HLS具有中间滚动的实时流在第一个中间滚动广告离开DVR窗口时停顿。</p> <p>· 20317：如果广告时间包含多个广告，则在切换到下一个广告或从广告切换到内容时，HLS实时流可能会停滞。</p> 
    <ul> 
     <li>HLS实时流的DVR窗口中的广告未解析。</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>SDK不遵循VAST adSource的VMAP响应中的序列属性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>20779： SDK不遵循VAST adSource的VMAP响应中的序列属性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>VMAP 1.0</td> 
   <td> </td> 
   <td>12014：不支持VMAP重复属性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>创意重新打包</td> 
   <td> </td> 
   <td>21464：如果广告时间中某个广告的创意重新打包失败，则完全丢弃广告响应。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表20：高级Ad Insertion功能(CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>内容类型</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox、IE、Chrome、Android Chrome中的HTML5</strong></td> 
   <td><strong>Safari中的HTML5、iOS和Safari</strong></td> 
   <td><strong>Chromecast（仅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>仅广告</td> 
   <td> </td> 
   <td>20056：播放器技术属性没有关联，因为它基于主内容，而在仅广告播放的情况下主内容为空</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>自定义广告策略</td> 
   <td> </td> 
   <td><p>· MP4广告和MP4内容不支持广告行为。</p> <p>· 13973：自定义广告行为 — SKIP策略在与MSE一起使用时不会引发完成事件。</p> <p>· 14939：自定义广告行为策略跳过和跳过广告时间不适用于DASH内容。</p> <p>· 17131：广告的第一帧可见，如果是SKIP广告时间策略，则恢复内容。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>伴随广告/横幅广告/可点击广告</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>使用引用播放器时，横幅广告不可见。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>· VPAID广告不支持广告行为。</p> <p>· 15032：不支持在广告时间将VPAID广告与MP4或HLS广告结合使用。</p> <p>· 19001：在Android和iOS上，使用MP4播放VPAID广告作为主内容时，可听到双声道，这是主内容之一，也是广告之一。</p> <p>· 20762：画中画(PIP)不支持VPAID广告。</p> <p>· 21172：未收到带有VPAID广告的HLS VOD内容的播放结束事件。</p> <p>· 21173：未针对HLS VOD内容和后置式广告VPAID收到onAdBreakCompleteEvent。</p> </td> 
   <td>播放器在VPAID广告和主内容之间切换时在正常模式和全屏模式之间切换。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表21：集成**

| **内容类型** | **功能** | **Flash** | **Firefox、IE、Chrome、Android Chrome中的HTML5** | **Safari中的HTML5、iOS和Safari** | **Chromecast（仅限DASH播放）** |
|---|---|---|---|---|---|
| VOD +实时 | Adobe Analytics VHL集成 |  | 19004：无法通过UI配置器工具进行Video Analytics跟踪。 |  |  |

## 有用资源 {#helpful-resources}

* 请参阅完整的帮助文档，网址为 [Adobe Primetime学习与支持](https://experienceleague.adobe.com/docs/primetime.html) 页面。

---
title: 浏览器TVSDK 2.4发行说明
description: 浏览器TVSDK 2.4发行说明介绍了浏览器TVSDK 2.4中新增的、受支持和不受支持的功能以及已知问题。
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

浏览器TVSDK 2.4发行说明介绍了浏览器TVSDK 2.4中新增的、受支持和不受支持的功能以及已知问题。

## 简介 {#introduction}

浏览器TVSDK是一个工具包，允许您向基于浏览器的视频播放器应用程序添加高级视频播放功能、内容保护和广告。

浏览器TVSDK 2.4提供了JavaScript API来构建基于浏览器的视频应用程序，并在以下模式中包含播放支持：

* 仅HTML5
* HTML5，带自动闪存回退
* Flash始终

此版本包括以下信息：

· [浏览器TVSDK API文档](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

· [浏览器TVSDK编程指南](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf).

· [适用于1.4 DHLS的TVSDK到浏览器TVSDK 2.4迁移指南](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

· [从浏览器TVSDK 2.4.6转换到版本2.4.7](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html).

·引用实施，包含在内部版本中。

>[!NOTE]
>
>*有关此版本的安全注意事项的完整列表，请参阅安全注意事项。

## 新增功能和受支持功能 {#what-s-new-and-supported-features}

此版本的浏览器TVSDK提供了可用于增强视频应用程序的新功能。

**2.4.12更新（版本204）中的新增功能**

作为浏览器TVSDK 2.4.12更新（版本204）的一部分，提供了以下添加内容：

* 更改了AdobePSDK.MediaPlayer的卷API的实施，以允许在播放静音时在iOS上自动播放。

·新的API， `auditudeSettings.ignoreVPAIDAds`，以允许忽略从Auditude服务器收到的VPAID广告。 API不适用于Flash回退。

**版本2.4.11**

浏览器TVSDK 2.4.11版本中提供了以下增强功能和新增功能：

· MSE和Flash回退模式支持HLS实时区段故障切换。

·支持 `AuditudeSettings.creativeRepackagingDomain` API现在也适用于MSE。 以前仅支持Flash回退模式。

·该版本包含针对关键客户问题的修复。 请参阅 *已修复的问题* 列表。

**版本2.4.10**

浏览器TVSDK 2.4.10版本中提供了以下增强功能和新增功能：

· TVSDK提供enableLogging()以启用或禁用日志记录。 请参阅 [API文档](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)，以便使用。

·使用Adobe Analytics时，TVSDK不再支持默认章节。 使用您的应用程序定义和管理章节。

·该版本包含针对关键客户问题的修复。 请参阅*问题修复*列表。

**版本2.4.9**

浏览器TVSDK 2.4.9版本中提供了以下增强功能和新增功能：

·支持具有时间不连续但没有间断标记的HLS VOD和实时流。

· HLS VOD和实时流的Safari视频标记支持ID3 v2.4.0帧。

·安全广告加载实施可确保根据API配置将广告服务器调用升级为安全HTTP。 有关详细信息，请参阅AdobePSDK.AdvertisingMetadata和AdobePSDK.ForceHttpsAdConfiguration类。 Flash回退模式不支持此功能。

·与VAST 3.0响应关联的广告ID信息和扩展信息现在由TVSDK提供给应用程序，并可用于实施广告测量的Moat集成。 有关详细信息，请参阅AdobePSDK.NetworkAdInfo API。 在Flash回退模式中不支持此功能。

· AdobePSDK.ForceHttpsConfiguration类不再可用。 成功者

AdobePSDK.ForceHttpsAdConfiguration类。

·现在有一个新的API，AdobePSDK.optimizeFlashCalls，可用于优化调用以改进Flash回退模式下的HLS播放体验。 默认情况下，此设置处于禁用状态。

**2.4.8更新（版本6002）中的新增功能**

此更新包含针对关键客户问题的修复。 请参阅 *已修复的问题*，以获取列表。

**版本2.4.8**

浏览器TVSDK 2.4.8版本中提供了以下增强功能和新增功能：

· SDK现在与Chrome EME兼容，并且从Chrome v58开始提供的最佳实践更改。 有关更多详细信息，请参阅 [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

· UI框架现在支持Flash、仅限广告和定位信息工作流中的HLS访问DRM。

· setDRMAuthenticateData API已添加到UI框架中。 要播放受Adobe访问DRM保护的流，请调用此API。 或者，也可以在播放器中指定drmAuthenticateData属性。 请参阅 [AdobePSDK.videoBehavior ](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)以了解详细信息。

**版本2.4.7**

以下功能在版本2.4.7中是新增的：

·在UI框架中添加UI配置器

您可以通过以下方式之一配置播放器：

·使用JSON对象

·使用API

为帮助生成JSON对象，浏览器TVSDK提供了**UI配置器**工具。

在此工具中，您可以选择各种设置，单击**测试配置**以验证设置，然后单击**下载配置**以下载设置。 下载文件后，您可以将此文件的内容作为JSON对象传递到ptp.videoPlayer API。

·在UI框架中添加了MediaPlayerItemConfig API

包括advertisingMetadata、advertisingFactory、adSigningMode、networkConfiguration、customRangeMetadata、useHardwareDecoder、subscribeTags、adTags、thumbnailScrubber、billingMetricsConfig在内的各种功能都可以通过MediaPlayerItemConfig进行配置。 有关更多信息，请参阅 [浏览器TVSDK API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* * [文档](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

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

可通过UI框架启用DRM配置和Analytics跟踪。

* 添加 `AdobePSDK.embedSWFinFullScreenDiv` API

此新API为播放器应用程序提供了选择div的灵活性，可将FlashFallback.swf文件嵌入到该div中。

* 已更换 `getVersion`API来自 `AdobePSDK.MediaPlayer` 类 `AdobePSDK.Version` 类。 有关详细信息，请参阅 `AdobePSDK.Version` API [此处](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html).

**版本2.4.6**

以下功能在版本2.4.6中是新增的：

* **Browserify支持**

Browserify允许您在浏览器中使用node.js样式模块。 您可以定义依赖项，并将所有内容浏览到一个JavaScript文件中。

* **帐单**

借助帐单，浏览器TVSDK可以收集播放器使用量度以向Primetime客户计费。

>[!NOTE]
>
>已在版本2.4.6中删除Enum PSDKErrorCode中已弃用的enum MediaPlayer.Events和已弃用的常量。有关更多信息，请参阅 [从浏览器TVSDK 2.4.5转换到版本2.4.6](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html).

**版本2.4.5**

以下功能在版本2.4.5中是新增的：

* **完整事件重播和广告**

   HLS完整事件重播(FER)流现在支持广告解析和广告行为。 要启用此支持，请将广告信令模式设置为 `MANIFEST_CUES` 创建 `MediaPlayerItemConfig` 对象。

* **MediaplayerView ScalePolicy支持**

   应用程序开发人员现在可以使用MediaplayerView scalePolicy属性为视图指定不同的scalePolicy。

* **变形内容支持**

   现在，使用MSE和Flash播放时支持变形内容播放。

* **选择性应用`withCredentials`**

When `withCredentials` 设置为true时， `Access-Control-Allow-Origin` 标头无法设置为通配符。 根据服务器的响应，浏览器TVSDK将有选择地设置 `withCredentials` 属性。 有关此支持的更多信息，请参阅 [浏览器TVSDK API文档](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

**版本2.4.4**

以下功能在版本2.4.4中新增：

* **Chromecast示例应用程序**

此版本支持发送者和接收者应用程序，该应用程序通过客户端广告插入演示了DASH VOD流和DASH Widevine流的播放。

* **高级故障切换支持**

此版本包含对HLS VOD流的高级故障切换用例（区段和服务器故障切换）的支持。

**版本2.4.3**

以下功能在版本2.4.3中新增：

* **短划线VOD的自定义标记**

   内联自定义标记（事件）可作为TimedMetadata对象订阅和接收。

* **播放不带扩展的流**

   现在支持不带扩展的HLS和DASH流。 对于清单文件，在加载资源时需要指定resourceType。 对于区段和VTT文件，Content-Type响应标头用于确定内容类型。

**版本2.4.2**

以下功能在版本2.4.2中新增：

* **API奇偶校验**

有关API奇偶校验的完整列表，请参阅 [适用于1.4 DHLS的TVSDK到浏览器TVSDK 2.4迁移指南](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

* **Sample-AES支持**

   此版本增加了对MSE和Flash回退上Sample-AES加密内容播放的支持。 删除了在Google Chrome上通过安全源托管AES内容的要求。

* **支持AAC容器**

   现在支持播放扩展名为.aac的文件。 这可以是纯音频流或替代音频。

   >[!NOTE]
   >
   >尚不支持AC3和增强的AC3编解码器。

* **标记化流播放**

通过内容交付网络(CDN)交付的HLS流有时可能会在清单和区段请求中使用身份验证令牌进行验证，并且这些令牌可以作为URL参数或Cookie标头提供。 现在支持播放此类流。

**版本2.4.1**

以下功能在版本2.4.1中新增：

* **UI框架**

此框架旨在加快基于JavaScript的视频播放器应用程序的UI开发，由API组成，这些API用于包含播放/暂停和音量等基本控件，以及用于轻松添加或删除元素（如推移栏状态和隐藏式字幕设置）。 您可以指定与控件关联的行为、创建自定义控件，以及为播放器UI设置外观。 这一切都通过框架实现，无需直接操作DOM结构。

* **实时流的HLS播放增强功能**

此版本支持由广告插入引起的不连续。 它使用EXT-PROGRAM-DATE-TIME标记，后跟EXT-MEDIA-SEQUENCE标记，在自适应比特率配置文件中进行同步，以便顺利播放。

* **VPAID 2.0支持**

视频播放器广告服务界面定义(VPAID)版本2.0为用户提供了丰富的媒体体验，并允许发布者更好地定位广告、跟踪广告展示次数，以及从视频内容中盈利。 此版本支持用于视频点播(VOD)内容的线性JavaScript VPAID广告。

* **自定义HLS标记**

媒体流可以在播放列表/清单文件中以标记形式携带其他元数据。 浏览器TVSDK允许您指定和订阅其他标记，并在清单中显示这些标记时收到通知。

* **播放器时间轴上显示的广告标记**

此版本支持在播放器时间轴上为VOD和实时内容显示广告标记。 您可以在引用播放器中看到此行为。

**在2.4中受支持**

版本2.4中提供了以下功能：

* **MP3音频播放**

   此版本支持在具有媒体源扩展(MSE)和Safari视频标记的浏览器上播放MP3音频。

* **MP4视频播放**

   支持以下功能：

   * 单个流播放
   * 具有广告行为和跟踪的前置和后置MP4广告
   * 具有广告行为和跟踪的前置和后置HLS广告
   * 具有广告行为和跟踪的前置和后置短划线广告

## 支持的平台 {#supported-platforms}

浏览器TVSDK对于需要运行的平台和软件级别有特定要求。 支持以下平台和软件级别：

### 桌面配置 {#desktop-configurations}

* Microsoft Windows 7:

   * Internet Explorer 11+
   * 铬33+
   * Firefox 38+

* Microsoft Windows 8.1

   * Internet Explorer 11+
   * 铬33+
   * Firefox 38+

* Microsoft Windows 10

   * Edge+

* Apple OS X

   * Safari 9及以上版本
   * 铬33+
   * Firefox 38+

### 移动Web配置 {#mobile-web-configurations}

* Android 4.4

   * 本机浏览器
   * 铬33+

* Android 5.0

   * 本机浏览器
   * 铬33+

* Android 6.0

   * ·铬33+

* AppleiOS9

   * Safari 9及以上版本
   * 铬33+

* AppleiOS10

   * Safari 9及以上版本
   * 铬33+

**Google Chromecast(第二代；（仅限短划线播放）**

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
   <td><p>HLS和DASH</p> </td> 
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
   <td><p>HLS和DASH</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Mozilla Firefox</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS和DASH</p> </td> 
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
   <td><p>HLS、达什</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
 </tbody> 
</table>

## 特征矩阵 {#feature-matrix}

以下是此版本支持和不支持的功能列表：

* *MP3音频功能 — 核心播放*
* *MP4视频功能 — 核心播放*
* *MP4视频功能 — 核心Ad Insertion*

>[!NOTE]
>
>*在以下功能矩阵表中，“Y”表示当前版本支持该功能。*

### MP3音频功能 {#mp-audio-features}

**表1:核心播放{#table-core-playback}**

| 类别 | 内容类型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 播放 | MP3 VOD | 常规播放（播放、暂停、搜寻） | 不受支持 | Y | Y |

1浏览器TVSDK视频标记不支持流和DRM。 在所有浏览器中，编解码器和容器支持并不相同。

2对于版本41或更低版本，Firefox默认为Flash Player。

### MP4音频功能 {#mp-audio-features-1}

**表2:核心播放**

| 类别 | 内容类型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 播放 | MP4 VOD | 常规播放（播放、暂停、搜寻） | 不受支持 | Y | Y |

**表3:核心Ad Insertion**

| 类别 | 内容类型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | MP4 VOD | 前置(MP4) | 不受支持 | Y | Y |
| Ad Insertion | MP4 VOD | 后置(MP4) | 不受支持 | Y | Y |

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
>*在以下功能矩阵表中，“Y”表示当前版本支持该功能。*

### HLS功能 {#hls-features}

支持以下功能：

**表4:HLS核心播放**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:Safari、iOS Safari</strong></p> </td> 
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
   <td><p>层VOD</p> </td> 
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
   <td><p>仅VOD</p> </td> 
   <td><p>仅VOD</p> </td> 
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
   <td><p>设置缓冲控制参数</p> </td> 
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
   <td>延迟绑定音频</td> 
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

**表5:HLS高级播放功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:Safari、iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>偏移时播放</p> </td> 
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
   <td><p>技巧游戏</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>平滑技巧游戏</p> </td> 
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
   <td><p>不连续标记支持</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>标记化流</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>帐单</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**表6:HLS内容保护功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:Safari、iOS Safari</strong></p> </td> 
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
   <td><p>不受支持</p> </td> 
   <td><p>FairPlay</p> </td> 
  </tr> 
 </tbody> 
</table>

**表7:HLS核心广告插入功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:Safari、iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>前置(MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>中置(HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>后置(MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>层VOD</p> </td> 
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

**表8:HLS高级广告插入功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:Safari、iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>仅限广告</p> </td> 
   <td><p>不受支持</p> </td> 
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
   <td><p>不受支持</p> </td> 
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

**表9:HLS集成{#table-hls-integrations}**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:Safari、iOS Safari</strong></p> </td> 
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

## 短划线特征矩阵 {#dash-feature-matrix}

以下是浏览器TVSDK中DASH功能的功能矩阵。

· *短划线核心播放功能*

· *短划线高级播放功能*

· *短划线内容保护功能*

· *短划线核心广告插入功能*

· *短划线高级广告插入功能*

· *DASH集成*

>[!NOTE]
>
>在以下功能矩阵表中，Y表示当前版本支持该功能。

### 短划线特征 {#dash-features}

支持以下功能：

**表10:短划线核心播放功能**

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
   <td><p>层VOD</p> </td> 
   <td><p>常规播放（播放、暂停和搜寻）</p> </td> 
   <td><p>不受支持</p> </td> 
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
   <td><p>仅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>故障转移</p> </td> 
   <td><p>仅VOD</p> </td> 
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
   <td><p>设置缓冲控制参数</p> </td> 
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
   <td><p>后期音频</p> </td> 
   <td><p>仅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>302重定向</p> </td> 
   <td><p>仅VOD</p> </td> 
  </tr> 
 </tbody> 
</table>

**表11:短划线高级播放功能**

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
   <td><p>偏移时播放</p> </td> 
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
   <td><p>戏法游戏</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>平滑技巧游戏</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>ID3解析</p> </td> 
   <td><p>不受支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>多期支持</p> </td> 
   <td><p>仅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>标记化流</p> </td> 
   <td><p>不受支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>帐单</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**表12:短划线内容保护功能**

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
   <td><p>不受支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>内容保护</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>Sample-AES</p> </td> 
   <td><p>不受支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>内容保护</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>·在Chrome、Firefox 47及更高版本以及Chromecast中使用Widevine</p> <p>·在Windows 8.1和Edge上的Internet Explorer上播放就绪</p> <p>·适用于Windows Firefox的Primetime DRM（仅限视频）</p> </td> 
  </tr> 
 </tbody> 
</table>

**表13:短划线核心广告插入功能**

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
   <td><p>前置（MP4/短划线）</p> </td> 
   <td><p>仅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>中置（短划线）</p> </td> 
   <td><p>仅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>后置（MP4/短划线）</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>层VOD</p> </td> 
   <td><p>广告分辨率和行为</p> </td> 
   <td><p>不受支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>默认广告策略</p> </td> 
   <td><p>仅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>仅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>仅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>创意重新打包（MP4到短划线）</p> </td> 
   <td><p>不支持</p> </td> 
  </tr> 
 </tbody> 
</table>

**表14:短划线高级广告插入功能**

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
   <td><p>仅限广告</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>定位参数</p> </td> 
   <td><p>仅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>自定义参数</p> </td> 
   <td><p>仅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>自定义广告策略</p> </td> 
   <td><p>不受支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>延迟广告加载</p> </td> 
   <td><p>不受支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>伴随广告、横幅广告、可点击广告</p> </td> 
   <td><p>不受支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>不受支持</p> </td> 
  </tr> 
 </tbody> 
</table>

**表15:DASH集成**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>类别</strong></p> </td> 
   <td><p><strong>内容类型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>集成</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>Adobe Analytics VHL集成</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## 已修复的问题 {#issues-fixed}

**2.4.12更新（版本204）中修复的问题**

在浏览器TVSDK版本2.4.12更新（版本204）中修复了以下问题：

· **21647** — 音频静音时，TVSDK应允许在iOS设备上自动播放视频。

· **21465** — 在播放DASH实时流后播放受DRM保护的DASH流时，收到错误密钥系统访问被拒绝。

· **21442** — 在以用户手势播放前置广告后，在iOS Web上启用内容自动播放。

· **21240** — 提供了用于筛选从Auditude/VMAP解析的VPAID广告的API。

**版本2.4.11中修复的问题**

已在浏览器TVSDK版本2.4.11中修复以下问题：

**核心播放功能：**

· **19192**:TVSDK现在实施TextFormat:bottomInset和TextFormat:safeArea。 由于这些增强功能，如果控制栏显示在屏幕上，则可以重新放置隐藏式字幕。

· **21009**:如果在出现不连续的搜寻时直到出现新字幕，屏幕上会保留隐藏式字幕。

· **21141**:在区段追加期间，由于存在争用条件，向回搜寻被拒绝。

· **21142**:使可搜寻的播放范围在播放器处于“初始化”状态时可用。 由于这些更改，现在支持在位启动会话。

· **21363**:608/708型隐藏式字幕在为短划线流插入广告后不同步。

**广告插入功能：**

· **21179**:现在，可以通过正确设置ad.primaryAsset.adParameters属性来解决VOD内容的中置相关问题（长时间暂停、黑色帧）。

· **21257**:如果MP4不是有效的mime类型，并且启用了创作重新打包功能，则会选择位速率最高的MP4文件进行转码。

· **21361**:TVSDK现在将广告系统和创作ID从VAST响应中作为创作包装请求中的查询参数传递，以支持其他标准化规则。

**版本2.4.10中修复的问题**

已在浏览器TVSDK版本2.4.10中修复以下问题：

**核心播放功能：**

· **21060**:包含中断和ISO BMFF框的HLS流在流结束时引发的编解码器错误无效。

· **21045**:播放列表中的首次视频播放完成后，自动播放在iOS上不起作用。

· **20975**:Chrome浏览器上的QoS提供程序将以NaN的形式返回帧率。

· **20823**:遇到没有数据的区段时引发不受支持的编解码器错误。

· **20769**:现在，SDK在进行搜寻时以当前比特率开头，而不是基于ABR策略立即切换。

· **20031**:在IE 11(Windows 8.1)上以纵向模式时，视频屏幕变小。 内容保护功能：

· **19316**:在HLS AES-128流的情况下，跳过解密失败的段。

**版本2.4.9中修复的问题**

在浏览器TVSDK版本2.4.9中修复了以下问题：

**核心播放功能：**

· **13407**:如果Firefox在播放期间停止发送“ontimeupdate”事件，则短划线流可能会停止。

· **16380**:在通过MSE对具有不匹配开始时间的区段进行混合音频视频内容播放期间，在ABR交换机上累积表示之间的音频同步错误，最终导致错误(Chromium问题#663686)。

· **17985**:在Firefox浏览器上播放特定ISO-BMFF流时，播放卡住(Firefox问题#1342913)。 自Firefox v53起，此问题已修复。

· **19141**:未捕获（在promise中）ReferenceError:宽度。

· **18997,19299**:区段边界处的视频闪烁问题。 这是因为SDK无法正确计算最后一个示例的合成时间偏移。

· **19780**:在Firefox v53上，HLS内容和HLS广告未开始播放(Firefox问题#354653)。

· **20046**:Program Date Time（程序日期时间）在作为定时元数据对象接收时将作为键接收，而不是作为值接收。

· **20047**:useDefaultResizeHandler因Flash回退而引发错误。

· **20179**:Flash回退不适用于Flash Playerv25.0.0.171。

· **20293**:Firefox会停止缓冲某些HLS流的数据，从而导致数据停止。

· **20626**:由于零持续时间的视频示例处理不正确，播放器在Chrome上引发媒体解码错误。

· **20078**:浏览器错误“超出配额”时播放停止。

· **18639**:在HLS实时流608 CC文本中，有时显示拼写错误。

· **20028**:ClosedCaptions size参数不会更改字体大小。

· **20613**:隐藏式字幕框彼此重叠，无法辨认。

**核心Ad Insertion(CSAI)功能：**

· **20043**:缺少包含多个广告和第三方重定向的广告展示和广告跟踪调用。

· **20044**:使用创意重新打包时，需要成功重新打包广告时间中的所有广告，否则广告时间将被完全丢弃。

· **20097**:跳过广告播放，主内容立即恢复，而不是在广告清单不可用时等待20秒的超时。

**版本2.4.8更新（版本6002）中修复的问题**

在浏览器TVSDK版本2.4.8更新（版本6002）中修复了以下问题：

· **14126:** 由于MSE源缓冲区中的内部间隙，在Firefox上播放可能会停止(问题#1316024)。 尝试搜寻以继续播放

· **19608:** 修复了对Auditude VMAP响应中的时间偏移值的执行问题。

· **19635:** 修复了Windows 10上Internet Explorer 11中的视频停滞问题。

· **19761:** 修复了HLS的ABR问题。

· **19780:** 修复了在Mozilla Firefox v53中损坏的HLS内容的广告播放。

· **19877和19744:** 这些问题修复了在执行搜寻操作后选择比特率时的不一致性。 现在，搜索时的比特率选择是当前比特率和启动时比特率的较低值。

· **19881:** 执行搜寻3-4次后，播放卡住并缓冲叠加将无限显示。

· **19884:** 确认符合Chrome 59测试版验证的媒体路径(VMP)要求。 bTVSDK能够使用Chrome 59测试版播放Widevine DRM内容。

· **19916:** UI-Framework上的DRM播放已中断。 现在，即使元数据中没有策略，也会调用acquireLicense。

**版本2.4.8中修复的问题**

在浏览器TVSDK 2.4.8版本中修复了以下问题：

· **10075**:在时间线之前进行搜寻时，未在Firefox和Chrome上收到播放结束事件，且未在Firefox上收到搜寻事件。

· **15775**:在Windows 8.1 Internet Explorer上未收到播放结束事件。

· **17306**:对于SSAI流，支持播放。 不支持跟踪拼合广告。

· **19142**:有时，倒退会导致视频播放器永远保持缓冲状态。

· **19218**:广告标记无法通过UI框架使用。

· **19219**:仅广告播放无法通过UI框架运行。

· **19222**:对播放列表请求一次AES-128密钥，然后从缓存中提供后续请求。 之前，会为每个区段请求该区段。

· **19597**:&quot;未捕获类型错误：在Chrome加那利内部版本中看到“无法读取未定义的属性“日志””。

· **19605**:adRequestDomain在Flash回退模式下不可用。

· **19608**:未为HLS实时流插入VMAP广告。 SDK现在会考虑提示标记，并且不依赖VMAP响应中的时间偏移值。

· **19637**:广告播放在广告结束时只会导致脚本错误。

· **19732**:CRS播放列表请求失败，并出现404错误。 现在，已更新来自浏览器TVSDK的1401和1403请求，以便处理这些请求。

· **19762**:acquireLicense ，用于在setAuthenticationToken之前调用，因为无论令牌的有效性如何，都会返回有效的许可证。 此问题现已修复，并且仅在setAuthenticationToken响应后调用acquireLicense。

**版本2.4.7中修复的问题**

在版本2.4.7中修复了以下问题：

· **8397**:如果区段不以关键帧开头，则通过Adobe Medium服务器生成的HLS实时流可能不会播放。

· **13606**:修复了Chrome浏览器上HLS流的多个搜寻相关问题。

· **14807**:在Chrome浏览器上，如果在play()后立即触发搜寻或暂停，则播放可能会停止，并出现错误DOMException:play()请求被调用中断……(Chromium第593273期)。

· **19085**:在重置播放器时，MediaPlayer参数（如volume、abrControlParameters和ccStyle）未设置为默认值。

**版本2.4.6中修复的问题**

在版本2.4.6中修复了以下问题：

· **18093**:在Flash回退模式下使用Flash Player版本24时，会返回订阅标记旁边标记的TimedMetadata。

**版本2.4.4中修复的问题**

在版本2.4.4中修复了以下问题：

· **8711**:对于MSE，默认情况下608/708字幕是两端对齐的。

· **13934**:播放HLS实时流时，广告的ABR设置不适用。

· **14079**:低DVR窗口的HLS实时流的寿命可能会失败，因为由于网络延迟问题，播放可能会落后。 单击实时点以继续播放。

· **15037**:播放器UI框架随附的示例在Windows 7的Microsoft Internet Explorer 10上不起作用。

· **15913**:对于HLS VOD流，在Chrome上，如果清单响应为304且未修改，则不会播放流。 自Chrome v55(Chromium问题633696)起，此问题已修复。

· **16103**:在Android Chrome上，在低带宽条件下，播放可能会因未捕获类型错误而停止：无法读取未定义错误的属性“programDateTime”。

· **16265**:对于HLS VOD和实时流，跨中断搜寻不起作用。

· **16709**:使用PDT和中断标记恢复HLS实时流可能会导致播放器在缓冲中卡住。

## 已知问题和限制 {#known-issues-and-limitations}

下面介绍了浏览器TVSDK中的限制和已知问题。

**表16:核心播放功能**

<table> 
 <tbody> 
  <tr> 
   <td><strong>内容类型</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5（在Firefox、IE、Chrome、Android Chrome中）</strong></td> 
   <td><strong>HTML5(位于Safari、iOS Safari中)</strong></td> 
   <td><strong>Chromecast（仅短划线播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>常规播放（播放、暂停、搜寻）</td> 
   <td><p>·不支持HLS以外的媒体格式。</p> <p>8799:Flash回退不处理混合内容，因此需要确保内容、广告和其他URL不会导致混合内容（内容安全且不安全）。</p> <p>· 19271:在Flash回退模式下，不支持通过UI框架进行多视图播放。</p> <p>·在Windows 7的Microsoft Internet Explorer 8和9上，无法回退Flash，因为SDK不支持这些版本。</p> <p>· 20262:Flash回退将自定义参数添加到定位信息列表。 对于Flash和MSE，自定义参数的优先级顺序也不同。</p> <p>· 20653：浏览器TVSDKFlash回退在Win10中无法通过Creators Update进行操作。</p> <p>·Flash回退适用于Flash Player版本23及更高版本。</p> <p>· 20087 - Chrome 59 Beta版，带</p> <p>Flash25.0.0.171</p> <p>测试版（默认），HLS播放在Flash回退模式下不起作用。 在金丝雀上还行。</p> </td> 
   <td><p>· 12563:由于MPD中不支持的音频编解码器字符串，带有音频编解码器的短划线流mp4a.40.02在Firefox上无法播放。 支持音频编解码器mp4a.40.2。</p> <p>15029:在UI-Framework的multiView中切换视频时，播放/暂停按钮不会相应地更新。</p> <p>· 16034：在Windows 8.1 IE上，调用reset()会导致MIME类型未知错误。 请重新加载媒体以继续播放。</p> <p>· 18235:在包含广告的短划线VOD流中，观察到某些搜寻问题。</p> <p>· 18727:MSE不支持错误API</p> <p>18750:在某些情况下，SDK和UI框架以及UI框架的状态更改事件可能会失序，在加载资源后添加的事件侦听器可能缺少IDLE和初始化StatusChange事件。</p> <p>· 18889:如果MediaPlayer处于ERROR状态，则不会返回视图对象。</p> <p>· 19039:如果为AdobePSDK。 MediaPlayer。 seekToLocal()的值大于EOF，则在出现MSE时，播放从头开始。</p> <p>· 19049:在播放过程中阻止视频时，在Chrome、IE、Firefox上Flash Player未报告错误状态。</p> <p>· 17205:在音频继续播放的同时，视频播放在播放未经过混合的流时停止数小时(Chromium问题# 664033)。</p> <p>· 12308:指定composition_time_offset的短划线流可能会在Chrome浏览器上对其应用timeStampOffset，从而导致负的解码时间，从而导致MEDIA_ERR_SRC_NOT_SUPPORTED错误(Chromium问题#398141)。</p> <p>· 14126:由于MSE源缓冲区中存在内部间隙，在Firefox上播放可能会停止(问题# 1316024)。 尝试搜寻以继续播放。</p> <p>· 19115:MS Edge和IE 11（Win 8.1和10）未在CORS重定向时将Origin设置为null，但失败，因为标头不为null，从而导致播放错误。</p> <p>· 19861：对于已播放的媒体，在源缓冲区上附加行为出现问题。 Chrome拒绝附加的片段（包括moov），从而导致后续解码错误。 (Chromium期#735335)</p> <p>19921:某些HLS内容即使成功缓冲仍停止播放(Chromium问题#713540)</p> <p>· 20444：在IE和Edge上寻求结束缓冲范围可能会导致播放停止。</p> <p>· 20511:有时，对于包含或不包含广告的HLS流，可以观察到搜寻拒绝。</p> <p>· 20743:在Windows 10 Chrome上，HLS实时流在MP4前置播放之前播放几秒钟。</p> <p>· 21043:由于缺少元数据，在初始加载时视频维度可能不正确。</p> <p>· 21115:如果播放列表中的视频有前置广告，则需要使用Android用户手势来开始播放。</p> <p>· HLS Live不支持时间戳滚动更新。</p> <p>·不支持AAC-SSR音频。</p> <p>不支持音频编解码器AC3和增强型AC3。</p> <p>·对于时间戳不连续但没有中断标记的流</p> <p>·由于跳转，播放可能出现故障和搜索错误。</p> <p>·内容持续时间和播放持续时间可能不匹配。</p> <p>·表示形式和呈现形式之间的不连续性应与其他方面相匹配，这可能导致同步和停滞问题。</p> <p>·字幕和WebVTT可能不会在流的末尾附近显示。</p> <p>·不支持跨时间戳跳转更改音频编解码器。</p> <p>·不支持广告插入。</p> <p>·快进特技模式可能导致Win 8.1 IE 11上的播放循环(MS问题#12446268)。</p> <p>短划线：</p> <p>·对于实时流 — 支持具有动态类型的实时配置文件。</p> <p>·对于VoD流 — 支持静态类型的实时配置文件。</p> <p>对于VoD流 — 点播用户档案未经广告工作流认证。</p> </td> 
   <td><p>·不支持短划线实时视频和短划线视频点播流。</p> <p>·iOS全屏模式下不支持PIP（画中画）视频播放。</p> <p>在Safari（视频标记）扩展中，如果没有正确的内容类型标头，则无法正常使用清单。</p> </td> 
   <td><p>·发送者应用程序中的应用程序ID必须与将接收者的URL注册为自定义接收者应用程序时生成的应用程序ID相同。</p> <p>·参考播放器经过DASH工作流程认证。 UI框架未经认证。</p> <p>有关支持的媒体编解码器列表，请参阅 <a href="https://developers.google.com/cast/docs/media"><em>此处</em></a>.</p> </td> 
  </tr> 
  <tr> 
   <td>层VOD</td> 
   <td>常规播放（播放、暂停、搜寻）</td> 
   <td> </td> 
   <td>18098:在HLS LBA FER流中观察到某些搜寻问题。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>自适应比特率</td> 
   <td><p>· 20079:在缓冲的范围内进行搜寻时重写缓冲区。</p> <p>20080:FlashABR行为与MSE一致。</p> </td> 
   <td><p>·由于与缓冲相关的限制，ABR流中仅音频的回退变体将被忽略。</p> <p>· 12289:在HLS/DASH流未混合的情况下，ABR控制参数不适用于音频。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>608/708字幕</td> 
   <td> </td> 
   <td><p>· 7810:在Android 4.4.4上，Chrome似乎不支持播放器使用的基本CSS字体系列，因此字体样式更改功能不起作用。</p> <p>·对于608个字幕，无法更改CC渠道。</p> <p>· 608字幕不支持高级样式功能。</p> <p>支持通过辅助功能标记发出的信号(608/708)的嵌入式字幕。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>· 5206:播放器在显示字幕时，会忽略WebVTT文件中的区域标记。</p> <p>·短划线：不支持碎片化/分段VTT文件。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>清单故障切换</td> 
   <td>21056:使用Flash回退，如果主流在播放期间返回404错误，则实时流不会发生故障转移。</td> 
   <td>清单故障切换仅适用于内容，而不适用于广告。</td> 
   <td>缺少的播放列表故障转移仅适用于HTTP错误代码404的Safari。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>高级故障切换</td> 
   <td> </td> 
   <td><p>·区段故障切换不支持跳过不可用的区段和继续播放。</p> <p>20533:播放列表中缺少的区段应当被视为“不连续”，并且应从下一个可用区段继续播放。</p> <p>21267:因故障转移而进行的流切换可能会导致下载较旧的区段。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>QoS和播放器通知</td> 
   <td>21129:帧率在“Flash回退”情况下不可用。</td> 
   <td><p>· 11170:</p> <p>Timed_Event不适用于具有MSE的浏览器TVSDK，而不适用于具有Flash回退的浏览器TVSDK。</p> <p>21129:不会计算实时流的帧速率。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>支持Cookie标头</td> 
   <td> </td> 
   <td> </td> 
   <td><p>Safari不支持withCredentials标记和Cookie标头。</p> <p>21051:要允许Safari中的Cookie，请启用首选项&gt;隐私中的“Cookie和网站数据”设置。</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>自定义标记</td> 
   <td>14763:不应支持以#开头的自定义标记。 现在，会在Flash回退期间为此类标记创建和报告TimedMetadata对象。</td> 
   <td>带内自定义标记的流未经认证。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>延迟绑定音频</td> 
   <td> </td> 
   <td><p>· HLS实时LBA流不支持广告插入。</p> <p>· 17273:在故障转移时，HLS VOD LBA流切换到默认呈现，无法切换回最后选定的内容。</p> <p>· 20251:HLS实时LBA流可能会在搜索时停止。</p> <p>· 20497:如果HLS LBA未混合流在流的末尾附近缺少音频或视频帧，则播放器会保持缓冲状态。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>302重定向</td> 
   <td> </td> 
   <td><p>15787:302</p> <p>windows Edge和IE浏览器不支持重定向优化，因为这些浏览器不支持XMLHttpRequest对象中的responseURL属性。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表17:高级播放功能**

<table> 
 <tbody> 
  <tr> 
   <td>内容类型</td> 
   <td>功能</td> 
   <td>Flash</td> 
   <td><strong>HTML5（在Firefox、IE、Chrome、Android Chrome中）</strong></td> 
   <td><strong>HTML5(位于Safari、iOS Safari中)</strong></td> 
   <td><strong>Chromecast（仅短划线播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>偏移时播放</td> 
   <td><p>不支持以特定偏移值开始播放MP4内容。</p> </td> 
   <td>20492:在内容从偏移值恢复之前，将播放偏移之前的中置广告。</td> 
   <td>iOS不支持带有偏移功能的播放。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>技巧游戏</td> 
   <td>无iFrame呈现的流无法使用平滑滴播。</td> 
   <td><p>· Firefox和Internet Explorer不支持适应特技播放，因此这些浏览器不提供反向特技模式。</p> <p>·在随广告一起播放内容时，不提供特技播放。</p> <p>· 10435:在DASH播放期间，在Internet Explorer(Win 8.1)上进行前向特技播放时，视频冻结</p> <p>间歇性。 之所以会出现这种情况，是因为我们使用的是视频元素playbackRate属性，而无需特技播放调整。</p> <p>14182:有时，在Chrome浏览器上回退期间，可能未收到搜寻事件，因此技巧模式将不起作用。</p> <p>· 14942:即使在非特技播放流的情况下，也可以在Android的Chrome上设置播放率，但将不应用设置，并且播放将以正常速率继续。</p> <p>· 17308:搜寻在Trickplay模式下不起作用。</p> <p>· 17309:在Chrome浏览器上，反向技巧模式的持续时间不能超过2秒。</p> <p>19272:对于DASH流，在Windows 10 Edge浏览器上，技巧播放可能无法从缓冲中恢复。</p> </td> 
   <td>不支持倒带技巧模式。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>ID3解析</td> 
   <td>20346:SDK还应返回ID3帧的文本编码字节。</td> 
   <td><p>SDK将忽略音频数据传输流(ADTS)中可用的ID3标记。</p> <p>· 12378:ID3定时元数据在支持MSE的Flash和浏览器上的不同时间进行解析，因此引用播放器时间轴上的显示行为也不同。</p> <p>· 19247:UI框架不支持解析ID3。</p> </td> 
   <td><p>· 20323:Safari未解析用于表示aac区段第一个示例时间戳的PRIV ID3标记(Safari问题#32422733)</p> <p>· 20350:在某些设备(包括MAC OS X 10.1、iPad 10)上，当处于特技模式时，Safari不提供提示更改事件，因此未收到ID3帧。 (Safari问题#32450526)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>不连续标记支持</td> 
   <td> </td> 
   <td><p>·包含中断的HLS流不支持客户端广告插入。</p> <p>·不允许跨HLS流中的中断更改音频编解码器。</p> <p>·具有不连续性标记的HLS流不支持音频轨道开关</p> </td> 
   <td>不连续序列号是在Safari上播放存在不连续的HLS流的一个要求。</td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表18:内容保护功能**

<table> 
 <tbody> 
  <tr> 
   <td><strong>内容类型</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5（在Firefox、IE、Chrome、Android Chrome中）</strong></td> 
   <td><strong>HTML5(位于Safari、iOS Safari中)</strong></td> 
   <td><strong>Chromecast（仅短划线播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>AES-128</td> 
   <td> </td> 
   <td>AES-128加密内容不支持字节范围。</td> 
   <td>12324:如果未指定IV标记，则HLS AES-128加密流无法在Safari上播放。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>DRM</td> 
   <td> </td> 
   <td><p>· 12660:HTML5播放器对过期的PlayReady加密短划线内容引发内部服务器错误。</p> <p>· 16720:如果缺少句点标记中的开始属性，则短划线DRM加密内容将不起作用。</p> <p>· 18589:带Xlink的受DRM保护的短划线VoD多时段流不支持播放。</p> <p>· 18653:使用多个键的WideIne多时段内容的播放在第一时段停止，并且无法切换到下一时段。</p> <p>· 18656:Playready MultiPeriod流，使用不同的密钥加密，无法播放。</p> <p>未对Dash的Playready 2.0进行认证。</p> <p> </p> <p> </p> </td> 
   <td>12602:Safari上的HLS Fairplay DRM元数据由HTML5播放器重复刷新</td> 
   <td><p>可以播放通过Bento4打包的DRM内容。 不会播放通过Offline Packager和Shaka Packager打包的内容。 不支持短划线播放就绪DRM。</p> </td> 
  </tr> 
 </tbody> 
</table>

**表19:核心Ad Insertion功能(CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>内容类型</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5（在Firefox、IE、Chrome、Android Chrome中）</strong></td> 
   <td><strong>HTML5(位于Safari、iOS Safari中)</strong></td> 
   <td><strong>Chromecast（仅短划线播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>前/中/后</td> 
   <td> </td> 
   <td><p>·具有HLS实时内容的前置广告在双播放器模式下播放。</p> <p>·不支持包含HLS内容的短划线广告和包含短划线内容的HLS广告。</p> <p>· 19002:在具有MSE adBreak的HTML5播放器中。 insertionType不返回正确的值来描述正确的插入类型，即插入的客户端和插入的服务器。</p> <p>1974年：在默认控制栏以全屏模式显示的移动设备(iOS、带有Chrome 33或更低版本的Android或本机浏览器)上，搜索栏和快进按钮在广告播放时可用。</p> <p>· 11048:如果使用媒体源扩展，从广告切换到HLS实时内容会不顺畅。</p> <p>· 16083:在Android 4.4 Chrome v52上，有时，包含HLS内容的HLS广告在播放停止后可能会导致管道解码错误。</p> <p>· 16097:未处理在广告时间期间遇到的错误，可能会导致主流停止播放。</p> <p>· 18095:HLS实时内容不支持MP4广告。</p> <p>19120:对HLS内容的HLS广告进行多次搜索可能会导致流停止播放。</p> <p>· 19131:在从前置广告时间切换到内容时，可能会显示缓冲叠加图。</p> <p>· 20296:对于HLS实时流，在DVR窗口中再次搜寻，然后再搜寻已解析的中间卷可能会导致播放停止。</p> <p>· 20298:HLS中间卷的实时流在第一个中间卷广告移出DVR窗口的瞬间停止。</p> <p>· 20317:如果广告时间包含多个广告，则在切换到下一个广告或从广告切换到内容时，HLS实时流可能会停止。</p> 
    <ul> 
     <li>无法解析HLS实时流的DVR窗口中的广告。</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>SDK在VAST adSource的VMAP响应中不执行序列属性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>20779:SDK不遵循VAST adSource的VMAP响应中的sequence属性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>VMAP 1.0</td> 
   <td> </td> 
   <td>12014:不支持VMAP重复属性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>创意重新打包</td> 
   <td> </td> 
   <td>21464:如果广告时间中某个广告的创意重新打包失败，则广告响应将完全丢弃。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表20:高级Ad Insertion功能(CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>内容类型</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5（在Firefox、IE、Chrome、Android Chrome中）</strong></td> 
   <td><strong>HTML5(位于Safari、iOS Safari中)</strong></td> 
   <td><strong>Chromecast（仅短划线播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>仅限广告</td> 
   <td> </td> 
   <td>20056:播放器技术属性没有相关性，因为它基于主内容，在“仅限广告”播放时，主内容为空</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>自定义广告策略</td> 
   <td> </td> 
   <td><p>· MP4广告和MP4内容不支持广告行为。</p> <p>· 13973:自定义广告行为 — 与MSE一起使用时，SKIP策略不会引发结束事件。</p> <p>· 14939:自定义广告行为策略跳过和跳过广告时间对短划线内容不起作用。</p> <p>· 17131:广告的第一帧可见，在“跳过”广告时间策略的情况下，内容会继续。</p> </td> 
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
   <td><p>· VPAID广告不支持广告行为。</p> <p>· 15032:不支持在广告时间将VPAID广告与MP4或HLS广告结合使用。</p> <p>· 19001:在Android和iOS上，当以MP4作为主内容播放VPAID广告时，可以听到双音轨、主内容之一和广告之一。</p> <p>· 20762:画中画(PIP)不支持VPAID广告。</p> <p>· 21172:未收到包含VPAID广告的HLS VOD内容的播放结束事件。</p> <p>· 21173:未收到HLS VOD内容和后置VPAID广告的onAdBreakCompleteEvent。</p> </td> 
   <td>在VPAID广告和主内容之间切换时，播放器在正常模式和全屏模式之间切换。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表21:集成**

| **内容类型** | **功能** | **Flash** | **HTML5（在Firefox、IE、Chrome、Android Chrome中）** | **HTML5(位于Safari、iOS Safari中)** | **Chromecast（仅短划线播放）** |
|---|---|---|---|---|---|
| VOD +实时 | Adobe Analytics VHL集成 |  | 19004:无法通过UI配置器工具进行Video Analytics跟踪。 |  |  |

## 有用资源 {#helpful-resources}

* 请参阅以下完整帮助文档： [Adobe Primetime学习与支持](https://experienceleague.adobe.com/docs/primetime.html) 页面。

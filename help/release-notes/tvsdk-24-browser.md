---
title: 浏览器TVSDK 2.4发行说明
description: 浏览器TVSDK 2.4发行说明描述了浏览器TVSDK 2.4中新增、支持和不支持的功能以及已知问题。
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '6812'
ht-degree: 0%

---


# 浏览器TVSDK 2.4发行说明{#browser-tvsdk-release-notes}

浏览器TVSDK 2.4发行说明描述了浏览器TVSDK 2.4中新增、支持和不支持的功能以及已知问题。

## 简介{#introduction}

浏览器TVSDK是一个工具包，允许您向基于浏览器的视频播放器应用程序添加高级视频播放功能、内容保护和广告。

浏览器TVSDK 2.4提供JavaScript API以构建基于浏览器的视频应用程序，并包括以下模式的回放支持：

* 仅HTML5
* 具有自动闪存回退的HTML5
* Flash始终

此版本包含以下信息：

· [浏览器TVSDK API文档](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)。

· [浏览器TVSDK编程指南](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf)。

· [TVSDK for 1.4 DHLS到浏览器TVSDK 2.4迁移指南](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html)。

· [从浏览器TVSDK 2.4.6转换为版本2.4.7](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html)。

·包含在构建中的参考实施。

>[!NOTE]
>
>*有关此版本的安全注意事项的完整列表，请参阅安全注意事项。

## 新增功能和支持的功能{#what-s-new-and-supported-features}

此版本的浏览器TVSDK提供了可用于增强视频应用程序的新功能。

**2.4.12更新（内部版本204）中的新增功能**

以下新增功能可作为浏览器TVSDK 2.4.12更新（内部版本204）的一部分提供：

* AdobePSDK.MediaPlayer的卷API的实现已更改，以允许在静音播放时在iOS上自动播放。

·新增了一个API，`auditudeSettings.ignoreVPAIDAds`，以允许忽略从Auditude服务器接收的VPAID广告。 API不适用于Flash回退。

**版本2.4.11**

以下增强和新增功能可作为浏览器TVSDK 2.4.11版本的一部分提供：

· MSE和Flash回退模式支持HLS实时区段故障转移。

·现在，`AuditudeSettings.creativeRepackagingDomain` API也支持MSE。 以前仅支持Flash回退模式。

·该版本包含针对关键客户问题的修复。 请参阅&#x200B;*已修复的问题*&#x200B;列表。

**版本2.4.10**

以下增强和新增功能可作为浏览器TVSDK 2.4.10版本的一部分提供：

· TVSDK提供enableLogging()以启用或禁用日志记录。 有关用法，请参阅[API文档](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)。

·使用Adobe Analytics时，TVSDK不再支持默认章节。 使用应用程序定义和管理章节。

·该版本包含针对关键客户问题的修复。 请参阅*问题已修复*列表。

**版本2.4.9**

以下增强和新增功能可作为浏览器TVSDK 2.4.9版本的一部分提供：

·支持具有时间不连续但没有间断标记的HLS VOD和实时流。

· HLS VOD和实时流的Safari视频标记支持ID3 v2.4.0帧。

·安全广告加载实施可确保广告服务器调用升级为基于API配置的安全HTTP。 有关详细信息，请参阅AdobePSDK.AdvertisingMetadata和AdobePSDK.ForceHttpsAdConfiguration类。 此功能在Flash回退模式中不受支持。

·与VAST 3.0响应相关的广告ID信息和扩展信息现在由TVSDK提供给应用程序，并可用于实施Moat集成以进行广告测量。 有关详细信息，请参阅AdobePSDK.NetworkAdInfo API。 在Flash回退模式中不支持此功能。

· AdobePSDK.ForceHttpsConfiguration类已不可用。 它成功

AdobePSDK.ForceHttpsAdConfiguration类。

·现在有新的API AdobePSDK.optimizeFlashCalls可用于优化调用以改善Flash回退模式下的HLS回放体验。 默认情况下，此选项处于禁用状态。

**2.4.8更新（内部版本6002）中的新增功能**

此更新包含针对关键客户问题的修复。 有关列表，请参阅&#x200B;*已修复问题*。

**版本2.4.8**

以下增强和新增功能可作为Browser TVSDK 2.4.8版本的一部分提供：

· SDK现在符合Chrome EME，并且从Chrome v58开始提供的最佳做法更改。 有关详细信息，请参阅[https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

· UI框架现在在Flash、仅限广告和定位信息工作流上支持HLS访问DRM。

· setDRMAuthenticateData API已添加到UI框架。 要播放使用Adobe Access DRM保护的流，请调用此API。 也可以在播放器中指定drmAuthenticateData属性。 有关详细信息，请参阅[AdobePSDK.videoBehavior ](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)。

**版本2.4.7**

以下功能是版本2.4.7中的新增功能：

·在UI框架中添加UI配置器

您可以通过以下方式之一配置播放器：

·使用JSON对象

·使用API

为了帮助生成JSON对象，浏览器TVSDK提供了**UI Configurator **工具。

在此工具中，您可以选择各种设置，单击**测试配置**验证设置，然后单击**下载配置**下载设置。 下载文件后，您可以将此文件的内容作为JSON对象传递给ptp.videoPlayer API。

·向UI框架添加MediaPlayerItemConfig API

可以通过MediaPlayerItemConfig配置各种功能，包括advertisingMetadata、advertisingFactory、adSigningMode、networkConfiguration、customRangeMetadata、useHardwareDecoder、subscriber、thumbnailScrubber、billingMetricsConfig。 有关详细信息，请参阅[浏览器TVSDK API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* * [文档](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)中的AdobePSDK.MediaPlayerItemConfig文档。

在UI框架中，已修改通过播放器配置传递网络配置的方式。

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

* 在UI框架中支持DRM和分析工作流

可通过UI框架启用DRM配置和分析跟踪。

* 添加了`AdobePSDK.embedSWFinFullScreenDiv` API

此新API为播放器应用程序提供了灵活性，用于选择可嵌入FlashFallback.swf文件的div。

* 已将`AdobePSDK.MediaPlayer`类中的`getVersion` API替换为`AdobePSDK.Version`类，以获取与TVSDK版本相关的信息。 有关详细信息，请参阅`AdobePSDK.Version` API [此处](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html)。

**版本2.4.6**

以下功能是版本2.4.6中的新增功能：

* **浏览证支持**

Browserify允许您在浏览器中使用node.js样式模块。 您可以定义依赖项和Browserify将所有内容捆绑到一个JavaScript文件中。

* **帐单**

借助账单，浏览器TVSDK可收集播放器使用量度以向Primetime客户收费。

>[!NOTE]
>
>版本2.4.6中已删除枚举PSDKErrorCode中已弃用的枚举MediaPlayer.事件和已弃用的常量。有关详细信息，请参阅[从浏览器TVSDK 2.4.5转换为版本2.4.6](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html)。

**版本2.4.5**

以下功能是版本2.4.5中的新增功能：

* **完整事件重放和广告**

   HLS完整事件重放(FER)流现在支持广告分辨率和广告行为。 要启用此支持，请在创建`MediaPlayerItemConfig`对象时将ad信令模式设置为`MANIFEST_CUES`。

* **MediaplayerView ScalePolicy支持**

   应用程序开发人员现在可以使用MediaplayerView scalePolicy属性为视图指定不同的scalePolicy。

* **变形内容支持**

   现在，使用MSE和Flash播放时支持变形内容播放。

* **选择性应用`withCredentials`**

将`withCredentials`设置为true时，不能将`Access-Control-Allow-Origin`标头设置为通配符。 根据服务器的响应，浏览器TVSDK将有选择地设置`withCredentials`属性。 有关此支持的详细信息，请参阅[浏览器TVSDK API文档](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)。

**版本2.4.4**

以下功能是版本2.4.4中的新增功能：

* **Chromecast范例应用程序**

此版本为发送方和接收方应用程序提供支持，这些应用程序演示了通过客户端和插入播放DASH VOD流和DASH Widevine流。

* **高级故障转移支持**

此版本包含对HLS VOD流的高级故障切换用例（段和服务器故障切换）的支持。

**版本2.4.3**

以下功能是版本2.4.3中的新增功能：

* **虚线VOD的自定义标签**

   可以将内联自定义标记(事件)订阅并作为TimedMetadata对象接收。

* **无扩展的流播放**

   现在支持不扩展的HLS和DASH流。 对于清单文件，加载资源时需要指定resourceType。 对于段和VTT文件，Content-Type响应标头用于确定内容类型。

**版本2.4.2**

以下功能是版本2.4.2中的新增功能：

* **API奇偶校验**

有关API奇偶校验的完整列表，请参阅[TVSDK for 1.4 DHLS至Browser TVSDK 2.4迁移指南](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html)。

* **Sample-AES支持**

   此版本增加了对MSE和Flash回退时Sample-AES加密内容回放的支持。 在Google Chrome上通过安全来源托管AES内容的要求已被删除。

* **支持AAC容器**

   现在支持播放扩展名为.aac的文件。 这可以是纯音频流或替代音频。

   >[!NOTE]
   >
   >尚不支持AC3和增强的AC3编解码器。

* **标记化流播放**

通过内容投放网络(CDN)交付的HLS流有时可以在清单和区段请求上使用身份验证令牌进行验证，这些令牌可以作为URL参数或Cookie头提供。 现在支持播放此类流。

**版本2.4.1**

以下功能是版本2.4.1中的新增功能：

* **UI框架**

此框架旨在加快基于JavaScript的视频播放器应用程序的UI开发，它包含API，用于包括播放/暂停和音量等基本控件以及轻松添加或删除诸如划动栏状态和隐藏字幕设置等元素。 您可以指定与控件关联的行为、创建自定义控件以及为播放器UI设置外观。 这一切都通过框架实现，无需直接操作DOM结构。

* **实时流的HLS播放增强**

此版本支持广告插入引起的不连续。 它使用EXT-项目-DATE-TIME标签后跟EXT-MEDIA-SEQUENCE标签来跨自适应比特率用户档案进行同步，以实现顺畅回放。

* **VPAID 2.0支持**

视频播放器广告服务界面定义(VPAID)2.0版为用户提供了丰富的媒体体验，使出版商能够更好地目标广告、跟踪广告印象并从视频内容受益。 此版本支持视频点播(VOD)内容的线性JavaScript VPAID广告。

* **自定义HLS标记**

媒体流可以以播放列表/清单文件中的标记形式携带其他元数据。 浏览器TVSDK允许您指定和订阅其他标记，并在清单中显示这些标记时通知您。

* **播放器时间轴上显示的广告标记**

此版本支持在VOD和实时内容的播放器时间轴上显示广告标记。 您可以在引用播放器中看到此行为。

**2.4中支持**

版本2.4中提供以下功能：

* **MP3音频回放**

   此版本支持在具有媒体源扩展(MSE)和Safari视频标记的浏览器上播放MP3音频。

* **MP4视频播放**

   支持以下功能：

   * 单流播放
   * 具有广告行为和跟踪功能的前置和后置MP4广告
   * 具有广告行为和跟踪功能的卷前和卷后HLS广告
   * 具有广告行为和跟踪功能的前放和后放DASH广告

## 支持的平台{#supported-platforms}

浏览器TVSDK对其需要运行的平台和软件级别有特定要求。 支持以下平台和软件级别：

### 桌面配置{#desktop-configurations}

* Microsoft Windows 7:

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft Windows 8.1

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft Windows 10

   * Edge+

* Apple OS X

   * Safari 9+
   * Chrome 33+
   * Firefox 38+

### 移动Web配置{#mobile-web-configurations}

* Android 4.4

   * 本机浏览器
   * Chrome 33+

* Android 5.0

   * 本机浏览器
   * Chrome 33+

* Android 6.0

   * · Chrome 33+

* Apple iOS 9

   * Safari 9+
   * Chrome 33+

* Apple iOS 10

   * Safari 9+
   * Chrome 33+

**Google Chromecast(第二代；（仅限DASH播放）**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>技术</strong> </p> </td> 
   <td><p><strong>浏览器TVSDK视频标</strong><sup>签1</sup></p> </td> 
   <td><p><strong>浏览器TVSDK MSE</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>默认技术</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>iOS</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>-</p> </td> 
   <td><p>视频标签</p> </td> 
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
   <td><p>视频标签</p> </td> 
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

## 功能矩阵{#feature-matrix}

以下列表了此版本的受支持和不受支持的功能：

* *MP3音频功能 — 核心回放*
* *MP4视频功能 — 核心播放*
* *MP4视频功能 — 核心Ad Insertion*

>[!NOTE]
>
>*在以下功能矩阵表中，“Y”表示当前版本中支持该功能。*

### MP3音频功能{#mp-audio-features}

**表1:核心播放{#table-core-playback}**

| 类别 | 内容类型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 播放 | MP3 VOD | 常规播放（播放、暂停、搜索） | 不支持 | Y | Y |

1浏览器TVSDK视频标签不支持流和DRM。 编解码器和容器支持在所有浏览器上不同。

2 Firefox默认为41版或更早版本的Flash Player。

### MP4音频功能{#mp-audio-features-1}

**表2:核心播放**

| 类别 | 内容类型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 播放 | MP4 VOD | 常规播放（播放、暂停、搜索） | 不支持 | Y | Y |

**表3:核心Ad Insertion**

| 类别 | 内容类型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | MP4 VOD | 前置(MP4) | 不支持 | Y | Y |
| Ad Insertion | MP4 VOD | 后置(MP4) | 不支持 | Y | Y |

有关HLS或DASH功能支持的详细信息，请参见下文。

## HLS功能矩阵{#hls-feature-matrix}

以下是浏览器TVSDK中HLS功能的功能列表。

* *HLS核心播放*
* *HLS高级回放功能*
* *HLS内容保护功能*
* *HLS核心广告插入功能*
* *HLS高级广告插入功能*
* *HLS集成*

>[!NOTE]
>
>*在以下功能矩阵表中，“Y”表示当前版本中支持该功能。*

### HLS功能{#hls-features}

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
   <td><p>常规播放（播放、暂停、搜索）</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>常规播放（播放、暂停和搜索）</p> </td> 
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
   <td><p>高级故障转移</p> </td> 
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
   <td><p>支持Cookie头</p> </td> 
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

**表5:HLS高级回放功能**

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
   <td><p>偏移时回放</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>纯音频回放</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Trick Play</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>流畅的技巧播放</p> </td> 
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
   <td><p>标记流</p> </td> 
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
   <td><p>不支持</p> </td> 
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
   <td><p>预卷(MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>中间卷(HLS)</p> </td> 
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
   <td><p>配套广告、横幅广告、可点击广告</p> </td> 
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

## 虚线功能矩阵{#dash-feature-matrix}

以下是浏览器TVSDK中DASH功能的功能表。

· *DASH核心播放功能*

· *虚线高级播放功能*

· *虚线内容保护功能*

· *虚线核心广告插入功能*

· *DASH高级广告插入功能*

· *DASH集成*

>[!NOTE]
>
>在以下功能矩阵表中，Y表示当前版本中支持该功能。

### 虚线功能{#dash-features}

支持以下功能：

**表10:DASH核心播放功能**

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
   <td><p>常规播放（播放、暂停、搜索）</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>常规播放（播放、暂停和搜索）</p> </td> 
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
   <td><p>支持Cookie头</p> </td> 
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
   <td><p>设置自适应比特率控件</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>自定义标记(EventStream)</p> </td> 
   <td><p>仅VOD（内联）</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>延迟音频</p> </td> 
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

**表11:DASH高级回放功能**

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
   <td><p>偏移时回放</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>纯音频回放</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>戏法</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>流畅的技巧播放</p> </td> 
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
   <td><p>多期支持</p> </td> 
   <td><p>仅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>标记流</p> </td> 
   <td><p>不支持</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>帐单</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**表12:DASH内容保护功能**

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
   <td><p>·在Chrome、Firefox 47及更高版本和Chromecast上使用Widevine</p> <p>·在Windows 8.1和Edge上的Internet Explorer上播放就绪</p> <p>·适用于Windows Firefox的Primetime DRM（仅视频）</p> </td> 
  </tr> 
 </tbody> 
</table>

**表13:DASH核心广告插入功能**

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
   <td><p>前滚(MP4/DASH)</p> </td> 
   <td><p>仅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +实时</p> </td> 
   <td><p>中角（短划线）</p> </td> 
   <td><p>仅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>滚动后(MP4/DASH)</p> </td> 
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
   <td><p>创意重新打包（MP4到破折）</p> </td> 
   <td><p>不支持</p> </td> 
  </tr> 
 </tbody> 
</table>

**表14:虚线高级广告插入功能**

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
   <td><p>配套广告、横幅广告、可点击广告</p> </td> 
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

## 修复了{#issues-fixed}的问题

**2.4.12更新（内部版本204）中修复的问题**

以下问题已在浏览器TVSDK版本2.4.12更新（内部版本204）中修复：

· **21647** — 当音频静音时，TVSDK应允许在iOS设备上自动播放视频。

· **21465** — 播放DASH实时流后播放受DRM保护的DASH流时，收到错误密钥系统访问拒绝。

· **21442** — 使用用户手势播放预卷广告后，在iOS Web上启用内容自动播放。

· **21240** — 提供的API用于过滤从Auditude/VMAP分析的VPAID广告。

**版本2.4.11中修复的问题**

以下问题已在浏览器TVSDK版本2.4.11中修复：

**核心播放功能：**

· **19192**:TVSDK现在实现TextFormat:bottomInset和TextFormat:safeArea。 由于这些增强功能，如果控件栏显示在屏幕上，则可以重新放置隐藏式字幕。

· **21009**:隐藏式字幕在出现新字幕前跨中断搜索时会保留在屏幕上。

· **21141**:在段追加期间，由于竞争条件，搜索返回被拒绝。

· **21142**:使可搜索的播放范围在播放器处于INITIALIZED状态时可用。 由于这些更改，现在支持在位开始会话。

· **21363**:在DASH流的广告插入后，608/708隐藏式字幕会失去同步。

**广告插入功能：**

· **21179**:现在，通过正确设置ad.primaryAsset.adParameters属性，解决了VOD内容的中间卷相关问题（长暂停、黑帧）。

· **21257**:如果MP4不是有效的mime类型，并且启用了创意重新打包功能，则会选择比特率最高的MP4文件进行转码。

· **21361**:TVSDK现在将广告系统和创意ID作为创意包装请求中的查询参数从VAST响应中传递，以支持其他规范化规则。

**版本2.4.10中修复的问题**

以下问题已在浏览器TVSDK版本2.4.10中修复：

**核心播放功能：**

· **21060**:HLS流引发的编解码器错误无效，该流包含中断，ISO BMFF框运行到流的末尾。

· **21045**:在播放列表中的第一个视频播放完成后，自动播放在iOS上不工作。

· **20975**:Chrome浏览器上的QoS提供商将帧速率返回为NaN。

· **20823**:遇到没有数据的段时引发不受支持的编解码器错误。

· **20769**:SDK现在使用当前位速率进行搜索，而不是基于ABR策略立即切换。

· **20031**:在IE11(Windows 8.1)上以纵向模式时，视频屏幕变小。 内容保护功能：

· **19316**:在HLS AES-128流中，跳过解密失败的段。

**版本2.4.9中修复的问题**

以下问题已在浏览器TVSDK版本2.4.9中修复：

**核心播放功能：**

· **13407**:如果Firefox在播放过程中停止发送“ontimeupdate”事件,DASH流可能会停止。

· **16380**:在通过MSE对具有不匹配开始时间的段进行混音内容播放期间，ABR交换机上会累积表示之间的音频同步错误，最终导致错误(Chromium问题#663686)。

· **17985**:在Firefox浏览器上播放特定ISO-BMFF流时，播放会卡住(Firefox问题#1342913)。 自Firefox v53起，此问题已修复。

· **19141**:未捕获（在承诺中）ReferenceError:宽度未定义。

· **18997, 19299**:段边界处的视频闪烁问题。 这是因为SDK未正确计算上一个范例的合成时间偏移。

· **19780**:播放不开始Firefox v53(Firefox问题#354653)上的HLS内容和HLS广告。

· **20046**:项目日期时间作为定时元数据对象接收时，将作为键而不是值接收。

· **20047**:useDefaultResizeHandler引发错误，返回Flash。

· **20179**:Flash回退无法与Flash Player v25.0.0.171一起使用。

· **20293**:Firefox会停止某些HLS流的缓冲数据，导致数据停止。

· **20626**:Player在Chrome上引发媒体解码错误，因为对零持续时间的视频样本的处理不正确。

· **20078**:浏览器错误“QuotaExceeded”上的播放暂停。

· **18639**:在HLS实时流608 CC文本中，有时显示拼写错误。

· **20028**:ClosedCaptions size参数不会更改字体大小。

· **20613**:隐藏式字幕框彼此重叠，无法辨认。

**核心Ad Insertion(CSAI)功能：**

· **20043**:具有多个广告和第三方重定向的广告印象和广告跟踪呼叫丢失。

· **20044**:使用创意重新打包时，广告中断中的所有广告都需要成功重新打包，否则广告中断将被完全放弃。

· **20097**:将跳过广告播放，并立即恢复主内容，而不是等待20秒的超时（如果广告清单不可用）。

**版本2.4.8更新（内部版本6002）中修复的问题**

以下问题已在浏览器TVSDK版本2.4.8更新（内部版本6002）中修复：

· **14126:**&#x200B;由于MSE源缓冲区的内部间隙，在Firefox上播放可能会停止(问题#1316024)。 尝试搜索以恢复播放

· **19608:**&#x200B;修复了对Auditude VMAP响应中的时间偏移值的保留。

· **19635:**&#x200B;在Windows 10上的Internet Explorer 11中修复视频停滞。

· **19761:**&#x200B;对HLS的ABR问题的修复。

· **19780:**&#x200B;修复了Mozilla Firefox v53中断的HLS内容的广告播放。

· **19877和19744:**&#x200B;这些问题修复了在搜索操作后选择比特率时的不一致性。 现在，搜索时的比特率选择是当前比特率和开始时的比特率的较低值。

· **19881:**&#x200B;执行3-4次搜索后，播放卡住和缓冲叠加将无限显示。

· **19884:**&#x200B;确认符合Chrome 59测试版验证媒体路径(VMP)要求。 bTVSDK能够用Chrome 59测试版播放Widevine DRM内容。

· **19916:**&#x200B;在UI-Framework上播放的DRM已中断。 现在，它调用acquireLicense，即使元数据中没有策略也是如此。

**版本2.4.8中修复的问题**

以下问题在浏览器TVSDK 2.4.8版中已修复：

· **10075**:在时间线之前搜索时，未在Firefox和Chrome上接收到播放完整事件，在Firefox上未收到搜索事件。

· **15775**:在Windows 8.1 Internet Explorer上未收到播放完整事件。

· **17306**:对于SSAI流，支持播放。 不支持拼接广告的跟踪。

· **19142**:有时，倒带会使视频播放器永远保持缓冲状态。

· **19218**:广告标记无法通过UI框架使用。

· **19219**:仅广告播放无法通过UI框架进行。

· **19222**:对播放列表请求一次AES-128密钥，并从缓存中提供后续请求。 之前，每个区段都会被请求。

· **19597**:&quot;未捕获的TypeError:无法读取未定义的属性“log””。

· **19605**:adRequestDomain在Flash回退模式下不可用。

· **19608**:未为HLS直播流插入VMAP广告。 SDK现在考虑提示标记，并且不依赖VMAP响应中的时间偏移值。

· **19637**:广告播放在广告结束时会导致脚本错误。

· **19732**:CRS播放列表请求失败，出现404错误。 浏览器TVSDK的1401和1403请求现已更新以处理。

· **19762**:acquireLicense在setAuthenticationToken之前调用，因为无论令牌有效性如何，都返回了有效许可证。 此问题现已修复，仅在setAuthenticationToken响应后调用acquireLicense。

**版本2.4.7中修复的问题**

版本2.4.7中修复了以下问题：

· **8397**:如果区段不与关键帧开始，则通过Adobe Medium服务器生成的HLS实时流可能无法播放。

· **13606**:修复了Chrome浏览器上HLS流的多个搜索相关问题。

· **14807**:在Chrome浏览器上，如果在play()后立即触发搜索或暂停，则播放可能会停止，并出现错误DOMException:play()请求被调用中断……(《铬》第593273期)。

· **19085**:MediaPlayer参数（如volume、abrControlParameters和ccStyle）未设置为“重置播放器时的默认值”。

**版本2.4.6中修复的问题**

版本2.4.6中修复了以下问题：

· **18093**:在“Flash Player回退”模式下使用Flash版本24时，将返回订阅标记旁边标记的TimedMetadata。

**版本2.4.4中修复的问题**

版本2.4.4中修复了以下问题：

· **8711**:对于MSE，默认情况下保留608/708字幕对齐。

· **13934**:播放HLS直播流时，不适用广告的ABR设置。

· **14079**:低DVR窗口的HLS实时流的寿命可能会失败，因为由于网络延迟问题，播放可能落后。 单击实时点以继续播放。

· **15037**:播放器UI框架附带的示例在Windows 7上的Microsoft Internet Explorer 10上不工作。

· **15913**:对于HLS VOD流，在Chrome上，如果清单响应为304且未修改，则流将不会播放。 此问题自Chrome v55以来已修复(Chromium问题633696)。

· **16103**:在Android Chrome上，在低带宽条件下，播放可能会因未捕获的TypeError而停止：无法读取未定义错误的属性“programDateTime”。

· **16265**:对于HLS VOD和实时流，跨间断搜索不起作用。

· **16709**:使用PDT和中断标记恢复HLS实时流可能会导致播放器在缓冲中卡住。

## 已知问题和限制{#known-issues-and-limitations}

下面提到了Browser TVSDK中的限制和已知问题。

**表16:核心播放功能**

<table> 
 <tbody> 
  <tr> 
   <td><strong>内容类型</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox中的HTML5、IE、Chrome、Android Chrome</strong></td> 
   <td><strong>Safari中的HTML5、iOS Safari</strong></td> 
   <td><strong>Chromecast（仅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>常规播放（播放、暂停、搜索）</td> 
   <td><p>·不支持HLS以外的媒体格式。</p> <p>8799:Flash回退不会处理混合内容，因此需要确保内容、广告和其他URL不会导致混合内容（安全内容和不安全内容一起）。</p> <p>· 19271:在Flash回退模式下，不支持通过UI框架进行多视图回放。</p> <p>·Flash回退在Windows 7上的Microsoft Internet Explorer 8和9上无效，因为SDK不支持这些版本。</p> <p>· 20262:Flash回退将自定义参数添加到定位信息列表。 同时，在Flash和MSE情况下，自定义参数的优先级顺序也不同。</p> <p>· 20653：浏览器TVSDKFlash回退在Win10上与Creators Update无效。</p> <p>· Flash Fallback可与Flash Player版本23及更高版本一起使用。</p> <p>· 20087 - Chrome 59 Beta，带</p> <p>Flash 25.0.0.171</p> <p>测试版（默认），HLS播放在Flash回退模式下不工作。 在加那利很管用。</p> </td> 
   <td><p>· 12563:由于MPD中不支持的音频编解码器字符串，带有音频编解码器mp4a.40.02的虚线流在Firefox上无法播放。 支持Audio Codec mp4a.40.2。</p> <p>15029:在UI-Framework中的multiView中切换视频时，播放/暂停按钮不会相应地更新。</p> <p>· 16034：在Windows 8.1 IE上，调用reset()会导致未知MIME类型错误。 请重新加载媒体以继续播放。</p> <p>· 18235:对于包含广告的DASH vod流，会发现某些搜索问题。</p> <p>· 18727:MSE不支持错误API</p> <p>18750:在某些情况下，SDK和UI框架的状态更改事件可能会失序，在UI框架中，加载资源后添加的事件监听器可能缺少IDLE和初始化状态更改事件。</p> <p>· 18889:如果MediaPlayer处于ERROR状态，则不返回视图对象。</p> <p>· 19039:如果是AdobePSDK。 MediaPlayer。 seekToLocal()的值大于EOF，然后在出现MSE时从头开始播放开始。</p> <p>· 19049:在播放视频时，当Flash Player被阻止时，Chrome、IE和Firefox上没有报告错误状态。</p> <p>· 17205:在音频继续播放的同时，视频播放在播放未经过混音的流时停止播放几个小时(Chromium问题# 664033)。</p> <p>· 12308:指定composition_time_offset的DASH流可能在Chrome浏览器上对其应用了timeStampOffset，导致负的解码时间，因此MEDIA_ERR_ SRC_NOT_SUPPORTED错误(Chromium期刊#398141)。</p> <p>· 14126:由于MSE源缓冲区中存在内部间隙，在Firefox上播放可能会停止(问题# 1316024)。 尝试搜索以恢复播放。</p> <p>· 19115:MS Edge和IE 11（Win 8.1和10）未在CORS重定向时将来源设置为null，但失败，因为标头不是null，导致播放错误。</p> <p>· 19861：在已播放的媒体的源缓冲区上附加行为的问题。 Chrome拒绝附加的片段，包括moov，导致后续解码错误。 (《铬》 #735335)</p> <p>19921:某些HLS内容的播放停止，即使已成功缓冲(Chromium问题#713540)</p> <p>· 20444：在IE和Edge上寻找缓冲范围的结尾可能导致播放停止。</p> <p>· 20511:有时，可以观察有无广告的HLS流的搜索拒绝。</p> <p>· 20743:在Windows 10 Chrome上，HLS实时流在MP4前滚播放前播放几秒钟。</p> <p>· 21043:由于缺少元数据，在初始加载时视频尺寸可能不正确。</p> <p>· 21115:如果播放列表中的视频提供了前置广告，则开始播放需要Android用户手势。</p> <p>· HLS Live不支持时间戳滚动。</p> <p>·不支持AAC-SSR音频。</p> <p>不支持音频编解码器AC3和增强的AC3。</p> <p>·对于具有时间戳间断但没有间断标记的流</p> <p>·由于跳转，播放可能出现故障和搜索不正确。</p> <p>·内容持续时间和播放持续时间可能不匹配。</p> <p>·表示形式和再现之间的不连续性应该与其他形式相同，这可能导致同步和停滞问题。</p> <p>·字幕和WebVTT可能不会在流末尾附近显示。</p> <p>·不支持跨时间戳跳转的音频编解码器更改。</p> <p>·不支持广告插入。</p> <p>·快进特技模式可能导致Win 8.1 IE 11上的回放循环(MS问题#12446268)。</p> <p>虚线：</p> <p>·对于实时流 — 支持动态类型的实时用户档案。</p> <p>·对于VoD流 — 支持静态类型的实时用户档案。</p> <p>对于VoD流 — 点播用户档案未针对广告工作流进行认证。</p> </td> 
   <td><p>·不支持DASH Live和DASH视频点播流。</p> <p>·在全屏模式下，iOS不支持PIP（画中画）视频回放。</p> <p>在Safari（视频标记）扩展上，如果没有正确的内容类型标题，则无法使用较少清单。</p> </td> 
   <td><p>·发送者应用程序中的applicationID需要与将接收者的URL注册为自定义接收者应用程序时生成的ID相同。</p> <p>·参考播放器经认证可用于DASH工作流。 UI框架未经过认证。</p> <p>有关受支持媒体编解码器的列表，请参阅<a href="https://developers.google.com/cast/docs/media"><em>此处</em></a>。</p> </td> 
  </tr> 
  <tr> 
   <td>FER VOD</td> 
   <td>常规播放（播放、暂停、搜索）</td> 
   <td> </td> 
   <td>18098:在HLS LBA FER流中观察到某些搜索问题。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>自适应比特率</td> 
   <td><p>· 20079:在缓冲范围内的搜索时重写缓冲区。</p> <p>20080:Flash ABR行为与MSE一致。</p> </td> 
   <td><p>·由于缓冲区相关限制，ABR流中的仅音频回退变体被忽略。</p> <p>· 12289:在未混合HLS/DASH流的情况下，ABR控制参数不应用音频。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>608/708字幕</td> 
   <td> </td> 
   <td><p>· 7810:在Android 4.4.4上，Chrome似乎不支持播放器使用的基本CSS字体系列，因此字体样式更改功能无效。</p> <p>·对于608个字幕，无法更改CC渠道。</p> <p>· 608个字幕不支持高级样式功能。</p> <p>支持通过“辅助功能”标签发出信号的嵌入式字幕(608/708)。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>· 5206:播放器在显示字幕时会忽略WebVTT文件中的区域标签。</p> <p>·短划线：不支持分段/分段VTT文件。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>清单故障转移</td> 
   <td>21056:使用Flash回退，如果主流在播放过程中返回404错误，则不会对实时流执行故障转移。</td> 
   <td>清单故障转移仅适用于内容，而不适用于广告。</td> 
   <td>缺少的播放列表故障转移仅对HTTP错误代码404在Safari上工作。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>高级故障转移</td> 
   <td> </td> 
   <td><p>·区段故障转移不支持跳过不可用的区段并继续播放。</p> <p>20533:播放列表中缺少的区段应被视为“中断”，并且应从下一个可用区段恢复播放。</p> <p>21267:由于故障转移而导致的流切换可能会导致下载旧段。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>QoS和播放器通知</td> 
   <td>21129:帧速率在“Flash回退”情况下不可用。</td> 
   <td><p>· 11170:</p> <p>Timed_事件不适用于MSE的浏览器TVSDK，而不适用于具有Flash回退的浏览器TVSDK。</p> <p>21129:不计算实时流的帧速率。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>支持Cookie头</td> 
   <td> </td> 
   <td> </td> 
   <td><p>withCredentials标志和cookie头在Safari上不受支持。</p> <p>21051:要在Safari中允许Cookie，请启用“首选项”&gt;“隐私”中的“Cookie和网站数据”设置。</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>自定义标记</td> 
   <td>14763:不应支持以#开头的自定义标记。 现在，在Flash回退期间为此类标记创建并报告TimedMetadata对象。</td> 
   <td>带带内自定义标记的流未经过认证。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>延迟绑定音频</td> 
   <td> </td> 
   <td><p>· HLS直播LBA流不支持广告插入。</p> <p>· 17273:在故障转移时，HLS VOD LBA流切换到默认再现，无法切换回上次选择的播放。</p> <p>· 20251:HLS实时LBA流可能在搜索时停止。</p> <p>· 20497:如果HLS LBA未混合流在流末尾附近缺少音频或视频帧，则播放器仍处于缓冲状态。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>302重定向</td> 
   <td> </td> 
   <td><p>15787:302</p> <p>windows Edge和IE浏览器不支持重定向优化，因为它们不支持XMLHttpRequest对象中的responseURL属性。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表17:高级回放功能**

<table> 
 <tbody> 
  <tr> 
   <td>内容类型</td> 
   <td>功能</td> 
   <td>Flash</td> 
   <td><strong>Firefox中的HTML5、IE、Chrome、Android Chrome</strong></td> 
   <td><strong>Safari中的HTML5、iOS Safari</strong></td> 
   <td><strong>Chromecast（仅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>偏移时回放</td> 
   <td><p>不支持以特定偏移值开始播放的MP4内容。</p> </td> 
   <td>20492:在从偏移值恢复内容之前播放偏移之前的中间广告。</td> 
   <td>iOS上不支持使用偏移功能播放。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Trick Play</td> 
   <td>“平滑滴播”不适用于没有iFrame再现的流。</td> 
   <td><p>· Firefox和Internet Explorer不支持“特技播放”调整，因此这些浏览器不提供“反向特技模式”。</p> <p>·在播放内容和广告时，不提供特技播放。</p> <p>· 10435:在DASH播放期间，视频在Internet Explorer上的前向特技播放时冻结(Win 8.1)</p> <p>间歇性。 这是因为我们使用了视频元素playbackRate属性，而没有特技播放调整。</p> <p>14182:有时，在Chrome浏览器上倒回时，可能无法接收搜索事件，因此技巧模式将无法工作。</p> <p>· 14942:即使在非特技播放流的情况下，也可以在Android的Chrome上设置播放速率，但将不应用设置，且播放将以正常速率继续。</p> <p>· 17308:在Trickplay模式下，搜索不起作用。</p> <p>· 17309:在Chrome浏览器上，反向技巧模式不能持续超过2秒。</p> <p>19272:在DASH流的情况下，技巧播放可能无法从Windows 10 Edge浏览器上的缓冲中恢复。</p> </td> 
   <td>不支持倒带技巧模式。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>ID3解析</td> 
   <td>20346:SDK还应返回ID3帧的文本编码字节。</td> 
   <td><p>SDK会忽略音频数据传输流(ADTS)中可用的ID3标记。</p> <p>· 12378:ID3定时元数据在Flash和浏览器上的不同时间进行分析，具有MSE支持，因此引用播放器时间轴上的显示行为也不同。</p> <p>· 19247:UI框架不支持ID3分析。</p> </td> 
   <td><p>· 20323:Safari未分析用于信号aac段第一个样本时间戳的PRIV ID3标记(Safari问题#32422733)</p> <p>· 20350:在某些设备（包括MAC OS X 10.1、iPad10）上，Safari在特技模式下时不提供提示更改事件，因此未收到ID3帧。 (Safari问题#32450526)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>间断标记支持</td> 
   <td> </td> 
   <td><p>·包含中断的HLS流不支持客户端广告插入。</p> <p>·不允许跨HLS流中的不连续性更改音频编解码器。</p> <p>·具有不连续标记的HLS流不支持音频轨道开关</p> </td> 
   <td>不连续序列号是在Safari上播放具有不连续性的HLS流的一个要求。</td> 
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
   <td><strong>Firefox中的HTML5、IE、Chrome、Android Chrome</strong></td> 
   <td><strong>Safari中的HTML5、iOS Safari</strong></td> 
   <td><strong>Chromecast（仅限DASH播放）</strong></td> 
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
   <td><p>· 12660:HTML5播放器会为过期的PlayReady加密虚线内容引发内部服务器错误。</p> <p>· 16720:如果缺少句点标签中的开始属性，则DASH DRM加密的内容将不起作用。</p> <p>· 18589:DRM保护的带Xlink的虚线VoD多时段流不支持播放。</p> <p>· 18653:使用多键的Widevine MultiPeriod内容的播放在第一个时段停止，无法切换到下一个时段。</p> <p>· 18656:Playready MultiPeriod流（使用不同密钥加密）无法播放。</p> <p>Playready 2.0 for Dash未通过认证。</p> <p> </p> <p> </p> </td> 
   <td>12602:HLS Fairplay DRM元数据由Safari上的HTML5播放器重复刷新</td> 
   <td><p>可以播放通过Bento4打包的DASH Widevine DRM内容。 无法播放通过Offline Packager和Shaka Packager打包的内容。 不支持DASH PlayReady DRM。</p> </td> 
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
   <td><strong>Firefox中的HTML5、IE、Chrome、Android Chrome</strong></td> 
   <td><strong>Safari中的HTML5、iOS Safari</strong></td> 
   <td><strong>Chromecast（仅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>前/中/后</td> 
   <td> </td> 
   <td><p>·具有HLS实时内容的预卷广告以双播放器模式播放。</p> <p>·不支持包含HLS内容的虚线广告和包含虚线内容的HLS广告。</p> <p>· 19002:在HTML5播放器中，具有MSE adBreak。 insertionType不返回正确值以描述正确的插入类型，即插入客户端或插入服务器。</p> <p>7794:在默认控制栏以全屏模式显示的移动设备（iOS、带Chrome 33或更低版本的Android或原生浏览器）上，搜索栏和快进按钮在广告播放时可用。</p> <p>· 11048:在媒体源扩展的情况下，从广告切换到HLS Live内容不是流畅的。</p> <p>· 16083:在Android 4.4 Chrome v52上，有时HLS广告包含HLS内容可能导致在停止播放后出现管道解码错误。</p> <p>· 16097:未处理广告中断期间遇到的错误，可能导致主流停止播放。</p> <p>· 18095:HLS实时内容不支持MP4广告。</p> <p>19120:对HLS内容的HLS广告进行多次搜索可能导致流停止播放。</p> <p>· 19131:在从前滚广告中断切换到内容时，可能会显示缓冲叠加。</p> <p>· 20296:对于HLS直播流，在DVR窗口中搜索后再搜索已解析的中间卷可能会导致播放停滞。</p> <p>· 20298:HLS中间卷实时流在第一个中间卷广告移出DVR窗口时停止。</p> <p>· 20317:如果广告中断包含多个广告，则在切换到下一个广告或从广告切换到内容时，HLS直播流可能会停止。</p> 
    <ul> 
     <li>未解析HLS实时流的DVR窗口中的广告。</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>SDK不遵守VAST adSource的VMAP响应内的序列属性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>20779:SDK不遵守VAST adSource的VMAP响应中的序列属性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>VMAP 1.0</td> 
   <td> </td> 
   <td>12014:不支持VMAP repeat属性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>创意重新打包</td> 
   <td> </td> 
   <td>21464:如果广告中断中的一个广告的创意重新打包失败，则广告响应将完全放弃。</td> 
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
   <td><strong>Firefox中的HTML5、IE、Chrome、Android Chrome</strong></td> 
   <td><strong>Safari中的HTML5、iOS Safari</strong></td> 
   <td><strong>Chromecast（仅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>仅广告</td> 
   <td> </td> 
   <td>20056:播放器技术属性不相关，因为它基于主内容，在“仅广告”播放时该内容为空</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +实时</td> 
   <td>自定义广告策略</td> 
   <td> </td> 
   <td><p>· MP4广告和MP4内容不支持广告行为。</p> <p>· 13973:自定义广告行为 — 与MSE一起使用时，SKIP策略不会引发完整事件。</p> <p>· 14939:自定义广告行为策略跳过和跳过广告中断对DASH内容无效。</p> <p>· 17131:广告的第一帧可见，然后内容在出现SKIP广告中断策略时继续。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>配套广告/横幅广告/可点击广告</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>使用参考播放器时，横幅广告不可见。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>· VPAID广告不支持广告行为。</p> <p>· 15032:不支持广告中断中与MP4或HLS广告结合的VPAID广告。</p> <p>· 19001:在Android和iOS上，当VPAID广告以MP4为主内容播放时，多次音轨可以听见，声音是主内容之一，广告之一。</p> <p>· 20762:画中画(PIP)不支持VPAID广告。</p> <p>· 21172:未收到包含VPAID广告的HLS VOD内容的播放完整事件。</p> <p>· 21173:未为HLS VOD内容和VPAID广告接收onAdBreakCompleteEvent。</p> </td> 
   <td>在VPAID广告和主内容之间切换时，播放器在正常模式和全屏模式之间切换。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表21:集成**

| **内容类型** | **功能** | **Flash** | **Firefox中的HTML5、IE、Chrome、Android Chrome** | **Safari中的HTML5、iOS Safari** | **Chromecast（仅限DASH播放）** |
|---|---|---|---|---|---|
| VOD +实时 | Adobe Analytics VHL集成 |  | 19004:视频分析跟踪无法通过UI Configurator Tool提供。 |  |  |

## 有用资源{#helpful-resources}

* 请参阅[Adobe Primetime学习和支持](https://helpx.adobe.com/support/primetime.html)页面上的完整帮助文档。
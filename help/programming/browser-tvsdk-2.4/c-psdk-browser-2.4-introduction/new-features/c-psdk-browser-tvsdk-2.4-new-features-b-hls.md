---
description: 浏览器TVSDK支持许多HLS功能，您可以实施这些功能来向视频应用程序添加功能。
title: 支持的HLS功能
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---


# 支持的HLS功能{#supported-hls-features}

浏览器TVSDK支持许多HLS功能，您可以实施这些功能来向视频应用程序添加功能。

* [HLS核心播放](#hls-core-playback)
* [HLS高级回放功能](#hls-advanced-playback)
* [HLS内容保护功能](#hls-content-protection)
* [HLS核心广告插入功能](#hls-core-ad-insertion)
* [HLS高级广告插入功能](#hls-advanced-ad-insertion)
* [HLS集成](#hls-integrations)

>[!TIP]
>
>在以下功能矩阵表中，![支持的图标](assets/supported15.png)表示当前版本中支持该功能。

>[!TIP]
>
>在Safari列“平台限制”中，表示不支持该用例，因为该平台不允许实现对它的支持。 插入时，使用SSAI。 如果播放限制对您很重要，则强制回退到Safari上的Flash，直到平台支持广告插入用例。

<!--<a id="section_9FB9193D5763448CB228B96164661738"></a>-->

支持以下功能：

<!-- 

Removed Nielsen row 
<table id="table_D9E2D82992554905A0A551CC71AFA189"> 
 <title>HLS integrations</title> 
 <tgroup cols="6"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" /> 
  <colspec colnum="4" colname="col4" colwidth="*" /> 
  <colspec colnum="5" colname="col5" colwidth="*" /> 
  <colspec colnum="6" colname="col7" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col1" morerows="1" class="entry"> Category </th> 
    <th colname="col2" morerows="1" class="entry"> Content type </th> 
    <th colname="col3" morerows="1" class="entry"> Feature </th> 
    <th colname="col4" morerows="1" class="entry"> Flash </th> 
    <th namest="col5" nameend="col7" class="entry"> HTML5 </th> 
   </tr> 
   <tr> 
    <th colname="col5" class="entry"> FF, IE, Chrome, Android Chrome </th> 
    <th colname="col7" class="entry"> Safari, iOS Safari </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Adobe Analytics VHL integration </td> 
    <td colname="col4">![supported icon](assets/supported15.png) </td> 
    <td colname="col5">![supported icon](assets/supported15.png) </td> 
    <td colname="col7">![supported icon](assets/supported15.png) </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Nielsen support </td> 
    <td colname="col4">![supported icon](assets/supported15.png) </td> 
    <td colname="col5">![supported icon](assets/supported15.png) </td> 
    <td colname="col7">![supported icon](assets/supported15.png) </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

 -->

## HLS集成{#hls-integrations}

| 类别 | 内容类型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 集成 | VOD +实时 | Adobe Analytics VHL集成 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |

## HLS高级广告插入功能(CSAI){#hls-advanced-ad-insertion}

| 类别 | 内容类型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD | 仅广告 | 不支持 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| Ad Insertion | VOD +实时 | 定位参数 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| Ad Insertion | VOD +实时 | 自定义广告策略 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | 平台限制 |
| Ad Insertion | VOD +实时 | 延迟广告加载 | ![支持图标](assets/supported15.png) | 不支持 | 平台限制 |
| Ad Insertion | VOD | 配套广告、横幅广告和可点击广告 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| Ad Insertion | VOD | VPAID 2.0 | SWF | JavaScript | JavaScript |

## HLS核心广告插入功能(CSAI){#hls-core-ad-insertion}

| 类别 | 内容类型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD +实时 | 前置 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| Ad Insertion | VOD +实时 | 中间 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | 平台限制 |
| Ad Insertion | VOD +实时 | 滚动后 | 仅VOD | 仅VOD | 仅VOD |
| Ad Insertion | FER VOD | 广告分辨率和行为 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | 平台限制 |
| Ad Insertion | VOD +实时 | 默认广告策略 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | 平台限制 |
| Ad Insertion | VOD +实时 | VAST 2.0/3.0 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| Ad Insertion | VOD +实时 | VMAP 1.0 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| Ad Insertion | VOD +实时 | CRS v3.1 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |

## HLS内容保护功能{#hls-content-protection}

| 类别 | 内容类型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 内容保护 | VOD +实时 | AES-128 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| 内容保护 | VOD +实时 | Sample-AES | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| 内容保护 | VOD | DRM | Adobe访问 | 不支持 | FairPlay |

## HLS高级回放功能{#hls-advanced-playback}

| 类别 | 内容类型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 播放 | VOD | 偏移时回放 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| 播放 | VOD | 仅音频回放 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| 播放 | VOD | 戏法 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| 播放 | VOD | 流畅的技巧 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | 平台限制 |
| 播放 | VOD +实时 | ID3解析 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | 不支持 |
| 播放 | VOD +实时 | 间断标记支持 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| 播放 | VOD +实时 | 标记流 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | 平台限制 |
| 播放 | VOD +实时 | 帐单 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| 播放 | VOD +实时 | Browserify | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |

## HLS核心播放{#hls-core-playback}

| 类别 | 内容类型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 播放 | VOD +实时 | 常规播放（播放、暂停、搜索） | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| 播放 | FER VOD | 常规播放（播放、暂停、搜索） | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| 播放 | VOD +实时 | 自适应比特率 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| 播放 | VOD +实时 | 608/708字幕 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| 播放 | VOD +实时 | WebVTT | ![支持图标](assets/supported15.png) | 仅VOD | 仅VOD |
| 播放 | VOD +实时 | 清单故障转移 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) |
| 播放 | VOD +实时 | 高级故障转移 | ![支持图标](assets/supported15.png) | 仅VOD | 平台限制 |
| 播放 | VOD +实时 | QoS和播放器通知 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | 有限的QoS支持 |
| 播放 | VOD +实时 | 支持Cookie头 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | 平台限制 |
| 播放 | VOD +实时 | 设置缓冲区控制参数 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | 平台限制 |
| 播放 | VOD +实时 | 设置自适应比特率控制 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | 平台限制 |
| 播放 | VOD +实时 | 自定义标记 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | 平台限制 |
| 播放 | VOD +实时 | 延迟绑定音频 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | 平台限制 |
| 播放 | VOD +实时 | 302重定向 | ![支持图标](assets/supported15.png) | ![支持图标](assets/supported15.png) | 平台限制 |
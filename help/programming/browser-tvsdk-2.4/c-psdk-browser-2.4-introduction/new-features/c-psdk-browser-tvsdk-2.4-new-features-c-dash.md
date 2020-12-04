---
description: 浏览器TVSDK支持许多DASH功能，您可以实施这些功能来向视频应用程序添加功能。
seo-description: 浏览器TVSDK支持许多DASH功能，您可以实施这些功能来向视频应用程序添加功能。
seo-title: 支持的DASH功能
title: 支持的DASH功能
uuid: 299516a4-09ed-4b8a-b0bf-a04f204f385a
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---


# 支持的DASH功能{#supported-dash-features}

浏览器TVSDK支持许多DASH功能，您可以实施这些功能来向视频应用程序添加功能。

* [DASH核心播放功能](#dash-core-playback)
* [DASH高级回放功能](#dash-advanced-playback)
* [DASH内容保护功能](#dash-content-protection)
* [DASH核心广告插入功能](#dash-core-ad-insertion)
* [DASH高级广告插入功能](#dash-advanced-insertion-features)
* [DASH集成](#dash-integrations)

>[!TIP]
>
>在以下功能矩阵表中，![](assets/supported15.png)
>表示该功能在当前版本中受支持。

支持以下功能：

<!-- 

<table id="table_lrb_p2g_xx"> 
 <title>DASH integrations</title> 
 <tgroup cols="4"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" /> 
  <colspec colnum="4" colname="col6" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col1" class="entry"> Category </th> 
    <th colname="col2" class="entry"> Content type </th> 
    <th colname="col3" class="entry"> Feature </th> 
    <th colname="col6" align="center" class="entry"> 
     <lines>
       HTML5 FF, IE, Chrome, Android Chrome
     </lines> </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Adobe Analytics VHL integration </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_14D9248BD1D8410E83AD27DB4AB3B6ED" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Nielsen support </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_EFA853CB763446B3B37F2CF6BCC53EE1" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Billing </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_B3A4E5937CEC4052977C08767219BC2B" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Browserify </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_3330E81B86C84AD391AEBFDFE911A47F" /> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

 -->

## DASH集成{#dash-integrations}

| 类别 | 内容类型 | 功能 | HTML5 FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| 集成 | VOD + Live | Adobe AnalyticsVHL集成 | ![](assets/supported15.png) |
| 集成 | VOD + Live | 计费 | ![](assets/supported15.png) |
| 集成 | VOD + Live | Browserify | ![](assets/supported15.png) |

## DASH高级广告插入功能(CSAI){#dash-advanced-insertion-features}

| 类别 | 内容类型 | 功能 | HTML5 FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| Ad Insertion | VOD | 仅广告 | 不支持 |
| Ad Insertion | VOD | 定位参数 | 仅VOD |
| Ad Insertion | VOD | 自定义参数 | 仅VOD |
| Ad Insertion | VOD + Live | 自定义广告策略 | 不支持 |
| Ad Insertion | VOD + Live | 延迟广告加载 | 不支持 |
| Ad Insertion | VOD | 伴侣广告、横幅广告和可点击广告 | 不支持 |
| Ad Insertion | VOD | VPAID 2.0 | 不支持 |

## DASH核心广告插入功能(CSAI){#dash-core-ad-insertion}

| 类别 | 内容类型 | 功能 | HTML5 FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| Ad Insertion | VOD + Live | 预卷 | 仅VOD |
| Ad Insertion | VOD + Live | 中间卷 | 仅VOD |
| Ad Insertion | VOD + Live | 后置 | 仅VOD |
| Ad Insertion | FER VOD | 广告分辨率和行为 | 不支持 |
| Ad Insertion | VOD + Live | 默认广告策略 | 仅VOD |
| Ad Insertion | VOD + Live | VAST 2.0/3.0 | 仅VOD |
| Ad Insertion | VOD + Live | VMAP 1.0 | 仅VOD |
| Ad Insertion | VOD + Live | CRS v3.1 | 仅VOD |

## DASH内容保护功能{#dash-content-protection}

<table id="table_hrb_p2g_xx">  
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 类别 </th> 
   <th colname="col2" class="entry"> 内容类型 </th> 
   <th colname="col3" class="entry"> 功能 </th> 
   <th colname="col6" class="entry"> HTML5 FF、IE、Chrome、Android Chrome</th>
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 内容保护 </td> 
   <td colname="col2"> VOD + Live </td> 
   <td colname="col3"> AES-128 </td> 
   <td colname="col6"> 不支持 </td>
  </tr> 
  <tr> 
   <td colname="col1"> 内容保护 </td> 
   <td colname="col2"> VOD + Live </td> 
   <td colname="col3"> Sample-AES </td> 
   <td colname="col6"> 不支持 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 内容保护 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3"> DRM </td> 
   <td colname="col6"> 
    <ul id="ul_irb_p2g_xx"> 
     <li id="li_C4643F2978BC4C8ABDB3E6C72C75A468">Widevine on 
      <ul id="ul_7047EA49AA3F40FE8F90E0ED6C028D83"> 
       <li id="li_B575735388D74D789D56BF373A470A6D">铬黄 </li> 
       <li id="li_855146E4AC3A48E69B65F0022E1C0156">Firefox 47+ </li> 
       <li id="li_BC06B0A6EAAC4FC991C713775A8BB4DA">Chromecast </li> 
      </ul> </li> 
     <li id="li_D48B51C2208F423CB85D08886C2E1C66">在Windows 8.1和Edge上的Internet Explorer上播放就绪 </li> 
     <li id="li_2786AC19387241A296E015EE6FD07F2D">Adobe访问Windows Firefox版（仅限视频） </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## DASH高级回放功能{#dash-advanced-playback}

| 类别 | 内容类型 | 功能 | HTML5、FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| 播放 | VOD | 偏移时回放 | ![](assets/supported15.png) |
| 播放 | VOD | 纯音频播放 | ![](assets/supported15.png) |
| 播放 | VOD | 技巧游戏 | ![](assets/supported15.png) |
| 播放 | VOD | 平滑技巧播放 | ![](assets/supported15.png) |
| 播放 | VOD + Live | ID3解析 | 不支持 |
| 播放 | VOD | 多期支持 | 仅VOD |
| 播放 | VOD + Live | 标记化流 | 不支持 |
| 播放 | VOD + Live | 计费 | ![](assets/supported15.png) |
| 播放 | VOD + Live | Browserify | ![](assets/supported15.png) |

## DASH核心播放功能{#dash-core-playback}

| 类别 | 内容类型 | 功能 | HTML5 FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| 播放 | VOD + Live | 常规播放（播放、暂停、搜索） | ![](assets/supported15.png) |
| 播放 | FER VOD | 常规播放（播放、暂停、搜索） | 不支持 |
| 播放 | VOD + Live | 自适应比特率 | ![](assets/supported15.png) |
| 播放 | VOD + Live | 608/708字幕 | ![](assets/supported15.png) |
| 播放 | VOD + Live | WebVTT | 仅VOD |
| 播放 | VOD + Live | 故障转移 | 仅VOD |
| 播放 | VOD + Live | QoS和播放器通知 | ![](assets/supported15.png) |
| 播放 | VOD + Live | 支持Cookie头 | ![](assets/supported15.png) |
| 播放 | VOD + Live | 设置缓冲区控制参数 | ![](assets/supported15.png) |
| 播放 | VOD + Live | 设置自适应比特率控制 | ![](assets/supported15.png) |
| 播放 | VOD + Live | 自定义标记(EventStream) | 仅VOD（内联） |
| 播放 | VOD + Live | 延迟绑定音频 | 仅VOD |
| 播放 | VOD + Live | 302重定向 | 仅VOD |
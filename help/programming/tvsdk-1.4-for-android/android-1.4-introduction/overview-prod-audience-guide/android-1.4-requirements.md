---
description: TVSDK要求对媒体内容、清单内容、DRM和软件版本具体要求。
seo-description: TVSDK要求对媒体内容、清单内容、DRM和软件版本具体要求。
seo-title: 要求
title: 要求
uuid: d5671444-cc83-48d4-8ce6-735d5f373795
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 要求 {#requirements}

TVSDK要求对媒体内容、清单内容、DRM和软件版本具体要求。

## 系统和软件要求 {#section_96E5B079900246E78682AE44D3F23068}

要使用TVSDK，请确保您的硬件、操作系统和应用程序版本均符合下面列出的最低要求。

| 操作系统 | Android 4.0或更高版本（最低API级别14） |
|---|---|
| CPU | 1 GHz单核或等效 |
| RAM | 256 MB |
| GPU | 回放需要硬件GPU |
| 架构 | x86（通过Houdini）、ARM64、ARMv7和ARMv8 |

## 内容和清单要求 {#section_72DD0E4DA9774DCCADB42887497F1386}

检查流和播放列表（清单）（包括DRM加密密钥）的限制和要求。

| Adobe Access DRM | 如果受DRM保护的流是多比特率(MBR)，则用于MBR的DRM加密密钥应与用于所有比特率流的密钥相同。 |
|---|---|
| 广告变体清单 | 必须具有与主内容的再现相同的位速率再现。 |

## #EXT-X-VERSION要求 {#section_49A33664651A46EC9ED888BA9C1C3F6D}

文件中的版 `#EXT-X-VERSION` 本会影 [!DNL .m3u8] 响应用程序可用的功能以及播放列表／清单中 `EXT` 有效的标记。

以下是有关标记的一 `#EXT-X-VERSION` 些信息，它指定了HLS协议版本：

* 该版本必须与HLS播放列表中的功能和属性相匹配；否则，可能会出现播放错误。 有关详细信息，请参 [阅HTTP实时流规范](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)。
* Adobe建议至少使用HLS版本2在基于TVSDK的客户端中回放。

   客户端和服务器必须通过以下方式实现这些版本：

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 至少使用此版本 </th> 
   <th colname="2" class="entry"> 使用这些功能 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> EXT-X-KEY标 <span class="codeph"> 签的IV属 </span> 性。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">浮点 <span class="codeph"> OVIFA持续 </span> 时间值 <p>持续时间标记( <span class="codeph"> #DIVOF:版本 </span>2中的&lt;duration&gt;,&lt;title&gt;)四舍五入为整数值。 版本3及更高版本要求准确指定浮点中的持续时间。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4 </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350">EXT- <span class="codeph"> X-BYTERANGE标 </span> 签 </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287"><span class="codeph"> EXT-X-I-FRAME-STREAM-INF标 </span> 签 </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">仅 <span class="codeph"> 限EXT-X-I-FRAMES标签 </span> </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B"><span class="codeph"> EXT-X-MEDIA标 </span> 签 </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">EXT- <span class="codeph"> X- </span> STREAM-INF标 <span class="codeph"> 签的音频和视频 </span> 属 <span class="codeph"></span> 性 </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">TVSDK备用音频 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>


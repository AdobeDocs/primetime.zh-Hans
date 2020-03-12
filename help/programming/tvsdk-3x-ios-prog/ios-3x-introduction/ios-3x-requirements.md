---
description: TVSDK对媒体内容、清单内容、DRM和软件版本有特定要求。
seo-description: TVSDK对媒体内容、清单内容、DRM和软件版本有特定要求。
seo-title: 要求
title: 要求
uuid: 06e61b9f-cda2-4813-8da4-fb3e0d88ad35
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 要求 {#requirements}

TVSDK要求媒体内容、清单内容、DRM和软件版本具有特定属性。

## 系统和软件要求 {#section_96E5B079900246E78682AE44D3F23068}

要使用TVSDK，请确保您的硬件、操作系统和应用程序版本均符合下面列出的最低要求。

| 操作系统 | iOS 7.0或更高版本 |
|---|---|
| Xcode | 适用于iOS 12的Xcode 10和适用于iOS 11的Xcode 9 |

## 内容和清单要求 {#section_72DD0E4DA9774DCCADB42887497F1386}

检查流和播放列表（清单）（包括DRM加密密钥）的限制和要求。

| 内容段关键帧 | 每个内容段必须以关键帧开头。 |
|---|---|
| 实时／线性视频中的序列号 | 必须在任何给定时间为主内容匹配所有位速率再现。 |

## EXT-X-VERSION要求 {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

清单文 `#EXT-X-VERSION` 件中的版 [!DNL .m3u8] 本会影响应用程序可用的功能以及有 `EXT` 效的标记。

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
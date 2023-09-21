---
description: TVSDK 对媒体内容、清单内容、DRM 和软件版本有特定的要求。
title: 要求
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 要求 {#requirements}

TVSDK需要媒体内容、清单内容、DRM和软件版本的特定属性。

## 系统和软件要求 {#section_96E5B079900246E78682AE44D3F23068}

要使用 TVSDK，请确保您的硬件、操作系统和应用程序版本均符合下面列出的最低要求。

| 操作系统 | iOS 7.0 或更高版本 |
|---|---|
| Xcode | Xcode 10 for ios 12 和 Xcode 9 for iOS 11 |

## 内容和清单要求 {#section_72DD0E4DA9774DCCADB42887497F1386}

检查流和播放列表（清单）的限制和要求，包括DRM加密密钥。

| 内容区段关键帧 | 每个内容区段必须以关键帧开头。 |
|---|---|
| 实时/线性视频中的序列号 | 在任何给定时间，主内容的所有比特率呈现形式都必须匹配。 |

## EXT-X 版本要求 {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

清单文件中 [!DNL .m3u8] 的版本 `#EXT-X-VERSION` 会影响应用程序可用的功能以及哪些 `EXT` 标记是有效的。

以下是有关 `#EXT-X-VERSION` 标记的一些信息，它指定了 hls) 协议版本：

* 版本必须与 HLS) 播放列表中的功能和属性相匹配;否则，可能会发生播放错误。 有关更多信息，请参阅 [ HTTP 实时流规范 ](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) 。
* Adobe Systems 建议在基于 TVSDK 的客户端中至少使用 HLS) 的版本2。

  客户端和服务器必须按以下方式实施版本：

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 至少使用此版本 </th> 
   <th colname="2" class="entry"> 要使用这些功能 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION：2 </span> </td> 
   <td colname="2"> 扩展 X 键 </span> 标记的 IV 属性 <span class="codeph"> 。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X 版本：3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784"><span class="codeph">浮点 EXTINF </span> 持续时间值 <p>持续时间标记（ <span class="codeph"> #EXTINF： </span>&lt;duration&gt;,&lt;title&gt;）已舍入为整数值。 &lt;/title&gt;&lt;/duration&gt;在浮点中，版本3及以上要求精确指定持续时间。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X 版本：4 </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350"><span class="codeph">EXT X-BYTERANGE </span> 标记 </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287"><span class="codeph">EXT-I-帧流-INF </span> 标记 </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">此 <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> 标记 </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">此 <span class="codeph"> EXT-X-MEDIA </span> 标记 </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">此 <span class="codeph"> 音频 </span> 和 <span class="codeph"> 视频 </span> 属性 <span class="codeph"> EXT-X-STREAM-INF </span> 标记 </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">TVSDK备用音频 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

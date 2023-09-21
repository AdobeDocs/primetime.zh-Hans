---
description: TVSDK 需要媒体内容、清单内容和软件版本的特定属性。
title: 要求
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 要求 {#requirements}

TVSDK需要媒体内容、清单内容和软件版本的特定属性。

## 系统和软件要求 {#section_61C32A0209C44230B392B113B85643EE}

要使用 TVSDK，请确保您的硬件、操作系统和应用程序版本均符合下面列出的最低要求。

操作系统： iOS 6.0 或更高版本

## 内容和清单要求 {#section_05FA02E2189742008DA09D87E66DCAB7}

检查流和播放列表（清单）（包括 DRM 加密密钥）的限制和要求。

| 内容区段关键帧 | 每个内容区段必须以关键帧开始。 |
|---|---|
| 实时/线性视频中的序列号 | 在任何给定时间，主内容的所有比特率演绎版必须匹配。 |

## #EXT-X-VERSION要求 {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

的版本 `#EXT-X-VERSION` 在 [!DNL .m3u8] 文件会影响您的应用程序可用的功能以及 `EXT` 标记在播放列表/清单中有效。

以下是有关 `#EXT-X-VERSION` 标记的一些信息，它指定了 hls) 协议版本：

* 版本必须与 HLS) 播放列表中的功能和属性相匹配;否则，可能会发生播放错误。

  有关更多信息，请参阅 [ HTTP 实时流规范 ](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) 。
* 如果标记未包含在母版或媒体播放列表中，或者未指定版本，则默认使用版本1。 不符合版本1的内容将无法播放。
* Adobe Systems 建议在基于 TVSDK 的客户端中至少使用版本2进行播放。

客户端和服务器必须按以下方式实施版本：

<table id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr> 
   <th colname="1" class="entry"> 至少使用此版本 </th> 
   <th colname="2" class="entry"> 要使用这些功能 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION：2 </span> </td> 
   <td colname="2"> 的IV属性 <span class="codeph"> EXT-X-KEY </span> 标记之前。 </td> 
  </tr> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X 版本：3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784"><span class="codeph">浮点 EXTINF </span> 持续时间值 <p>持续时间标记（ <span class="codeph"> #EXTINF： </span>&lt;duration&gt;,&lt;title&gt;）已舍入为整数值。 &lt;/title&gt;&lt;/duration&gt;版本3及以上版本要求持续时间与浮点数完全相同。 </p> </li> 
     <li id="li_8DF5E91F1D5D4E19894595E1FE0A5EDE"> TVSDK 功能，例如广告插入和无缝 ABR </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p> <span class="codeph"> EXT-X 版本：4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_99E24D013E3141308B5A57446A9B8033"> 
      <li id="li_F36E65ADD2CA451C82FF18DBD5667927"><span class="codeph">EXT X-BYTERANGE </span> 标记 </li> 
      <li id="li_8C653168A7B84D11AC233E7548A8D2EF"><span class="codeph">EXT-I-帧流-INF </span> 标记 </li> 
      <li id="li_2922B34717CB4F6189068529CDBE6D10">此 <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> 标记 </li> 
      <li id="li_D015D78E217641D7867EB509E9F9EEE2">此 <span class="codeph"> EXT-X-MEDIA </span> 标记 </li> 
      <li id="li_CA068EA381984F5497FE67617CA8BB34">此 <span class="codeph"> 音频 </span> 和 <span class="codeph"> 视频 </span> 属性 <span class="codeph"> EXT-X-STREAM-INF </span> 标记 </li> 
      <li id="li_EE78CC7D194A4EB2897F9AE8E4B081B8"> TVSDK备用音频 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

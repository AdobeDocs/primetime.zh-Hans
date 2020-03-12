---
description: TVSDK要求媒体内容、清单内容和软件版本的特定属性。
seo-description: TVSDK要求媒体内容、清单内容和软件版本的特定属性。
seo-title: 要求
title: 要求
uuid: 7e5fb176-4c3f-4c12-9080-3afced28627b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 要求 {#requirements}

TVSDK要求媒体内容、清单内容和软件版本的特定属性。

## 系统和软件要求 {#section_61C32A0209C44230B392B113B85643EE}

要使用TVSDK，请确保您的硬件、操作系统和应用程序版本均符合下面列出的最低要求。

操作系统：iOS 6.0或更高版本

## 内容和清单要求 {#section_05FA02E2189742008DA09D87E66DCAB7}

检查流和播放列表（清单）（包括DRM加密密钥）的限制和要求。

| 内容段关键帧 | 每个内容段必须以关键帧开头。 |
|---|---|
| 实时／线性视频中的序列号 | 必须在任何给定时间为主内容匹配所有位速率再现。 |

## #EXT-X-VERSION要求 {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

文件中的版 `#EXT-X-VERSION` 本会影 [!DNL .m3u8] 响应用程序可用的功能以及播放列表／清单中 `EXT` 有效的标记。

以下是有关标记的一 `#EXT-X-VERSION` 些信息，它指定了HLS协议版本：

* 该版本必须与HLS播放列表中的功能和属性相匹配；否则，可能会出现播放错误。

   有关详细信息，请参 [阅HTTP实时流规范](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)。
* 如果主播放列表或媒体播放列表中不包含标记，或者如果未指定版本，则默认情况下使用版本1。 不符合版本1的内容将不播放。
* Adobe建议至少使用版本2在基于TVSDK的客户端中回放。

客户端和服务器必须通过以下方式实现这些版本：

<table id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr> 
   <th colname="1" class="entry"> 至少使用此版本 </th> 
   <th colname="2" class="entry"> 使用这些功能 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> EXT-X-KEY标 <span class="codeph"> 签的IV属 </span> 性。 </td> 
  </tr> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">浮点 <span class="codeph"> OVIFA持续 </span> 时间值 <p>持续时间标记( <span class="codeph"> #DIVOF:版本 </span>2中的&lt;duration&gt;,&lt;title&gt;)四舍五入为整数值。 版本3及更高版本要求持续时间在浮点中精确。 </p> </li> 
     <li id="li_8DF5E91F1D5D4E19894595E1FE0A5EDE"> TVSDK功能，如广告插入和无缝ABR </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_99E24D013E3141308B5A57446A9B8033"> 
      <li id="li_F36E65ADD2CA451C82FF18DBD5667927">EXT- <span class="codeph"> X-BYTERANGE标 </span> 签 </li> 
      <li id="li_8C653168A7B84D11AC233E7548A8D2EF"><span class="codeph"> EXT-X-I-FRAME-STREAM-INF标 </span> 签 </li> 
      <li id="li_2922B34717CB4F6189068529CDBE6D10">仅 <span class="codeph"> 限EXT-X-I-FRAMES标签 </span> </li> 
      <li id="li_D015D78E217641D7867EB509E9F9EEE2"><span class="codeph"> EXT-X-MEDIA标 </span> 签 </li> 
      <li id="li_CA068EA381984F5497FE67617CA8BB34">EXT- <span class="codeph"> X- </span> STREAM-INF标 <span class="codeph"> 签的音频和视频 </span> 属 <span class="codeph"></span> 性 </li> 
      <li id="li_EE78CC7D194A4EB2897F9AE8E4B081B8"> TVSDK备用音频 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

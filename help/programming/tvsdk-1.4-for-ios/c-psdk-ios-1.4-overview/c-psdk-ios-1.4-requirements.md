---
description: TVSDK需要媒体内容、清单内容和软件版本的特定属性。
title: 要求
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# 要求{#requirements}

TVSDK需要媒体内容、清单内容和软件版本的特定属性。

## 系统和软件要求{#section_61C32A0209C44230B392B113B85643EE}

要使用TVSDK，请确保您的硬件、操作系统和应用程序版本均符合以下列最低要求。

操作系统：iOS 6.0或更高版本

## 内容和清单要求{#section_05FA02E2189742008DA09D87E66DCAB7}

检查流和播放列表（清单）（包括DRM加密密钥）的限制和要求。

| 内容段关键帧 | 每个内容段必须以关键帧开头。 |
|---|---|
| 实时/线性视频中的序列号 | 必须在任何给定时间的主要内容的所有比特率再现之间匹配。 |

## #EXT-X-VERSION要求{#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

[!DNL .m3u8]文件中`#EXT-X-VERSION`的版本会影响应用程序可用的功能以及播放列表/清单中的`EXT`标记有效。

以下是有关`#EXT-X-VERSION`标记的一些信息，该标记指定HLS协议版本：

* 版本必须与HLS播放列表中的功能和属性相匹配；否则，可能会出现播放错误。

   有关详细信息，请参阅[HTTP实时流规范](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)。
* 如果标记未包含在主控或媒体播放列表中，或者未指定版本，则默认情况下使用版本1。 不符合版本1的内容将不播放。
* Adobe建议使用至少版本2在基于TVSDK的客户端中回放。

客户端和服务器必须通过以下方式实现这些版本：

<table id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr> 
   <th colname="1" class="entry"> 至少使用此版本 </th> 
   <th colname="2" class="entry"> 要使用这些功能 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2  </span> </td> 
   <td colname="2"> <span class="codeph"> EXT-X-KEY </span>标记的IV属性。 </td> 
  </tr> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">浮点<span class="codeph"> OVIF </span>持续时间值 <p>持续时间标记(<span class="codeph"> #EXTINF:版本2中的</span>&lt;duration&gt;,&lt;title&gt;)已舍入为整数值。 版本3及更高版本要求持续时间在浮点中精确。 </p> </li> 
     <li id="li_8DF5E91F1D5D4E19894595E1FE0A5EDE"> TVSDK功能，如广告插入和无缝ABR </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4  </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_99E24D013E3141308B5A57446A9B8033"> 
      <li id="li_F36E65ADD2CA451C82FF18DBD5667927"><span class="codeph"> EXT-X-BYTERANGE </span>标签 </li> 
      <li id="li_8C653168A7B84D11AC233E7548A8D2EF"><span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span>标签 </li> 
      <li id="li_2922B34717CB4F6189068529CDBE6D10"><span class="codeph"> EXT-X-I-FRAMES-ONLY </span>标签 </li> 
      <li id="li_D015D78E217641D7867EB509E9F9EEE2"><span class="codeph"> EXT-X-MEDIA </span>标签 </li> 
      <li id="li_CA068EA381984F5497FE67617CA8BB34"><span class="codeph"> EXT-X-STREAM-INF </span>标签的<span class="codeph"> AUDIO </span>和<span class="codeph"> VIDEO </span>属性 </li> 
      <li id="li_EE78CC7D194A4EB2897F9AE8E4B081B8"> TVSDK备用音频 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

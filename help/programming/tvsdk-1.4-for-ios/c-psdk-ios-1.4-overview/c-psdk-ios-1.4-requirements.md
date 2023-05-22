---
description: TVSDK需要媒体内容、清单内容和软件版本的特定属性。
title: 需求
exl-id: 2b81ae19-7907-4038-80e1-f579a8c04540
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 需求 {#requirements}

TVSDK需要媒體內容、資訊清單內容和軟體版本的特定屬性。

## 系统和软件要求 {#section_61C32A0209C44230B392B113B85643EE}

要使用TVSDK，请确保您的硬件、操作系统和应用程序版本均满足下面列出的最低要求。

操作系统：iOS 6.0或更高版本

## 内容和清单要求 {#section_05FA02E2189742008DA09D87E66DCAB7}

检查流和播放列表（清单）的限制和要求，包括DRM加密密钥。

| 内容区段关键帧 | 每个内容区段必须以关键帧开头。 |
|---|---|
| 即時/線性視訊中的序號 | 在任何指定時間，主要內容的所有位元速率轉譯之間都必須相符。 |

## #EXT-X-VERSION統需求 {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

的版本 `#EXT-X-VERSION` 在 [!DNL .m3u8] 檔案會影響您的應用程式可使用哪些功能，以及 `EXT` 標籤在您的播放清單/資訊清單中有效。

以下是关于指定HLS协议版本的`#EXT-X-VERSION`标记的一些信息：

* 版本必须与HLS播放列表中的功能和属性匹配；否则，可能会发生播放错误。

   有关详细信息，请参阅[HTTP实时流规范](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)。
* 如果标记未包含在主控或媒体播放列表中，或者未指定版本，则默认情况下使用版本1。不符合版本1的内容将不会播放。
* Adobe建议在基于TVSDK的客户端中至少使用版本2进行播放。

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
   <td colname="2"> 的IV屬性 <span class="codeph"> EXT-X-KEY </span> 標籤之間。 </td> 
  </tr> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">浮点<span class="codeph"> EXTINF </span>持续时间值 <p>版本2中的持续时间标记(<span class="codeph"> #EXTINF： </span>&lt;duration&gt;，&lt;title&gt;)已四舍五入到整数值。Version 3 and above require durations to be exact in floating point. </p> </li> 
     <li id="li_8DF5E91F1D5D4E19894595E1FE0A5EDE"> 版本3及更高版本要求持续时间必须以浮点精确表示。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_99E24D013E3141308B5A57446A9B8033"> 
      <li id="li_F36E65ADD2CA451C82FF18DBD5667927"><span class="codeph"> EXT-X-BYTERANGE </span>标记 </li> 
      <li id="li_8C653168A7B84D11AC233E7548A8D2EF"><span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span>标记 </li> 
      <li id="li_2922B34717CB4F6189068529CDBE6D10">此 <span class="codeph"> 僅限EXT-X-I-FRAMES </span> 標籤 </li> 
      <li id="li_D015D78E217641D7867EB509E9F9EEE2">此 <span class="codeph"> EXT-X-MEDIA </span> 標籤 </li> 
      <li id="li_CA068EA381984F5497FE67617CA8BB34">此 <span class="codeph"> 音訊 </span> 和 <span class="codeph"> 視訊 </span> 屬性 <span class="codeph"> EXT-X-STREAM-INF </span> 標籤 </li> 
      <li id="li_EE78CC7D194A4EB2897F9AE8E4B081B8"> TVSDK替代音訊 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

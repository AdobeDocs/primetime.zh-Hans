---
description: M3u8 文件中的 EXT 版本版本会影响您应用程序可用的功能以及播放列表/清单中有效的外部标记。
title: EXT-X 版本要求
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# EXT-X 版本要求{#ext-x-version-requirements}

M3u8 文件中 #EXT-X 版本的版本会影响您的应用程序可用的功能以及播放列表/清单中的哪些外部标记是有效的。

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

以下是有关 `#EXT-X-VERSION` 标记的一些信息，它指定了 hls) 协议版本：

* 版本必须与 HLS) 播放列表中的功能和属性相匹配;否则，可能会发生播放错误。

  有关更多信息，请参阅 [ HTTP 实时流规范 ](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) 。
* 版本必须与 HLS) 播放列表中的功能和属性相匹配;否则，可能会发生播放错误。

  有关更多信息，请参阅 [ HTTP 实时流规范 ](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) 。
* Adobe Systems 建议至少使用版本2，以便在基于视频的客户端中播放。

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
   <td colname="1"> <span class="codeph"> EXT-X 版本：2 </span> </td> 
   <td colname="2"> 扩展 X 键 </span> 标记的 IV 属性 <span class="codeph"> 。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X 版本：3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784"><span class="codeph">浮点 EXTINF </span> 持续时间值 <p>持续时间标记（ <span class="codeph"> #EXTINF： </span>&lt;duration&gt;,&lt;title&gt;）已舍入为整数值。 &lt;/title&gt;&lt;/duration&gt;版本3及以上版本要求持续时间与浮点数完全相同。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <p> <span class="codeph"> EXT-X 版本：4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_83D61E909D0C413FBDAB7A4A0BE1F03C"> 
      <li id="li_5071F2BE2DB74BBFB1F23B3B30C5CFD6"><span class="codeph">EXT X-BYTERANGE </span> 标记 </li> 
      <li id="li_A093F448567D475AB44656D4600BCBD6"><span class="codeph">EXT-I-帧流-INF </span> 标记 </li> 
      <li id="li_1084AE3B10FD4EB387D25EEDDFBBC8CD"><span class="codeph">EXT-I-仅限 </span> 框架标记 </li> 
      <li id="li_4FEFA36E300C403DBB77BB4DA46DB4EB"><span class="codeph">EXT X MEDIA </span> 标记 </li> 
      <li id="li_E53D81AED45C47AEA346FA3A1B191E5C">此 <span class="codeph"> 音频 </span> 和 <span class="codeph"> 视频 </span> 属性 <span class="codeph"> EXT-X-STREAM-INF </span> 标记 </li> 
      <li id="li_2E99A4971B8046F3845CF3D4D363CCCF">TVSDK 替代音频 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

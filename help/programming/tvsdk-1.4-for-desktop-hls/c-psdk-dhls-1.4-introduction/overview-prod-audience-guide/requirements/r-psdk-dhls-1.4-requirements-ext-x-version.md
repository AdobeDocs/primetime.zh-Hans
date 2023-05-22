---
description: .m3u8文件中的EXT-X-VERSION版本会影响应用程序可用的功能以及播放列表/清单中有效的EXT标记。
title: EXT-X-VERSION要求
exl-id: ee778fe1-d050-4c90-af8d-6600fff72e52
source-git-commit: e2a796dc5eb017929297d127cc79b65ba51a0c75
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# EXT-X-VERSION要求{#ext-x-version-requirements}

.m3u8文件中的#EXT-X-VERSION版本会影响应用程序可用的功能以及播放列表/清单中有效的EXT标记。

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

以下是关于指定HLS协议版本的`#EXT-X-VERSION`标记的一些信息：

* 版本必须与HLS播放列表中的功能和属性匹配；否则，可能会发生播放错误。

   有关详细信息，请参阅[HTTP实时流规范](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)。
* 版本必须与HLS播放列表中的功能和属性匹配；否则，可能会发生播放错误。

   有关详细信息，请参阅[HTTP实时流规范](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)。
* Adobe建议在基于客户端的播放中使用至少版本2。

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
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> <span class="codeph"> EXT-X-KEY </span>标记的IV特性。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">浮点<span class="codeph"> EXTINF </span>持续时间值 <p>版本2中的持续时间标记(<span class="codeph"> #EXTINF： </span>&lt;duration&gt;，&lt;title&gt;)已四舍五入到整数值。版本3及更高版本要求持续时间必须以浮点精确表示。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_83D61E909D0C413FBDAB7A4A0BE1F03C"> 
      <li id="li_5071F2BE2DB74BBFB1F23B3B30C5CFD6"><span class="codeph"> EXT-X-BYTERANGE </span>标记 </li> 
      <li id="li_A093F448567D475AB44656D4600BCBD6"><span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span>标记 </li> 
      <li id="li_1084AE3B10FD4EB387D25EEDDFBBC8CD"><span class="codeph"> EXT-X-I-FRAMES-ONLY </span>标记 </li> 
      <li id="li_4FEFA36E300C403DBB77BB4DA46DB4EB"><span class="codeph"> EXT-X-MEDIA </span>标记 </li> 
      <li id="li_E53D81AED45C47AEA346FA3A1B191E5C">此 <span class="codeph"> 音訊 </span> 和 <span class="codeph"> 視訊 </span> 屬性 <span class="codeph"> EXT-X-STREAM-INF </span> 標籤 </li> 
      <li id="li_2E99A4971B8046F3845CF3D4D363CCCF">TVSDK备用音频 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

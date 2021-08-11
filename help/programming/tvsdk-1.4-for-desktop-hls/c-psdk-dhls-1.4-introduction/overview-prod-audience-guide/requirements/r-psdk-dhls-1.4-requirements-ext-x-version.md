---
description: .m3u8文件中的“#”EXT-X-VERSION的版本会影响应用程序可用的功能以及播放列表/清单中有效的EXT标记。
title: EXT-X-VERSION要求
exl-id: ee778fe1-d050-4c90-af8d-6600fff72e52
source-git-commit: 8610792a7410dab59d42ab7771b534c2c1670ad2
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# `#`EXT-X-VERSION要求{#ext-x-version-requirements}

.m3u8文件#EXT-X-VERSION的版本会影响应用程序可用的功能以及播放列表/清单中有效的EXT标记。

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

以下是有关`#EXT-X-VERSION`标记的一些信息，该标记指定HLS协议版本：

* 该版本必须与HLS播放列表中的功能和属性相匹配；否则，可能会发生播放错误。

   有关更多信息，请参阅[HTTP实时流规范](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)。
* 该版本必须与HLS播放列表中的功能和属性相匹配；否则，可能会发生播放错误。

   有关更多信息，请参阅[HTTP实时流规范](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)。
* Adobe建议至少使用版本2在基于客户端的客户端中播放。

   客户端和服务器必须通过以下方式实施这些版本：

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 至少使用此版本 </th> 
   <th colname="2" class="entry"> 要使用这些功能，请 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2  </span> </td> 
   <td colname="2"> <span class="codeph"> EXT-X-KEY </span>标记的IV属性。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">浮点<span class="codeph"> DIVOF </span>持续时间值 <p>持续时间标记(<span class="codeph"> #EXTINF:版本2中的</span>&lt;持续时间&gt;、&lt;标题&gt;)已四舍五入为整数值。 版本3及更高版本要求持续时间精确地位于浮点中。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4  </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_83D61E909D0C413FBDAB7A4A0BE1F03C"> 
      <li id="li_5071F2BE2DB74BBFB1F23B3B30C5CFD6"><span class="codeph"> EXT-X-BYTERANGE </span>标记 </li> 
      <li id="li_A093F448567D475AB44656D4600BCBD6"><span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span>标记 </li> 
      <li id="li_1084AE3B10FD4EB387D25EEDDFBBC8CD"><span class="codeph"> EXT-X-I-FRAMES-ONLY </span>标记 </li> 
      <li id="li_4FEFA36E300C403DBB77BB4DA46DB4EB"><span class="codeph"> EXT-X-MEDIA </span>标记 </li> 
      <li id="li_E53D81AED45C47AEA346FA3A1B191E5C"><span class="codeph"> EXT-X-STREAM-INF </span>标记的<span class="codeph"> AUDIO </span>和<span class="codeph"> VIDEO </span>属性 </li> 
      <li id="li_2E99A4971B8046F3845CF3D4D363CCCF">TVSDK替代音频 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

---
description: .m3u8文件中的“#”EXT-X-VERSION的版本会影响应用程序可用的功能以及播放列表/清单中有效的EXT标记。
title: “#”EXT-X-VERSION要求
exl-id: 1b7c205b-c6b1-416f-885a-d1cd23d8e803
source-git-commit: 8610792a7410dab59d42ab7771b534c2c1670ad2
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# `#`EXT-X-VERSION要求{#ext-x-version-requirements}

.m3u8文件#EXT-X-VERSION的版本会影响应用程序可用的功能以及播放列表/清单中有效的EXT标记。

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

以下是有关`#EXT-X-VERSION`标记的一些信息，该标记指定HLS协议版本：

* 该版本必须与HLS播放列表中的功能和属性相匹配；否则，可能会发生播放错误。 有关更多信息，请参阅[HTTP实时流规范](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)。
* Adobe建议至少使用版本2在基于浏览器TVSDK的客户端中播放。

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
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">浮点<span class="codeph"> DIVOF </span>持续时间值 <p>持续时间标记(<span class="codeph"> #EXTINF:版本2中的</span>&lt;持续时间&gt;、&lt;标题&gt;)已四舍五入为整数值。 版本3及更高版本要求持续时间精确地位于浮点中。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4  </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B"><span class="codeph"> EXT-X-MEDIA </span>标记 </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD"><span class="codeph"> EXT-X-STREAM-INF </span>标记的<span class="codeph"> AUDIO </span>和<span class="codeph"> VIDEO </span>属性 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

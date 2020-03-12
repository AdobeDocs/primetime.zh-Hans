---
description: .m3u8文件中的#EXT-X-VERSION版本会影响应用程序可用的功能以及播放列表／清单中有效的EXT标记。
seo-description: .m3u8文件中的#EXT-X-VERSION版本会影响应用程序可用的功能以及播放列表／清单中有效的EXT标记。
seo-title: '#EXT-X-VERSION要求'
title: '#EXT-X-VERSION要求'
uuid: 8d22930f-4faf-4a40-b1f0-507886cd8938
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# #EXT-X-VERSION要求{#ext-x-version-requirements}

.m3u8文件中的#EXT-X-VERSION版本会影响应用程序可用的功能以及播放列表／清单中有效的EXT标记。

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

以下是有关标记的一 `#EXT-X-VERSION` 些信息，它指定了HLS协议版本：

* 该版本必须与HLS播放列表中的功能和属性相匹配；否则，可能会出现播放错误。 有关详细信息，请参 [阅HTTP实时流规范](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)。
* Adobe建议至少使用版本2在基于浏览器TVSDK的客户端中回放。

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
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">浮点 <span class="codeph"> OVIFA持续 </span> 时间值 <p>持续时间标记( <span class="codeph"> #DIVOF:版本 </span>2中的&lt;duration&gt;,&lt;title&gt;)四舍五入为整数值。 版本3及更高版本要求持续时间在浮点中精确。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4 </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B"><span class="codeph"> EXT-X-MEDIA标 </span> 签 </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">EXT- <span class="codeph"> X- </span> STREAM-INF标 <span class="codeph"> 签的音频和视频 </span> 属 <span class="codeph"></span> 性 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>


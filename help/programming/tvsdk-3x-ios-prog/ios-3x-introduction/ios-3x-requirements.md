---
description: TVSDK對媒體內容、資訊清單內容、DRM和軟體版本有特定需求。
title: 需求
exl-id: 8c611ad4-ad04-4bab-83b9-0d8fb6c5cf3d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 需求 {#requirements}

TVSDK需要媒體內容、資訊清單內容、DRM和軟體版本的特定屬性。

## 系统和软件要求 {#section_96E5B079900246E78682AE44D3F23068}

要使用TVSDK，请确保您的硬件、操作系统和应用程序版本都满足下面列出的最低要求。

| 操作系统 | iOS 7.0或更高版本 |
|---|---|
| Xcode | iOS 12的Xcode 10和iOS 11的Xcode 9 |

## 内容和清单要求 {#section_72DD0E4DA9774DCCADB42887497F1386}

檢查串流和播放清單（資訊清單）的限制和需求，包括DRM加密金鑰。

| 內容區段關鍵畫面 | 每個內容區段都必須以關鍵框架開頭。 |
|---|---|
| 即時/線性視訊中的序號 | 在任何给定时间，主内容的所有比特率演绎版必须匹配。 |

## EXT-X-VERSION要求 {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

[!DNL .m3u8]清单文件中的`#EXT-X-VERSION`版本会影响应用程序可用的功能以及`EXT`标记是否有效。

以下是关于指定HLS协议版本的`#EXT-X-VERSION`标记的一些信息：

* 版本必须与HLS播放列表中的功能和属性匹配；否则，可能会发生播放错误。有关详细信息，请参阅[HTTP实时流规范](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)。
* Adobe建议在基于TVSDK的客户端中至少使用版本2的HLS进行播放。

   客户端和服务器必须按以下方式实施版本：

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 至少使用此版本 </th> 
   <th colname="2" class="entry"> 若要使用這些功能 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION：2 </span> </td> 
   <td colname="2"> <span class="codeph"> EXT-X-KEY </span>标记的IV特性。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION：3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">浮点<span class="codeph"> EXTINF </span>持续时间值 <p>版本2中的持续时间标记(<span class="codeph"> #EXTINF： </span>&lt;duration&gt;，&lt;title&gt;)已四舍五入到整数值。版本3及更高版本要求以浮点精确指定持续时间。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION：4 </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350"><span class="codeph"> EXT-X-BYTERANGE </span>标记 </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287"><span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span>标记 </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">此 <span class="codeph"> 僅限EXT-X-I-FRAMES </span> 標籤 </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">此 <span class="codeph"> EXT-X-MEDIA </span> 標籤 </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">此 <span class="codeph"> 音訊 </span> 和 <span class="codeph"> 視訊 </span> 屬性 <span class="codeph"> EXT-X-STREAM-INF </span> 標籤 </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">TVSDK替代音訊 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

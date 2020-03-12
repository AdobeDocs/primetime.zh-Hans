---
description: 广告信令模式指定视频流应在何处获得广告信息。
seo-description: 广告信令模式指定视频流应在何处获得广告信息。
seo-title: 广告信令模式
title: 广告信令模式
uuid: 111b7e43-e97c-4069-a273-4f9f6280453e
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 广告信令模式 {#ad-signaling-mode-overview}

广告信令模式指定视频流应在何处获得广告信息。

有效值为 `DEFAULT`、 `SERVER_MAP`和 `MANIFEST_CUES`。

下表描述了各种类型 `AdSignalingMode` 的HLS流的值的影响：

<table frame="all" colsep="1" rowsep="1" id="table_AdSignalingMode"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> </th> 
   <th colname="2" class="entry"> 默认 </th> 
   <th colname="3" class="entry"> 清单提示 </th> 
   <th colname="4" class="entry"> 广告服务器地图 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> 视频点播(VOD) </td> 
   <td colname="2"> 
    <ul id="ul_E79DA79107364D0D8B46A1859CA75B5C"> 
     <li id="li_B259ED87743F463095071F58DC840E39"> 使用服务器地图进行位置检测 </li> 
     <li id="li_8957E4151466467BA6C954E5010E34EA"> 插入广告 </li> 
    </ul> </td> 
   <td colname="3"> 
    <ul id="ul_D462C76717D94DE09915BDF6E9B3FB68"> 
     <li id="li_FB46108F4AD9457D99D2618ABEF7DBD1"> 使用流内提示进行位置检测 </li> 
     <li id="li_C3F7FBB98F524CEF97D17318C292E9EA"> 将预卷广告插入主流 </li> 
     <li id="li_A56E1545F84840DFA6D065DA60E98C31"> 中间卷广告取代主流 </li> 
    </ul> </td> 
   <td colname="4"> 
    <ul id="ul_F10192B1B6F745CBB0D4C1A6D52A57B4"> 
     <li id="li_2ADACF71FA5F4A08A00A3399F5593420"> 使用服务器地图进行位置检测 </li> 
     <li id="li_1201085B9C554A4BBD471E7EB2E363AC"> 插入广告 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> 实时／线性 </td> 
   <td colname="2"> 
    <ul id="ul_82AAC9EE056F49E999F809536A96C2F8"> 
     <li id="li_73BAD2BAA95F4592808B77F8DA436237"> 使用清单提示进行放置检测 </li> 
     <li id="li_A97B6F61078D4149A984B2412021E103"> 广告取代主流 </li> 
    </ul> </td> 
   <td colname="3"> 
    <ul id="ul_CAED2D4F46334D76AE025482881BF843"> 
     <li id="li_A8023845A037482DBFDEF7EF247FECFD"> 使用流内提示进行位置检测 </li> 
     <li id="li_62A3CDAD249344EB89043B2AE0F4D7FF"> 广告取代主流 </li> 
    </ul> </td> 
   <td colname="4"> 不支持 </td> 
  </tr> 
 </tbody> 
</table>


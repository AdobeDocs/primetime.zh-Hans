---
description: 广告信令模式指定视频流应在何处获得广告信息。
title: 广告信令模式
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 广告信令模式{#ad-signaling-mode}

广告信令模式指定视频流应在何处获得广告信息。

有效值为`PTAdSignalingModeDefault`、`PTAdSignalingModeManifestCues`和`PTAdSignalingModeServerMap`。

下表描述了各种HLS流类型的`AdSignalingMode`值的影响：

<table frame="all" colsep="1" rowsep="1" id="table_AdSignalingMode"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> </th> 
   <th colname="2" class="entry"> 默认 </th> 
   <th colname="3" class="entry"> 清单提示 </th> 
   <th colname="4" class="entry"> 广告服务器映射 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> 视频点播(VOD) </td> 
   <td colname="2"> 
    <ul id="ul_E79DA79107364D0D8B46A1859CA75B5C"> 
     <li id="li_B259ED87743F463095071F58DC840E39"> <p>使用服务器映射进行位置检测 </p> </li> 
     <li id="li_8957E4151466467BA6C954E5010E34EA"> <p>插入广告 </p> </li> 
    </ul> </td> 
   <td colname="3"> 
    <ul id="ul_D462C76717D94DE09915BDF6E9B3FB68"> 
     <li id="li_FB46108F4AD9457D99D2618ABEF7DBD1"> <p>使用流内提示进行位置检测 </p> </li> 
     <li id="li_C3F7FBB98F524CEF97D17318C292E9EA"> <p>在主流中插入预卷广告 </p> </li> 
     <li id="li_A56E1545F84840DFA6D065DA60E98C31"> <p>中间滚动广告取代主流 </p> </li> 
    </ul> </td> 
   <td colname="4"> 
    <ul id="ul_F10192B1B6F745CBB0D4C1A6D52A57B4"> 
     <li id="li_2ADACF71FA5F4A08A00A3399F5593420"> <p>使用服务器映射进行位置检测 </p> </li> 
     <li id="li_1201085B9C554A4BBD471E7EB2E363AC"> <p>插入广告 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> 实时/线性 </td> 
   <td colname="2"> 
    <ul id="ul_82AAC9EE056F49E999F809536A96C2F8"> 
     <li id="li_73BAD2BAA95F4592808B77F8DA436237"> <p>使用清单提示进行位置检测 </p> </li> 
     <li id="li_A97B6F61078D4149A984B2412021E103"> <p>广告替换主流 </p> </li> 
    </ul> </td> 
   <td colname="3"> 
    <ul id="ul_CAED2D4F46334D76AE025482881BF843"> 
     <li id="li_A8023845A037482DBFDEF7EF247FECFD"> <p>使用流内提示进行位置检测 </p> </li> 
     <li id="li_62A3CDAD249344EB89043B2AE0F4D7FF"> <p>广告替换主流 </p> </li> 
    </ul> </td> 
   <td colname="4"> 不支持 </td> 
  </tr> 
 </tbody> 
</table>


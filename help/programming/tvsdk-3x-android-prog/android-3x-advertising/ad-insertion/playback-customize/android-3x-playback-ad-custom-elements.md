---
description: TVSDK提供了可用于自定义包含广告的内容播放行为的类和方法。
title: 用于广告播放的API元素
exl-id: 1114d00b-e853-47a5-af29-253df615692e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 用于广告播放的API元素 {#api-elements-for-ad-playback}

TVSDK提供了可用于自定义包含广告的内容播放行为的类和方法。

以下API元素对于自定义播放非常有用：

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>API元素 </b></th> 
   <th colname="col2" class="entry"> <b>支持广告的内容</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdvertisingMetadata </span> </td> 
   <td colname="col2">控制是否应将广告时间标记为已观看者观看，如果是，则何时将其标记为已观看。 使用设置并获取受监视的策略 <span class="codeph"> setAdBreakAsWatched</span> 和 <span class="codeph"> getAdBreakAsWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreakPolicy</span> </td> 
   <td colname="col2"> 枚举广告时间的可能播放策略。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicy</span> </td> 
   <td colname="col2"> 枚举广告的可能播放策略。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicySelector </span> </td> 
   <td colname="col2"> 允许自定义TVSDK广告行为的界面。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> DefaultAdPolicySelector </span> </td> 
   <td colname="col2"> 实现默认TVSDK行为的类。 您的应用程序可以覆盖此类以自定义默认行为，而无需实现完整的接口。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="apiname"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> getLocalTime</span> <p>这是播放的本地时间，不包括置入的广告时间。 </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> seekToLocal</span>. <p>在此处，搜寻相对于流中的本地时间进行。 </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>时间轴上的虚拟位置被转换为本地位置。 </p> </li> 
    </ul> <p>重要提示：  <span class="codeph"> getLocalTime</span> 在 <span class="codeph"> MediaPlayer</span> 返回相对于原始内容的当前时间，不含动态拼接的广告。 <span class="codeph"> getLocalTime</span> 在 <span class="codeph"> 广告时间</span> 返回相对于原始内容的分隔开始时间。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> 广告时间</span> </td> 
   <td colname="col2"><span class="codeph"> isWatched</span> 属性。 指示查看器是否观看了广告。 </td> 
  </tr> 
 </tbody> 
</table>

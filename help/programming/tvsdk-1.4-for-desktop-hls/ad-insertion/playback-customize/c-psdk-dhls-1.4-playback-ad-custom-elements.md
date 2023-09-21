---
description: TVSDK提供了一些类和方法，您可以使用它们自定义包含广告的内容的播放行为。
title: 广告播放的API元素
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 广告播放的API元素{#api-elements-for-ad-playback}

TVSDK提供了一些类和方法，您可以使用它们自定义包含广告的内容的播放行为。

以下API元素对于自定义播放非常有用：

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> API元素 </th> 
   <th colname="col2" class="entry"> 支持广告的内容 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdvertisingMetadata</span> </td> 
   <td colname="col2">控制是否应将广告时间标记为已被观看者观看，如果是，何时将其标记为已观看。 使用设置和获取受监视的策略 
    <pre>
     该 
     <span class="codeph"> adBreakAsWatched</span> 属性。
    </pre> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdBreakPolicy</span> </td> 
   <td colname="col2"> 枚举广告时间的可能播放策略。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicy</span> </td> 
   <td colname="col2"> 枚举广告的可能播放策略。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicySelector</span> </td> 
   <td colname="col2"> 允许自定义TVSDK广告行为的界面。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DefaultAdPolicySelector</span> </td> 
   <td colname="col2"> 实现默认TVSDK行为的类。 您的应用程序可以覆盖此类以自定义默认行为，而无需实现完整的接口。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> localTime</span>. <p>这是播放的本地时间，不包括置入的广告时间。 </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocal</span>. <p>在此处，搜寻相对于流中的本地时间进行。 </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>时间轴上的虚拟位置被转换为本地位置。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 时间线项目</span> </td> 
   <td colname="col2"> 
    <ul id="ul_99AD34F823DB4F10937EE39DAD0C0B72"> 
     <li id="li_87E2DA15ECE74CFE9C9FBBE8F4B62440"><span class="codeph"> 已观看</span>. <p>指示查看器是否已观看广告。 </p> </li> 
     <li id="li_A9E5A9CF701C48BC94C93F28C114778D"><span class="codeph"> localRange</span>. <p>相对于原始内容的广告时间或广告的开始位置和持续时间。 </p> </li> 
     <li id="li_070BDA0BF4184863AF44652BD5A0CCEC"><span class="codeph"> virtualrange</span>. <p>在考虑所有置入的广告时间后，虚拟时间轴上广告时间或广告的开始位置和持续时间。 </p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

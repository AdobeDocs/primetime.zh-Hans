---
description: TVSDK提供了类和方法，您可以使用它们自定义包含广告的内容的播放行为。
seo-description: TVSDK提供了类和方法，您可以使用它们自定义包含广告的内容的播放行为。
seo-title: 用于广告播放的API元素
title: 用于广告播放的API元素
uuid: 61ebbfd7-696c-4a5b-8dbb-682770cd5840
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 用于广告播放的API元素{#api-elements-for-ad-playback}

TVSDK提供了类和方法，您可以使用它们自定义包含广告的内容的播放行为。

以下API元素对于自定义播放很有用：

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> API元素 </th> 
   <th colname="col2" class="entry"> 支持广告的内容 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> 广告元数据</span> </td> 
   <td colname="col2">控制广告分时段是否应标记为已被查看者观看，如果是，何时标记。 使用 
    <ph>
     adBreakAsWatched <span class="codeph"> 属性</span> 。
    </ph> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdBreakPolicy</span> </td> 
   <td colname="col2"> 枚举广告中断的可能播放策略。 </td> 
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
   <td colname="col2"> 实现默认TVSDK行为的类。 应用程序可以覆盖此类，以自定义默认行为，而无需实现完整的界面。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> localTime</span>。 <p>这是播放的本地时间，不包括已放置的广告中断。 </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocal</span>。 <p>此处，搜索相对于流中的本地时间进行。 </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>。 <p>时间轴上的虚拟位置将转换为本地位置。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> TimelineItem</span> </td> 
   <td colname="col2"> 
    <ul id="ul_99AD34F823DB4F10937EE39DAD0C0B72"> 
     <li id="li_87E2DA15ECE74CFE9C9FBBE8F4B62440"><span class="codeph"> 观看</span>。 <p>指示查看器是否已观看广告。 </p> </li> 
     <li id="li_A9E5A9CF701C48BC94C93F28C114778D"><span class="codeph"> localRange</span>。 <p>广告中断或广告相对于原始内容的开始位置和持续时间。 </p> </li> 
     <li id="li_070BDA0BF4184863AF44652BD5A0CCEC"><span class="codeph"> virtualRange</span>。 <p>在考虑所有已放置广告中断后，虚拟时间线上广告中断或广告的开始位置和持续时间。 </p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>


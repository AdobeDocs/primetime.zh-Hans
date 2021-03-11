---
description: TVSDK提供可用于自定义包含广告的内容的播放行为的类和方法。
title: 用于广告播放的API元素
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# 广告播放{#api-elements-for-ad-playback}的API元素

TVSDK提供可用于自定义包含广告的内容的播放行为的类和方法。

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
   <td colname="col2">控制是否应将广告中断标记为已被查看者观看，如果是，何时标记。 使用<span class="codeph"> setAdBreakAsWatched</span>和<span class="codeph"> getAdBreakAsWatched</span>设置和获取监视策略。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdBreakPolicy</span> </td> 
   <td colname="col2"> 枚举广告中断的可能播放策略。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicy</span> </td> 
   <td colname="col2"> 枚举广告可能的播放策略。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicySelector</span> </td> 
   <td colname="col2"> 允许自定义TVSDK广告行为的界面。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DefaultAdPolicySelector</span> </td> 
   <td colname="col2"> 实现默认TVSDK行为的类。 您的应用程序可以覆盖此类，以自定义默认行为，而无需实现完整的界面。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> getLocalTime</span>。 <p>这是播放的本地时间，不包括已放置广告中断。 </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> seekToLocal</span>。 <p>此处，搜索相对于流中的本地时间发生。 </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>。 <p>时间轴上的虚拟位置将转换为本地位置。 </p> </li> 
    </ul> <p>重要说明： <span class="codeph"> MediaPlayer</span>中的<span class="codeph"> getLocalTime</span>返回相对于原始内容的当前时间，而不动态拼接广告。 <span class="codeph"> </span> getLocalTimein  <span class="codeph"> </span> AdBreak返回中断相对于原始内容的开始时间。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdBreak</span> </td> 
   <td colname="col2"><span class="codeph"> </span> isWatchedproperty。指示查看器是否已观看该广告。 </td> 
  </tr> 
 </tbody> 
</table>


---
description: TVSDK提供了类和方法，您可以使用它们自定义包含广告的内容的播放行为。
seo-description: TVSDK提供了类和方法，您可以使用它们自定义包含广告的内容的播放行为。
seo-title: 用于广告播放的API元素
title: 用于广告播放的API元素
uuid: 5e21e709-8446-4fed-8711-aa4f629f1147
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 用于广告播放的API元素 {#api-elements-for-ad-playback}

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
   <td colname="col1"><span class="apiname"> 广告元数据 </span> </td> 
   <td colname="col2">控制广告分时段是否应标记为已被查看者观看，如果是，何时标记。 使用setAdBreakAsWatched和getAdBreakAsWatched设置并获 <span class="codeph"> 取监视策略</span><span class="codeph"></span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreakPolicy</span> </td> 
   <td colname="col2"> 枚举广告中断的可能播放策略。 </td> 
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
   <td colname="col2"> 实现默认TVSDK行为的类。 应用程序可以覆盖此类，以自定义默认行为，而无需实现完整的界面。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="apiname"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> getLocalTime</span> <p>这是播放的本地时间，不包括已放置的广告中断。 </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> seekToLocal</span>。 <p>此处，搜索相对于流中的本地时间进行。 </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>。 <p>时间轴上的虚拟位置将转换为本地位置。 </p> </li> 
    </ul> <p>重要说明： <span class="codeph"> MediaPlayer中的</span> getLocalTime <span class="codeph"></span> 返回与原始内容相对的当前时间，而不动态拼接广告。 <span class="codeph"> AdBreak中的</span> getLocalTime <span class="codeph"></span> 返回中断相对于原始内容的开始时间。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreak</span> </td> 
   <td colname="col2"><span class="codeph"> isWatched属性</span> 。 指示查看器是否已观看广告。 </td> 
  </tr> 
 </tbody> 
</table>

